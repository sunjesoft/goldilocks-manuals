<a id="e9ec9dbb7f8caa83"></a>

# 46. gdump

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/e9ec9dbb7f8caa83)  
> Tag: `26c.1_0_tag`

[← 45. gloader/gloadernet (Upload/download Tool)](45-gloader-gloadernet-upload-download-tool.md) · [Table of contents](../README.md) · [47. tablediff →](47-tablediff.md)

<a id="6f1448c2ab6a0329"></a>
## Overview of gdump

<a id="a7036c23159bdba3"></a>
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
- Location
- Change tracking file

<a id="604eeb534e91a19a"></a>
### Argument

gdump usage is divided into the mandatory argument and the optional argument, and the optional arguments are used differently according to the file types to be dumped.

```
gdump file_type file_name [options]
```

<a id="9be3ea0af82db6fb"></a>
#### Mandatory Argument

The mandatory argument is used in an order of the file type and and the file path.

```
file_type: CONTROL | REDO_LOG | DATAFILE | PROPERTY | BACKUP | COMMIT_LOG | LOG_BUFFER | PEND_BUFFER | LOCATION | CHANGE_TRACK
file_name: file name to dump
```

<a id="3f2ffbd9ce3d5b86"></a>
##### file_type Argument

- CONTROL: It is a control file. It is located in *&lt;GOLDILOCKS_DATA&gt;/wal*, and its file extension is *.ctl*.
- REDO_LOG: It is a log file (online/archived redo log file). It is located in *&lt;GOLDILOCKS_DATA&gt;/wal* or in *&lt;GOLDILOCKS_DATA&gt;/archive_log*, and its file extension is *.log*.
- DATAFILE: It is a datafile. It is located in *&lt;GOLDILOCKS_DATA&gt;/db*, and its file extension is *.dbf*.
- PROPERTY: It is a binary property file. It is located in *&lt;GOLDILOCKS_DATA&gt;/conf*, and the default file name is *goldilocks.properties.binary*.
- BACKUP: It is an incremental backup file. It is located in *&lt;GOLDILOCKS_DATA&gt;/backup*, and its file extension is *.inc*.
- COMMIT_LOG: It is a commit.log file located in *&lt;GOLDILOCKS_DATA&gt;/wal*.
- LOG_BUFFER: It is a file of which a log buffer located in the memory is stored. The log buffer is stored in a file by executing gsyncher.
- PEND_BUFFER: It is a file of which a pending log buffer located in the memory is stored. The pending log buffer is stored in a file by executing gsyncher.
- LOCATION: It is the file that stores the location information of the members in the cluser.
- CHANGE_TRACK: It is a file containing the changed information during the incremental backup of a disk tablespace.

> An attempt to the dump of broken control file fails.

<a id="ecb5dfd1eedcbd87"></a>
#### Optional Argument

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

<a id="f9b8a5e929e3ac7b"></a>
##### Description

<a id="8a19d9a775d52cc2"></a>
<table><thead><tr><th align="center" valign="middle">Name</th><th align="center" valign="middle">Available<br>file type</th><th align="center" valign="middle">Description</th></tr></thead><tbody><tr><td valign="middle">--silent</td><td valign="middle">All</td><td valign="middle">It does not output copyright, version, the execution time.</td></tr><tr><td valign="middle">--section</td><td valign="middle">Control file</td><td valign="middle">It refers to the section of control file to be dumped.<br><ul><li>sys: System section</li><li>log: Log section</li><li>db: Database section</li><li>backup: Incremental backup section</li><li>all: All sections (The default value)</li></ul></td></tr><tr><td rowspan="2" valign="middle">--header</td><td valign="middle">Datafile</td><td valign="middle">It dumps only the header of the datafile.<br>If not set, it does not display the header.</td></tr><tr><td>Log file</td><td>It dumps only the header of the log file.</td></tr><tr><td rowspan="3" valign="middle">--number</td><td valign="middle">Datafile</td><td valign="middle">It is a page number to be dumped. (The default value is 0.)</td></tr><tr><td valign="middle">Log file</td><td valign="middle">It is a log number to be dumped. (The default value is 0, and it dumps the log bigger than the specified number.)</td></tr><tr><td valign="middle">Incremental backup file</td><td valign="middle">It is a page number to be dumped. (The default value is 0, and it dumps the page bigger than the specified number.)</td></tr><tr><td rowspan="3" valign="middle">--fetch</td><td valign="middle">Datafile</td><td valign="middle">It is a number of pages to be dumped. (The default value is 1.)</td></tr><tr><td valign="middle">Log file</td><td valign="middle">It is a number of logs to be dumped. (The default value is the whole logs.)</td></tr><tr><td valign="middle">Incremental backup file</td><td valign="middle">It is a number of pages to be dumped. (The default value is the whole pages.)</td></tr><tr><td valign="middle">--offset</td><td valign="middle">Log file</td><td valign="middle">It is valid only when --number option argument is set, and it refers to the position apart as far as offset from the value set in number. (The default value is 0.)</td></tr><tr><td valign="middle">--body</td><td valign="middle">Incremental backup file</td><td valign="middle">It displays the header of page (header) or the header and page (all).<br>If not set, it does not display anything. (The default value is none).</td></tr><tr><td valign="middle">--tbs</td><td valign="middle">Incremental backup file</td><td valign="middle">It is valid only when --body option is set.<br>It specifies the certain tablespace number in the incremental backup file.<br>If not set, it refers to all tablespace.</td></tr><tr><td>--all</td><td>Log file</td><td>It dumps all including invalid logs.</td></tr></tbody></table>

