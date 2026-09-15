<a id="1f5f3388fc1982b2"></a>

# 35. gdump

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/1f5f3388fc1982b2)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 34. gloader/gloadernet (Upload/download Tool)](34-gloader-gloadernet-upload-download-tool.md) · [전체 목차](../README.md) · [36. tablediff →](36-tablediff.md)

<a id="88e0dc36db23cbb1"></a>
## gdump 개요

<a id="902fef42a38df548"></a>
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

<a id="1fcb6c553bc51878"></a>
### 인자

gdump는 필수 인자와 옵션 인자로 구분되어 사용되고 옵션 인자는 덤프하려는 파일의 유형에 따라 다르게 사용된다

```
gdump file_type file_name [options]
```

<a id="7e567e7b5e83da64"></a>
#### 필수 인자

필수 인자는 파일 유형, 파일 경로 순으로 사용된다.

```
file_type:  CONTROL | LOG | DATA | PROPERTY | BACKUP | COMMIT_LOG | LOG_BUFFER | PEND_BUFFER
file_name:  file name to dump
```

<a id="a4362ca86871fab9"></a>
##### file_type 인자

- CONTROL: Control file이다. &lt;GOLDILOCKS_DATA&gt;/wal 에 위치하고, 확장자는 .ctl 이다.
- Log: Log file (online/ archived redo log file) 이다. &lt;GOLDILOCKS_DATA&gt;/wal 또는 &lt;GOLDILOCKS_DATA&gt;/archive_log 에 위치하고, 확장자는 .log 이다.
- DATA: Datafile 이다. &lt;GOLDILOCKS_DATA&gt;/db에 위치하고 확장자는 .dbf 이다.
- PROPERTY: Binary property file을 의미한다. &lt;GOLDILOCKS_DATA&gt;/conf 에 위치하고 파일의 기본 이름은 goldilocks.properties.binary 이다.
- BACKUP: Incremental backup file을 의미한다. &lt;GOLDILOCKS_DATA&gt;/backup 에 위치하고, 확장자는 .inc 이다.
- COMMIT_LOG: &lt;GOLDILOCKS_DATA&gt;/wal 에 위치한 commit.log 파일이다.
- LOG_BUFFER: 메모리에 있는 log buffer를 file로 저장한 것이다. gsyncher를 실행하면 log buffer를 file로 저장한다.
- PEND_BUFFER: 메모리에 있는 pending log buffer를 file로 저장한 것이다. gsyncher를 실행하면 pending log buffer를 file로 저장한다.

> 깨진 control file에 대해 덤프를 시도하면 실패한다.

<a id="dd5fb13bc01f16bc"></a>
#### 옵션 인자

```
-S  --silent                                silent
   file_type = CONTROL
      -s, --section  sys | log | db | backup | all  dump controlfile section(default all)
   file_type = DATA
      -h, --header                          dump datafile header
      -n, --number   INTEGER ( >= 0 )       (log or page) sequence number
      -f, --fetch    INTEGER ( >= 1 )       dump as much as count
   file_type = LOG
      -h, --header
      -n, --number   INTEGER ( >= 0 )       (log or page) sequence number
      -o, --offset   INTEGER                offset of lsn(usable if set lsn)
      -f, --fetch    INTEGER ( >= 1 )       dump as much as count
      -a, --all 
   file_type = BACKUP
      -b, --body     header | all           dump incremental body(default all)
      -t, --tbs                             dump specific tablespace body(usage if set body)
      -n, --number   INTEGER ( >= 0 )       (log or page) sequence number
      -f, --fetch    INTEGER ( >= 1 )       dump as much as count
```

<a id="f26065b03c06eeac"></a>
##### 설명

