<a id="a2ffdb24cdb1db88"></a>

# 43. gsyncher

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/a2ffdb24cdb1db88)  
> Tag: `22c.1_10_tag`

[← 42. tablediff](42-tablediff.md) · [Table of contents](../README.md) · [44. gmon →](44-gmon.md)

<a id="4a975aa3081f92ea"></a>
## Overview of gsyncher

<a id="c9ec8e7c9bea485e"></a>
### Definition

gsyncher is a utility provided by GOLDILOCKS, and which synchronizes the log of shared memory and the logfile of disk.  
When the server is abnormally terminated, gsyncher synchronizes the latest log of shared memory and the logfile, then records it.

<a id="3dd6ec6b0603a471"></a>
### Features

- gsyncher can not be executed during the server operation. 
- The STARTUP stage of the server in which gsyncher can be executed is OPEN phase. 
- When executing gsyncher, all other applications of the shared memory should be terminated. 
- During gsyncher execution, the logfile can be switched and in this case, the controlfile is generated.
- gsyncher backups the controlfile and logfile in which the logs are reflected, in advance.
- gsyncher can be executed after restoring the damaged controlfile.

<a id="5661a3ee9ef60835"></a>
### Usage

```
gsyncher [options]
```

<a id="f1e3ac217f9ebcc1"></a>
### Options

```
-l  --log               Log trace msg
-s  --silent            Do not print message
-f  --home              home directory
-c  --copy-right        Do not print copy right
-b  --backup-path       Backup directory
-h  --help              Print help message
```

<a id="8df0e1edbf5d5631"></a>
## Examples

- Example 1: gsyncher is executed during the server is normally operating.

```
$ gsyncher -l

[SHARED MEM] Attached to shm - Name(_STATIC), Key(21128)

[SHARED MEM] Detached from shm.

ERR-HY000(53002): gmaster is active
```

- Example 2: The server is not on the STARTUP stage on which gsyncher can be executed.

```
$ gsyncher -l

[SHARED MEM] Attached to shm - Name(_STATIC), Key(21128)

[SHARED MEM] Detached from shm.

ERR-HY000(53000): invalid phase(MOUNT): executable phase is OPEN
```

- Example 3: When executing gsyncher, the progress is displayed. The execution result is total buffer (0) bytes, and all logs are flushed to the logfile, so there is not a log to be synchronized.

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

    - gsyncher operations are recorded in logfile by using --log option.

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

- Example 4: The logs from lsn 130786 to lsn 131012 are flushed to the log group 1.

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

- Example 5: If the logfile switch occurs during gsyncher operation, it is reflected in the controlfile.

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

[← 42. tablediff](42-tablediff.md) · [Table of contents](../README.md) · [44. gmon →](44-gmon.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
