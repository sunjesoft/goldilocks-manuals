<a id="515b53d7c2e15b60"></a>

# 46. gdump

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/515b53d7c2e15b60)  
> 태그: `26c.1_0_tag`

[← 45. gloader/gloadernet (Upload/download Tool)](45-gloader-gloadernet-upload-download-tool.md) · [전체 목차](../README.md) · [47. tablediff →](47-tablediff.md)

<a id="82a76062bc6037da"></a>
## gdump 개요

<a id="3c1767b730ed1c56"></a>
### 정의

gdump는 GOLDILOCKS에서 제공하는 유틸리티로써 database가 관리하는 다음과 같은 binary file들을 text 형태로 dump한다.

- Control file
- Datafile
- Log file
- Incremental backup file
- Property file
- Commit log file
- Log buffer file
- Pending log buffer file
- Location
- Change tracking file

<a id="342966b22bee2bcb"></a>
### 인자

gdump는 필수 인자와 옵션 인자로 구분되어 사용되고 옵션 인자는 덤프하려는 파일의 유형에 따라 다르게 사용된다.

```
gdump file_type file_name [options]
```

<a id="5db48e5496a50441"></a>
#### 필수 인자

필수 인자는 파일 유형, 파일의 경로 순으로 사용된다.

```
file_type: CONTROL | REDO_LOG | DATAFILE | PROPERTY | BACKUP | COMMIT_LOG | LOG_BUFFER | PEND_BUFFER | LOCATION | CHANGE_TRACK
file_name: file name to dump
```

<a id="636247c8f5ee1f57"></a>
##### file_type 인자

- CONTROL: Control file이다. &lt;GOLDILOCKS_DATA&gt;/wal 에 위치하고, 확장자는 .ctl 이다.
- REDO_LOG: Log file (online/ archived redo log file) 이다. &lt;GOLDILOCKS_DATA&gt;/wal 또는 &lt;GOLDILOCKS_DATA&gt;/archive_log 에 위치하고, 확장자는 .log 이다.
- DATAFILE: Datafile 이다. &lt;GOLDILOCKS_DATA&gt;/db에 위치하고 확장자는 .dbf 이다.
- PROPERTY: Binary property file을 의미한다. &lt;GOLDILOCKS_DATA&gt;/conf 에 위치하고 파일의 기본 이름은 goldilocks.properties.binary 이다.
- BACKUP: Incremental backup file을 의미한다. &lt;GOLDILOCKS_DATA&gt;/backup 에 위치하고, 확장자는 .inc 이다.
- COMMIT_LOG: &lt;GOLDILOCKS_DATA&gt;/wal 에 위치한 commit.log 파일이다.
- LOG_BUFFER: 메모리에 있는 log buffer를 file로 저장한 것이다. gsyncher를 실행하면 log buffer를 file로 저장한다.
- PEND_BUFFER: 메모리에 있는 pending log buffer를 file로 저장한 것이다. gsyncher를 실행하면 pending log buffer를 file로 저장한다.
- LOCATION: Cluster 에서 멤버들의 위치 정보를 저장하고 있는 파일이다.
- CHANGE_TRACK: 디스크 테이블스페이스의 증분 백업 시 변경된 정보를 담고 있는 파일이다.

> 손상된 control file에 dump를 시도하면 실패한다.

<a id="2dba8d1e35c8e257"></a>
#### 옵션 인자

```
-S  --silent                                            silent
file_type = CONTROL
   -s, --section  sys | log | db | backup | cluster | all  dump file section(default all)
file_type = DATAFILE
   -h, --header                                            dump (log or data) file header
   -n, --number   INTEGER ( >= 0 )                         (log or page) sequence number
   -f, --fetch    INTEGER ( >= 1 )                         dump as much as count
file_type = REDO_LOG
   -h, --header                                            dump (log or data) file header
   -n, --number   INTEGER ( >= 0 )                         (log or page) sequence number
   -o, --offset   INTEGER                                  offset of lsn(usable if set lsn)
   -f, --fetch    INTEGER ( >= 1 )                         dump as much as count
   -a, --all                                               dump all log blocks including invalid log blocks
file_type = BACKUP
   -b, --body     none | header | all                      dump incremental body(default none)
   -t, --tbs                                               dump specific tablespace body(usable if set body)
   -n, --number   INTEGER ( >= 0 )                         (log or page) sequence number
   -f, --fetch    INTEGER ( >= 1 )                         dump as much as count
file_type = CHANGE_TRACK
   -h, --header                                            dump (log or data) file header
   -t, --tbs                                               dump specific tablespace
   -d, --datafile                                          dump specific datafile
```

<a id="b4043fa78e50e50d"></a>
##### 설명