<a id="36818ed67d1a1a38"></a>
<table><thead><tr><th align="center" valign="middle">인자 이름</th><th align="center" valign="middle">사용 가능한<br>파일 유형</th><th align="center" valign="middle">설명</th></tr></thead><tbody><tr><td valign="middle">--silent</td><td valign="middle">All</td><td valign="middle">Copyright와 version, 수행 시간 등을 표시하지 않는다.</td></tr><tr><td valign="middle">--section</td><td valign="middle">Control file</td><td valign="middle">덤프할 control file의 섹션을 의미한다.<br><ul><li>sys: System section</li><li>log: Log section</li><li>db: Database section</li><li>backup: Incremental backup section</li><li>all: All sections (기본값)</li></ul></td></tr><tr><td rowspan="2" valign="middle">--header</td><td valign="middle">Datafile</td><td valign="middle">Datafile을 덤프할 때 헤더만 덤프한다.<br>설정되지 않으면 헤더를 표시하지 않는다.</td></tr><tr><td valign="middle">Log file</td><td valign="middle">Log file을 덤프할 때 헤더만 덤프한다.</td></tr><tr><td rowspan="3" valign="middle">--number</td><td valign="middle">Datafile</td><td valign="middle">덤프할 page 번호를 나타낸다. (기본값은 0이다.)</td></tr><tr><td valign="middle">Log file</td><td valign="middle">덤프할 log 번호를 나타낸다. (기본값은 0이고 지정한 번호보다 큰 log를 덤프한다).</td></tr><tr><td valign="middle">Incremental backup file</td><td valign="middle">덤프할 page 번호를 나타낸다. (기본값은 0이고 지정한 번호보다 큰 page를 덤프한다).</td></tr><tr><td rowspan="3" valign="middle">--fetch</td><td valign="middle">Datafile</td><td valign="middle">덤프할 page 개수이다. (기본값은 1이다.)</td></tr><tr><td valign="middle">Log file</td><td valign="middle">덤프할 log 개수이다. (기본값은 전체 log이다.)</td></tr><tr><td valign="middle">Incremental backup file</td><td valign="middle">덤프할 page 개수이다. (기본값은 전체 page이다.)</td></tr><tr><td valign="middle">--offset</td><td valign="middle">Log file</td><td valign="middle">--number 옵션 인자가 설정되었을 때만 유효하고, number 인자에 설정된 값에서 offset만큼 떨어진 위치를 의미한다. (기본값은 0이다.)</td></tr><tr><td valign="middle">--body</td><td valign="middle">Incremental backup file</td><td valign="middle">Page의 헤더 (header) 또는 헤더와 페이지 (all)를 표시한다.<br>설정하지 않으면 아무것도 표시하지 않는다. (기본값은 none이다.)</td></tr><tr><td valign="middle">--tbs</td><td valign="middle">Incremental backup file</td><td valign="middle">--body 옵션 인자가 설정되었을 때만 유효하다.<br>Incremental backup file에서 특정 테이블스페이스 번호를 지정한다.<br>설정하지 않으면 모든 테이블스페이스를 의미한다.</td></tr><tr><td valign="middle">--all</td><td valign="middle">Logl file</td><td valign="middle">유효하지 않은 log를 포함하여 덤프한다.</td></tr></tbody></table>

> 프로퍼티 파일을 덤프할 때는 옵션을 사용하지 않는다.

<a id="9930f3723c0eaf7f"></a>
## 사용 예

<a id="29648d021126dd67"></a>
### Control File

- 시스템 영역 덤프

```
$ gdump control control_0.ctl --section sys --silent
 [SYSTEM SECTION]
-----------------------------------------------------------
  SERVER STATE                      : SERVICE
  DATA STORE MODE                   : TDS
  LAST CHECKPOINT LSN               : 136976
  INCREMENTAL BACKUP CHUNK COUNT    : 1
  INCREMENTAL BACKUP SECTION OFFSET : 512
  LOG  SECTION OFFSET               : 8704
  DB   SECTION OFFSET               : 13312
```

- 로그 영역 덤프

```
$ gdump control control_0.ctl --section log --silent
[LOG SECTION]
-----------------------------------------------------------
   DATABASE CREATION TIME : 2014-08-25 18:37:11.299610

  [CHECKPOINT]
    LID                               :  0,54834,13
    LSN                               :  136976
    RECOVERY LSN                      :  136976
    ARCHIVELOG MODE                   :  ARCHIVELOG
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
      MEMBER #0     : "/home/lkh/work/product/Gliese/home/wal/redo_0_0.log"
```

- Database 영역 덤프

