<a id="16d0bc3ea14d2e15"></a>

# 43. gtrclogger

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/16d0bc3ea14d2e15)  
> Tag: `20c.1_30_tag`

[← 42. gmon](42-gmon.md) · [Table of contents](../README.md) · [44. glocator →](44-glocator.md)

<a id="39cf802c31fd90d4"></a>
## Overview of gtrclogger

<a id="9ec89aa1ae9da1b3"></a>
### Definition

gtrclogger is a utility remotely collecting logs of GOLDILOCKS.

GOLDILOCKS basically records events and trace logs which occur in a server, in system.trc file of the specified directory of SYSTEM_LOGGER_DIR of property. (The default value is $GOLDILOCKS_DATA/trc)

If multiple different instances are being operated, trace logs occur in each server should be separately monitored. For that, gtrclogger makes trace logs of each different GOLDILOCKS instances to be collected in a single spot. gtrclogger receives trace logs of various GOLDILOCKS being operated in a different device with udp, and stores them in a file.

gtrclogger receives trace logs from the remote GOLDILOCKS and records them in a file. For that, the remote GOLDILOCKS should have the following transfer properties.

- TRACE_LOGGER
- TRACE_LOGGER_REMOTE_HOST
- TRACE_LOGGER_REMOTE_PORT

<a id="cc50a8f41ddac6e7"></a>
### Features

- gtrclogger can be operated regardless of server operation.
- Even when it receives trace logs from various servers, it sequentially stores them in a file.
- A trace log is basically stored as $(GOLDILOCKS_DATA)/trc/system.rmt.trc.
- If system.rmt.trc is bigger than 10M bytes , it is backuped as system.rmt.trc_*date*_Index.

<a id="b1814fd423e1d544"></a>
### Usage

```
gtrclogger [options]
```

<a id="a2017c3dae95f765"></a>
### Options

```
-s  --start        start gtrclogger
-q  --stop         stop gtrclogger
-p  --port         udp port for receive log (1024 ~ 49151): default 21470
-d  --dir          write file directory: default $(GOLDILOCKS_DATA)/system.rmt.trc
-h  --help         show gtrclogger help messages
```

<a id="cb726a85ba2d20a9"></a>
## Examples

- Example 1: Execute gtrclogger by using the default port (21470) and the default directory($GOLDILOCKS_DATA/trc).

```
$ gtrclogger --start

gtrclogger is started successfully.
```

- Example 2: Receive a trace log with two ports (21471, 21472) and set the directory as $GOLDILOCKS_DATA/rmt_trc, then execute gtrclogger.

```
$ gtrclogger -s -p 21471 -p 21472 -d $GOLDILOCKS_HOME/rmt_trc


ERR-HY000(11040): No such object 
(/home/lym1/workspace/product/Gliese/home/rmt_trc/system.rmt.trc)

$ mkdir $GOLDILOCKS_HOME/rmt_trc

$ gtrclogger -s -p 21471 -p 21472 -d $GOLDILOCKS_HOME/rmt_trc

gtrclogger is started successfully.
```

- Example 3: Terminate gtrclogger.

```
$ gtrclogger -q

Stop Done.
```

---

[← 42. gmon](42-gmon.md) · [Table of contents](../README.md) · [44. glocator →](44-glocator.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