<a id="f614d385f3fc3ae1"></a>
<table><thead><tr><th align="center" valign="middle">인자 이름</th><th align="center" valign="middle">사용 가능한<br>파일 유형</th><th align="center" valign="middle">설명</th></tr></thead><tbody><tr><td valign="middle">--silent</td><td valign="middle">All</td><td valign="middle">Copyright와 version, 수행 시간 등을 표시하지 않는다.</td></tr><tr><td valign="middle">--section</td><td valign="middle">Control file</td><td valign="middle">덤프할 control file의 섹션을 의미한다.<br><ul><li>sys: System section</li><li>log: Log section</li><li>db: Database section</li><li>backup: Incremental backup section</li><li>all: All sections (기본값)</li></ul></td></tr><tr><td rowspan="2" valign="middle">--header</td><td valign="middle">Datafile</td><td valign="middle">Datafile을 덤프할 때 헤더만 덤프한다.<br>설정되지 않으면 헤더를 표시하지 않는다.</td></tr><tr><td valign="middle">Log file</td><td valign="middle">Log file을 덤프할 때 헤더만 덤프한다.</td></tr><tr><td rowspan="3" valign="middle">--number</td><td valign="middle">Datafile</td><td valign="middle">덤프할 page 번호를 나타낸다. (기본값은 0이다.)</td></tr><tr><td valign="middle">Log file</td><td valign="middle">덤프할 log 번호를 나타낸다. (기본값은 0이고 지정한 번호보다 큰 log를 덤프한다).</td></tr><tr><td valign="middle">Incremental backup file</td><td valign="middle">덤프할 page 번호를 나타낸다. (기본값은 0이고 지정한 번호보다 큰 page를 덤프한다.)</td></tr><tr><td rowspan="3" valign="middle">--fetch</td><td valign="middle">Datafile</td><td valign="middle">덤프할 page 개수이다. (기본값은 1이다.)</td></tr><tr><td valign="middle">Log file</td><td valign="middle">덤프할 log 개수이다. (기본값은 전체 log 이다.)</td></tr><tr><td valign="middle">Incremental backup file</td><td valign="middle">덤프할 page의 개수이다. (기본값은 전체 page 이다.)</td></tr><tr><td valign="middle">--offset</td><td valign="middle">Log file</td><td valign="middle">--number 옵션 인자가 설정되었을 때만 유효하고, number 인자에 설정된 값에서 offset만큼 떨어진 위치를 의미한다. (기본값은 0이다.)</td></tr><tr><td valign="middle">--body</td><td valign="middle">Incremental backup file</td><td valign="middle">Page의 헤더 (header) 또는 헤더와 페이지 (all)를 표시한다.<br>설정하지 않으면 아무것도 표시하지 않는다. (기본값은 none이다.)</td></tr><tr><td valign="middle">--tbs</td><td valign="middle">Incremental backup file</td><td valign="middle">--body 옵션 인자가 설정되었을 때만 유효하다.<br>Incremental backup file에서 특정 테이블스페이스 번호를 지정한다.<br>설정하지 않으면 모든 테이블스페이스를 의미한다.</td></tr><tr><td valign="middle">--all</td><td valign="middle">Log file</td><td valign="middle">유효하지 않은 log를 포함하여 덤프한다.</td></tr></tbody></table>

> 프로퍼티 파일을 덤프할 때는 옵션을 사용하지 않는다.

<a id="c43b07f8c8144ff9"></a>
## 사용 예

<a id="c2f420841e48734a"></a>
### Control file

- 시스템 영역 덤프

```
$ gdump control control_0.ctl --section sys --silent

 [SYSTEM SECTION]
-----------------------------------------------------------
  DATABASE CREATED                  : YES
  DATA STORE MODE                   : TDS
  VALID SEQUENCE NUMBER             : 58
  SIGNATURE                         : 373BB782744611F19F71CF68EBCB0533
  DATABASE CREATION TIME            : 2026-06-30 14:40:34.838925
  LOCAL MEMBER NAME                 : -
  LOCAL MEMBER POSITION             : -1
  LOCAL GROUP NAME                  : -
  LOCAL JOIN GCN                    : 0
  MAX NODE COUNT                    : 0
  LOCAL_CLUSTER_DEFINED             : NO
  LAST CHECKPOINT LSN               : 246557
  INCREMENTAL BACKUP RECORD COUNT   : 0
```

- 로그 영역 덤프

```
$ gdump control control_0.ctl --section log --silent

 [LOG SECTION]
-----------------------------------------------------------

  [CHECKPOINT]
    LID                               :  0,113621,13
    LSN                               :  241763
    RESETLOG LSN                      :  -1
    ARCHIVELOG MODE                   :  NOARCHIVELOG
    LAST INACTIVATED LOGFILE SEQUENCE :  -1

  [LOG STREAM]
    STATE          :  ACTIVE
    GROUP COUNT    :  4
    BLOCK SIZE     :  512
    FILE SEQUENCE  :  0

    [LOG GROUP #0]
      STATE         : CURRENT
      SIZE          : 104857600
      MEMBER COUNT  : 1
      FILE SEQUENCE : 0
      PREV LAST LSN : -1
      MEMBER #0     : (ACTIVE) "/home/mkkim2/work/product/Gliese/home/wal/redo_0_0.log"
```

- Database 영역 덤프