```
$ gdump control control_0.ctl --section db --silent
 [DB SECTION]
-----------------------------------------------------------
  [DATABASE]
    TRANSACTION_TABLE_SIZE : 1024
    UNDO_RELATION_COUNT    : 128
    TABLESPACE COUNT       : 4
    NEW TABLESPACE ID      : 4

  [TABLESPACE #0] 
   NAME          :  DICTIONARY_TBS
   ATTRIBUTES    :  MEMORY | PERSISTENT | DICT
   STATE         :  CREATED
   LOGGING STATE :  LOGGING
   ONLINE STATE  :  ONLINE
   EXTENT_SIZE   :  8
   RELATION_ID   :  0

   [DATAFILE #0]
     SIZE  :  134209536
     STATE :  CREATED
     NAME  :  "/home/lkh/work/product/Gliese/home/db/system_dict.dbf"
```

- Incremental backup 영역 덤프

```
$ gdump control control_0.ctl --section backup --silent
[INCREMENTAL BACKUP SECTION]
-----------------------------------------------------------
[ BACKUP #0 ]
FILE PATH : /home/lkh/work/product/Gliese/home/backup/databaseD20140825T183902L0S0.inc
BACKUP LSN : 136976
BACKUP LEVEL : 0
BACKUP OBJECT : database
[ BACKUP #1 ]
FILE PATH : /home/lkh/work/product/Gliese/home/backup/controlD20140825T183904L0S0.inc
BACKUP LSN : 136976
BACKUP LEVEL : 0
BACKUP OBJECT : control
```

<a id="ca616365e97db16d"></a>
### Datafile

- 데이터 파일 system_dict.dbf의 첫 번째 page를 덤프한다.

```
$ gdump data system_dict.dbf --silent
  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 0
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(EXT_BLOCK_MAP), FREENESS(FREE), LSN(107938), TIMESTAMP(1408959438472006), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0), AGABLE SCN(0), SELF ID(0,0)
----------------------------------------------------------------------------
 0000    0200000004000000 A2A5010000000000 4643D5EE70010500 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0300000000000000
 0040    0000000000000000 0000000000000000 0000000000000000 0200000001000000
 0060    0200000001000000 0320000001000000 0000000000000000 0000000000000000
 0080    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 00A0    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 00C0    0000000000000000 0000000000000000 0000000000000000 0000000000000000
....
```

- 데이터 파일 system_dict.dbf의 100 번째 page부터 세 개의 page를 덤프한다.

```
$ gdump data system_dict.dbf --number 100 --fetch 3 --silent
  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 100
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(BITMAP_HEADER), FREENESS(INSERTABLE), LSN(348), TIMESTAMP(1408959438472006), PARENT RID(0,57,4), SEGMENT ID(4294967296), MAX VIEW SCN(0), AGABLE SCN(0), SELF ID(0,1
00)
----------------------------------------------------------------------------
 0000    0400000003000000 5C01000000000000 4643D5EE70010500 0000390004000000
 0020    0000000001000000 0000000000000000 0000000000000000 80C0317800000000
 0040    0000000000000000 0000000000000000 0000000064000000 0100000001000002
 0060    FFFFFFFFFFFFFFFF 0100000000000000 0000000000000000 0000000000000000
 0080    0000000000000000 0200000001000000 7303000072030000 6E00010000000000
 00A0    3700000000000000 0000000000000000 0000000000000000 0000000000000000
 00C0    0000000000000000 0000000000000000 0000000000000000 0000000000000000
....
 1FC0    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 1FE0    0000000000000000 0000000000000000 0000000000000000 5C01000000000000

  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 101
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(BITMAP_HEADER), FREENESS(INSERTABLE), LSN(353), TIMESTAMP(1408959438472006), PARENT RID(0,58,4), SEGMENT ID(4294967296), MAX VIEW SCN(0), AGABLE SCN(0), SELF ID(0,1
01)
----------------------------------------------------------------------------
 0000    0400000003000000 6101000000000000 4643D5EE70010500 00003A0004000000
 0020    0000000001000000 0000000000000000 0000000000000000 00BF317800000000
 0040    0000000000000000 0000000000000000 0000000065000000 0100000001000002
 0060    FFFFFFFFFFFFFFFF 0100000000000000 0000000000000000 0000000000000000
 0080    0000000000000000 0200000001000000 8303000082030000 7000010000000000
 00A0    3800000000000000 0000000000000000 0000000000000000 0000000000000000
 00C0    0000000000000000 0000000000000000 0000000000000000 0000000000000000
....
 1FC0    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 1FE0    0000000000000000 0000000000000000 0000000000000000 6101000000000000

  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 102
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(BITMAP_HEADER), FREENESS(INSERTABLE), LSN(358), TIMESTAMP(1408959438472006), PARENT RID(0,59,4), SEGMENT ID(4294967296), MAX VIEW SCN(0), AGABLE SCN(0), SELF ID(0,1
02)
----------------------------------------------------------------------------
 0000    0400000003000000 6601000000000000 4643D5EE70010500 00003B0004000000
 0020    0000000001000000 0000000000000000 0000000000000000 C0BD317800000000
 0040    0000000000000000 0000000000000000 0000000066000000 0100000001000002
 0060    FFFFFFFFFFFFFFFF 0100000000000000 0000000000000000 0000000000000000
 0080    0000000000000000 0200000001000000 9303000092030000 7200010000000000
 00A0    3900000000000000 0000000000000000 0000000000000000 0000000000000000
 00C0    0000000000000000 0000000000000000 0000000000000000 0000000000000000
....
```

