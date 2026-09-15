<a id="2e68b28ee18d1919"></a>

# 35. gdump

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/2e68b28ee18d1919)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 34. gloader/gloadernet (Upload/download Tool)](34-gloader-gloadernet-upload-download-tool.md) · [Table of contents](../README.md) · [36. tablediff →](36-tablediff.md)

<a id="d88e06759b1143ba"></a>
## Overview of gdump

<a id="dad645a71067ce4d"></a>
### Definition

gdump is a utility provided by GOLDILOCKS, and it dumps the following binary files managed by the database in text form.

- Control file
- Datafile
- Log file
- Incremental backup file
- Property file
- Commit log file
- Log buffer file
- Pending log buffer file

<a id="941bed614a125f0a"></a>
### Argument

gdump usage is divided into the mandatory argument and the optional argument, and the optional arguments are used differently according to the file types to be dumped.

```
gdump file_type file_name [options]
```

<a id="ecdf6b8436d41631"></a>
#### Mandatory Argument

The mandatory argument is used in an order of the file type and and the file path.

```
file_type:  CONTROL | LOG | DATA | PROPERTY | BACKUP | COMMIT_LOG | LOG_BUFFER | PEND_BUFFER
file_name:  file name to dump
```

<a id="b1cf1d70eac506e7"></a>
##### file_type Argument

- CONTROL: It is a control file. It is located in *&lt;GOLDILOCKS_DATA&gt;/wal*, and its file extension is *.ctl*.
- Log: It is a log file(Online/Archived redo log file). It is located in *&lt;GOLDILOCKS_DATA&gt;/wal* or in *&lt;GOLDILOCKS_DATA&gt;/archive_log*, and its file extension is *.log*.
- DATA: It is a datafile. It is located in *&lt;GOLDILOCKS_DATA&gt;/db*, and its file extension is *.dbf*.
- PROPERTY: It is a binary property file. It is located in *&lt;GOLDILOCKS_DATA&gt;/conf*, and the default file name is *goldilocks.properties.binary*.
- BACKUP: It is an incremental backup file. It is located in *&lt;GOLDILOCKS_DATA&gt;/backup*, and its file extension is *.inc*.
- COMMIT_LOG: It is a commit.log file located in *&lt;GOLDILOCKS_DATA&gt;/wal*.
- LOG_BUFFER: It is a file of which a log buffer located in the memory is stored. The log buffer is stored in a file by executing gsyncher.
- PEND_BUFFER: It is a file of which a pending log buffer located in the memory is stored. The pending log buffer is stored in a file by executing gsyncher.

> An attempt to the dump of broken control file fails.

<a id="79d7289256ff2e7a"></a>
#### Optional Argument

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

<a id="f2730d7c40b78130"></a>
##### Description

<a id="5b326289b3bb0a27"></a>
<table><thead><tr><th align="center" valign="middle">Name</th><th align="center" valign="middle">Available<br>file type</th><th align="center" valign="middle">Description</th></tr></thead><tbody><tr><td valign="middle">--silent</td><td valign="middle">All</td><td valign="middle">It does not output copyright, version, the execution time.</td></tr><tr><td valign="middle">--section</td><td valign="middle">Control file</td><td valign="middle">It refers to the section of control file to be dumped.<br><ul><li>sys: System section</li><li>log: Log section</li><li>db: Database section</li><li>backup: Incremental backup section</li><li>all: All sections (The default value)</li></ul></td></tr><tr><td rowspan="2" valign="middle">--header</td><td valign="middle">Datafile</td><td valign="middle">It dumps only the header of the datafile.<br>If not set, it does not display the header.</td></tr><tr><td>Log file</td><td>It dumps only the header of the log file.</td></tr><tr><td rowspan="3" valign="middle">--number</td><td valign="middle">Datafile</td><td valign="middle">It is a page number to be dumped. (The default value is 0.)</td></tr><tr><td valign="middle">Log file</td><td valign="middle">It is a log number to be dumped. (The default value is 0, and it dumps the log bigger than the specified number.)</td></tr><tr><td valign="middle">Incremental backup file</td><td valign="middle">It is a page number to be dumped. (The default value is 0, and it dumps the page bigger than the specified number.)</td></tr><tr><td rowspan="3" valign="middle">--fetch</td><td valign="middle">Datafile</td><td valign="middle">It is a number of pages to be dumped. (The default value is 1.)</td></tr><tr><td valign="middle">Log file</td><td valign="middle">It is a number of logs to be dumped. (The default value is the whole logs.)</td></tr><tr><td valign="middle">Incremental backup file</td><td valign="middle">It is a number of pages to be dumped. (The default value is the whole pages.)</td></tr><tr><td valign="middle">--offset</td><td valign="middle">Log file</td><td valign="middle">It is valid only when --number option argument is set, and it refers to the position apart as far as offset from the value set in number. (The default value is 0.)</td></tr><tr><td valign="middle">--body</td><td valign="middle">Incremental backup file</td><td valign="middle">It displays the header of page (header) or the header and page (all).<br>If not set, it does not display anything. (The default value is none).</td></tr><tr><td valign="middle">--tbs</td><td valign="middle">Incremental backup file</td><td valign="middle">It is valid only when --body option is set.<br>It specifies the certain tablespace number in the incremental backup file.<br>If not set, it refers to all tablespace.</td></tr><tr><td>--all</td><td>Logl file</td><td>It dumps all including invalid logs.</td></tr></tbody></table>