```
$ gdump control control_0.ctl --section db --silent

 [DB SECTION]
-----------------------------------------------------------
  [DATABASE]
    TRANSACTION_TABLE_SIZE : 1024
    UNDO_RELATION_COUNT    : 128
    TABLESPACE COUNT       : 6
    NEW TABLESPACE ID      : 6
    NEW DATAFILE SEQUENCE  : 6
    CHANGE TRACKING STATE  : enable
    CHANGE TRACKING FILE   : /db/gl_change_tracking_file.ctf

  [TABLESPACE #0] 
   NAME          :  DICTIONARY_TBS
   ATTRIBUTES    :  MEMORY | PERSISTENT | DICT
   STATE         :  CREATED
   LOGGING STATE :  LOGGING
   ONLINE STATE  :  ONLINE
   EXTENT_SIZE   :  8
   RELATION_ID   :  0

   [DATAFILE #0]
     SIZE      :  268435456
     AUTOEXTEN :  OFF
     NEXT      :  0
     MAXSIZE   :  268435456
     STATE     :  CREATED
     NAME      :  "/home/mkkim2/work/product/Gliese/home/db/system_dict.dbf"
     CHKPT LSN : 241763
     CHKPT LID : (0, 113621, 13)
```

- Incremental backup 영역 덤프

```
% gdump control control_0.ctl --section backup --silent

 [INCREMENTAL BACKUP SECTION]
-----------------------------------------------------------
  [ BACKUP DB #0 ]
           FILE NAME     : database_D20250915_T121207_L0_Q0_P0.inc
           BACKUP LSN    : 241619
           BACKUP LEVEL  : 0
           PIECE SEQ     : 0
           BACKUP TIME   : 2025-10-15 12:12:08.520125
           BACKUP OBJECT : database
  [ BACKUP DB #1 ]
           FILE NAME     : control_D20250915_T121208_L0_Q1.inc
           BACKUP LSN    : 241619
           BACKUP TIME   : 2025-10-15 12:12:08.658602
           BACKUP OBJECT : control
  [ BACKUP DB #2 ]
           FILE NAME     : database_D20250915_T121210_L0_Q2_P0.inc
           BACKUP LSN    : 241621
           BACKUP LEVEL  : 0
           PIECE SEQ     : 0
           BACKUP TIME   : 2025-10-15 12:12:11.508272
           BACKUP OBJECT : database
  [ BACKUP DB #3 ]
           FILE NAME     : control_D20250915_T121211_L0_Q3.inc
           BACKUP LSN    : 241621
           BACKUP TIME   : 2025-10-15 12:12:11.647210
           BACKUP OBJECT : control
```

<a id="2a28f7460b064f8e"></a>
### Datafile

- 데이터 파일 system_dict.dbf의 첫 번째 page를 덤프한다.

```
$ gdump datafile system_dict.dbf --silent

  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 0
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(EXT_BLOCK_MAP), RELATION_TYPE(NONDEFINED), FREENESS(FREE), LSN(16463), TIMESTAMP(1760497867007267), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0.0.0), AGABLE SCN(0.0.0), SELF ID(0,0)
----------------------------------------------------------------------------
 0000    0200000004000000 4F40000000000000 23A5FDD929410600 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0000000000000000 0200000000000000
 0060    0000000000000000 0000000000000000 0000FFFF00000000 0400000001000000
 0080    0200000002000000 0320000001000000 0440000001000000 0560000001000000
```

- 데이터 파일 system_dict.dbf의 100 번째 page부터 세 개의 page를 덤프한다.

```
$ gdump datafile system_dict.dbf --number 100 --fetch 3 --silent

  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 100
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(BITMAP_HEADER), RELATION_TYPE(NONDEFINED), FREENESS(INSERTABLE), LSN(376), TIMESTAMP(1760497867007267), PARENT RID(0,57,4), SEGMENT ID(4294967297), MAX VIEW SCN(0.0.0), AGABLE SCN(0.0.-9223372036854775808), SELF ID(0,100)
----------------------------------------------------------------------------
 0000    0400000003000000 7801000000000000 23A5FDD929410600 0000390004000000
 0020    0100000001000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0000000000000080 40CB617800000000
 0060    0000000000000000 0000000000000000 0000FFFF64000000 010000000100FFFF
 0080    0100000064000000 0100000000000000 0000000000000000 0000000000000000
...

  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 101
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(BITMAP_HEADER), RELATION_TYPE(NONDEFINED), FREENESS(INSERTABLE), LSN(381), TIMESTAMP(1760497867007267), PARENT RID(0,58,4), SEGMENT ID(4294967297), MAX VIEW SCN(0.0.0), AGABLE SCN(0.0.-9223372036854775808), SELF ID(0,101)
----------------------------------------------------------------------------
 0000    0400000003000000 7D01000000000000 23A5FDD929410600 00003A0004000000
 0020    0100000001000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0000000000000080 40CC617800000000
 0060    0000000000000000 0000000000000000 0000FFFF65000000 010000000100FFFF
 0080    0100000065000000 0100000000000000 0000000000000000 0000000000000000
...

  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 102
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(BITMAP_HEADER), RELATION_TYPE(NONDEFINED), FREENESS(INSERTABLE), LSN(386), TIMESTAMP(1760497867007267), PARENT RID(0,59,4), SEGMENT ID(4294967297), MAX VIEW SCN(0.0.0), AGABLE SCN(0.0.-9223372036854775808), SELF ID(0,102)
----------------------------------------------------------------------------
 0000    0400000003000000 8201000000000000 23A5FDD929410600 00003B0004000000
 0020    0100000001000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0000000000000080 80CD617800000000
 0060    0000000000000000 0000000000000000 0000FFFF66000000 010000000100FFFF
 0080    0100000066000000 0100000000000000 0000000000000000 0000000000000000
...
```