- 데이터 파일 system_dict.dbf의 header를 덤프한다.

```
$ gdump data system_dict.dbf --header --silent
  FILE                   : system_dict.dbf
  Tablespace Physical Id : 0
  Datafile Id            : 0
  Last Checkpoint Lsn    : 136976
  Creation TIME          : 2014-08-25 18:37:18.472006
```

<a id="e584a544df4fe456"></a>
### Log File

- 온라인 redo log file인 redo_0_0.log 전체를 덤프한다.

```
$ gdump log redo_0_0.log --silent
===========================================================
 [LOG FILE HEADER]
-----------------------------------------------------------
 LOG_GROUP_ID    : 0
 BLOCK_SIZE      : 512
 FILE_SIZE       : 104857600
 FILE_SEQUENCE   : 0
 PREV_LAST_LSN   : -1
 CREATION TIME   : 2014-08-25 18:37:13.315283
===========================================================

[LOG #0] : BLOCK(0), LSN(0), SIZE(1132), PIECE_COUNT(1), TRANS_ID(FFFFFFFFFFFF0001), RID(0,-1,0)
[PIECE #0] : TYPE(MEMORY_FILE_CREATE), SIZE(1116), CLASS(DATAFILE), REDO_TYPE(CONTROL_FILE), PROPAGATE_LOG(YES), RID(0,0,0)
 FFFFFFFF2F686F6D 652F6C6B682F776F 726B2F70726F6475 63742F476C696573    ..../hom e/lkh/wo rk/produ ct/Glies
 652F686F6D652F64 622F73797374656D 5F646963742E6462 6600000000000000    e/home/d b/system _dict.db f.......
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
[LOG #1] : BLOCK(3), LSN(1), SIZE(232), PIECE_COUNT(1), TRANS_ID(FFFFFFFFFFFF0001), RID(0,0,0)
[PIECE #0] : TYPE(MEMORY_TBS_CREATE), SIZE(216), CLASS(DATAFILE), REDO_TYPE(CONTROL_FILE), PROPAGATE_LOG(YES), RID(0,0,0)

... 중략 ...
```

- redo_0_0.log의 100번 log sequence number에서 다섯 개의 offset만큼 떨어진 log로부터 세 개의 log를 덤프한다.

