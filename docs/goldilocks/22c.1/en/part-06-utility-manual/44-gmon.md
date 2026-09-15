<a id="aad8ad5b6410ad8c"></a>

# 44. gmon

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/aad8ad5b6410ad8c)  
> Tag: `22c.1_10_tag`

[← 43. gsyncher](43-gsyncher.md) · [Table of contents](../README.md) · [45. gtrclogger →](45-gtrclogger.md)

<a id="b61c7128bd7028fc"></a>
## Overview of gmon

<a id="5fe3c94987f51c19"></a>
### Definition

gmon is a database (gmaster) process monitoring utility provided by GOLDILOCKS.

<a id="2a8b9b47a099e06c"></a>
### Features

gmon monitors whether database process (gmaster) is operated, and when the process is abnormally terminated, not by user's SHUTDOWN, then it executes [gsyncher](43-gsyncher.md#a2ffdb24cdb1db88) and terminates the process. It intends to reduce the loss of logs by executing gsyncher.

gmon can be set to be automatically operated by setting the server property GMON_AUTOSTART to 1, or a user can directly executes gmon.

> A single gmaster process can monitor only one gmon process.

<a id="48fc53885b4c2ba3"></a>
### Usage

```
gmon [options]
```

<a id="98120674726ca982"></a>
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

<a id="99236e7d9424e491"></a>
#### start

It starts gmon.

<a id="2bb5d287b1c8aec1"></a>
#### stop

It stops gmon.

<a id="3aa052c32de35387"></a>
#### status

It checks the status of gmon process.

<a id="fb7972564ec01cf8"></a>
#### home

It is the database home directory. If it is omitted, then it uses the value set in GOLDILOCKS_DATA environment variable.

<a id="39dd69cada699ecc"></a>
#### uds_dir

It sets the directory in which unix domain socket is created. The maximum length of the directory is 50 bytes. The default value is /tmp.

<a id="56fb16a289bcf738"></a>
#### silent

It does not output the result message.

<a id="79159b03a8939e23"></a>
#### no-copyright

It does not output copyright and version.

<a id="a12a911d03b4e363"></a>
#### help

It outputs the help message.

<a id="c7a8d0bc02bcb5a7"></a>
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