- 데이터 파일 system_dict.dbf의 header를 덤프한다.

```
$ % gdump datafile system_dict.dbf --header --silent
  FILE                   : system_dict.dbf
  Tablespace Physical Id : 0
  Datafile Id            : 0
  Last Checkpoint Lsn    : 241621
  Last Checkpoint Lid    : (0, 113546, 13)
  Stable Lsn             : 241620
  Creation TIME          : 2025-10-15 12:11:07.007267
  Database signature     : 96B3E2F4A97411F0AF329989273B4AC8
  Database file sequence : 0
```

<a id="dc7f4a19f914ef77"></a>
### Log file

- 온라인 redo log file인 redo_0_0.log 전체를 덤프한다.

```
$ gdump redo_log redo_0_0.log --silent

===========================================================
 [LOG FILE HEADER]
-----------------------------------------------------------
 LOG_GROUP_ID    : 0
 BLOCK_SIZE      : 512
 FILE_SIZE       : 104857600
 FILE_SEQUENCE   : 0
 PREV_LAST_LSN   : -1
 CREATION TIME   : 2025-10-15 12:11:06.103257
 SIGNATURE       : 96B3E2F4A97411F0AF329989273B4AC8
 SWITCH OFF TIME : 1970-01-01 09:00:00.000000
 SWITCH OFF SCN  : (0.0.0)
===========================================================

[LOG #0] : BLOCK(0), LSN(0), SIZE(1148), PIECE_COUNT(1), TRANS_ID(FFFFFFFFFFFF0001), TRANS_SEQ(0), RID(0,0,0)
[PIECE #0] : TYPE(FILE_CREATE), SIZE(1132), CLASS(DATAFILE), REDO_TYPE(DATAFILE), PROPAGATE_LOG(YES), RID(0,0,0)
 000000002F686F6D 652F6D6B6B696D32 2F776F726B2F7072 6F647563742F476C    ..../home/mkkim2 /work/product/Gl
 696573652F686F6D 652F64622F737973 74656D5F64696374 2E64626600000000    iese/home/db/system_dict .dbf....
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........

... 이하 생략 ...
```

- redo_0_0.log의 100번 log sequence number에서 다섯 개의 offset만큼 떨어진 log로부터 세 개의 log를 덤프한다.

```
$ gdump redo_log redo_0_0.log --number 100 --offset 5 --fetch 3 --silent

===========================================================
 [LOG FILE HEADER]
-----------------------------------------------------------
 LOG_GROUP_ID    : 0
 BLOCK_SIZE      : 512
 FILE_SIZE       : 104857600
 FILE_SEQUENCE   : 0
 PREV_LAST_LSN   : -1
 CREATION TIME   : 2025-10-15 12:11:06.103257
 SIGNATURE       : 96B3E2F4A97411F0AF329989273B4AC8
 SWITCH OFF TIME : 1970-01-01 09:00:00.000000
 SWITCH OFF SCN  : (0.0.0)
===========================================================

[LOG #0] : BLOCK(117), LSN(105), SIZE(41), PIECE_COUNT(2), TRANS_ID(FFFFFFFFFFFF0001), TRANS_SEQ(0), RID(0,0,18)
[PIECE #0] : TYPE(INIT_RELATION_HEADER), SIZE(8), CLASS(ACCESS), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,232,18)
 0500000000000000                                                       ........                           
[PIECE #1] : TYPE(BYTES), SIZE(1), CLASS(RECOVERY), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,210,18)
 01                                                                     .                                  

[LOG #1] : BLOCK(117), LSN(106), SIZE(1088), PIECE_COUNT(8), TRANS_ID(FFFFFFFFFFFF0001), TRANS_SEQ(0), RID(0,0,0)
[PIECE #0] : TYPE(INIT_PAGE), SIZE(120), CLASS(PAGE_ACCESS), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,0,51)
 0100000004000000 0000000000000000 23A5FDD929410600 0000FFFF00000000    ........ ........ #...)A.. ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000FFFF33000000                     ........ ........ ....3...         
[PIECE #1] : TYPE(INIT_PAGE), SIZE(120), CLASS(PAGE_ACCESS), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,0,52)
 0100000004000000 0000000000000000 23A5FDD929410600 0000FFFF00000000    ........ ........ #...)A.. ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000FFFF34000000                     ........ ........ ....4...         
[PIECE #2] : TYPE(INIT_PAGE), SIZE(120), CLASS(PAGE_ACCESS), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,0,53)
 0100000004000000 0000000000000000 23A5FDD929410600 0000FFFF00000000    ........ ........ #...)A.. ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000FFFF35000000                     ........ ........ ....5...         
[PIECE #3] : TYPE(INIT_PAGE), SIZE(120), CLASS(PAGE_ACCESS), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,0,54)
 0100000004000000 0000000000000000 23A5FDD929410600 0000FFFF00000000    ........ ........ #...)A.. ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000FFFF36000000                     ........ ........ ....6...         
[PIECE #4] : TYPE(INIT_PAGE), SIZE(120), CLASS(PAGE_ACCESS), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,0,55)
 0100000004000000 0000000000000000 23A5FDD929410600 0000FFFF00000000    ........ ........ #...)A.. ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000FFFF37000000                     ........ ........ ....7...         
[PIECE #5] : TYPE(INIT_PAGE), SIZE(120), CLASS(PAGE_ACCESS), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,0,56)
 0100000004000000 0000000000000000 23A5FDD929410600 0000FFFF00000000    ........ ........ #...)A.. ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000FFFF38000000                     ........ ........ ....8...         
[PIECE #6] : TYPE(INIT_PAGE), SIZE(120), CLASS(PAGE_ACCESS), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,0,57)
 0100000004000000 0000000000000000 23A5FDD929410600 0000FFFF00000000    ........ ........ #...)A.. ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000FFFF39000000                     ........ ........ ....9...         
[PIECE #7] : TYPE(INIT_PAGE), SIZE(120), CLASS(PAGE_ACCESS), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,0,58)
 0100000004000000 0000000000000000 23A5FDD929410600 0000FFFF00000000    ........ ........ #...)A.. ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000FFFF3A000000                     ........ ........ ....:...         

[LOG #2] : BLOCK(119), LSN(107), SIZE(40), PIECE_COUNT(2), TRANS_ID(FFFFFFFFFFFF0001), TRANS_SEQ(0), RID(0,0,1)
[PIECE #0] : TYPE(ALLOC_EXTENT), SIZE(0), CLASS(TABLESPACE), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,6,2)
[PIECE #1] : TYPE(BITMAP_ADD_EXTENT), SIZE(8), CLASS(SEGMENT), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,2,3)
 0600020000000000                                                       ........
```