```
$ gdump log redo_0_0.log --number 100 --offset 5 --fetch 3 --silent

===========================================================
 [LOG FILE HEADER]
-----------------------------------------------------------
 LOG_GROUP_ID    : 0
 BLOCK_SIZE      : 512
 FILE_SIZE       : 104857600
 FILE_SEQUENCE   : 0
 PREV_LAST_LSN   : -1
 CREATION TIME   : 2014-08-25 18:37:13.315283
===========================================================

[LOG #0] : BLOCK(105), LSN(105), SIZE(24), PIECE_COUNT(1), TRANS_ID(FFFFFFFFFFFF0001), RID(0,0,55)
[PIECE #0] : TYPE(INIT_RELATION_HEADER), SIZE(8), CLASS(ACCESS), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,160,55)
 0A00000000000000                                                       ........                           

[LOG #1] : BLOCK(105), LSN(106), SIZE(240), PIECE_COUNT(4), TRANS_ID(FFFFFFFFFFFF0001), RID(0,0,56)
[PIECE #0] : TYPE(INIT_PAGE), SIZE(88), CLASS(PAGE_ACCESS), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,0,56)
 0400000004000000 0000000000000000 4643D5EE70010500 00000D0004000000    ........ ........ FC..p... ........
 0000000001000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 0000000038000000                     ........ ........ ....8...         
[PIECE #1] : TYPE(MEMORY_BITMAP_UPDATE_LEAF_STATUS), SIZE(24), CLASS(SEGMENT), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,13,4)
 0400000003000000 0000000000000000 0000000000000000                     ........ ........ ........         
[PIECE #2] : TYPE(BYTES), SIZE(8), CLASS(RECOVERY), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(0,4,56)
 0400000003000000                                                       ........                           

[LOG #2] : BLOCK(105), LSN(107), SIZE(832), PIECE_COUNT(8), TRANS_ID(FFFFFFFFFFFF0001), RID(0,-1,0)
[PIECE #0] : TYPE(INIT_PAGE), SIZE(88), CLASS(PAGE_ACCESS), REDO_TYPE(PAGE), PROPAGATE_LOG(YES), RID(1,0,178)
 0100000004000000 0000000000000000 BED7F8EE70010500 0000FFFF00000000    ........ ........ ....p... ........
 0000000000000000 0000000000000000 0000000000000000 0000000000000000    ........ ........ ........ ........
 0000000000000000 0000000000000000 01000000B2000000                     ........ ........ ........
```

<a id="5db4e4fb08bbf40a"></a>
### Incremental Backup File

- Incremental backup 정보를 덤프한다.
    - 다음과 같이 databaseD20140825T183902L0S0.inc에서 파일의 헤더와 테일만 덤프한다.

```
$ gdump backup databaseD20140825T183902L0S0.inc --silent

 INCREMENTAL FILE HEADER 
----------------------------------------------------------------------------
  OBJECT TYPE(DATABASE), TBS COUNT(3), BODY SIZE(62742528)
  LSN: PREV(0), MAX (136976), CHKPT(136976)
  CHKPT LID: File Seq No(0), Block Info1(877344), Block Info2(13)
----------------------------------------------------------------------------

 INCREMENTAL FILE TAIL
----------------------------------------------------------------------------
  TABLESPACE ID(000), BACKUP PAGE COUNT(05372), TABLESPACE OFFSET(8192)
  TABLESPACE ID(001), BACKUP PAGE COUNT(02090), TABLESPACE OFFSET(44015616)
  TABLESPACE ID(002), BACKUP PAGE COUNT(00197), TABLESPACE OFFSET(61136896)
```

- Incremental backup 전체 페이지에 대해 페이지 헤더와 페이지 바디를 덤프한다.
    - 다음과 같이 databaseD20140825T183902L0S0.inc에서 모든 테이블스페이스의 전체 페이지를 덤프한다.