> An option is not used when dumping the property file.

<a id="d3c23465cd227590"></a>
## Examples of Using gdump

<a id="e06e7ac97bfb34d0"></a>
### Control File

- Dumping system section

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

- Dumping log section

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

- Dumping database section

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

- Dumping incremental backup section

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

<a id="6dc461b4a41e2ece"></a>
### Datafile

- Dumping the first page of datafile *system_dict.dbf*

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

- Dumping three pages from the 100th page of datafile *system_dict.dbf*

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

- Dumping the header of datafile *system_dict.dbf*

```
$ gdump data system_dict.dbf --header --silent
  FILE                   : system_dict.dbf
  Tablespace Physical Id : 0
  Datafile Id            : 0
  Last Checkpoint Lsn    : 136976
  Creation TIME          : 2014-08-25 18:37:18.472006
```

<a id="bbe3b07ae20ee75f"></a>
### Log File

- It dumps all of online redo log file *redo_0_0.log.*

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

... Ellipsis ...
```

- It dumps three logs from a log which is away as far as five offsets from log sequence number 100 in *redo_0_0.log*.

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

<a id="c1fbd895a8d4dd44"></a>
### Incremental Backup File

- It dumps incremental backup information.
    - Only header and tail of file in *databaseD20140825T183902L0S0.inc* are dumped as follows.

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

- It dumps header and body of page for the entire page of incremental backup.
    - The entire page of all tablespaces in *databaseD20140825T183902L0S0.inc* is dumped as follows.

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
... Ellipsis ...
  TABLESPACE ID : 0
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 1
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(BITMAP_HEADER), FREENESS(FREE), LSN(100016), TIMESTAMP(1408959438472006), PARENT RID(0,-1,0), SEGMENT ID(4294967296), MAX VIEW SCN(0), AGABLE SCN(0), SELF ID(0,1)
----------------------------------------------------------------------------
 0000    0400000004000000 B086010000000000 4643D5EE70010500 0000FFFF00000000
 0020    0000000001000000 0000000000000000 0000000000000000 802A327800000000
 0040   
... Ellipsis ...

  TABLESPACE ID : 2
  DATAFILE ID : 0
  PAGE SEQUENCE ID : 24580
----------------------------------------------------------------------------
  [PHYSICAL HEADER] TYPE(EXT_MAP), FREENESS(FREE), LSN(24), TIMESTAMP(1408959441642963), PARENT RID(0,-1,0), SEGMENT ID(0), MAX VIEW SCN(0), AGABLE SCN(0), SELF ID(2,24580)
----------------------------------------------------------------------------
 0000    0300000004000000 1800000000000000 D3A505EF70010500 0000FFFF00000000
 0020    0000000000000000 0000000000000000 0000000000000000 0000000000000000
 0040    0000000000000000 0000000000000000 0200000004600000 1E001E0000001E00
... Ellipsis ...
```

- It dumps header and body of page whose page number is bigger than the specified number in incremental backup.
    - The pages whose page number is bigger than 1,000 of all tablespaces in *databaseD20140825T183902L0S0.inc *are dumped as follows.

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
... Ellipsis ...
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
... The rest is omitted ...
```

- It dumps header and body of page for the specified number of the specified tablespace in incremental backup.
    - The page of number 1,000 in the tablespace of number 0 in *database D20140825T183902L0S0.inc* is dumped as follows.

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
... The rest is omitted ...
```

<a id="1c7b5736ca21120b"></a>
### Property File

- PAGE_CHECKSUM_TYPE which is the one of the property is set by using gsql as follows.

```
gSQL> ALTER SYSTEM SET PAGE_CHECKSUM_TYPE = 1 SCOPE = BOTH;

System altered.
```

- The binary property file of GOLDILOCKS is dumped as follows.

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

<a id="fcd2084f1d5e9561"></a>
### Commit Log

The commit log file is dumped as follows.

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

<a id="a080b0d3b7d3be7f"></a>
### Log Buffer File

The log buffer file created after executing gsyncher is dumped as follows.  
For more information, refer to [gsyncher](37-gsyncher.md#cb2b01693453923e).

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

<a id="d3064d2557d756ec"></a>
### Pending Log Buffer File

The pending log buffer file created after executing gsyncher is dumped as follows.  
For more information, refer to [gsyncher](37-gsyncher.md#cb2b01693453923e).

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

[← 34. gloader/gloadernet (Upload/download Tool)](34-gloader-gloadernet-upload-download-tool.md) · [Table of contents](../README.md) · [36. tablediff →](36-tablediff.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