<a id="2056a86f3fde7d28"></a>
### Incremental Backup File

- Incremental backup 정보를 덤프한다.
    - 다음과 같이 database_D20250915_T121207_L0_Q0_P0.inc에서 파일의 헤더와 테일만 덤프한다.

```
$ gdump backup database_D20250915_T121207_L0_Q0_P0.inc --silent

 INCREMENTAL BACKUP FILE HEADER 
----------------------------------------------------------------------------
  Backup object                                      : DATABASE
  Datafile count                                     : 5
  Backup body size                                   : 146137088
  Last checkpoint lsn of previous incremental backup : 0
  Max page lsn of incremental backup                 : 241619
  Last checkpoint lsn of incremental backup          : 241619
  Last checkpoint lid of incremental backup          : (0, 113545, 13)
  Stable lsn                                         : 241619
  Database signature                                 : 96B3E2F4A97411F0AF329989273B4AC8
----------------------------------------------------------------------------

 INCREMENTAL BACKUP FILE TAIL
----------------------------------------------------------------------------

 List of backed up tablespaces : 
----------------------------------------------------------------------------
  Tablespace id(0) : datafile id(0), backup page count(15158), total page count(32765)
  Tablespace id(1) : datafile id(0), backup page count(2090), total page count(4090)
  Tablespace id(2) : datafile id(0), backup page count(197), total page count(25573)
  Tablespace id(4) : datafile id(0), backup page count(5), total page count(25573)
  Tablespace id(5) : datafile id(0), backup page count(389), total page count(25573)
```

- Incremental backup 전체 페이지에 대해 페이지 헤더와 페이지 바디를 덤프한다.
    - 다음과 같이 database_D20250915_T121207_L0_Q0_P0.inc에서 모든 테이블스페이스의 전체 페이지를 덤프한다.

```
$ gdump backup database_D20250915_T121207_L0_Q0_P0.inc --silent --body all

 INCREMENTAL BACKUP FILE HEADER 
----------------------------------------------------------------------------
  Backup object                                      : DATABASE
  Datafile count                                     : 5
  Backup body size                                   : 146137088
  Last checkpoint lsn of previous incremental backup : 0
  Max page lsn of incremental backup                 : 241619
  Last checkpoint lsn of incremental backup          : 241619
  Last checkpoint lid of incremental backup          : (0, 113545, 13)
  Stable lsn                                         : 241619
  Database signature                                 : 96B3E2F4A97411F0AF329989273B4AC8
----------------------------------------------------------------------------

 INCREMENTAL BACKUP FILE TAIL
----------------------------------------------------------------------------

 List of backed up tablespaces : 
----------------------------------------------------------------------------
  Tablespace id(0) : datafile id(0), backup page count(15158), total page count(32765)
  Tablespace id(1) : datafile id(0), backup page count(2090), total page count(4090)
  Tablespace id(2) : datafile id(0), backup page count(197), total page count(25573)
  Tablespace id(4) : datafile id(0), backup page count(5), total page count(25573)
  Tablespace id(5) : datafile id(0), backup page count(389), total page count(25573)

  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 0
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(EXT_BLOCK_MAP), RELATION_TYPE(NONDEFINED), FREENESS(FREE), LSN(16463), TIMESTAMP(1760497867007267), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0.0.0), AGABLE SCN(0.0.0), SELF ID(0,0)
----------------------------------------------------------------------------
 0000    020000000400FF7F 4F40000000000000 23A5FDD929410600 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0060    0000000000000000 0000000000000000 0000FFFF00000000 0400000001000000
 0080    0200000002000000 0320000001000000 0440000001000000 0560000001000000

... 중략 ...

  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 2
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(EXT_MAP), RELATION_TYPE(NONDEFINED), FREENESS(FULL), LSN(16461), TIMESTAMP(1760497867007267), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0.0.0), AGABLE SCN(0.0.0), SELF ID(0,2)
----------------------------------------------------------------------------
 0000    030000000100FF7F 4D40000000000000 23A5FDD929410600 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0060    0000000000000000 0000000000000000 0000FFFF02000000 0004000400040000
 0080    FFFFFFFFFFFFFFFF FFFFFFFFFFFFFFFF FFFFFFFFFFFFFFFF FFFFFFFFFFFFFFFF

... 이하 생략 ...
```