```
$ gdump backup databaseD20140724T123414L0S0.inc --body all

 INCREMENTAL FILE HEADER 
----------------------------------------------------------------------------
  OBJECT TYPE(DATABASE), TBS COUNT(3), BODY SIZE(62742528)
  LSN: PREV(0), MAX (136976), CHKPT(136976)
  CHKPT LID: File Seq No(0), Block Info1(877344), Block Info2(13)
----------------------------------------------------------------------------

 INCREMENTAL FILE TAIL
----------------------------------------------------------------------------
  TABLESPACE ID(000), BACKUP PAGE COUNT(05372), TABLESPACE OFFSET(8192)
  TABLESPACE ID(001), BACKUP PAGE COUNT(02090), TABLESPACE OFFSET(44015616)
  TABLESPACE ID(002), BACKUP PAGE COUNT(00197), TABLESPACE OFFSET(61136896)

  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 0
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(EXT_BLOCK_MAP), FREENESS(FREE), LSN(107938), TIMESTAMP(1408959438472006), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0), AGABLE SCN(0), SELF ID(0,0)
----------------------------------------------------------------------------
 0000    0200000004000000 A2A5010000000000 4643D5EE70010500 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0000000000000000 0200000001000000
 0060    0200000001000000 0320000001000000 0000000000000000 0000000000000000
 0080    0000000000000000 0000000000000000 0000000000000000 0000000000000000
... 중략 ...
  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 1
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(BITMAP_HEADER), FREENESS(FREE), LSN(100016), TIMESTAMP(1408959438472006), PARENT RID(0,-1,0), SEGMENT ID(4294967296), MAX VIEW SCN(0), AGABLE SCN(0), SELF ID(0,1)
----------------------------------------------------------------------------
 0000    0400000004000000 B086010000000000 4643D5EE70010500 0000FFFF00000000
 0020    0000000001000000 0000000000000000 0000000000000000 802A327800000000
 0040   
... 중략 ...

  TABLESPACE ID : 2
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 24580
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(EXT_MAP), FREENESS(FREE), LSN(24), TIMESTAMP(1408959441642963), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0), AGABLE SCN(0), SELF ID(2,24580)
----------------------------------------------------------------------------
 0000    0300000004000000 1800000000000000 D3A505EF70010500 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0200000004600000 1E001E0000001E00
... 중략 ...
```

- Incremental backup에 지정된 수보다 큰 페이지에 대해 페이지 헤더와 페이지 바디를 덤프한다.
    - 다음과 같이 databaseD20140825T183902L0S0.inc에서 모든 테이블스페이스의 1000번 이상인 페이지를 덤프한다.

```
$ gdump backup databaseD20140724T123414L0S0.inc --number 10000 --body all
 INCREMENTAL FILE HEADER 
----------------------------------------------------------------------------
  OBJECT TYPE(DATABASE), TBS COUNT(3), BODY SIZE(62742528)
  LSN: PREV(0), MAX (136976), CHKPT(136976)
  CHKPT LID: File Seq No(0), Block Info1(877344), Block Info2(13)
----------------------------------------------------------------------------

 INCREMENTAL FILE TAIL
----------------------------------------------------------------------------
  TABLESPACE ID(000), BACKUP PAGE COUNT(05372), TABLESPACE OFFSET(8192)
  TABLESPACE ID(001), BACKUP PAGE COUNT(02090), TABLESPACE OFFSET(44015616)
  TABLESPACE ID(002), BACKUP PAGE COUNT(00197), TABLESPACE OFFSET(61136896)

  TABLESPACE ID : 2
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 16387
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(EXT_MAP), FREENESS(FREE), LSN(22), TIMESTAMP(1408959441642963), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0), AGABLE SCN(0), SELF ID(2,16387)
----------------------------------------------------------------------------
 0000    0300000004000000 1600000000000000 D3A505EF70010500 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0200000003400000 0001000100000001
 0060    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0080    0000000000000000 0000000000000000 0000000000000000 0000000000000000
... 중략 ...
  TABLESPACE ID : 2
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 24580
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(EXT_MAP), FREENESS(FREE), LSN(24), TIMESTAMP(1408959441642963), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0), AGABLE SCN(0), SELF ID(2,24580)
----------------------------------------------------------------------------
 0000    0300000004000000 1800000000000000 D3A505EF70010500 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0200000004600000 1E001E0000001E00
 0060    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0080    0000000000000000 0000000000000000 0000000000000000 0000000000000000
... 이하 생략 ...
```

- Incremental backup의 지정된 테이블스페이스의 지정된 수에 대한 페이지 헤더와 바디를 덤프한다.
    - 다음과 같이 database D20140825T183902L0S0.inc에서 테이블스페이스 0번의 1000번 페이지를 덤프한다.

