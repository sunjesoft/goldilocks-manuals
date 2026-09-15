<a id="22730943ba691278"></a>

# 42. gmon

> Source: [GOLDILOCKS 20c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/en/22730943ba691278)  
> Tag: `20c.1_30_tag`

[← 41. gsyncher](41-gsyncher.md) · [Table of contents](../README.md) · [43. gtrclogger →](43-gtrclogger.md)

<a id="094d52cd65ab02ce"></a>
## Overview of gmon

<a id="d13a5ac6e2687666"></a>
### Definition

gmon is a database (gmaster) process monitoring utility provided by GOLDILOCKS.

<a id="77c7d727bd0d9757"></a>
### Features

gmon monitors whether database process (gmaster) is operated, and when the process is abnormally terminated, not by user's SHUTDOWN, then it executes [gsyncher](41-gsyncher.md#5fef76169e91367b) and terminates the process. It intends to reduce the loss of logs by executing gsyncher.

gmon can be set to be automatically operated by setting the server property GMON_AUTOSTART to 1, or a user can directly executes gmon.

> A single gmaster process can monitor only one gmon process.

<a id="e2d8f21c544ef925"></a>
### Usage

```
gmon [options]
```

<a id="381997aead0a2971"></a>
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

<a id="8b55ebdc3871b765"></a>
#### start

It starts gmon.

<a id="a3581cbe95ca3554"></a>
#### stop

It stops gmon.

<a id="f442a0ae5c8be358"></a>
#### status

It checks the status of gmon process.

<a id="0fc67fb303475d16"></a>
#### home

It is the database home directory. If it is omitted, then it uses the value set in GOLDILOCKS_DATA environment variable.

<a id="9a449bcbfd2e70e1"></a>
#### uds_dir

It sets the directory in which unix domain socket is created. The maximum length of the directory is 50 bytes. The default value is /tmp.

<a id="312ef584f279fc43"></a>
#### silent

It does not output the result message.

<a id="e216c4db1e45827b"></a>
#### no-copyright

It does not output copyright and version.

<a id="0ed0e23832717d2c"></a>
#### help

It outputs the help message.

<a id="20813e03f234c579"></a>
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

[← 41. gsyncher](41-gsyncher.md) · [Table of contents](../README.md) · [43. gtrclogger →](43-gtrclogger.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