- Incremental backup에 지정된 수보다 큰 페이지에 대해 페이지 헤더와 페이지 바디를 덤프한다.
    - 다음과 같이 database_D20250915_T121207_L0_Q0_P0.inc에서 모든 테이블스페이스의 10,000번 이상인 페이지를 덤프한다.

```
$ gdump backup database_D20250915_T121207_L0_Q0_P0.inc --silent --number 10000 --body all

 INCREMENTAL BACKUP FILE HEADER 
----------------------------------------------------------------------------
  Backup object                                      : DATABASE
  Datafile count                                     : 5
  Backup body size                                   : 146137088
  Last checkpoint lsn of previous incremental backup : 0
  Max page lsn of incremental backup                 : 241619
  Last checkpoint lsn of incremental backup          : 241619
  Last checkpoint lid of incremental backup          : (0, 113545, 13)
  Stable lsn                                         : 241619
  Database signature                                 : 96B3E2F4A97411F0AF329989273B4AC8
----------------------------------------------------------------------------

 INCREMENTAL BACKUP FILE TAIL
----------------------------------------------------------------------------

 List of backed up tablespaces : 
----------------------------------------------------------------------------
  Tablespace id(0) : datafile id(0), backup page count(15158), total page count(32765)
  Tablespace id(1) : datafile id(0), backup page count(2090), total page count(4090)
  Tablespace id(2) : datafile id(0), backup page count(197), total page count(25573)
  Tablespace id(4) : datafile id(0), backup page count(5), total page count(25573)
  Tablespace id(5) : datafile id(0), backup page count(389), total page count(25573)

  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 16388
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(EXT_MAP), RELATION_TYPE(NONDEFINED), FREENESS(FREE), LSN(211231), TIMESTAMP(1760497867007267), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0.0.0), AGABLE SCN(0.0.0), SELF ID(0,16388)
----------------------------------------------------------------------------
 0000    0300000004000000 1F39030000000000 23A5FDD929410600 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0060    0000000000000000 0000000000000000 0000FFFF04400000 000400043603CA00
 0080    FFFFFFFFFFFFFFFF FFFFFFFFFFFFFFFF FFFFFFFFFFFFFFFF FFFFFFFFFFFFFFFF

... 중략 ...

  TABLESPACE ID : 2
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 16387
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(EXT_MAP), RELATION_TYPE(NONDEFINED), FREENESS(FREE), LSN(26), TIMESTAMP(1760497868175032), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0.0.0), AGABLE SCN(0.0.0), SELF ID(2,16387)
----------------------------------------------------------------------------
 0000    030000000400FF7F 1A00000000000000 B8760FDA29410600 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0060    0000000000000000 0000000000000000 0200FFFF03400000 0001000100000001
 0080    0000000000000000 0000000000000000 0000000000000000 0000000000000000

... 이하 생략 ...
```

- Incremental backup의 지정된 테이블스페이스의 지정된 수에 대한 페이지 헤더와 바디를 덤프한다.
    - 다음과 같이 database_D20250915_T121207_L0_Q0_P0.inc에서 테이블스페이스 0번의 1000번 페이지를 덤프한다.