> An option is not used when dumping the property file.

<a id="70bdef2b6674b014"></a>
## Examples of Using gdump

<a id="eb7f7a14b1e5b6e8"></a>
### Control File

- Dumping system section

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

- Dumping log section

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

- Dumping database section

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

- Dumping incremental backup section

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

<a id="28698aec50bf60f5"></a>
### Datafile

- Dumping the first page of datafile *system_dict.dbf*

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

- Dumping three pages from the 100th page of datafile *system_dict.dbf*

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

- Dumping the header of datafile *system_dict.dbf*

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

<a id="68909bf5e3cd84ff"></a>
### Log File

- It dumps all of online redo log file *redo_0_0.log.*

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

... Ellipsis ...
```

- It dumps three logs from a log which is away as far as five offsets from log sequence number 100 in *redo_0_0.log*.

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

<a id="4c61be7ca01ecaf9"></a>
### Incremental Backup File

- It dumps incremental backup information.
    - Only header and tail of file in database_D20250915_T121207_L0_Q0_P0.inc are dumped as follows.

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

- It dumps header and body of page for the entire page of incremental backup.
    - The entire page of all tablespaces in database_D20250915_T121207_L0_Q0_P0.inc is dumped as follows.

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

... Ellipsis ...

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

... Ellipsis ...
```

- It dumps the header and the body of the page which is bigger than the specified number in incremental backup.
    - The pages which are bigger than 10,000 of all tablespaces in database_D20250915_T121207_L0_Q0_P0.inc are dumped as follows.

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

... Ellipsis ...

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

... Ellipsis ...
```

- It dumps the header and the body of page for the specified number of the specified tablespace in incremental backup.
    - The page of number 1,000 in the tablespace of number 0 in database_D20250915_T121207_L0_Q0_P0.inc is dumped as follows.

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

... Ellipsis ...
```

<a id="5c4ab7a6f1c4b633"></a>
### Property File

- PAGE_CHECKSUM_TYPE which is the one of the property is set by using gsql as follows.

```
gSQL> ALTER SYSTEM SET PAGE_CHECKSUM_TYPE = 1 SCOPE = BOTH;

System altered.
```

- The binary property file of GOLDILOCKS is dumped as follows.

```
$ gdump property goldilocks.properties.binary --silent
PAGE_CHECKSUM_TYPE = 1
```

<a id="e3d88fec853e6655"></a>
### Commit Log

The commit log file is dumped as follows.

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

.. Ellipsis ..
```

<a id="85b5b6d5078a476a"></a>
### Log Buffer File

The log buffer file created after executing gsyncher is dumped as follows.  
For more information, refer to [gsyncher](48-gsyncher.md#4e78be33fcfcdc9d).

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

<a id="540953665d5ffde5"></a>
### Pending Log Buffer File

The pending log buffer file created after executing gsyncher is dumped as follows.  
For more information, refer to [gsyncher](48-gsyncher.md#4e78be33fcfcdc9d).

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

<a id="3daeba5a3bd6c25b"></a>
### Location

The location file is dumped as follows.

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

<a id="4e096018a9453de1"></a>
### Change Tracking File

- It dumps the change tracking file.
    - It dumps only the header of the file gl_change_tracking_file.ctf.

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

- It dumps only the information for tablespace 4 stored in the change tracking file.

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

- It dumps all information stored in the change tracking file.

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

[← 45. gloader/gloadernet (Upload/download Tool)](45-gloader-gloadernet-upload-download-tool.md) · [Table of contents](../README.md) · [47. tablediff →](47-tablediff.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
