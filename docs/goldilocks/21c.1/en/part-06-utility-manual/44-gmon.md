<a id="b19ecf91de7af603"></a>

# 44. gmon

> Source: [GOLDILOCKS 21c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/en/b19ecf91de7af603)  
> Tag: `21c.1_35_tag`

[← 43. gsyncher](43-gsyncher.md) · [Table of contents](../README.md) · [45. gtrclogger →](45-gtrclogger.md)

<a id="1529a8e7c8759269"></a>
## Overview of gmon

<a id="85b57c7f966af56b"></a>
### Definition

gmon is a database (gmaster) process monitoring utility provided by GOLDILOCKS.

<a id="1b7cc6b615755755"></a>
### Features

gmon monitors whether database process (gmaster) is operated, and when the process is abnormally terminated, not by user's SHUTDOWN, then it executes [gsyncher](43-gsyncher.md#9f71f535c86af64c) and terminates the process. It intends to reduce the loss of logs by executing gsyncher.

gmon can be set to be automatically operated by setting the server property GMON_AUTOSTART to 1, or a user can directly executes gmon.

> A single gmaster process can monitor only one gmon process.

<a id="c1d40076390a4f92"></a>
### Usage

```
gmon [options]
```

<a id="0feaae79d1451fdc"></a>
### Options

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

<a id="01a5893144baa5bd"></a>
#### start

It starts gmon.

<a id="824c8ad88deafa4d"></a>
#### stop

It stops gmon.

<a id="737f3108ec4f8ee8"></a>
#### status

It checks the status of gmon process.

<a id="14f74423a00298c0"></a>
#### home

It is the database home directory. If it is omitted, then it uses the value set in GOLDILOCKS_DATA environment variable.

<a id="49f170341ba7b283"></a>
#### uds_dir

It sets the directory in which unix domain socket is created. The maximum length of the directory is 50 bytes. The default value is /tmp.

<a id="1cde379dbdc2ee3f"></a>
#### silent

It does not output the result message.

<a id="4269b90801c040f1"></a>
#### no-copyright

It does not output copyright and version.

<a id="c591d23a2da25dc2"></a>
#### help

It outputs the help message.

<a id="9af28316dd083024"></a>
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

[← 43. gsyncher](43-gsyncher.md) · [Table of contents](../README.md) · [45. gtrclogger →](45-gtrclogger.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