```
$ gdump backup database_D20250915_T121207_L0_Q0_P0.inc --tbs 0 --number 1000 --body all --fetch 1 --silent

 INCREMENTAL BACKUP FILE HEADER 
----------------------------------------------------------------------------
  Backup object                                      : DATABASE
  Datafile count                                     : 5
  Backup body size                                   : 146137088
  Last checkpoint lsn of previous incremental backup : 0
  Max page lsn of incremental backup                 : 241619
  Last checkpoint lsn of incremental backup          : 241619
  Last checkpoint lid of incremental backup          : (0, 113545, 13)
  Stable lsn                                         : 241619
  Database signature                                 : 96B3E2F4A97411F0AF329989273B4AC8
----------------------------------------------------------------------------

 INCREMENTAL BACKUP FILE TAIL
----------------------------------------------------------------------------

 List of backed up tablespaces : 
----------------------------------------------------------------------------
  Tablespace id(0) : datafile id(0), backup page count(15158), total page count(32765)
  Tablespace id(1) : datafile id(0), backup page count(2090), total page count(4090)
  Tablespace id(2) : datafile id(0), backup page count(197), total page count(25573)
  Tablespace id(4) : datafile id(0), backup page count(5), total page count(25573)
  Tablespace id(5) : datafile id(0), backup page count(389), total page count(25573)

  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 1000
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(UNFORMAT), RELATION_TYPE(NONDEFINED), FREENESS(FREE), LSN(1120), TIMESTAMP(1760497867007267), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0.0.0), AGABLE SCN(0.0.0), SELF ID(0,1
000)
----------------------------------------------------------------------------
 0000    010000000400FF7F 6004000000000000 23A5FDD929410600 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0060    0000000000000000 0000000000000000 0000FFFFE8030000 0000000000000000
 0080    0000000000000000 0000000000000000 0000000000000000 0000000000000000

... 이하 생략 ...
```

<a id="8aaceaedbb3fa62a"></a>
### Property File

- 다음과 같이 gsql을 이용하여 property 중 하나인 PAGE_CHECKSUM_TYPE을 설정한다.

```
gSQL> ALTER SYSTEM SET PAGE_CHECKSUM_TYPE = 1 SCOPE = BOTH;

System altered.
```

- 다음과 같이 GOLDILOCKS의 binary 프로퍼티 파일을 덤프한다.

```
$ gdump property goldilocks.properties.binary --silent
PAGE_CHECKSUM_TYPE = 1
```

<a id="6129caaef3c5ec45"></a>
### Commit Log

다음과 같이 commit log file을 덤프한다.

```
$ gdump commit_log commit_0.log --silent

===========================================================
 [COMMIT LOG FILE HEADER]
-----------------------------------------------------------
 FILE_SEQUENCE   : 0
 FILE_SIZE       : 1048576
 MAX_BLOCK_COUNT : 2047
 BLOCK_SIZE      : 512
 SIGNATURE       : 8C00055EA8CF11F0891F61BAF91C7701
===========================================================

[BLOCK(0), LOG_COUNT(8)]
 TRANS_ID(3.2.30081087), COMMIT_SCN(120.0.63218), INDOUBT_BEHAVIOR(FORGET), PREV_LOG_FILE_SEQ(-1), PREV_LOG_BLOCK_SEQ(-1), PREV_LOG_SLOT_SEQ(-1) 
 TRANS_ID(1.0.1179711), COMMIT_SCN(81.0.62673), INDOUBT_BEHAVIOR(FORGET), PREV_LOG_FILE_SEQ(-1), PREV_LOG_BLOCK_SEQ(-1), PREV_LOG_SLOT_SEQ(-1) 

.. 이하 생략 ..
```

<a id="50a480119d4dbd74"></a>
### Log Buffer File