```
gdump backup databaseD20140825T183902L0S0.inc --tbs 0 --number 1000 --body all --fetch 1 --silent | more

 INCREMENTAL FILE HEADER 
----------------------------------------------------------------------------
  OBJECT TYPE(DATABASE), TBS COUNT(3), BODY SIZE(62742528)
  LSN: PREV(0), MAX (136976), CHKPT(136976)
  CHKPT LID: File Seq No(0), Block Info1(877344), Block Info2(13)
----------------------------------------------------------------------------

 INCREMENTAL FILE TAIL
----------------------------------------------------------------------------
  TABLESPACE ID(000), BACKUP PAGE COUNT(05372), TABLESPACE OFFSET(8192)
  TABLESPACE ID(001), BACKUP PAGE COUNT(02090), TABLESPACE OFFSET(44015616)
  TABLESPACE ID(002), BACKUP PAGE COUNT(00197), TABLESPACE OFFSET(61136896)

  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 1000
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(UNFORMAT), FREENESS(FREE), LSN(6307), TIMESTAMP(1408959438472006), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0), AGABLE SCN(0), SELF ID(0,1000)
----------------------------------------------------------------------------
 0000    0100000004000000 A318000000000000 4643D5EE70010500 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 00000000E8030000 0000000000000000
 0060    0000000000000000 0000000000000000 0000000000000000 0000000000000000
... 이하 생략 ...
```

<a id="bb4c69e88633cb39"></a>
### Property File

- 다음과 같이 gsql을 이용하여 property 중 하나인 PAGE_CHECKSUM_TYPE을 설정한다.

```
gSQL> ALTER SYSTEM SET PAGE_CHECKSUM_TYPE = 1 SCOPE = BOTH;

System altered.
```

- 다음과 같이 GOLDILOCKS의 binary 프로퍼티 파일을 덤프한다.

```
$ gdump property goldilocks.properties.binary


===========================================================
FILE: goldilocks.properties.binary
TYPE: PROPERTY-BINARY
TIME: 2014-08-29 12:45:13.853448
===========================================================
PAGE_CHECKSUM_TYPE = 1

===========================================================
TIME: 2014-08-29 12:45:13.853627
===========================================================
```

<a id="f4c8ceb6d5b335ec"></a>
### Commit Log

다음과 같이 commit log file을 덤프한다.

```
$ gdump commit_log commit.log

===========================================================
FILE: commit.log
TYPE: COMMIT LOG FILE
TIME: 2017-03-23 11:47:42.555368
===========================================================

===========================================================
 [COMMIT LOG FILE HEADER]
-----------------------------------------------------------
 FILE_SEQUENCE   : 0
 FILE_SIZE       : 104857600
 MAX_BLOCK_COUNT : 204800
 SIGNATURE       : 5DAABFECBDCD11E68785A3701A679D47
===========================================================

[BLOCK(0), LOG_COUNT(1)]
 TRANS_ID(1.0.59899956), COMMIT_SCN(16603.645.17371), INDOUBT_BEHAVIOR(FORGET), SYNC_GLOBAL_TABLE_SCN(TRUE), PREV_LOG_FILE_SEQ(-1), PREV_LOG_BLOCK_SEQ(-1), PREV_LOG_SLOT_SEQ(-1)
```

<a id="448d2316e6d0ee35"></a>
### Log Buffer File

다음과 같이 gsyncher를 실행한 후에 생성된 log buffer file을 덤프한다.  
자세한 내용은 [gsyncher](37-gsyncher.md#d209d39e430501eb)를 참조한다.

```
$ gdump log_buffer logbuffer.log

===========================================================
FILE: logbuffer.log
TYPE: LOG BUFFER FILE
TIME: 2017-03-23 11:10:12.787400
===========================================================

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

<a id="8e2a4423eb818fb9"></a>
### Pending Log Buffer File

다음과 같이 gsyncher를 실행한 후에 생성된 pending log buffer file을 덤프한다.   
자세한 내용은 [gsyncher](37-gsyncher.md#d209d39e430501eb)를 참조한다.

```
$ gdump pend_buffer pendbuffer.log

===========================================================
FILE: pendbuffer.log
TYPE: PEND BUFFER FILE
TIME: 2017-03-23 11:10:29.603646
===========================================================

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

---

[← 34. gloader/gloadernet (Upload/download Tool)](34-gloader-gloadernet-upload-download-tool.md) · [전체 목차](../README.md) · [36. tablediff →](36-tablediff.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
