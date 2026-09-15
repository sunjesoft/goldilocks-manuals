<a id="56128d6ab4d8ee05"></a>

# 49. gmon

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/56128d6ab4d8ee05)  
> Tag: `26c.1_0_tag`

[← 48. gsyncher](48-gsyncher.md) · [Table of contents](../README.md) · [50. gtrclogger →](50-gtrclogger.md)

<a id="f063593b6d4f5273"></a>
## Overview of gmon

<a id="0855c008993bc77d"></a>
### Definition

gmon is a database (gmaster) process monitoring utility provided by GOLDILOCKS.

<a id="d5ea91af4e10937a"></a>
### Features

gmon monitors whether database process (gmaster) is operated, and when the process is abnormally terminated, not by user's SHUTDOWN, then it executes [gsyncher](48-gsyncher.md#f852b2d8494b3d8f) and terminates the process. It intends to reduce the loss of logs by executing gsyncher.

gmon can be set to be automatically operated by setting the server property GMON_AUTOSTART to 1, or a user can directly executes gmon.

> A single gmaster process can monitor only one gmon process.

<a id="7b3de9986d2a40ac"></a>
### Usage

```
gmon [options]
```

<a id="f245d94619c657e2"></a>
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

<a id="2e7c273ad273774d"></a>
#### start

It starts gmon.

<a id="a2c33fe50cd5e368"></a>
#### stop

It stops gmon.

<a id="d59379b06fb2411e"></a>
#### status

It checks the status of gmon process.

<a id="af5ae4563e50aba6"></a>
#### home

It is the database home directory. If it is omitted, then it uses the value set in GOLDILOCKS_DATA environment variable.

<a id="414fef66fad854e1"></a>
#### uds_dir

It sets the directory in which unix domain socket is created. The maximum length of the directory is 50 bytes. The default value is /tmp.

<a id="08b886a18054f371"></a>
#### silent

It does not output the result message.

<a id="84988983483b1e81"></a>
#### no-copyright

It does not output copyright and version.

<a id="569f5efbe4b79a0f"></a>
#### help

It outputs the help message.

<a id="47b3f00855c55cf0"></a>
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

[← 48. gsyncher](48-gsyncher.md) · [Table of contents](../README.md) · [50. gtrclogger →](50-gtrclogger.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