다음과 같이 gsyncher를 실행한 후에 생성된 log buffer file을 덤프한다.  
자세한 내용은 [gsyncher](48-gsyncher.md#81f32f04a959c43f)를 참조한다.

```
$ gdump log_buffer logbuffer.log --silent

===========================================================
 [LOG BUFFER FILE HEADER]
-----------------------------------------------------------
 REAR_FILE_BLOCK_SEQ_NO   : 203410
 FRONT_FILE_BLOCK_SEQ_NO  : 203410
 REAR_SBSN                : 797213
 REAR_LSN                 : 375933
 REAR_LID                 : (3, 3254496, 161)
 FRONT_SBSN               : 797212
 FRONT_LSN                : 375933
 FILE_SEQ_NO              : 3
 BUFFER_SIZE              : 10485760
 BUFFER_BLOCK_COUNT       : 20480
 BLOCK_OFFSET             : 13
 GROUP_COMMIT_LSN         : 336688
 LOG_SWITCHING_SBSN       : -1
===========================================================
```

<a id="60a4b7ba58c1ad08"></a>
### Pending Log Buffer File

다음과 같이 gsyncher를 실행한 후에 생성된 pending log buffer file을 덤프한다.  
자세한 내용은 [gsyncher](48-gsyncher.md#81f32f04a959c43f)를 참조한다.

```
$ gdump pend_buffer pendbuffer.log --silent

===========================================================
 [PEND LOG BUFFER FILE HEADER]
 PEND_LOG_BUFFER COUNT : 4
-----------------------------------------------------------
 PEND_LOG_BUFFER NO. : 0
 PEND_BUFFER_SIZE    : 1048576
 BUFFER_BLOCK_COUNT  : 16384
 FRONT_PBSN          : 102
 REAR_PBSN           : 102
 FRONT_LSN           : -1
 REAR_LSN            : 327055
-----------------------------------------------------------
 PEND_LOG_BUFFER NO. : 1
 PEND_BUFFER_SIZE    : 1048576
 BUFFER_BLOCK_COUNT  : 16384
 FRONT_PBSN          : 0
 REAR_PBSN           : 0
 FRONT_LSN           : -1
 REAR_LSN            : -1
-----------------------------------------------------------
 PEND_LOG_BUFFER NO. : 2
 PEND_BUFFER_SIZE    : 1048576
 BUFFER_BLOCK_COUNT  : 16384
 FRONT_PBSN          : 0
 REAR_PBSN           : 0
 FRONT_LSN           : -1
 REAR_LSN            : -1
-----------------------------------------------------------
 PEND_LOG_BUFFER NO. : 3
 PEND_BUFFER_SIZE    : 1048576
 BUFFER_BLOCK_COUNT  : 16384
 FRONT_PBSN          : 0
 REAR_PBSN           : 0
 FRONT_LSN           : -1
 REAR_LSN            : -1
-----------------------------------------------------------
===========================================================
```

<a id="d109c7846c9e9a1c"></a>
### Location

다음과 같이 location file을 덤프한다.

```
$ gdump location location.ctl --silent

 [G1N2]
   CLUSTER_MEMBER_HOST : 127.0.0.1
   CLUSTER_MEMBER_PORT : 11250

 [G2N2]
   CLUSTER_MEMBER_HOST : 127.0.0.1
   CLUSTER_MEMBER_PORT : 12250

 [G2N1]
   CLUSTER_MEMBER_HOST : 127.0.0.1
   CLUSTER_MEMBER_PORT : 12150

 [G3N1]
   CLUSTER_MEMBER_HOST : 127.0.0.1
   CLUSTER_MEMBER_PORT : 13150

 [G3N2]
   CLUSTER_MEMBER_HOST : 127.0.0.1
   CLUSTER_MEMBER_PORT : 13250

 [G1N1]
   CLUSTER_MEMBER_HOST : 127.0.0.1
   CLUSTER_MEMBER_PORT : 11150
```

<a id="9d45eb672b79279b"></a>
### Change Tracking File

- Change tracking file을 덤프한다.
    - 다음과 같이 gl_change_tracking_file.ctf에서 파일의 헤더만 덤프한다.

```
$ gdump change_track gl_change_tracking_file.ctf --silent --header

===========================================================
 [CHANGE TRACKING FILE HEADER]
-----------------------------------------------------------
 FILE                              : gl_change_tracking_file.ctf
 Bitmap Block Count                : 2
 Change Tracking Extent Page Count : 32
 Last Checkpoint Lsn               : 266948
 Creation TIME                     : 2026-06-30 14:11:52.028413
 Database signature                : 8A802748744111F1B7547DCB04412231
 Checksum                          : 1163808367
===========================================================
```

- Change tracking file 에 저장된 정보 중에 4번 tablespace에 해당하는 정보만 덤프한다.

```
$ gdump change_track gl_change_tracking_file.ctf --silent --tbs 4

===========================================================
 [CHANGE TRACKING FILE HEADER]
-----------------------------------------------------------
 FILE                              : gl_change_tracking_file.ctf
 Bitmap Block Count                : 2
 Change Tracking Extent Page Count : 32
 Last Checkpoint Lsn               : 266948
 Creation TIME                     : 2026-06-30 14:11:52.028413
 Database signature                : 8A802748744111F1B7547DCB04412231
 Checksum                          : 1163808367
===========================================================

 [CHANGE TRACKING BLOCK SECTION]
-----------------------------------------------------------

 [TABLESPACE(4), DATAFILE(0)] - state(enabled)
---------------------------------------------------------------------------------------------------
[      0:F] [     32:F] [     64:F] [     96:F] [    128:F] [    160:F] [    192:F] [    224:F] 
[    256:F] 
---------------------------------------------------------------------------------------------------
```

- Change tracking file 에 저장된 모든 정보를 덤프한다.

```
$ gdump change_track gl_change_tracking_file.ctf --silent

===========================================================
 [CHANGE TRACKING FILE HEADER]
-----------------------------------------------------------
 FILE                              : gl_change_tracking_file.ctf
 Bitmap Block Count                : 2
 Change Tracking Extent Page Count : 32
 Last Checkpoint Lsn               : 266948
 Creation TIME                     : 2026-06-30 14:11:52.028413
 Database signature                : 8A802748744111F1B7547DCB04412231
 Checksum                          : 1163808367
===========================================================

 [CHANGE TRACKING BLOCK SECTION]
-----------------------------------------------------------

 [TABLESPACE(4), DATAFILE(0)] - state(enabled)
---------------------------------------------------------------------------------------------------
[      0:F] [     32:F] [     64:F] [     96:F] [    128:F] [    160:F] [    192:F] [    224:F] 
[    256:F] 
---------------------------------------------------------------------------------------------------

 [TABLESPACE(7), DATAFILE(0)] - state(enabled)
---------------------------------------------------------------------------------------------------
[      0:F] [     32:F] [     64:F] [     96:F] [    128:F] [    160:F] [    192:F] [    224:F] 
[    256:F] 
---------------------------------------------------------------------------------------------------
```

---

[← 45. gloader/gloadernet (Upload/download Tool)](45-gloader-gloadernet-upload-download-tool.md) · [전체 목차](../README.md) · [47. tablediff →](47-tablediff.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
