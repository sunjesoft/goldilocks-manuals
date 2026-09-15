<a id="4c0e0ec502be9530"></a>

# 38. gmon

> Source: [GOLDILOCKS 3.2 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/en/4c0e0ec502be9530)  
> Tag: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 37. gsyncher](37-gsyncher.md) · [Table of contents](../README.md) · [39. gtrclogger →](39-gtrclogger.md)

<a id="7237cb086f7a5a09"></a>
## Overview of gmon

<a id="7e9d1938a02e28ee"></a>
### Definition

gmon is a database (gmaster) process monitoring utility provided by GOLDILOCKS.

<a id="cb566bc6cad798e3"></a>
### Features

gmon monitors whether database process (gmaster) is operated, and when the process is abnormally terminated, not by user's SHUTDOWN, then it executes [gsyncher](37-gsyncher.md#097dfe44174f4c1c) and terminates the process. It intends to reduce the loss of logs by executing gsyncher.

gmon can be set to be automatically operated by setting the server property GMON_AUTOSTART to 1, or a user can directly executes gmon.

> A single gmaster process can monitor only one gmon process.

<a id="3855835bee2389a8"></a>
### Usage

```
gmon [options]
```

<a id="0bdf052391d0a71f"></a>
### Options

```
-s  --start        Start gmon
-t  --stop         Stop gmon
-u  --status       Get gmon status
-o  --home         gmaster home path
-l  --silent       Suppress display message 
-r  --no-copyright Suppress display copy right and version
-h  --help         Print help messages
```

<a id="6fe4ae4b9b5d7bd1"></a>
## Examples

- Example 1: Execute gmon by using the default path ($GOLDILOCKS_DATA).

```
$ gmon --start

gmon is started.
```

- Example 2: Execute gmon by specifying home path. When a relative path is used, home path is specified based on $GOLDILOCKS_DATA.

```
$ gmon --start --home g1n1_home

gmon is started.
```

- Example 3: Execute gmon by specifying home path as an absolute path. When an absolute path is used, the specified path is specified as a home path.

```
$ gmon --start --home /g1n1_home

gmon is started.
```

- Example 4: Check the status of gmon process.

```
$ gmon --status --home /g1n1_home

gmon is running(19119).
```

- Example 5: Terminate the gmon process.

```
$ gmon --stop --home /g1n1_home

gmon is stopped.
```

---

[← 37. gsyncher](37-gsyncher.md) · [Table of contents](../README.md) · [39. gtrclogger →](39-gtrclogger.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
