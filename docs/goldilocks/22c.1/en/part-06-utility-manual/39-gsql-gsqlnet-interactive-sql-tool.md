<a id="bf347457eae52c08"></a>

# 39. gsql/gsqlnet (Interactive SQL Tool)

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/bf347457eae52c08)  
> Tag: `22c.1_10_tag`

[← 38. glsnr](38-glsnr.md) · [Table of contents](../README.md) · [40. gloader/gloadernet(Upload/download Tool) →](40-gloader-gloadernet-upload-download-tool.md)

<a id="84a0c3f1813998ed"></a>
## Overview of gsql

The followings are execution files.

**Execution files**

<a id="bbe39d34880094f6"></a>
| Execution file name | Description |
| --- | --- |
| gsql | It is used in Direct Attach (D/A) environment. |
| gsqlnet | It is used in Client/ Server (C/S) environment. |

> All commands supported by gsql are equally supported by gsqlnet.

<a id="190d83d92738f3ad"></a>
### Definition

gsql is an interactive utility for processing SQL statements provided by GOLDILOCKS.

Using gsql, a user can query the results of the SELECT statement as well as execute SQL statements without any application.

gsql program executes the SQL statement, and queries a brief information of the objects such as tables and indexes through the gsql specific commands beginning with `\`, and it provides various features such as startup or shutdown of the server, controlling the output, and querying the execution plan of SQL statement.

<a id="fa0ba62de29349af"></a>
### Examples

This chapter describes the method of creating/dropping the table, manipulating data, performing a query by using gsql.

gsql is operated in an interactive mode as follows. When connecting normally, it waits for entering the SQL statement or gsql command with *gSQL>* prompt.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL>
```

Create a table by executing [CREATE TABLE](../part-03-sql-manual/19-sql-references-c-g.md#78614830d4f324f4) statement and commit the transaction as follows.

```
gSQL> CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) );                 

Table created.

gSQL> COMMIT;

Commit complete.
```

Insert the data into the created table by executing [INSERT INTO](../part-03-sql-manual/20-sql-references-h-z.md#c320b7c55cfa93d3) statement, then commit the transaction as follows. The second INSERT statement is an example of inserting two rows.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'leekmo' );

1 row created.
```

- Two rows are inserted.

```
gSQL> INSERT INTO t1 VALUES ( 2, 'mkkim' ), ( 3, 'xcom73' );

2 rows created.

gSQL> COMMIT;

Commit complete.
```

The column addr is added to the table and data is updated by executing [UPDATE](../part-03-sql-manual/20-sql-references-h-z.md#0fd4667c35dfb8f0) statement as follows.

```
gSQL> ALTER TABLE t1 ADD COLUMN ( addr VARCHAR(1024) );

Table altered.

gSQL> UPDATE t1 SET addr = 'Seoul, Korea' WHERE id = 1;

1 row updated.

gSQL> UPDATE t1 SET addr = 'Inchon, Korea' WHERE id = 3;

1 row updated.

gSQL> COMMIT;

Commit complete.
```

The inserted data is queried by using [SELECT](../part-03-sql-manual/20-sql-references-h-z.md#a7590d034ddcacce) query as follows. The query result consists of the header representing column names and the information of each row in a single line. NULL is expressed in lowercase null.

```
gSQL> SELECT * FROM t1 ORDER BY 1;

ID NAME   ADDR         
-- ------ -------------
 1 leekmo Seoul, Korea 
 2 mkkim  null         
 3 xcom73 Inchon, Korea

3 rows selected.
```

A host variable is declared, and the value is put in the host variable then a query using the host variable is performed as follows.

```
gSQL> \var v_id INTEGER
gSQL> \exec :v_id := 1
gSQL> SELECT * FROM t1 WHERE id = :v_id;

ID NAME   ADDR        
-- ------ ------------
 1 leekmo Seoul, Korea

1 row selected.
```

The SQL statement is prepared by using [`\prepare sql`](#81d591bf1367796d) and the SELECT statement above is repeatedly performed by using [`\exec`](#6bf5fe8d586bd235), changing the value of host variable. ODBC and JDBC simulate prepare/ execute operation in gsql interactive mode as follows.

```
gSQL> \var v_id INTEGER
gSQL> \prepare sql SELECT * FROM t1 WHERE id = :v_id;

SQL prepared.

gSQL> \exec :v_id := 2
gSQL> \exec

ID NAME  ADDR
-- ----- ----
 2 mkkim null

1 row selected.

gSQL> \exec :v_id := 3
gSQL> \exec

ID NAME   ADDR         
-- ------ -------------
 3 xcom73 Inchon, Korea

1 row selected.
```

A scrollable cursor is declared in an embedded SQL, ODBC, JDBC, and the data retrieval using the cursor is simulated via gsql as follows. The cursor cur1 declared by using [DECLARE cursor_name](../part-03-sql-manual/19-sql-references-c-g.md#0871779c00d431a8) is the scrollable KEYSET cursor and various fetch orientations may be used by using [FETCH cursor_name](../part-03-sql-manual/19-sql-references-c-g.md#c65c0d3544ea9773).

```
gSQL> \var v_id INTEGER
gSQL> \var v_name VARCHAR(128)
gSQL> DECLARE cur1 KEYSET CURSOR FOR SELECT id, name FROM t1 ORDER BY id;

Cursor declared.

gSQL> OPEN cur1;

Cursor is open.

gSQL> FETCH cur1 INTO :v_id, :v_name;

V_ID V_NAME
---- ------
   1 leekmo

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_name;

V_ID V_NAME
---- ------
   2 mkkim 

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_name;

V_ID V_NAME
---- ------
   3 xcom73

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_name;

no rows fetched.

gSQL> FETCH ABSOLUTE 2 cur1 INTO :v_id, :v_name;

V_ID V_NAME
---- ------
   2 mkkim 

1 row fetched.

gSQL> FETCH PRIOR cur1 INTO :v_id, :v_name;

V_ID V_NAME
---- ------
   1 leekmo

1 row fetched.

gSQL> CLOSE cur1;

Cursor closed.
```

The created table t1 is dropped and the gsql interactive mode is terminated as follows.

```
gSQL> DROP TABLE t1;

Table dropped.

gSQL> COMMIT;

Commit complete.

gSQL> \q
%
```

<a id="113e7c013607cb66"></a>
## Executing gsql

<a id="f4bfd6618385f2f3"></a>
### Information of gsql

Refer to the following options.

**Options**

<a id="13c0fe47ace71462"></a>
| Option | Description |
| --- | --- |
| [--help](#e3dc43a828e43183) | Option list |
| [--version](#1ee15cbdf84830f0) | gsql version information |

A user can view the gsql command options which are executable at the shell prompt via [--help](#e3dc43a828e43183) option as follows.

```
% gsql --help

Usage 

    gsql [user_name [password]] [options]

Arguments:

    user_name       user name
    password        password

Options:

    --version                      print version information and exit
    --import       FILE            import sql FILE

... Ellipsis ...

%
```

gsql program has a version separate from GOLDILOCKS server version, and the version is viewed by using [--version](#1ee15cbdf84830f0) option as follows. It is recommended to use the gsql program in the same version as the GOLDILOCKS server.

```
% gsql --version

%
```

The version of GOLDILOCKS server can be view via [VERSION](../part-03-sql-manual/17-built-in-function-references.md#4c4cf16c3fb15e3f) function as follows.

```
gSQL> SELECT version() FROM dual;

VERSION()                            
-------------------------------------

1 row selected.
```

<a id="b1d130b60be8d2ed"></a>
### Server Connection

Refer to the following options.

**Options**

<a id="31c648a291672265"></a>
| Option | Description |
| --- | --- |
| [Username Password](#2193872f8b5e647a) | It is the user and password of connection. |
| [--as {SYSDBA\|ADMIN}](#e734f0be33270c01) | It specifies the connection role. |
| [--conn-string](#fdab3ae572f6d7e8) | It specifies the connection string. |
| [--dsn](#9857293bcc9a1306) | It specifies Data Source Name (DSN). |

<a id="fb436b1cf15cfbda"></a>
#### User Connection

Using gsql program, it can be connected to GOLDILOCKS server in various ways.

The simplest way to connect is using a username and password as follows. The following is an example that the test user connects to it by using the test password. When successfully connected, it operates in an interactive mode and the *gSQL>* prompt waits for the user command.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL>
```

The following is an example that an error occurs when using an invalid username or password. When the login is failed, an error message is displayed and then the gsql program is terminated.

```
% gsql test invalid_password

ERR-28000(16004): invalid username/password; logon denied
%
```

The following is an example that an error occurs when the GOLDILOCKS server does not run. The gsql program is terminated with the error message as follows.

```
% gsql test test

ERR-HY000(11031): Unable to attach the shared memory segment

%
```

In addition, it can be connected via the following options. For more details, refer to the respective link.

- [--conn-string](#fdab3ae572f6d7e8)
- [--dsn](#9857293bcc9a1306)

<a id="683fa482a1c0cdf0"></a>
#### SYSDBA Connection

The [--as {SYSDBA|ADMIN}](#e734f0be33270c01) option is used to drive the server or to connect to SYSDBA role which has full access privilege on the database.

The following is an example of connecting with --as sysdba in the state of when the GOLDILOCKS server is not driven. *gSQL>* prompt is waiting in the state which is ready to drive GOLDILOCKS with the message *Connected to an idle instance*.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL>
```

The following is an example of connecting with --as sysdba when the GOLDILOCKS server is already driven.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL>
```

For more information, refer to [Startup and Shutdown Server](#30a646b9d93b86a8).

<a id="adc8d912d16595c4"></a>
#### Quit gsql

gsql is quit by using `\quit` or `\q` command as follows.   
For more information, refer to `[\quit](#2e2015c9e8b6a9bb).`

```
gSQL> \quit
%
```

<a id="6d621c177e1f81f3"></a>
### Controlling Interactive Mode

Refer to the following options.

**Options**

<a id="3817ee51ef75980c"></a>
| Option | Description |
| --- | --- |
| [--prompt](#92dd1cb2c92f7507) | It specifies the prompt. |
| [--no-prompt](#ebd2b4b62b6e77f6) | It removes the prompt. |
| [--import](#dbec8ec874315003) | It executes the SQL file with input. |
| [--silent](#fc2272b10d0efc38) | When executing the SQL file, the command and the result are not displayed. |
| [--enable-color](#2e3f552cbdd00e2d) | The query result is displayed by grouping per row. |

<a id="014c03aeb616dde2"></a>
#### Controlling Prompt

When starting an interactive mode, the prompt may be changed by using --prompt option as follows. The following is an example that the prompt is changed to *GOLDILOCKS>* prompt, not to *gSQL>* prompt.

```
% gsql test test --prompt GOLDILOCKS

Connected to GOLDILOCKS Database.

GOLDILOCKS>
```

For more information about controlling the prompt, refer to the following options.

- [--prompt](#92dd1cb2c92f7507)
- [--no-prompt](#ebd2b4b62b6e77f6)

<a id="3e36967d9681f6ab"></a>
#### Executing from File

When processing batch operation by using gsql program, the SQL statement included in the file may be executed by using --import option. The following is an example of executing PerformanceViewSchema.sql file in the $GOLDILOCKS_HOME/admin directory. The example uses --silent option not to output the execution results.

```
% cd $GOLDILOCKS_HOME/admin
% gsql --as SYSDBA --import 'PerformanceViewSchema.sql' --silent
%
```

For more information about executing gsql from the file, refer to the following options.

- [--import](#dbec8ec874315003)
- [--silent](#fc2272b10d0efc38)
- [--enable-color](#2e3f552cbdd00e2d)

<a id="627c8c1ced797fda"></a>
### Storing gsql configuration

<a id="96e94b73174fa4f8"></a>
#### gsql Configuration File (gsql.ini)

The gsql configuration file (.gsql.ini) consists of options which is automatically applied when gsql starts up, and it should be in the directory $HOME.

A user can set multiple dsn in the configuration file, and can specify different options for each dsn. If a user do not enter dsn when gsql starts up, the options in GOLDILOCKS are applied.

<a id="22aafb2bf0424feb"></a>
#### Example

```
[GOLDILOCKS]

AUTOCOMMIT = OFF
AUTOTRACE = OFF
LINESIZE = 80
PAGESIZE = 20
VERTICAL = OFF
TIME = OFF
TIMING = OFF
ERROR = ON
COLSIZE = 8192
NUMSIZE = 20
DDLSIZE = 10000
HISTORY = 128
```

**Options**

<a id="36e86986f64706b0"></a>
| Option | Minimum value | Maximum value | Default value |
| --- | --- | --- | --- |
| [AUTOCOMMIT](#538d21c1f6551b86) | OFF | ON | OFF |
| [AUTOTRACE](#e462737e3684880f) | OFF | ON/TRACEONLY | OFF |
| [LINESIZE](#42daf702d2eace6a) | 1 | 10000 | 80 |
| [PAGESIZE](#881be7eb5569cdac) | 1 | 10000 | 20 |
| [VERTICAL](#969c6bd29ccd83a7) | OFF | ON | OFF |
| [TIME](#d3bd36d4c60a2bd6) | OFF | ON | OFF |
| [TIMING](#dacb5d2a2fc8e430) | OFF | ON | OFF |
| [ERROR](#96d9811f810ed53a) | ON | OFF | ON |
| [COLSIZE](#29513cfc2f8c8c50) | 1 | 10485760 | 8192 |
| [NUMSIZE](#c01ce4b4112a0598) | 1 | 50 | 20 |
| [DDLSIZE](#58135d3dceacd86f) | 1 | 10485760 | 10000 |
| [HISTORY](#3ec7cb10d93a1a99) | 0 | 100000 | 128 |

> If .gsql.ini does not exist or the option value is invalid, it is ignored.

<a id="d39d76d42b81643e"></a>
#### glogin.sql

glogin.sql is a global configuration file and it is positioned in $GOLDILOCKS_DATA/conf/glogin.sql. If glogin.sql file exists when driving gsql, then it reads the file and executed the statement included in the file. In this way, all gsql sessions are set (e.g.line size).

<a id="6a6802c908928387"></a>
#### login.sql

login.sql is a user configuration file. If login.sql file exists in the current directory when driving gsql, then it reads the file and executed the statement included in the file.   
The login.sql configuration takes precedence over the glogin.sql configuration.

<a id="cfe3060b29284e7b"></a>
## Using Interactive Command

<a id="3922b4912cec977a"></a>
### gsql Interactive Mode Commnad

Refer to the following commands.

**Commands**

<a id="3885480a320295c7"></a>
| gsql command | Description |
| --- | --- |
| [`\help`](#1fc4a542f71f7089) | gsql command list |

gsql program operates in an interactive mode through [Server Connection](#b1d130b60be8d2ed) as follows.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL>
```

A user may enter the SQL statement on the prompt line then execute it or enter the unique command which is executable in an gsql interactive mode then execute it. The gsql command begins with `back-slash(\)` to distinguish it from the SQL statement. The gsql command which begins with `back-slash(\)` can not be used in the application, while SQL statement can be directly used in the application.

> The gsql interactive mode command begins with `\`.

The following is an example of executing SQL statement in an interactive mode.

```
gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.
```

The following is an example of executing the same SELECT statement by using [`\exec sql`](#1f59b89b0868c63c), gsql command. `\exec sql` command is a unique gsql command although the syntax of `\ exec sql `is as same as the syntax of EXEC SQL referring to the beginning of SQL statement in an [Embedded SQL](../part-05-developer-manual/33-embedded-sql.md#64f644ef5c219c38).

```
gSQL> \exec sql SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.
```

The current time can be output on the prompt by setting via [`\set time`](#d3bd36d4c60a2bd6).

```
gSQL> \set time on
12:45:34 gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.

12:45:37 gSQL>
```

The unique commands of gsql interactive mode can be queried with the command [`\help`](#1fc4a542f71f7089) as follows.

```
gSQL> \help

\help                     
\q[uit]                   
\i[mport] {'FILE'}               Import SQL 
\ed[it] [{'FILE'|[HISTORY] num}] Edit SQL statement  
\\                               Executes the most recent history entry 
\{n}                             Executes n'th history entry 
\hi[story]                       Show history entries 
\desc     {[schema.]table_name}  Show table description 
\idesc    {[schema.]index_name}  Show index description 
\spo[ol]  ['filename' | OFF]     Stores query results in a file 
\ho[st]   [command]              Executes an operating system command 
\set vertical     {ON|OFF} 
\set time         {ON|OFF} 
\set timing       {ON|OFF} 
\set color        {ON|OFF} 
\set error        {ON|OFF} 
\set autocommit   {ON|OFF} 
\set autotrace    {ON|TRACEONLY|OFF} 
\set serveroutput {ON|OFF}
\set heading      {ON|OFF}
\set linesize     {n}      0 < n <= 100000
\set pagesize     {n}      0 < n <= 100000
\set colsize      {n}      0 < n <= 104857600
\set numsize      {n}      0 < n <= 50
\set ddlsize      {n}      0 < n <= 100000
\set history      {n}      n <= 100000 ( if n < 0, clear history buffer ) 
\set sqlprompt    "prompt_sql" 
\var             {host_var_name} {INTEGER|BIGINT|VARCHAR(n)} 
\exec            [{:host_var_name} := {constant}] 
\exec sql        {sql string}                   
\prepare sql     {sql string}                   
\dynamic sql     {host_var_name}                
\explain plan    [{ON|ONLY}] {sql string}       
\print           [{host_var_name}]              
\ddl_cluster                        
\ddl_db                             
\ddl_tablespace    {name}           
\ddl_profile       {name}           
\ddl_auth          {name}           
\ddl_schema        {name}           
\ddl_table         {[schema.]name}  
\ddl_constraint    {[schema.]name}  
\ddl_index         {[schema.]name}  
\ddl_view          {[schema.]name}  
\ddl_sequence      {[schema.]name}  
\ddl_synonym       {[schema.]name}  
\ddl_public_synonym {name}           
\ddl_procedure     {[schema.]name}  
\ddl_package       {[schema.]name}
\startup         {[nomount|mount|open]}                   
\shutdown        {[abort|immediate|transactional|normal]} 
\cstartup        {[nomount|mount|open]}                   
\cshutdown       {[abort|immediate|transactional|normal]} 
\connect         userid password [as {sysdba|admin}]
```

<a id="30a646b9d93b86a8"></a>
### Startup and Shutdown Server

Refer to the following commands.

**Commands**

<a id="b4789c275cfe49f2"></a>
| gsql Commad | Description |
| --- | --- |
| [`\startup`](#b08fd63635320af0) | It starts up the server. |
| [`\shutdown`](#12d8dd68e6403350) | It shuts down the server. |
| [`\cstartup`](#eaaadc4537241a95) | It starts up the server for the cluster environment. |
| [`\cshutdown`](#efc83a8dfba6b5c9) | It shuts down the server for the cluster environment. |

<a id="f84260dc5ade3646"></a>
#### Standalone

It should be connected by using SYSDBA role or ADMIN role as follows to startup or shutdown the server.

- SYSDBA role
    - It has all privileges related to DBA such as the server startup or shutdown. 
- ADMIN role
    - It has the same privileges as SYSDBA but it is allowed to connect only one session.
    - It is the role for when a valid session does not exist or for emergency connection under abnormal circumstances.

The following is an example of connecting by using SYSDBA role when the GOLDILOCKS server is not driven.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL>
```

gsql is connected to an idle instance in the state of when GOLDILOCKS server does not exist. gsql drives the GOLDILOCKS server on the specific step through [`\startup`](#b08fd63635320af0) and connects to the server. The following is an example of driving the GOLDILOCKS server on NOMOUNT phase.

```
gSQL> \startup NOMOUNT

Startup success

gSQL>
```

[`\startup`](#b08fd63635320af0) command is used only when initially driving GOLDILOCKS. Each step of the GOLDILOCKS server is switched by using [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references-a-b.md#6b3352cd0d97f557) after driving the GOLDILOCKS server and connecting to the server.

```
gSQL> ALTER SYSTEM MOUNT DATABASE;

System altered.

gSQL> ALTER SYSTEM OPEN DATABASE;

System altered.

gSQL>
```

`\startup` command is executed without any extra option as follows when GOLDILOCKS server is driven on OPEN phase whose service is available without switching the step.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL> \startup

Startup success

gSQL>
```

If the server is already driven on a certain step, `\startup` command outputs an error message as follows. Unless the server is driven up to OPEN phase, it may be driven on OPEN phase by using ALTER SYSTEM as follows.

```
% gsql sys gliese--as sysdba

Connected to GOLDILOCKS Database.

gSQL> \startup

ERR-HY000(11029): shared memory segment exists 

gSQL> ALTER SYSTEM MOUNT DATABASE;

System altered.

gSQL> ALTER SYSTEM OPEN DATABASE;

System altered.

gSQL>
```

For more information about the server startup, refer to the followings.

- Step of the server startup: [Multi-level Startup](../part-02-administration-manual/5-basic-management-of-goldilocks-database.md#83b0b11e83fe4d59)
- Command for the initial server startup: [`\startup`](#b08fd63635320af0)
- Altering the server step: [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references-a-b.md#6b3352cd0d97f557)

`\shutdown` command is used as follows to shutdown the server. For more information about the server shutdown, refer to [`\shutdown`](#12d8dd68e6403350).

```
gSQL> \shutdown

Shutdown success

gSQL>
```

<a id="c32123e4eaeac3ed"></a>
#### Cluster

LOCATOR_DSN property should be defined in odbc.ini file to startup or shutdown the server by using `\cstartup` command and `\cshutdown` command, and it should be connected with SYSDBA role or ADMIN role by using gsqlnet.

The following is an example of connecting with SYSDBA role by using gsqlnet when GOLDILOCKS server is not driven.

```
% gsqlnet sys gliese --as sysdba

Connected to an idle instance.

gSQL>
```

The following is an example of driving GOLDILOCKS server on LOCAL OPEN phase by using `\cstartup` command. Then it switches the server to OPEN phase.

```
gSQL> \cstartup LOCAL OPEN

Startup success

gSQL> ALTER SYSTEM OPEN GLOBAL DATABASE;

System altered.

gSQL>
```

`\cstartup` command and `\cshutdown` command are used in C/S environment, so glsnr should be on service on all servers to startup or shutdown the server.

The following is an example of trying to drive GOLDILOCKS server when glsnr is not on service.

```
gSQL> \cstartup

ERR-HY000(58000): MEMBER(G1N1): the sender failed to connect to the member(1)
ERR-HY000(11067): MEMBER(G1N1): fail to connect to a host with a socket : connect() : stnConnect() returned errno(111)

gSQL>
```

The following is an example of defining LOCATOR_DSN property and LOCATOR DSN property in [odbc.ini file](../part-05-developer-manual/31-odbc.md#725df1c9d28dbaab).

```
% cat .odbc.ini
# Edit the SYSTEM or USER DSN ini file (/etc/odbc.ini or ~/.odbc.ini) and add a data source using the syntax:
[GOLDILOCKS]
HOST=127.0.0.1
PORT=20101
UID=test
PWD=test
LOCATOR_DSN=LOCATOR

[LOCATOR]
FILE=/home/test/.locator.ini
```

The following is an example of trying to drive the server when LOCATOR_DSN property is not defined in odbc.ini file.

```
gSQL> \cstartup

ERR-HY000(40057): not specified valid location information

gSQL>
```

Commands excluding `\`CSTARTUP {LOCAL | GLOBAL} OPEN are applied only to the corresponding GOLDILOCKS server. Therefore, other servers should be started up to LOCAL OPEN phase for multi-level startup by using [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references-a-b.md#6b3352cd0d97f557) after `\CSTARTUP NOMOUNT, MOUN` commands.

The following is an example of trying multi-level startup after `\CSTARTUP MOUNT`. The corresponding server is started on MOUNT phase, but the other server is not started up to LOCAL OPEN phase, so an error occurs.

```
gSQL> \CSTARTUP MOUNT

Startup success

gSQL> ALTER SYSTEM OPEN LOCAL DATABASE;

System altered.

gSQL> ALTER SYSTEM OPEN GLOBAL DATABASE;

ERR-HY000(58000): MEMBER(G1N1): the sender failed to connect to the member(1)
ERR-HY000(11067): MEMBER(G1N1): fail to connect to a host with a socket : connect() : stnConnect() returned errno(111)

gSQL>
```

For more information about the server startup, refer to the followings.

- Step of the server startup: [Multi-level Startup](../part-02-administration-manual/5-basic-management-of-goldilocks-database.md#83b0b11e83fe4d59)
- Command for the initial server startup: [`\cstartup`](#eaaadc4537241a95)
- Altering the server step: [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references-a-b.md#6b3352cd0d97f557)

`\cshutdown` command is used as follows to shutdown the entire server. For more information about the entire server shutdown, refer to [`\cshutdown`](#efc83a8dfba6b5c9).

```
gSQL> \cshutdown

Shutdown success

gSQL>
```

<a id="2b33746bbbeeb93d"></a>
### Executing SQL Statements

Refer to the following commands.

**Commands**

<a id="43057416e26d85b0"></a>
| gsql commad | Description |
| --- | --- |
| [`\import`](#1995ecbe7942efd3) | It executes SQL file. |
| [`\set autocommit`](#538d21c1f6551b86) | It automatically COMMITs whenever executing the SQL statement. |
| [SQL References](../part-03-sql-manual/18-sql-references-a-b.md#7607d7d7354775f5) | It is a type of SQL statement. |

<a id="14d45d5d05384e14"></a>
#### Entering SQL Statement

In an interactive mode, gsql outputs the interactive mode prompt gSQL> and waits for a user input. After entering the SQL statement, gsql performs the SQL statement by transferring it to the server. In an interactive mode, the SQL statement is completed by entering semi-colon (;), then entering <kbd>enter</kbd>. After executing the SQL statement, gsql outputs the result and the prompt gSQL>, and then waits for user input.

The following is an example of entering the SQL statement on a single line and executing it.

```
gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.

gSQL>
```

The following is an example of entering SQL statement across multiple lines and executing it. If <kbd>enter</kbd> is used in the state of which the SQL statement is not completed, gsql outputs the line number, moves to the next line and waits for user input.

```
gSQL> SELECT id, name
2
```

When a user continuously completes entering all SQL statements, then enters semicolon (;) and <kbd>enter</kbd> as follows, the SQL statement is executed and *gSQL>* prompt waits for the next command.

```
gSQL> SELECT id, name
2 FROM t1
3 WHERE id > 0;

ID NAME  
-- ------
 1 leekmo
 2 mkkim 
 3 xcom73

3 rows selected.

gSQL>
```

The SQL statement is not recognized to be completed of input because the semi-colon (;) within the single quote (') is recognized as a string.

```
gSQL> SELECT id, ';'            
2 FROM t1
3 WHERE id = 1;

ID ';'
-- ---
 1 ;  

1 row selected.

gSQL>
```

<a id="bdb3e90e12a86605"></a>
#### Entering SQL Statement from File

In an interactive mode, `\import` is used to execute the SQL statement from the file, not to execute it by directly entering the SQL statement. The following is an example of executing multiple SQL statements by reading the file sample.sql. For more information, refer to [`\import`](#1995ecbe7942efd3).

```
gSQL> \import 'sample.sql'
```

- Drop table

```
DROP TABLE IF EXISTS t1;

Table dropped.
```

- Create table

```
CREATE TABLE t1 
(
    id   INTEGER PRIMARY KEY,
    name VARCHAR(128),
    addr VARCHAR(128)
);

Table created.
```

- Create index

```
CREATE INDEX t1_idx_name ON t1(name);

Index created.
```

- Insert three rows

```
INSERT INTO t1 
       VALUES ( 1, 'leekmo', 'Seoul, Korea'  ),
              ( 2, 'mkkim' , 'Seoul, Korea'  ),
              ( 3, 'xcom73', 'Inchon, Korea' );

3 rows created.
```

- Commit transaction

```
COMMIT;

Commit complete.

gSQL>
```

<a id="c1bccdd8592af2cc"></a>
#### gsql Comment

The comments in an interactive mode are as same as those in the SQL statement. The comments input from the file via the [--import](#dbec8ec874315003) option is also as same as those in the SQL statement. For more information about comments on SQL statement, refer to [Comments](../part-03-sql-manual/11-sql-elements.md#49ffe3ea6c4c9c20).

The following is an example of using the line comment in an interactive mode.

```
gSQL> -- outside line-comment     
gSQL> SELECT id, name
2 FROM t1 -- inside line-comment
3 WHERE id = 1;

ID NAME  
-- ------
 1 leekmo

1 row selected.

gSQL>
```

The following is an example of executing the file content with the `\import` command. It is treated in the same way as the comment in an interactive mode. And *gSQL>* prompt waits for the next SQL statement after all contents of the file are executed.

```
gSQL> \import 'sample.sql'
```

- Drop table

```
DROP TABLE IF EXISTS t1;

Table dropped.
```

- Create table

```
CREATE TABLE t1 
(
    id   INTEGER PRIMARY KEY,
    name VARCHAR(128),
    addr VARCHAR(128)
);

Table created.
```

- Create index

```
CREATE INDEX t1_idx_name ON t1(name);

Index created.
```

- Insert three rows

```
INSERT INTO t1 
       VALUES ( 1, 'leekmo', 'Seoul, Korea'  ),
              ( 2, 'mkkim' , 'Seoul, Korea'  ),
              ( 3, 'xcom73', 'Inchon, Korea' );

3 rows created.
```

- Commit transaction

```
COMMIT;

Commit complete.

gSQL>
```

The following is an example of using the multi-line comment in an interactive mode.

```
gSQL> SELECT id, name
2     /*
3     multi-line
4     comment
5     */
6     FROM t1
7     WHERE id = 1;

ID NAME  
-- ------
 1 leekmo

1 row selected.

gSQL>
```

The comments which is available in gsql interactive mode are as same as those in the SQL statement. For more information about the comments, refer to [Comments](../part-03-sql-manual/11-sql-elements.md#49ffe3ea6c4c9c20) of SQL statement.

<a id="c992fd5ce8803649"></a>
#### SQL Execution Result

When a user performs a query such as SELECT statement in an interactive mode, gsql outputs the query results. The query result consists of the header with the column names, the data of the query result, and summary the query results at the end.

The following is an example of executing the SELECT statement.

```
gSQL> SELECT * FROM t1;

ID NAME   ADDR         
-- ------ -------------
 1 leekmo Seoul, Korea 
 2 mkkim  Seoul, Korea 
 3 xcom73 Inchon, Korea

3 rows selected.

gSQL>
```

In the example above, the header of output results consists of the column name and the hyphen (-) which distinguishes it from data. The query result is displayed in the middle of the output result, each row of query result is displayed on a single line, and each column value is separated with the space. The summary of the query result is displayed at the end. In this case, it refers that three rows are retrieved.

[Data Definition Language](../part-03-sql-manual/12-sql-languages.md#fe780c8e5922c3cf), [Data Manipulation Language](../part-03-sql-manual/12-sql-languages.md#4d76098f8bb537f0), [Control Language](../part-03-sql-manual/12-sql-languages.md#801b6e594b7ede55) statements (except for SQL query) displays the summarized information of the execution result corresponding to the SQL statements characteristics.

The followings are the examples of respectively executing the DDL, DML, Control Language, displaying the results.

- DDL statement

```
gSQL> CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) );

Table created.
```

- DML statement

```
gSQL> INSERT INTO t1 VALUES ( 1, 'leekmo' );

1 row created.
```

- Transaction control statement

```
gSQL> COMMIT;

Commit complete.

gSQL>
```

<a id="b785a46f777103dd"></a>
#### SQL Execution Error

The error which occurs during executing the SQL statement consists of the following information when it.

- SQLSTATE information: SQLSTATE value of SQL standard 
- Error code: Unique error code value of GOLDILOCKS
- Error message: An error message describing the cause of error

The following is an example of an error when executing the SELECT statement. The error message consists of that value of ERR-42000 corresponds to SQLSTATE and the unique error code of GOLDILOCKS is the value of (16040) and a table or view corresponding to invalid_table does not exist at line 2.

```
gSQL> SELECT id, name
2       FROM invalid_table
3      WHERE id > 0;

ERR-42000(16040): table or view does not exist : 
      FROM invalid_table
           *
ERROR at line 2:

gSQL>
```

<a id="0bec16b508673000"></a>
#### Interactive Command Execution Result

The interactive commands used together with SQL statements displays the same results and errors as those executing SQL statements.

The following is an example of preparing the SQL statement by using [`\prepare sql`](#81d591bf1367796d)  and executing it by using [`\exec`](#6bf5fe8d586bd235).

```
gSQL> \prepare sql SELECT * FROM t1;     

SQL prepared.

gSQL> \exec

ID NAME   ADDR         
-- ------ -------------
 1 leekmo Seoul, Korea 
 2 mkkim  Seoul, Korea 
 3 xcom73 Inchon, Korea

3 rows selected.

gSQL>
```

The following is an example of an error occurred in the SQL statement when using [`\prepare sql`](#81d591bf1367796d). It displays an error which is as same as that occurs when executing the SQL statement.

- An error of `\prepare` sql command

```
gSQL> \prepare sql SELECT * FROM invalid_table;

ERR-42000(16040): table or view does not exist : 
SELECT * FROM invalid_table
              *
ERROR at line 1:
```

- An error of the same SQL statement

```
gSQL> SELECT * FROM invalid_table;

ERR-42000(16040): table or view does not exist : 
SELECT * FROM invalid_table
              *
ERROR at line 1:

gSQL>
```

If the gsql commands in an interactive mode do not include the SQL statement or when the command does not have any result to display, only *gSQL>* prompt is displayed without any extra message when the command is successfully performed.

The following is an example of successfully performing the interactive command without a message. The error message is displayed when an error occurs.

- When the interactive gsql command is normally performed

```
gSQL> \var v1 INTEGER
gSQL> \exec :v1 := 1
```

- When the interactive gsql command causes an error

```
gSQL> \var v2 INVALID TYPE

ERR-42000(40000): syntax error 
\var v2 INVALID TYPE
........^     ^
Error at line 1

gSQL>
```

For more information about the performance result of the interactive command, refer to the description and example of the interactive command in [Interactive Command References](#e19b8f83d1f70038).

<a id="199571ff537edfa6"></a>
#### Autocommitting SQL statement

The SQL statements in the gsql interactive mode may commit or roll back the transaction by using the [COMMIT](../part-03-sql-manual/19-sql-references-c-g.md#4f7ae244eb8d32e6) or [ROLLBACK](../part-03-sql-manual/20-sql-references-h-z.md#126809f09298a063) statement.

The following is an example of performing COMMIT or ROLLBACK after performing multiple INSERT statements. Whereas the first INSERT statement is successfully committed by COMMIT, the second and third INSERT statements are rolled back by ROLLBACK in the following example.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'leekmo' );

1 row created.

gSQL> COMMIT;

Commit complete.

gSQL> INSERT INTO t1 VALUES ( 2, 'mkkim' );

1 row created.

gSQL> INSERT INTO t1 VALUES ( 3, 'xcom73' );

1 row created.

gSQL> ROLLBACK;

Rollback complete.

gSQL> SELECT * FROM t1;

ID NAME  
-- ------
 1 leekmo

1 row selected.

gSQL>
```

If a user wants to automatically COMMIT every transaction whenever performing the SQL statements, it can be controlled by using the [`\set autocommit`](#538d21c1f6551b86) as follows. When performing the same SQL statement as the example above, each SQL statement is automatically committed, so the transaction of the second and the third INSERT statements are completed regardless of ROLLBACK.

```
gSQL> \set autocommit on
gSQL> INSERT INTO t1 VALUES ( 1, 'leekmo' );

1 row created.

gSQL> COMMIT;

Commit complete.

gSQL> INSERT INTO t1 VALUES ( 2, 'mkkim' );

1 row created.

gSQL> INSERT INTO t1 VALUES ( 3, 'xcom73' );

1 row created.

gSQL> ROLLBACK;

Rollback complete.

gSQL> SELECT * FROM t1;

ID NAME  
-- ------
 1 leekmo
 2 mkkim 
 3 xcom73

3 rows selected.

gSQL>
```

For more information about controlling automatic COMMIT, refer to [`\set autocommit`](#538d21c1f6551b86).

<a id="8d1b43c5d4c24fd9"></a>
#### Forced Termination of SQL Statement Being Executed

SQL statements being executed in an interactive mode is forcibly terminated by entering <kbd>Ctrl</kbd>+<kbd>C</kbd>.

The following is an example of which the SELECT statement being executed for a long time is forcibly terminated. If <kbd>Ctrl</kbd>+<kbd>C</kbd> is entered by using a keyboard during performing the SQL statement, the error message, operation canceled, is displayed and the SQL statement is forcibly terminated.

```
gSQL> SELECT COUNT(*)
  FROM 
       t1 AS v01,
       t1 AS v02,
       t1 AS v03,
       t1 AS v04,
       t1 AS v05,
       t1 AS v06,
       t1 AS v07,
       t1 AS v08,
       t1 AS v09,
       t1 AS v10,
       t1 AS v11,
       t1 AS v12,
       t1 AS v13,
       t1 AS v14,
       t1 AS v15,
       t1 AS v16,
       t1 AS v17,
       t1 AS v18,
       t1 AS v19,
       t1 AS v20;
2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 
^C
ERR-HY008(13043): operation canceled

gSQL>
```

<a id="075e95c93c7d4690"></a>
### Controlling Output Result

Refer to the following commands.

**Commands**

<a id="f08bd1a3f96ae0e0"></a>
| gsql command | Description |
| --- | --- |
| [`\set color`](#a173748685f1d9f4) | It identifies each row with different color. |
| [`\set colsize`](#29513cfc2f8c8c50) | It controls the maximum size of the column results. |
| [`\set error`](#96d9811f810ed53a) | It controls whether an error message is displayed. |
| [`\set linesize`](#42daf702d2eace6a) | It controls the maximum output length of the row. |
| [`\set numsize`](#c01ce4b4112a0598) | It controls the maximum number of digit of the numeric value. |
| [`\set pagesize`](#881be7eb5569cdac) | It controls the number of row to be included in a page. |
| [`\set timing`](#dacb5d2a2fc8e430) | It outputs the execution time of the SQL statement. |
| [`\set vertical`](#969c6bd29ccd83a7) | It displays each column in a single line. |

<a id="a980cf772eb5dcf7"></a>
#### Controlling Page Configuration

As described in [SQL Execution Result](#c992fd5ce8803649), the query results display the column names in the header, displays the data, then the summary information at the end.

If there are many query results, they are divided into the unit of pagesize (default value is 20), and each page outputs the column names and data set. When the output of all pages is completed, the summary information is displayed at the end.

The following is an example of the output of query results by changing the pagesize to 5. For more information about controlling the pagesize, refer to [`\set pagesize`](#881be7eb5569cdac).

```
gSQL> \set pagesize 5
gSQL> SELECT table_schema, table_name FROM dictionary WHERE table_name like 'ALL_%' FETCH 20;

TABLE_SCHEMA      TABLE_NAME        
----------------- ------------------
DICTIONARY_SCHEMA ALL_ALL_TABLES    
DICTIONARY_SCHEMA ALL_COL_COMMENTS  
DICTIONARY_SCHEMA ALL_COL_PRIVS     
DICTIONARY_SCHEMA ALL_COL_PRIVS_MADE
DICTIONARY_SCHEMA ALL_COL_PRIVS_RECD

TABLE_SCHEMA      TABLE_NAME       
----------------- -----------------
DICTIONARY_SCHEMA ALL_CONSTRAINTS  
DICTIONARY_SCHEMA ALL_CONS_COLUMNS 
DICTIONARY_SCHEMA ALL_DB_PRIVS     
DICTIONARY_SCHEMA ALL_DB_PRIVS_MADE
DICTIONARY_SCHEMA ALL_DB_PRIVS_RECD

TABLE_SCHEMA      TABLE_NAME      
----------------- ----------------
DICTIONARY_SCHEMA ALL_INDEXES     
DICTIONARY_SCHEMA ALL_IND_COLUMNS 
DICTIONARY_SCHEMA ALL_SCHEMAS     
DICTIONARY_SCHEMA ALL_SCHEMA_PATH 
DICTIONARY_SCHEMA ALL_SCHEMA_PRIVS

TABLE_SCHEMA      TABLE_NAME           
----------------- ---------------------
DICTIONARY_SCHEMA ALL_SCHEMA_PRIVS_MADE
DICTIONARY_SCHEMA ALL_SCHEMA_PRIVS_RECD
DICTIONARY_SCHEMA ALL_SEQUENCES        
DICTIONARY_SCHEMA ALL_SEQ_PRIVS        
DICTIONARY_SCHEMA ALL_SEQ_PRIVS_MADE   

20 rows selected.

gSQL>
```

Each row of the query result is output in linesize unit (default value is 80). If the row length of the result is bigger than linesize, it is output on the next line.

The following is an example of the query result before and after the linesize is adjusted to 200. For more information about controlling linesize, refer to [`\set linesize`](#42daf702d2eace6a).

```
gSQL> SELECT * FROM dict_columns WHERE table_name = 'USER_TABLES' FETCH 3;

TABLE_SCHEMA      TABLE_NAME  COLUMN_NAME    
----------------- ----------- ---------------
COMMENTS                                   
-------------------------------------------
DICTIONARY_SCHEMA USER_TABLES TABLE_SCHEMA   
Schema of the table                        
DICTIONARY_SCHEMA USER_TABLES TABLE_NAME     
Name of the table                          
DICTIONARY_SCHEMA USER_TABLES TABLESPACE_NAME
Name of the tablespace containing the table

3 rows selected.
```

- Set the linesize to 200.

```
gSQL> \set linesize 200
gSQL> SELECT * FROM dict_columns WHERE table_name = 'USER_TABLES' FETCH 3;

TABLE_SCHEMA      TABLE_NAME  COLUMN_NAME     COMMENTS                                   
----------------- ----------- --------------- -------------------------------------------
DICTIONARY_SCHEMA USER_TABLES TABLE_SCHEMA    Schema of the table                        
DICTIONARY_SCHEMA USER_TABLES TABLE_NAME      Name of the table                          
DICTIONARY_SCHEMA USER_TABLES TABLESPACE_NAME Name of the tablespace containing the table

3 rows selected.

gSQL>
```

To increase the readability of each row on the terminal by differentiating rows, each row can be output by varying the color through [`\set color`](#a173748685f1d9f4) as described below. For more information, refer to [`\set color`](#a173748685f1d9f4).

```
gSQL> \set color on
gSQL> SELECT table_schema, table_name FROM dictionary WHERE table_name like 'ALL_%' FETCH 10;

TABLE_SCHEMA      TABLE_NAME        
----------------- ------------------
DICTIONARY_SCHEMA ALL_ALL_TABLES    
DICTIONARY_SCHEMA ALL_COL_COMMENTS  
DICTIONARY_SCHEMA ALL_COL_PRIVS     
DICTIONARY_SCHEMA ALL_COL_PRIVS_MADE
DICTIONARY_SCHEMA ALL_COL_PRIVS_RECD
DICTIONARY_SCHEMA ALL_CONSTRAINTS   
DICTIONARY_SCHEMA ALL_CONS_COLUMNS  
DICTIONARY_SCHEMA ALL_DB_PRIVS      
DICTIONARY_SCHEMA ALL_DB_PRIVS_MADE 
DICTIONARY_SCHEMA ALL_DB_PRIVS_RECD 

10 rows selected.

gSQL>
```

To output the query result rows in the column unit on a single line, not in the line unit, `\set vertical on` is used. The following is an example of displaying the query results in a column unit. For more information, refer to [`\set vertical`](#969c6bd29ccd83a7).

```
gSQL> SELECT * FROM v$system_stat FETCH 5;

STAT_NAME             STAT_VALUE COMMENTS                                                 
--------------------- ---------- ---------------------------------------------------------
SYSTEM_SAR                     3 system available resource( 0:none, 1:session 2:database )
MAX_ENVIRONMENT_COUNT        128 maximum environment count                                
FREE_ENVIRONMENT_ID            3 available environment identifier                         
MAX_SESSION_COUNT            128 maximum session count                                    
FREE_SESSION_ID                4 available session identifier                             

5 rows selected.

gSQL> \set vertical on
gSQL> SELECT * FROM v$system_stat FETCH 5;

               STAT_NAME # SYSTEM_SAR
              STAT_VALUE # 3
                COMMENTS # system available resource( 0:none, 1:session 2:database )

               STAT_NAME # MAX_ENVIRONMENT_COUNT
              STAT_VALUE # 128
                COMMENTS # maximum environment count

               STAT_NAME # FREE_ENVIRONMENT_ID
              STAT_VALUE # 3
                COMMENTS # available environment identifier

               STAT_NAME # MAX_SESSION_COUNT
              STAT_VALUE # 128
                COMMENTS # maximum session count

               STAT_NAME # FREE_SESSION_ID
              STAT_VALUE # 4
                COMMENTS # available session identifier


5 rows selected.

gSQL>
```

<a id="c1875f1c80d26145"></a>
#### Controlling Data Output

gsql converts all data included in the query result to a string, then outputs it.

For a numeric data type, numsize (default value is 20) is output in the digit unit, and a numeric value bigger than numsize is output in an exponent form. The following is an example of controlling the output by using the numsize. For more information, refer to [`\set numsize`](#c01ce4b4112a0598).

```
gSQL> SELECT num, ( num * num ) AS result FROM t1;

          NUM               RESULT
------------- --------------------
1234567890123 1.52415787532276E+24

1 row selected.

gSQL> \set numsize 50
gSQL> SELECT num, ( num * num ) AS result FROM t1;

          NUM                    RESULT
------------- -------------------------
1234567890123 1524157875322755800955129

1 row selected.

gSQL>
```

The output of the numeric value may be controlled in various ways by using the [TO_CHAR( number )](../part-03-sql-manual/17-built-in-function-references.md#d69061b89662a768) function as the following example.

```
gSQL> SELECT num, TO_CHAR( num * num, '$999,999,999,999,999,999,999,999,999' ) AS result FROM t1;

          NUM RESULT                               
------------- -------------------------------------
1234567890123    $1,524,157,875,322,755,800,955,129

1 row selected.

gSQL>
```

For the date/ time data types such as DATE/ TIME/ TIMESTAMP, gsql determines the output type by using the property information as follows.

- [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#7ea8c558693ab9b8)
- [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#f745ba729e1e8deb)
- [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#226a187670420c2f)
- [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#fff3ca3eeeea7a35)
- [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#6a87f7e07e80669e)

The property is used when the format information is not entered in the functions such as TO_CHAR(), TO_DATE(). When connected for the first time, gsql acquires the property information and uses it to output the date/ time data value, whereas the property above is used only when the application using ODBC or JDBC uses the functions such as TO_CHAR(), TO_DATE() in SQL statement. When the property is changed to the following SQL statement in an interactive mode, gsql uses the updated property information.

- [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#92680bbe05326073)
- [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references-a-b.md#77b4edc18193b02e)

The following is an example of controlling the output for the DATE column.

```
gSQL> SELECT enter_date FROM t1;

ENTER_DATE
----------
2014-08-26

1 row selected.

gSQL> ALTER SESSION SET NLS_DATE_FORMAT = 'DD-MON-YYYY';

Session altered.

gSQL> SELECT enter_date FROM t1;

ENTER_DATE 
-----------
26-AUG-2014

1 row selected.

gSQL>
```

The output of the date/ time value can be controlled by using [TO_CHAR( datetime )](../part-03-sql-manual/17-built-in-function-references.md#24c99d6f3463acf6) function without altering property as follows.

```
gSQL> SELECT TO_CHAR( enter_date, 'DD-MON-YYYY' ) as result FROM t1;

RESULT          
----------------
26-AUG-2016

1 row selected.

gSQL>
```

A binary string such as BINARY or VARBINARY is output as hex values as follows.

```
gSQL> select * from t1;

BINARY_VALUE        
--------------------
A010002F370000000000

1 row selected.

gSQL>
```

The data of the LONG VARCHAR, LONG VARBINARY type may include a very long string, so it outputs the data as much as colsize (default value is 8192). The following is an example of outputting the part of the TEXT column data of LONG VARCHAR data type by reducing the colsize. The whole data may be output by increasing the colsize. For more information, refer to [`\set colsize`](#29513cfc2f8c8c50).

```
gSQL> \set colsize 100
gSQL> SELECT view_name, text FROM all_views WHERE view_name = 'ALL_ALL_TABLES';

VIEW_NAME      TEXT                                                  
-------------- ------------------------------------------------------
ALL_ALL_TABLES SELECT                                                
                      auth.AUTHORIZATION_NAME                ❶ OWNER
                    , sch.SCHEMA_NAME                                

1 row selected.

gSQL>
```

<a id="2cc803f6a2fc5322"></a>
#### Execution Time of SQL Statement

The execution time of the SQL statement is output by using `\set timing on` as follows. For more information, refer to [`\set timing`](#dacb5d2a2fc8e430).

```
gSQL> \set timing on
gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.

Elapsed time: 0.08500 ms
```

<a id="eded9c82fcf4f1c4"></a>
### Logging Output Result

All results performed in gsql are simultaneously logged to the file when they are output on the terminal.

**Commands**

<a id="8fc0366368f7352c"></a>
| gsql command | Description |
| --- | --- |
| `\spool` | It logs the output result to a file. |

For more information about the features related to logging output results, refer to the commands of [`\spool`](#b7d07f5598c0ed0c).

The output result is logged as the following example.

- Start to log the execution result on result.txt

```
gSQL> \SPOOL 'result.txt'
```

- Check the spool status

```
gSQL> \SPOOL
 
currently spooling to result.txt

gSQL> SELECT * FROM T1 WHERE C1 < 10;
```

- Stop the spool feature

```
gSQL> \SPOOL OFF
```

<a id="3af234050ed6e63c"></a>
### Querying SQL Object Information

The information about SQL objects may be queried with the views of [DICTIONARY_SCHEMA](../part-02-administration-manual/9-database-information.md#fd116a7f066a7767), [INFORMATION_SCHEMA](../part-02-administration-manual/9-database-information.md#ee5a1a28f6ab5db9).

**Commands**

<a id="44901b0bc67d60dc"></a>
| gsql command | Description |
| --- | --- |
| [`\desc`](#37ddcc5f12fda169) | It queries the table information. |
| [`\idesc`](#104a85d31246002d) | It queries the index information. |

For example, there are the table and index created as follows.

```
CREATE TABLE t1 
(
    id   INTEGER PRIMARY KEY,
    name VARCHAR(128),
    addr VARCHAR(128)
);

CREATE INDEX t1_idx_name ON t1(name);
```

A user may query the information related to the table by performing a series of SQL statements as follows.

```
gSQL> SELECT table_schema, table_name FROM user_tables WHERE table_name = 'T1';

TABLE_SCHEMA TABLE_NAME
------------ ----------
PUBLIC       T1        

1 row selected.

gSQL> SELECT column_name, data_type, nullable FROM user_tab_columns WHERE table_schema = 'PUBLIC' AND table_name = 'T1';

COLUMN_NAME DATA_TYPE         NULLABLE
----------- ----------------- --------
ID          NUMBER            N       
NAME        CHARACTER VARYING Y       
ADDR        CHARACTER VARYING Y       

3 rows selected.

gSQL> SELECT index_name FROM user_indexes WHERE table_schema = 'PUBLIC' AND table_name = 'T1';

INDEX_NAME          
--------------------
T1_PRIMARY_KEY_INDEX
T1_IDX_NAME         

2 rows selected.

gSQL>
```

gsql may easily query the information related to the table by using `\desc` as follows. For more information about the output, refer to [`\desc`](#37ddcc5f12fda169).

```
gSQL> \desc t1

COLUMN_NAME TYPE                   IS_NULLABLE
----------- ---------------------- -----------
ID          NUMBER(10,0)           FALSE      
NAME        VARCHAR(128)           TRUE       
ADDR        VARCHAR(128)           TRUE       

INDEX_NAME           TABLESPACE_NAME INDEX_TYPE IS_UNIQUE COLUMNS
-------------------- --------------- ---------- --------- -------
T1_PRIMARY_KEY_INDEX MEM_TEMP_TBS    BTREE      TRUE      ID     
T1_IDX_NAME          MEM_TEMP_TBS    BTREE      FALSE     NAME   

CONSTRAINT_NAME CONSTRAINT_TYPE ASSOCIATED_INDEX     COLUMNS
--------------- --------------- -------------------- -------
T1_PRIMARY_KEY  PRIMARY KEY     T1_PRIMARY_KEY_INDEX ID     

gSQL>
```

`\idesc` describes the information related to the index as the following example. For more information, refer to [`\idesc`](#104a85d31246002d).

```
gSQL> \idesc t1_idx_name

COLUMN_NAME ORDINAL_POSITION IS_ASCENDING_ORDER IS_NULLS_FIRST
----------- ---------------- ------------------ --------------
NAME                       1 TRUE               FALSE         

gSQL>
```

<a id="74da56547db88a47"></a>
### Output DDL Statement of SQL Object

The following gsql commands output the DDL statement corresponding to the current state of the SQL object. As well as the CREATE statement which creates the SQL object, DDL statement of the related object may be output through the various options.

> The objects stored in the recycle bin are not output.

**Commands**

<a id="eecdf54c53d43ad6"></a>
| gsql command | Description |
| --- | --- |
| [`\ddl_cluster`](#0f59116afaf841a9) | It outputs the cluster-related DDL. |
| [`\ddl_db`](#2b12df2779f07dce) | It outputs the database-related DDL. |
| [`\ddl_tablespace`](#709988ed6249b4b4) | It outputs the tablespace-related DDL. |
| [`\ddl_profile`](#0b5ef20f54332314) | It outputs the profile-related DDL. |
| [`\ddl_audit_policy`](#e113a955e7bd812e) | It outputs the audit policy-related DDL. |
| [`\ddl_auth`](#be76567242f385a0) | It outputs the account-related DDL. |
| [`\ddl_schema`](#6cc04567194b0f52) | It outputs the schema-related DDL. |
| [`\ddl_public_synonym`](#45ceb9b4306308e9) | It outputs the public synonym-related DDL. |
| [`\ddl_table`](#93feba0884aff3da) | It outputs the table-related DDL. |
| [`\ddl_constraint`](#b4894103cc335441) | It outputs the constraint-related DDL. |
| [`\ddl_index`](#61c711afa481b5c1) | It outputs the index-related DDL. |
| [`\ddl_view`](#0205fa731c743d17) | It outputs the view-related DDL. |
| [`\ddl_sequence`](#7ca05c84662a43b5) | It outputs the sequence-related DDL. |
| [`\ddl_synonym`](#5d56473b41117e8d) | It outputs the synonym-related DDL. |
| [`\ddl_procedure`](#6d70ed7500698e9b) | It outputs the procedure-related DDL. |
| [`\ddl_package`](#1af1e56ac5d40d3a) | It outputs the package-related DDL. |
| [`\set ddlsize`](#58135d3dceacd86f) | It controls the size of the DDL output buffer. |

For example, the orders table is created as follows.

```
gSQL> 
CREATE TABLE ORDERS
(
    O_ID         INTEGER,
    O_D_ID       INTEGER, 
    O_W_ID       INTEGER,
    O_C_ID       INTEGER,
    O_ENTRY_D    TIMESTAMP,
    O_CARRIER_ID INTEGER,
    O_OL_CNT     NUMERIC(8), 
    O_ALL_LOCAL  NUMERIC(1),

    PRIMARY KEY(O_W_ID, O_D_ID, O_ID) INDEX ORDERS_PK_IDX
);

Table created.
```

The CREATE TABLE statement which created the orders table in the example above is output by using `\ddl_table` as follows.

```
gSQL> \ddl_table orders CREATE

SET SESSION AUTHORIZATION "TEST"; 
CREATE TABLE "PUBLIC"."ORDERS" 
    ( 
        "O_ID" NUMBER( 10, 0 )
      , "O_D_ID" NUMBER( 10, 0 )
      , "O_W_ID" NUMBER( 10, 0 )
      , "O_C_ID" NUMBER( 10, 0 )
      , "O_ENTRY_D" TIMESTAMP( 6 ) WITHOUT TIME ZONE
      , "O_CARRIER_ID" NUMBER( 10, 0 )
      , "O_OL_CNT" NUMBER( 8, 0 )
      , "O_ALL_LOCAL" NUMBER( 1, 0 )
    ) 
    PCTFREE  10 
    PCTUSED  60 
    INITRANS 4 
    MAXTRANS 8 
    STORAGE 
    ( 
        INITIAL 524288 
        NEXT    262144 
        MINSIZE 524288 
        MAXSIZE 35184372088832 
    ) 
    TABLESPACE "MEM_DATA_TBS" 
;
```

From the example above, SET AUTHORIZATION statement refers to the owner who performed CREATE TABLE statement. The CREATE TABLE statement is output together with the information that the user does not input such as the schema name to which the table belongs, the tablespace name in which the table is stored and the physical information of the table.

DDL corresponding to the constraints generated in the table is output by using the CONSTRAINT option of `\ddl_table` as follows.

```
gSQL> \ddl_table orders CONSTRAINT


SET SESSION AUTHORIZATION "TEST"; 
ALTER TABLE "PUBLIC"."ORDERS" 
    ADD CONSTRAINT "PUBLIC"."ORDERS_PRIMARY_KEY" 
    PRIMARY KEY 
    ( 
        "O_W_ID" ASC NULLS LAST
      , "O_D_ID" ASC NULLS LAST
      , "O_ID" ASC NULLS LAST
    ) 
    INDEX "ORDERS_PK_IDX" 
    PCTFREE  10 
    INITRANS 4 
    MAXTRANS 8 
    STORAGE 
    ( 
        INITIAL 524288 
        NEXT    262144 
        MINSIZE 524288 
        MAXSIZE 35184372088832 
    ) 
    TABLESPACE "MEM_TEMP_TBS" 
    NOT DEFERRABLE
    INITIALLY IMMEDIATE
;
```

For more information, refer to the gsql command corresponding to the SQL object.

> If a user uses the command such as `\ddl_table` and simultaneously performs DDL on the relevant SQL object, it may output different results, so DDL should not be simultaneously performed.

<a id="280f1af4ff737820"></a>
### Controlling History

gsql controls the history of executed SQL statements in an interactive mode.

**Commands**

<a id="c3e8df2ab241b3a3"></a>
| gsql command | Description |
| --- | --- |
| [`\\`](#e9fcaf4386815ef7) | It executes the previous SQL. |
| [`\{n}`](#cfaf01b3c6c630d9) | It executes the SQL statement corresponding to the history number. |
| [`\history`](#abb530db4014a1ab) | It queries the SQL execution history. |
| [`\set history`](#3ec7cb10d93a1a99) | It controls the number of history buffer. |

The following is an example of executing SQL statement which has already been performed may be performed again.

• The most recent successfully executed SQL statement is executed again.

```
gSQL> \\

DUMMY
-----
X    

1 row selected.

gSQL> \history

ID SQL                                            
-- -----------------------------------------------
 1 DROP TABLE IF EXISTS t1                        
 2 CREATE TABLE t1                                
   (                                              
       id   INTEGER PRIMARY KEY,                  
       name VARCHAR(128),                         
       addr VARCHAR(128)                          
   )                                              
 3 CREATE INDEX t1_idx_name ON t1(name)           
 4 INSERT INTO t1                                 
          VALUES ( 1, 'leekmo', 'Seoul, Korea'  ),
                 ( 2, 'mkkim' , 'Seoul, Korea'  ),
                 ( 3, 'xcom73', 'Inchon, Korea' ) 
 5 COMMIT                                         
 6 select * from t1
```

• The first SQL in the history is executed.

```
gSQL> \1   

Table dropped.
```

For more information about the history related features of gsql, refer to [Commands ](#c3e8df2ab241b3a3).

<a id="c8a62d249407e9e2"></a>
### Editing SQL

It edits the SQL statement by using the text editor. The text editor to be used may be specified in the environment variable EDITOR. If the environment variable EDITOR does not exist, vi is used by default.

**Command**

<a id="5cfaea136eefcc60"></a>
| gsql command | Description |
| --- | --- |
| `\edit` | It edits the SQL statement by using the text editor. |

When using the editing features, gsql runs the editor and hands over control to it. The user can freely edit the SQL statements with the editor. When the editor ends, the control is handed over to gsql, and its content will be added as the last history.

The SQL statement edited by the editor may be executed through the last history execution command `\\`.

> Only a single SQL statement can be edited with the SQL editor. An error occurs when executing multiple SQL statements.

The followings may be edited by using `\edit`.

- The most recently performed SQL statement
- The SQL statement stored in a file
- The SQL statement stored in the gsql history

For more information about the edit-related features in gsql, refer to [`\edit`](#7b352f8446079c8a).

The SQL statement may be edited as the following example.

• The most recently performed SQL statement is edited.

```
gSQL> SELECT * FROM T1;
C1
--
 1
11
2 rows selected.
gSQL> \EDIT
SELECT * FROM T1 WHERE C1 < 10;
```

• The edited SQL statement is executed.

```
gSQL> \\
C1
--
 1
1 row selected.
```

<a id="036c28865dcc79ea"></a>
### Controlling Connection

Refer to the following commands.

**Commands**

<a id="7b7d7de4deaba005"></a>
| gsql command | Description |
| --- | --- |
| [`\connect`](#7081c130d290bfdc) | It connects with a new user. |
| [`\quit`](#2e2015c9e8b6a9bb) | It quits the connection. |

It is connected with a new user by using `\connect` in an interactive mode as follows. The existing session is terminated and a new session is created by using `\connect`. For more information, refer to [`\connect`](#7081c130d290bfdc).

```
gSQL> \connect test test
gSQL>
```

The user may be changed by using the [SET SESSION AUTHORIZATION user_identifier](../part-03-sql-manual/20-sql-references-h-z.md#753627e383c21539) statement as follows. `\`connect commits all transactions being executed and creates a new session whereas the SET SESSION AUTHORIZATION statement changes the user while keeping intact the existing sessions.

```
gSQL> SET SESSION AUTHORIZATION test;

Session set.

gSQL>
```

Interactive mode is terminated by using `\quit` as follows. For more information, refer to [`\quit`](#2e2015c9e8b6a9bb).

```
gSQL> \quit
%
```

<a id="968f20506f384240"></a>
### Using Host Variable

gsql declares a host variable in an interactive mode, and assigns a value to the host variable, then uses the host variable together with the SQL statement.

**Commands**

<a id="eff85f94535ec9ff"></a>
| gsql command | Description |
| --- | --- |
| [`\var`](#466b7f8794c4595b) | It declares the host variable. |
| [`\exec :var := value`](#7b19e6e57e1e5fdd) | It assigns the value to the host variable. |
| [`\print`](#40764010c6ea1a78) | It outputs the value of the host variable. |
| [`\dynamic sql :var`](#0260325eb794a7de) | It executes SQL statements stored in the host variable. |

The following is an example of declaring the host variable by using [`\var`](#466b7f8794c4595b), and assigning the value to the host variable by using [`\exec :var := value`](#7b19e6e57e1e5fdd), and querying the value of the host variable by using [`\print`](#40764010c6ea1a78). For more information, refer to each command.

```
gSQL> \var v_id INTEGER
gSQL> \exec :v_id := 1
gSQL> \print v_id

V_ID
----
   1

gSQL>
```

The variable declared in an interactive mode may be used as the input parameter in the SQL statement as follows.

```
gSQL> SELECT * FROM t1 WHERE id = :v_id;

ID NAME   ADDR        
-- ------ ------------
 1 leekmo Seoul, Korea

1 row selected.

gSQL>
```

The variable declared in an interactive mode may be used as the output parameter in the SQL statement as follows.

```
gSQL> SELECT id INTO :v_id FROM t1 WHERE name = 'mkkim';

V_ID
----
   2

1 row selected.

gSQL>
```

<a id="f4f4c5d06001a42e"></a>
### Controlling Method of Treating SQL Statement

The SQL process methods which are frequently used when processing the SQL such as the execution of prepare/ execute statement or the retrieval by using the cursor may be simulated by using the gsql interactive mode command before developing the application.

**Commands**

<a id="44fea68cf194f857"></a>
| gsql command | Description |
| --- | --- |
| [`\exec sql`](#1f59b89b0868c63c) | It directly executes the SQL statement. |
| [`\prepare sql`](#81d591bf1367796d) | It prepares the SQL statement. |
| [`\exec`](#6bf5fe8d586bd235) | It executes the prepared SQL statement. |
| [`\dynamic sql :var`](#0260325eb794a7de) | It executes the SQL statement stored in the host variable. |

The following Java application is a part of code in $GOLDILOCKS_HOME/sample/JDBC/JdbcSample.java.

```
public static void main(String[] args) throws SQLException
    {
        Connection con = createConnectionByDriverManager("TEST", "test");
        Statement stmt = con.createStatement();
        stmt.execute("CREATE TABLE SAMPLE_TABLE ( ID INTEGER, NAME CHAR(20) )");
        PreparedStatement pstmt = con.prepareStatement("INSERT INTO SAMPLE_TABLE VALUES (?, ?)");
        pstmt.setInt(1, 100);
        pstmt.setString(2, "Tom");
        pstmt.executeUpdate();
        pstmt.setInt(1, 200);
        pstmt.setString(2, "Jerry");
        pstmt.executeUpdate();
        ResultSet rs = stmt.executeQuery("SELECT * FROM SAMPLE_TABLE");
        while (rs.next())
        {
            System.out.println("ID = " + rs.getInt(1) + ": " + rs.getString(2));
        }
        rs.close();
        stmt.close();
        pstmt.close();
        con.close();

        Connection con2 = createConnectionByDataSource("TEST", "test");
        Statement stmt2 = con2.createStatement();
        stmt2.execute("DROP TABLE SAMPLE_TABLE");
        stmt2.close();
        con2.close();
    }
```

The implementation above which used the PreparedStatement class of Java code may be simulated by using [`\prepare sql`](#81d591bf1367796d) and [`\exec`](#6bf5fe8d586bd235) as follows.

```
gSQL> \connect test test
gSQL> \var v_int INTEGER
gSQL> \var v_string VARCHAR(128)
gSQL> CREATE TABLE SAMPLE_TABLE ( ID INTEGER, NAME CHAR(20) );

Table created.

gSQL> \prepare sql INSERT INTO SAMPLE_TABLE VALUES (:v_int, :v_string);

SQL prepared.

gSQL> \exec :v_int := 100
gSQL> \exec :v_string := 'Tom'
gSQL> \exec

1 row created.

gSQL> \exec :v_int := 200
gSQL> \exec :v_string := 'Jerry'
gSQL> \exec

1 row created.

gSQL> SELECT * FROM SAMPLE_TABLE;

 ID NAME                
--- --------------------
100 Tom                 
200 Jerry               

2 rows selected.

gSQL> \connect test test
gSQL> DROP TABLE SAMPLE_TABLE;

Table dropped.

gSQL> \quit
%
```

The following embedded SQL program is a part of code in $GOLDILOCKS_HOME/sample/EmbeddedSQL/sample2.gc.

```
int main(int argc, char **argv)
{

    EXEC SQL BEGIN DECLARE SECTION;
    int          sEmpNo;
    varchar      sEName[20 + 1];
    char         sJob[20];
    long         sSalary;
    EXEC SQL END DECLARE SECTION;

    ... Ellipsis ...
```

• Retrieve employee

```
EXEC SQL
        DECLARE EMP_CUR CURSOR FOR
        SELECT empno, ename, job, sal
        FROM   EMP;

    EXEC SQL OPEN EMP_CUR;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }

    printf(" EMPNO    ENAME                JOB      SALARY\n");
    printf("====== ==================== ========== ========\n");

    while( 1 )
    {
        EXEC SQL
            FETCH EMP_CUR
            INTO  :sEmpNo, :sEName, :sJob, :sSalary;

        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
            goto fail_exit;
        }

        sRecordCount ++;

        printf("%6d %20s %10s %8ld\n",
               sEmpNo, sEName.arr, sJob, sSalary);
    }

    printf("====== ==================== ========== ========\n");
    printf("Record Count = %d\n", sRecordCount);
    printf("====== ==================== ========== ========\n");

    EXEC SQL CLOSE EMP_CUR;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
    
    ... Ellipsis ...

}
```

The query processing which uses the cursor in an embedded SQL program above may be simulated in gsql interactive mode as follows.

```
gSQL> \var sEmpNo INTEGER
gSQL> \var sEName VARCHAR(20)
gSQL> \var sJob CHAR(20)
gSQL> \var sSalary BIGINT
gSQL> DECLARE EMP_CUR CURSOR FOR
        SELECT empno, ename, job, sal
        FROM   EMP;

Cursor declared.

gSQL> OPEN EMP_CUR;

Cursor is open.

gSQL> FETCH EMP_CUR
            INTO  :sEmpNo, :sEName, :sJob, :sSalary; 

SEMPNO SENAME SJOB                 SSALARY
------ ------ -------------------- -------
  2854 Park   RND                      800

1 row fetched.

gSQL> FETCH EMP_CUR
            INTO  :sEmpNo, :sEName, :sJob, :sSalary; 

SEMPNO SENAME SJOB                 SSALARY
------ ------ -------------------- -------
  2098 Kim    SALESMAN                1600

1 row fetched.

gSQL> FETCH EMP_CUR
            INTO  :sEmpNo, :sEName, :sJob, :sSalary; 

SEMPNO SENAME SJOB                 SSALARY
------ ------ -------------------- -------
  2175 Choi   SALESMAN                1250

1 row fetched.

gSQL> CLOSE EMP_CUR;

Cursor closed.

gSQL>
```

> The following statements are limitedly used in an embedded SQL in other DBMS. On the other hand, in GOLDILOCKS, the followings are used not only in an embedded SQL but also can be used as an argument of SQL processing functions when developing the application of ODBC or JDBC.  
> 
> 
> - [SELECT .. INTO](../part-03-sql-manual/20-sql-references-h-z.md#62c0547d8bd310b3)
> - [DECLARE cursor_name](../part-03-sql-manual/19-sql-references-c-g.md#0871779c00d431a8)
> - [OPEN cursor_name](../part-03-sql-manual/20-sql-references-h-z.md#a52c4df668fbd9cb)
> - [FETCH cursor_name](../part-03-sql-manual/19-sql-references-c-g.md#c65c0d3544ea9773)
> - [CLOSE cursor_name](../part-03-sql-manual/19-sql-references-c-g.md#e85469aa112b48af)
> 

<a id="e46c495534c79340"></a>
### Information of SQL Execution Plan

Refer to the following commands.

**Command**

<a id="da8fcb689d196cdb"></a>
| gsql Command | Description |
| --- | --- |
| [`\explain plan`](#619d085ddbb3b859) | It outputs the execution plan for the SQL statement. |
| [`\set autotrace`](#e462737e3684880f) | It sets whether to output the execution plan. |

The execution plan of the SQL statement is viewed in an interactive mode by using `\explain plan` or `\set autotrace` as follows. For more information about the command, refer to [`\explain plan`](#619d085ddbb3b859) or [`\set autotrace`](#e462737e3684880f), and for more information about the analysis of execution plan, refer to [SQL Execution Plan](../part-03-sql-manual/15-sql-tuning.md#eb7fd3cec4fcfcc2).

The following is an example of executing the query No.4 of TPC-H benchmark by using the `\explain plan`.

```
\explain plan
select
    o_orderpriority,
    count(*) as order_count
from
    orders
where
      o_orderdate >= date '1993-07-01'
  and o_orderdate < date '1993-07-01' + interval '3' month
  and exists (
               select
                      *
                 from
                      lineitem
                where
                      l_orderkey = o_orderkey
                  and l_commitdate < l_receiptdate
             )
group by
    o_orderpriority
order by
    o_orderpriority;

O_ORDERPRIORITY ORDER_COUNT
--------------- -----------
1-URGENT              10594
2-HIGH                10476
3-MEDIUM              10410
4-NOT SPECIFIED       10556
5-LOW                 10487

5 rows selected.

>>>  start print plan

< Execution Plan >
=====================================================================================
|  IDX  |  NODE DESCRIPTION                                            |       ROWS |
-------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |            |
|    1  |    SORT INSTANT ACCESS                                       |          5 |
|    2  |      GROUP HASH INSTANT ACCESS                               |          5 |
|    3  |        NESTED LOOP JOIN (LEFT SEMI)                          |      52523 |
|    4  |          TABLE ACCESS ("ORDERS")                             |      57218 |
|    5  |          INDEX ACCESS ("LINEITEM, LINEITEM_PK_INDEX")        |      52523 |
=====================================================================================

     1  -  SORT KEY : "ORDERS.O_ORDERPRIORITY ASC NULLS LAST"
           RECORD COLUMNS : COUNT(*)
           READ COLUMNS : O_ORDERPRIORITY, COUNT(*)
     2  -  AGGREGATIONS : COUNT(*)
           GROUPING COLUMNS : O_ORDERPRIORITY
           RECORD COLUMNS : COUNT(*)
           READ COLUMNS : O_ORDERPRIORITY, COUNT(*)
     3  -  JOINED COLUMNS : ORDERS.O_ORDERPRIORITY
     4  -  READ COLUMNS : O_ORDERKEY, O_ORDERDATE, O_ORDERPRIORITY
             PHYSICAL FILTER : O_ORDERDATE >= CAST( '1993-07-01' AS DATE ) AND O_ORDERDATE < ( CAST( '1993-07-01' AS DATE ) + CAST( '3' AS INTERVAL(MONTH) ) )
     5  -  READ INDEX COLUMNS : L_ORDERKEY
           READ TABLE COLUMNS : L_COMMITDATE, L_RECEIPTDATE
             MIN RANGE : L_ORDERKEY = {O_ORDERKEY}
             MAX RANGE : L_ORDERKEY = {O_ORDERKEY}
             PHYSICAL TABLE FILTER : L_COMMITDATE < L_RECEIPTDATE

<<<  end print plan
```

<a id="6c4d6fd77803494a"></a>
## Command Option Reference

This chapter describes the options for performing gsql command at the shell prompt.

<a id="2193872f8b5e647a"></a>
### Username Password

<a id="18eed5a545346351"></a>
#### Description

It connects to GOLDILOCKS by using the username and password.

<a id="0af9bd7efe671924"></a>
#### Examples

The following is an example of connecting to GOLDILOCKS with the test user.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL>
```

The following is an example of failing to connect to GOLDILOCKS with the invalid username or password.

```
% gsql invalid_user invalid_password

ERR-28000(16004): invalid username/password; logon denied

%
```

<a id="e734f0be33270c01"></a>
### --as {SYSDBA|ADMIN}

<a id="c52203e5a5e1b756"></a>
#### Description

It connects to GOLDILOCKS with SYSDBA role or ADMIN role.  
For more information about the description of the role, refer to [Startup and Shutdown Server](#30a646b9d93b86a8).

```
% gsql sys gliese --as sysdba
```

<a id="78cad437dadf394b"></a>
#### Example

The following is an example of connecting to GOLDILOCKS with SYSDBA role.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL>
```

<a id="fdab3ae572f6d7e8"></a>
### --conn-string

<a id="4ae025e7829e4cbd"></a>
#### Description

It connects to GOLDILOCKS by using the connection string.  
The details of the connection string to be described should used in a form as same as the input string of the ODBC function, [SQLDriverConnect](../part-05-developer-manual/31-odbc.md#d5616fec7967bb99). For more information about the connection string, refer to [SQLDriverConnect](../part-05-developer-manual/31-odbc.md#d5616fec7967bb99) function.

<a id="9d3b80aff5c925f2"></a>
#### Example

The following is an example of connecting to GOLDILOCKS with --conn-string.

```
% gsql --conn-string 'DSN=GOLDILOCKS;UID=test;PWD=test'

Connected to GOLDILOCKS Database.

gSQL>
```

<a id="9857293bcc9a1306"></a>
### --dsn

<a id="d70fe48b3cb07820"></a>
#### Description

It connects to GOLDILOCKS by using Data Source Name (DSN) defined in the file odbc.ini.  
DSN should be defined in the odbc.ini file. For more information about the odbc.ini file, refer to [DSN Configuration on UNIX](../part-05-developer-manual/31-odbc.md#3647d910468482d2).  
If DSN is omitted, the default value is GOLDILOCKS.

<a id="2857beb1aff61a7e"></a>
#### Examples

The following is an example of connecting to GOLDILOCKS with DSN.

```
% gsql test test --dsn GOLDILOCKS

Connected to GOLDILOCKS Database.

gSQL>
```

The content of odbc.ini file used in the example above is as follows.

```
[GOLDILOCKS]
DATE_FORMAT = YYYY-MM-DD
TIME_FORMAT = HH24:MI:SS.FF6
```

> gsql does not recognize HOST, PORT of odbc.ini file property.

<a id="2e3f552cbdd00e2d"></a>
### --enable-color

<a id="91702f39d98425e4"></a>
#### Description

It outputs each row of query results in a different color on the terminal to easily distinguish them.  
Each row of the query results is output with a different color in an interactive mode, and it is also applied to the results of the SELECT statement included in the file by using the [--import](#dbec8ec874315003) option.

<a id="1ca726c27f0ace50"></a>
#### Examples

The following is an example of performing gsql by using the --enable-color option, then outputting the query results in an interactive mode.

```
% gsql test test --enable-color

Connected to GOLDILOCKS Database.

gSQL> SELECT id, addr FROM t1;

ID ADDR         
-- -------------
 1 Seoul, Korea 
 2 Seoul, Korea 
 3 Inchon, Korea

3 rows selected.

gSQL>
```

The following is an example of executing a SELECT query included in the file by using the --import option.

```
% gsql test test --import 'sample_select.sql' --enable-color
SELECT id, addr FROM t1;

ID ADDR         
-- -------------
 1 Seoul, Korea 
 2 Seoul, Korea 
 3 Inchon, Korea

3 rows selected.

%
```

<a id="e3dc43a828e43183"></a>
### --help

<a id="3e8a1c8e6d613866"></a>
#### Description

It briefly displays the option list of gsql program.

<a id="79de35b0db3abfdc"></a>
#### Example

The following is an example of using the --help option.

```
% gsql --help

Usage 

    gsql [user_name [password]] [options]

Arguments:

    user_name       user name
    password        password

Options:

    --version                      print version information and exit
    --import       FILE            import sql FILE
    --no-prompt                    suppresses the display of the banner and prompts
    --dsn          DSN             dsn string (default is GOLDILOCKS)
    --conn-string  'CONN-STRING'   connection string
    --prompt       STRING          change prompt string
    --enable-color                 enable colored text
    --as           {SYSDBA|ADMIN}  privilege
    --silent                       suppresses the display of the result message and echoing of commands
    --help                         print help message

%
```

<a id="dbec8ec874315003"></a>
### --import

<a id="8daac92519682d48"></a>
#### Description

It performs the SQL statement which is not an interactive mode in the file in batch.  
The file name is enclosed in a single quote ('), and it can use an absolute or relative path.

<a id="32d70ece8d183d8e"></a>
#### Examples

The following is an example of executing the SQL statement by using the absolute path of the file.

```
% gsql test test --import '/home/goldilocks/sample.sql'
DROP TABLE IF EXISTS t1;

Table dropped.

CREATE TABLE t1 
(
    id   INTEGER PRIMARY KEY,
    name VARCHAR(128),
    addr VARCHAR(128)
);

Table created.


CREATE INDEX t1_idx_name ON t1(name);

Index created.


INSERT INTO t1 
       VALUES ( 1, 'leekmo', 'Seoul, Korea'  ),
              ( 2, 'mkkim' , 'Seoul, Korea'  ),
              ( 3, 'xcom73', 'Inchon, Korea' );

3 rows created.

COMMIT;

Commit complete.

%
```

The following is an example of executing the SQL statement by using the relative path of the file.

```
% gsql test test --import 'sample.sql'
DROP TABLE IF EXISTS t1;

Table dropped.

CREATE TABLE t1 
(
    id   INTEGER PRIMARY KEY,
    name VARCHAR(128),
    addr VARCHAR(128)
);

Table created.


CREATE INDEX t1_idx_name ON t1(name);

Index created.


INSERT INTO t1 
       VALUES ( 1, 'leekmo', 'Seoul, Korea'  ),
              ( 2, 'mkkim' , 'Seoul, Korea'  ),
              ( 3, 'xcom73', 'Inchon, Korea' );

3 rows created.

COMMIT;

Commit complete.

%
```

<a id="ebd2b4b62b6e77f6"></a>
### --no-prompt

<a id="f3e2d949b6ac7272"></a>
#### Description

It does not output the prompt when performing an interactive mode.

<a id="5190f5d3c2dbacde"></a>
#### Example

The following is an example of using --no-prompt.

```
% gsql test test --no-prompt
SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.
```

<a id="92dd1cb2c92f7507"></a>
### --prompt

<a id="95cc012a123da390"></a>
#### Description

It sets the gsql prompt when performing an interactive mode.  
The default value is gSQL.  
The special characters or spaces are enclosed in double quotes (") as follows.

```
% gsql test test --prompt "GOLDILOCKS Venus.3.2"
```

<a id="d0a670f3e7edef2f"></a>
#### Example

The following is an example of which the prompt is changed to GOLDILOCKS in an interactive mode by using the --prompt option.

```
% gsql test test --prompt GOLDILOCKS

Connected to GOLDILOCKS Database.

GOLDILOCKS> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.

GOLDILOCKS>
```

<a id="fc2272b10d0efc38"></a>
### --silent

<a id="2cd5ceb93dd6c121"></a>
#### Description

It does not output the results of SQL statement.  
It is useful when executing large amounts of SQL statements by reading the file with [--import](#dbec8ec874315003) command.  
The --silent option is also applied when operating in an interactive mode.

<a id="c28b8ef29e45592c"></a>
#### Example

The following is an example of executing the DictionarySchema.sql file in the $GOLDILOCKS_HOME/admin directory by using the --silent option.

```
% gsql sys gliese --as sysdba --import 'DictionarySchema.sql' --silent
%
```

<a id="1ee15cbdf84830f0"></a>
### --version

<a id="7a4fd7c1fe81c74b"></a>
#### Description

It outputs the version information of the gsql program.  
It is recommended to use the gsql program with the version as same as the version of GOLDILOCKS. The GOLDILOCKS version can be viewed via the SQL function [VERSION](../part-03-sql-manual/17-built-in-function-references.md#4c4cf16c3fb15e3f) as follows.

```
gSQL> SELECT version() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="fc58dff73d9890d4"></a>
#### Example

The following is an example of using the --version option.

```
% gsql --version

%
```

<a id="e19b8f83d1f70038"></a>
## Interactive Command References

All gsql-specific commands start with backslash `(\)` in an interactive mode.

<a id="e9fcaf4386815ef7"></a>
### `\\`

<a id="9c334552e9a1c20d"></a>
#### Syntax

```
\\
```

<a id="1841b0b4eca62080"></a>
#### Description

It executes the most recent successfully executed SQL statement.

<a id="dd3d77f33611212e"></a>
#### Examples

```
gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.
```

• It executes the most recent successfully executed SQL statement.

```
gSQL> \\

DUMMY
-----
X    

1 row selected.

gSQL> SELECT * FROM invalid_table;

ERR-42000(16040): table or view does not exist : 
SELECT * FROM invalid_table
              *
ERROR at line 1:
```

• It executes the most recent successfully executed SQL statement rather than executing the failed SQL statement.

```
gSQL> \\

DUMMY
-----
X    

1 row selected.
```

<a id="7081c130d290bfdc"></a>
### `\connect`

<a id="a9b0e88eefe7f8e0"></a>
#### Syntax

```
\connect username password [as sysdba]
```

<a id="1933c284ab0ffe9f"></a>
#### Description

It is newly connected with the entered username and password.  
If any uncommitted transaction exists, it performs COMMIT.

<a id="ff1ded975a42a202"></a>
#### Examples

The following is an example of connecting with the test account.

```
gSQL> \connect test test
gSQL>
```

An error occurs if the password is invalid as follows.

```
gSQL> \connect test invalid_password

ERR-28000(16004): invalid username/password; logon denied

gSQL> SELECT * FROM dual;

ERR-08003(40044): connection does not exist
```

The following is an example of connecting with the SYSDBA role.

```
gSQL> \connect sys gliese as sysdba
gSQL>
```

<a id="eaaadc4537241a95"></a>
### `\cstartup`

<a id="01c92bffa3248c22"></a>
#### Syntax

```
\cstartup
\cstartup nomount
\cstartup mount
\cstartup open
\cstartup local open
\cstartup global open
```

<a id="b58df62269491ad3"></a>
#### Description

It starts up GOLDILOCKS server in a cluster environment.

To execute `\cstartup` command, it should connect with SYSDBA role or ADMIN role. For more information about how to connect with SYSDBA role, refer to [startup and shutdown server](#30a646b9d93b86a8).

- `\cstartup nomount`
    - It starts up the corresponding server on NOMOUNT phase.
- `\cstartup mount`
    - It starts up the corresponding server on MOUNT phase.
- `\cstartup local open`
    - It starts up the corresponding server and other servers on LOCAL OPEN phase.
- `\cstartup global open`
    - It startsup all servers on GLOBAL OPEN phase.
- `\cstartup open`
    - It is as same as `\cstartup global open`.
- `\cstartup`
    - It is as same as `\cstartup global open`.

`\cstartup local open`  command and `\cstartup global open` command startup the corresponding server and other servers to the corresponding phase. Other commands are applied only to the corresponding server, so the server should be started up to LOCAL OPEN phase for the multi-level startup using [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references-a-b.md#6b3352cd0d97f557).

The server startup phases are classified as NOMOUNT, MOUNT, LOCAL OPEN, GLOBAL OPEN. For more information, refer to [multi-level startup](../part-02-administration-manual/5-basic-management-of-goldilocks-database.md#83b0b11e83fe4d59).

[ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references-a-b.md#6b3352cd0d97f557) should be performed to move on to the next phase after executing `\cstartup` command.

`\cstartup` using glocator can be viewed via [CSTARTUP and CSHUTDOWN](46-glocator.md#ea4e957f202dfc60).


> 
> - It is command used only in a C/S environment. It can be used only in gsqlnet.
> - Commands other than `\cstartup nomount/ mount` affects on the corresponding server and other servers. Therefore, if LOCATOR_DSN is not specified in [odbc.ini file](../part-05-developer-manual/31-odbc.md#725df1c9d28dbaab), then an error occurs.
> 

<a id="6b876d410f627995"></a>
#### Example

The following is an example of starting up GOLDILOCKS.

```
% gsqlnet sys gliese --as sysdba

Connected to an idle instance.

gSQL> \cstartup

Startup success
```

<a id="efc83a8dfba6b5c9"></a>
### `\cshutdown`

<a id="175487731de8b63d"></a>
#### Syntax

```
\cshutdown
\cshutdown abort
\cshutdown immediate
\cshutdown transactional
\cshutdown normal
```

<a id="f4fb70f49cd10f64"></a>
#### Description

It shuts down GOLDILOCKS server in a cluster environment.

To execute `\cshutdown` command, it should connect with SYSDBA role or ADMIN role. For more information about how to connect with SYSDBA role, refer to [startup and shutdown server](#30a646b9d93b86a8).

- `\`cshutdown normal
    - It blocks the connection from the new session and waits for all currently connected sessions to be terminated, then performs the checkpoint and shuts down the server.
- `\`cshutdown transactional
    - It blocks the start of a new transaction and waits for all currently running transactions to be terminated, then performs the checkpoint and shuts down the server.
- `\`cshutdown immediate
    - It blocks the execution of a new unit operation (e.g. FETCH, EXECUTE), waits for all currently running unit operations to be terminated, then rolls back all transactions and performs the checkpoint and shuts down the server.
- `\`cshutdown abort
    - The server is forcibly shut down immediately regardless of the status of the currently connected session.
- `\`cshutdown
    - It is as same as `\`cshutdown normal.

`\cshutdown` using glocator can be viewed via [CSTARTUP and CSHUTDOWN](46-glocator.md#ea4e957f202dfc60).

> • It is command used only in a C/S environment. It can be used only in gsqlnet.  
> • Commands other than `\cshutdown` affects on the corresponding server and other servers. Therefore, if LOCATOR_DSN is not specified in [odbc.ini file](../part-05-developer-manual/31-odbc.md#725df1c9d28dbaab), then an error occurs.

<a id="a168a005d0abe8f2"></a>
#### Example

The following is an example of shutting down GOLDILOCKS.

```
% gsqlnet sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \cshutdown

Shutdown success

gSQL>
```

<a id="0f59116afaf841a9"></a>
### `\ddl_cluster`

<a id="b4518dd2ee86b03b"></a>
#### Syntax

```
\ddl_cluster
```

<a id="9f2166327e68be90"></a>
#### Description

It outputs a cluster DDL corresponding to the current status of a cluster system.  
This statement is valid in a cluster system.

<a id="f12dbcbe1e72f62e"></a>
#### Example

The following is an example of executing `\ddl_cluster` command for a cluster system consisting as 3 x 2.

```
gSQL> \ddl_cluster


SET SESSION AUTHORIZATION "SYS";
CREATE CLUSTER GROUP "G1"
       CLUSTER MEMBER "G1N1" HOST '127.0.0.1' PORT '10110'
;
COMMIT;

SET SESSION AUTHORIZATION "SYS";
ALTER CLUSTER GROUP "G1" ADD
      CLUSTER MEMBER "G1N2" HOST '127.0.0.1' PORT '10120'
;
COMMIT;

SET SESSION AUTHORIZATION "SYS";
CREATE CLUSTER GROUP "G2"
       CLUSTER MEMBER "G2N1" HOST '127.0.0.1' PORT '10210'
;
COMMIT;

SET SESSION AUTHORIZATION "SYS";
ALTER CLUSTER GROUP "G2" ADD
      CLUSTER MEMBER "G2N2" HOST '127.0.0.1' PORT '10220'
;
COMMIT;

SET SESSION AUTHORIZATION "SYS";
CREATE CLUSTER GROUP "G3"
       CLUSTER MEMBER "G3N1" HOST '127.0.0.1' PORT '10310'
;
COMMIT;

SET SESSION AUTHORIZATION "SYS";
ALTER CLUSTER GROUP "G3" ADD
      CLUSTER MEMBER "G3N2" HOST '127.0.0.1' PORT '10320'
;
```

<a id="2b12df2779f07dce"></a>
### `\ddl_db`

<a id="7f163d2c18e74d56"></a>
#### Syntax

```
\ddl_db 
\ddl_db GRANT
\ddl_db COMMENT
```

<a id="5499432706f843ca"></a>
#### Description

It outputs the DDL statements corresponding to the current state of the database object.

> The objects stored in the recycle bin are not output.

**`\ddl_db` commands**

<a id="77eca1b10e46cb9c"></a>
| Command | Description |
| --- | --- |
| `\ddl_db` | It outputs the DDL statements of all objects created in the database. |
| `\ddl_db GRANT` | It outputs the GRANT .. ON DATABASE statement corresponding to the privilege information on the database object. |
| `\ddl_db COMMENT` | It outputs the COMMENT ON DATABASE statement corresponding to the comment information on the database object. |

The result of `\ddl_db` command without any option outputs the DDL statements in the following order.

- Database DDL
- Tablespace DDL
- Profile DDL
- Authorization DDL
- Schema DDL
- Authorization schema path DDL
- Database privilege DDL
- Tablespace privilege DDL
- Schema privilege DDL
- Public synonym DDL
- Table DDL
- Table privilege DDL
- Table option DDL
- Constraint DDL
- Index DDL
- View DDL
- View privilege DDL
- Sequence DDL
- Sequence privilege DDL
- Synonym DDL
- Stored procedure/ function DDL
- Package DDL
- Audit policy DDL

However, the information related to the following schemas which include the dictionary information are not output.

- DICTIONARY_SCHEMA
- INFORMATION_SCHEMA
- PERFORMANCE_VIEW_SCHEMA
- DEFINITION_SCHEMA
- FIXED_TABLE_SCHEMA

The DDL statement for the schema above which includes the dictionary information can be output by using [`\ddl_schema`](#6cc04567194b0f52).

<a id="5b9a9a7ea7893899"></a>
#### Examples

The following is an example of executing `\ddl_db`.

```
gSQL> \ddl_db
```

• Database DDL

```
SET SESSION AUTHORIZATION "SYS"; 
COMMENT 
    ON DATABASE 
    IS 'goldilocks database' 
;
```

• Tablespace DDL

```
SET SESSION AUTHORIZATION "SYS"; 
CREATE MEMORY DATA TABLESPACE "TEST_TBS" 
    DATAFILE '/home/GOLDILOCKS/workspace/product/Gliese/home/db/test1.dbf' 
        SIZE 10477568 REUSE 
    ONLINE 
    LOGGING 
    EXTSIZE 262144 
;

SET SESSION AUTHORIZATION "SYS"; 
ALTER TABLESPACE "TEST_TBS" 
    ADD DATAFILE '/home/GOLDILOCKS/workspace/product/Gliese/home/db/test2.dbf' 
        SIZE 10477568 REUSE 
;

SET SESSION AUTHORIZATION "SYS"; 
ALTER TABLESPACE "TEST_TBS" 
    ADD DATAFILE '/home/GOLDILOCKS/workspace/product/Gliese/home/db/test3.dbf' 
        SIZE 10477568 REUSE 
;

SET SESSION AUTHORIZATION "SYS"; 
COMMENT 
    ON TABLESPACE "TEST_TBS" 
    IS 'comment tablespace TPC data' 
;

SET SESSION AUTHORIZATION "SYS"; 
CREATE MEMORY TEMPORARY TABLESPACE "TEMP_TBS" 
    MEMORY 'test_mem' 
        SIZE 10477568 
    EXTSIZE 262144 
;

... Ellipsis ...
```

• Sequence privilege DDL

```
SET SESSION AUTHORIZATION "H_USER"; 
GRANT 
    USAGE ON SEQUENCE "H_USER"."H_SEQ" 
    TO "PUBLIC" 
;

SET SESSION AUTHORIZATION "H_USER"; 
GRANT 
    USAGE ON SEQUENCE "H_USER"."H_SEQ" 
    TO "TEST" 
    WITH GRANT OPTION 
;

SET SESSION AUTHORIZATION "H_USER"; 
GRANT 
    USAGE ON SEQUENCE "H_USER"."H_SEQ" 
    TO "C_USER" 
;

SET SESSION AUTHORIZATION "C_USER"; 
GRANT 
    USAGE ON SEQUENCE "C_USER"."C_SEQ" 
    TO "TEST" 
;

SET SESSION AUTHORIZATION "C_USER"; 
GRANT 
    USAGE ON SEQUENCE "C_USER"."C_SEQ" 
    TO "H_USER" 
;
```

The following is an example of executing `\ddl_db GRANT`.

```
gSQL> \ddl_db GRANT


SET SESSION AUTHORIZATION "SYS"; 
GRANT 
    ALTER DATABASE ON DATABASE 
    TO "TEST" 
    WITH GRANT OPTION 
;

SET SESSION AUTHORIZATION "SYS"; 
GRANT 
    ALTER SYSTEM ON DATABASE 
    TO "TEST" 
    WITH GRANT OPTION 
;

... Ellipsis ...
```

<a id="709988ed6249b4b4"></a>
### `\ddl_tablespace`

<a id="13b584ef05fa6123"></a>
#### Syntax

```
\ddl_tablespace name
\ddl_tablespace name CREATE
\ddl_tablespace name ALTER
\ddl_tablespace name TABLE
\ddl_tablespace name CONSTRAINT
\ddl_tablespace name INDEX
\ddl_tablespace name GRANT
\ddl_tablespace name COMMENT
```

<a id="27e2624b59cae781"></a>
#### Description

It outputs the DDL statements for the current state of the tablespace object.

> The objects stored in the recycle bin are not output.

**`\ddl_tablespace` commands**

<a id="c03063569f2c1904"></a>
| Command | Description |
| --- | --- |
| `\ddl_tablespace name` | It performs all options below. |
| `\ddl_tablespace name CREATE` | It outputs the CREATE TABLESPACE statement of the tablespace object. |
| `\ddl_tablespace name ALTER` | It outputs the ALTER TABLESPACE statements for the datafile or memory added to the tablespace. |
| `\ddl_tablespace name TABLE` | It outputs the CREATE TABLE statements of the tables stored in the tablespace. |
| `\ddl_tablespace name CONSTRAINT` | It outputs the ALTER TABLE statements of the constraints stored in the tablespace. |
| `\ddl_tablespace name INDEX` | It outputs the CREATE INDEX statements of the indexes stored in the tablespace. |
| `\ddl_tablespace name GRANT` | It outputs the GRANT .. ON TABLESPACE statement for the privilege information on the tablespace. |
| `\ddl_tablespace name COMMENT` | It outputs the COMMENT ON TABLESPACE statement corresponding o the comment on the tablespace. |

<a id="30ccd0fa281b4a3d"></a>
#### Examples

The following is an example of executing `\ddl_tablespace CREATE`.

```
gSQL> \ddl_tablespace test_tbs CREATE


SET SESSION AUTHORIZATION "SYS"; 
CREATE MEMORY DATA TABLESPACE "TEST_TBS" 
    DATAFILE '/home/GOLDILOCKS/workspace/product/Gliese/home/db/test1.dbf' 
        SIZE 10477568 REUSE 
    ONLINE  
    EXTSIZE 262144 
;
```

The following is an example of executing `\ddl_tablespace ALTER`.

```
gSQL> \ddl_tablespace test_tbs ALTER


SET SESSION AUTHORIZATION "SYS"; 
ALTER TABLESPACE "TEST_TBS" 
    ADD DATAFILE 
        '/home/GOLDILOCKS/workspace/product/Gliese/home/db/test2.dbf' 
        SIZE 10477568 REUSE 
      , 
        '/home/GOLDILOCKS/workspace/product/Gliese/home/db/test3.dbf' 
        SIZE 10477568 REUSE 
;
```

<a id="0b5ef20f54332314"></a>
### `\ddl_profile`

<a id="c502d0442493c3c2"></a>
#### Syntax

```
\ddl_profile name
\ddl_profile name CREATE
\ddl_profile name COMMENT
```

<a id="ef29caa957711040"></a>
#### Description

It outputs the DDL statement for the current state of the profile object.

**`\ddl_profile` commands**

<a id="10522b7d39307d07"></a>
| Command | Description |
| --- | --- |
| `\ddl_profile name` | It performs all options below. |
| `\ddl_profile name CREATE` | It outputs the CREATE PROFILE statement of the profile object. |
| `\ddl_profile name COMMENT` | It outputs the COMMENT ON PROFILE statement corresponding to the comment on the profile. |

<a id="468182a239290522"></a>
#### Example

The following is an example of executing `\ddl_profile CREATE`.

```
gSQL> \ddl_profile prof1 CREATE


SET SESSION AUTHORIZATION "SYS"; 
CREATE PROFILE "PROF1" LIMIT 
    FAILED_LOGIN_ATTEMPTS   DEFAULT 
    PASSWORD_LOCK_TIME   1/86400 
    PASSWORD_LIFE_TIME   UNLIMITED 
    PASSWORD_GRACE_TIME   100 
    PASSWORD_REUSE_MAX   DEFAULT 
    PASSWORD_REUSE_TIME   DEFAULT 
    PASSWORD_VERIFY_FUNCTION   KISA_VERIFY_FUNCTION 
;
COMMIT;
```

<a id="e113a955e7bd812e"></a>
### `\ddl_audit_policy`

<a id="d4bdc9ac1e987eed"></a>
#### Syntax

```
\ddl_audit_policy name
\ddl_audit_policy name CREATE
\ddl_audit_policy name AUDIT
\ddl_audit_policy name COMMENT
```

<a id="9dd9a657ca0589f0"></a>
#### Description

It outputs the DDL statement for the current state of the audit policy object.

> The objects stored in the recycle bin are not output.

**`\ddl_audit_policy` commands**

<a id="89878a4781188872"></a>
| Command | Description |
| --- | --- |
| `\ddl_audit_policy name` | It perform all options below. |
| `\ddl_audit_policy name CREATE` | It outputs CREATE AUDIT POLICY statement of the audit policy object. |
| `\ddl_audit_policy name AUDIT` | It outputs AUDIT POLICY statement of the audit policy object. |
| `\ddl_audit_policy name COMMENT` | It outputs the COMMENT ON AUDIT POLICY statement corresponding to the comment on the audit policy. |

<a id="14fbae18b8cc7523"></a>
#### Examples

The following is an example of executing `\ddl_audit_policy CREATE`.

```
gSQL> \ddl_audit_policy p1 CREATE


SET SESSION AUTHORIZATION "SYS"; 
CREATE AUDIT POLICY "P1"  
       ACTIONS SELECT ON "PUBLIC"."T1" 
             , INSERT ON "PUBLIC"."T1" 
             , UPDATE ON "PUBLIC"."T2" 
             , ALL ON "PUBLIC"."SEQ1" 
             , SELECT ON "PUBLIC"."SEQ2" 
             , EXECUTE ON "PUBLIC"."FUNC2" 
;
COMMIT;
```

<a id="be76567242f385a0"></a>
### `\ddl_auth`

<a id="41de38cf385dcdc4"></a>
#### Syntax

```
\ddl_auth name
\ddl_auth name CREATE
\ddl_auth name SCHEMA PATH
\ddl_auth name SCHEMA
\ddl_auth name TABLE
\ddl_auth name CONSTRAINT
\ddl_auth name INDEX
\ddl_auth name VIEW
\ddl_auth name SEQUENCE
\ddl_auth name SYNONYM
\ddl_auth name PROCEDURE
\ddl_auth name PACKAGE
\ddl_auth name COMMENT
```

<a id="16196a0a31ff9505"></a>
#### Description

It outputs the DDL statements for the current state of the account object.

> The objects stored in the recycle bin are not output.

**`\ddl_auth` commands**

<a id="897553a5f0d2207c"></a>
| Command | Description |
| --- | --- |
| `\ddl_auth name` | It performs all options below. |
| `\ddl_auth name CREATE` | It outputs the CREATE USER statement of the user object. |
| `\ddl_auth name SCHEMA` | It outputs the CREATE SCHEMA statement of schemas owned by a user. |
| `\ddl_auth name SCHEMA PATH` | It outputs the ALTER USER statement corresponding to the schema path of the account. |
| `\ddl_auth name TABLE` | It outputs the CREATE TABLE statements of tables owned by a user. |
| `\ddl_auth name CONSTRAINT` | It outputs the ALTER TABLE statements of constraints owned by a user. |
| `\ddl_auth name INDEX` | It outputs the CREATE INDEX statements of indexes owned by a user. |
| `\ddl_auth name VIEW` | It outputs the CREATE VIEW statements of views owned by a user. |
| `\ddl_auth name SEQUENCE` | It outputs the CREATE SEQUENCE statements of sequences owned by a user. |
| `\ddl_auth name SYNONYM` | It outputs the CREATE SYNONYM statements of synonyms owned by a user. |
| `\ddl_auth name PROCEDURE` | It outputs the CREATE PROCEDURE/ FUNCTION statements of procedures and functions owned by a user. |
| `\ddl_auth name PACKAGE` | It outputs the CREATE PACKAGE/PACKAGE BODY statements of packages owned by a user. |
| `\ddl_auth name COMMENT` | It outputs the COMMENT ON AUTHORIZATION statement corresponding to comments on the account. |

<a id="07c0c2c2c642ee4e"></a>
#### Examples

The following is an example of executing `\ddl_auth CREATE`.

```
gSQL> \ddl_auth h_user CREATE


SET SESSION AUTHORIZATION "SYS"; 
CREATE USER "H_USER" 
    IDENTIFIED BY H_USER 
    DEFAULT TABLESPACE "TEST_TBS" 
    TEMPORARY TABLESPACE "TEMP_TBS" 
    WITHOUT SCHEMA 
;
```

The following is an example of executing `\ddl_auth SCHEMA`.

```
gSQL> \ddl_auth h_user SCHEMA


SET SESSION AUTHORIZATION "SYS"; 
CREATE SCHEMA "H_USER" 
    AUTHORIZATION "H_USER" 
;
```

The following is an example of executing `\ddl_auth TABLE`.

```
gSQL> \ddl_auth h_user TABLE

SET SESSION AUTHORIZATION "H_USER"; 
CREATE TABLE "H_USER"."REGION" 
    ( 
        "R_REGIONKEY" NUMBER( 10, 0 )
      , "R_NAME" CHARACTER( 25 OCTETS )
      , "R_COMMENT" CHARACTER VARYING( 152 OCTETS )
    ) 
    PCTFREE  10 
    PCTUSED  60 
    INITRANS 4 
    MAXTRANS 8 
    STORAGE 
    ( 
        INITIAL 524288 
        NEXT    262144 
        MINSIZE 524288 
        MAXSIZE 35184372088832 
    ) 
    TABLESPACE "TEST_TBS" 
;

SET SESSION AUTHORIZATION "H_USER"; 
CREATE TABLE "H_USER"."NATION" 
    ( 
        "N_NATIONKEY" NUMBER( 10, 0 )
      , "N_NAME" CHARACTER( 25 OCTETS )
      , "N_REGIONKEY" NUMBER( 10, 0 )
      , "N_COMMENT" CHARACTER VARYING( 152 OCTETS )
    ) 
    PCTFREE  10 
    PCTUSED  60 
    INITRANS 4 
    MAXTRANS 8 
    STORAGE 
    ( 
        INITIAL 524288 
        NEXT    262144 
        MINSIZE 524288 
        MAXSIZE 35184372088832 
    ) 
    TABLESPACE "TEST_TBS" 
;
```

<a id="6cc04567194b0f52"></a>
### `\ddl_schema`

<a id="2566fad632855a9d"></a>
#### Syntax

```
\ddl_schema name
\ddl_schema name CREATE
\ddl_schema name TABLE
\ddl_schema name CONSTRAINT
\ddl_schema name INDEX
\ddl_schema name VIEW
\ddl_schema name SEQUENCE
\ddl_schema name SYNONYM
\ddl_schema name PROCEDURE
\ddl_schema name PACKAGE
\ddl_schema name GRANT
\ddl_schema name COMMENT
```

<a id="850a61cac5a64c93"></a>
#### Description

It outputs the DDL statements for the current state of the schema object.

> The objects stored in the recycle bin are not output.

**`\ddl_schema` commands**

<a id="b9ca7e86451d2e9b"></a>
| Command | Description |
| --- | --- |
| `\ddl_schema name` | It performs all options below. |
| `\ddl_schema name CREATE` | It outputs the CREATE SCHEMA statement of the schema object. |
| `\ddl_schema name TABLE` | It outputs the CREATE TABLE statements of the tables which belong to the schema. |
| `\ddl_schema name CONSTRAINT` | It outputs the ALTER TABLE statements of the constraints which belong to the schema. |
| `\ddl_schema name INDEX` | It outputs the CREATE INDEX statements of the indexes which belong to the schema. |
| `\ddl_schema name VIEW` | It outputs the CREATE VIEW statements of the views which belong to the schema. |
| `\ddl_schema name SEQUENCE` | It outputs the CREATE SEQUENCE statements of the sequences which belong to the schema. |
| `\ddl_schema name SYNONYM` | It outputs the CREATE SYNONYM statements of the synonyms which belong to the schema. |
| `\ddl_schema name PROCEDURE` | It outputs the CREATE PROCEDURE/ FUNCTION statements of the procedures and functions which belong to the schema. |
| `\ddl_schema name PACKAGE` | It outputs the CREATE PACKAGE/PACKAGE BODY statements of the package which belong to the schema. |
| `\ddl_schema name GRANT` | It outputs the GRANT .. ON SCHEMA statement for the privilege information on the schema. |
| `\ddl_schema name COMMENT` | It outputs the COMMENT ON SCHEMA statement corresponding to the comment on the schema. |

<a id="3b290f7ffad28cd4"></a>
#### Examples

The following is an example of executing `\ddl_schema CREATE`.

```
gSQL> \ddl_schema h_user CREATE


SET SESSION AUTHORIZATION "SYS"; 
CREATE SCHEMA "H_USER" 
    AUTHORIZATION "H_USER" 
;
```

The following is an example of executing `\ddl_schema CONSTRAINT`.

```
gSQL> \ddl_schema h_user CONSTRAINT


SET SESSION AUTHORIZATION "H_USER"; 
ALTER TABLE "H_USER"."REGION" 
    ADD CONSTRAINT "H_USER"."REGION_PK" 
    PRIMARY KEY 
    ( 
        "R_REGIONKEY" ASC NULLS LAST
    ) 
    INDEX "REGION_PK_INDEX" 
    PCTFREE  10 
    INITRANS 4 
    MAXTRANS 8 
    STORAGE 
    ( 
        INITIAL 524288 
        NEXT    262144 
        MINSIZE 524288 
        MAXSIZE 35184372088832 
    ) 
    TABLESPACE "TEMP_TBS" 
    NOT DEFERRABLE
    INITIALLY IMMEDIATE
;

SET SESSION AUTHORIZATION "H_USER"; 
ALTER TABLE "H_USER"."NATION" 
    ADD CONSTRAINT "H_USER"."NATION_PK" 
    PRIMARY KEY 
    ( 
        "N_NATIONKEY" ASC NULLS LAST
    ) 
    INDEX "NATION_PK_INDEX" 
    PCTFREE  10 
    INITRANS 4 
    MAXTRANS 8 
    STORAGE 
    ( 
        INITIAL 524288 
        NEXT    262144 
        MINSIZE 524288 
        MAXSIZE 35184372088832 
    ) 
    TABLESPACE "TEMP_TBS" 
    NOT DEFERRABLE
    INITIALLY IMMEDIATE
;

SET SESSION AUTHORIZATION "H_USER"; 
ALTER TABLE "H_USER"."SUPPLIER" 
    ADD CONSTRAINT "H_USER"."SUPPLIER_PK" 
    PRIMARY KEY 
    ( 
        "S_SUPPKEY" ASC NULLS LAST
    ) 
    INDEX "SUPPLIER_PK_INDEX" 
    PCTFREE  10 
    INITRANS 4 
    MAXTRANS 8 
    STORAGE 
    ( 
        INITIAL 524288 
        NEXT    262144 
        MINSIZE 524288 
        MAXSIZE 35184372088832 
    ) 
    TABLESPACE "TEMP_TBS" 
    NOT DEFERRABLE
    INITIALLY IMMEDIATE
;
```

<a id="45ceb9b4306308e9"></a>
### `\ddl_public_synonym`

<a id="80a6004d1b7d5de1"></a>
#### Syntax

```
\ddl_public_synonym name
\ddl_public_synonym name CREATE
```

<a id="7d2dfc5dae483fb6"></a>
#### Description

It outputs the DDL statements for the current state of the public synonym object.

**`\ddl_public_synonym` commands**

<a id="33c56213573de539"></a>
| Command | Description |
| --- | --- |
| `\ddl_public_synonym` | It performs all options below. |
| `\ddl_public_synonym name CREATE` | It outputs the CREATE PUBLIC SYNONYM statement of the public synonym object. |

<a id="0d36a799b68c6d2e"></a>
#### Example

The following is an example of executing `\ddl_public_synonym CREATE`.

```
gSQL> \ddl_public_synonym pubsyn CREATE

SET SESSION AUTHORIZATION "SYS"; 
CREATE PUBLIC SYNONYM "PUBSYN" FOR "PUBLIC"."T1"
;
COMMIT;
```

<a id="93feba0884aff3da"></a>
### `\ddl_table`

<a id="5dc3321b7dfb825d"></a>
#### Syntax

```
\ddl_table name
\ddl_table name CREATE
\ddl_table name CONSTRAINT
\ddl_table name INDEX
\ddl_table name IDENTITY
\ddl_table name SUPPLEMENTAL
\ddl_table name GRANT
\ddl_table name COMMENT
```

<a id="5004849e12f5d1ab"></a>
#### Description

It outputs the DDL statements for the current state of the table object.

> The objects stored in the recycle bin are not output.

**`\ddl_table` commands**

<a id="b2d1d393dfb84d9b"></a>
| Command | Description |
| --- | --- |
| `\ddl_table name` | It performs all options below. |
| `\ddl_table name CREATE` | It outputs the CREATE TABLE statement of the table object. |
| `\ddl_table name CONSTRAINT ` | It outputs the ALTER TABLE statements of the constraints created in the table. |
| `\ddl_table name INDEX` | It outputs the CREATE INDEX statements of the indexes created in the table. |
| `\ddl_table name IDENTITY` | It outputs the ALTER TABLE statement for the restart value if the table has an identity column. |
| `\ddl_table name SUPPLEMENTAL` | It outputs the ALTER TABLE statement if the supplemental log option is set on the table. |
| `\ddl_table name GRANT` | It outputs the GRANT .. ON TABLE statement for the privilege information on the table. |
| `\ddl_table name COMMENT` | It outputs the COMMENT ON TABLE statement corresponding to the comment on the table. |

<a id="45b523ad4202aff9"></a>
#### Examples

The following is an example of executing `\ddl_table CREATE`.

```
gSQL> \ddl_table h_user.orders CREATE

SET SESSION AUTHORIZATION "H_USER"; 
CREATE TABLE "H_USER"."ORDERS" 
    ( 
        "O_ORDERKEY" NUMBER( 10, 0 )
      , "O_CUSTKEY" NUMBER( 10, 0 )
      , "O_ORDERSTATUS" CHARACTER( 1 OCTETS )
      , "O_TOTALPRICE" NUMBER( 12, 2 )
      , "O_ORDERDATE" DATE
      , "O_ORDERPRIORITY" CHARACTER( 15 OCTETS )
      , "O_CLERK" CHARACTER( 15 OCTETS )
      , "O_SHIPPRIORITY" NUMBER( 10, 0 )
      , "O_COMMENT" CHARACTER VARYING( 79 OCTETS )
    ) 
    PCTFREE  10 
    PCTUSED  60 
    INITRANS 4 
    MAXTRANS 8 
    STORAGE 
    ( 
        INITIAL 524288 
        NEXT    262144 
        MINSIZE 524288 
        MAXSIZE 35184372088832 
    ) 
    TABLESPACE "TEST_TBS" 
;
```

The following is an example of executing `\ddl_table GRANT`.

```
gSQL> \ddl_table h_user.nation GRANT


SET SESSION AUTHORIZATION "H_USER"; 
GRANT 
    DELETE ON TABLE "H_USER"."NATION" 
    TO "TEST" 
;

SET SESSION AUTHORIZATION "H_USER"; 
GRANT 
    SELECT ( "N_NATIONKEY" ) ON TABLE "H_USER"."NATION" 
    TO "C_USER" 
;

SET SESSION AUTHORIZATION "H_USER"; 
GRANT 
    SELECT ( "N_NAME" ) ON TABLE "H_USER"."NATION" 
    TO "C_USER" 
;
```

<a id="b4894103cc335441"></a>
### `\ddl_constraint`

<a id="234a8e01cd7cfd47"></a>
#### Syntax

```
\ddl_constraint name
\ddl_constraint name ALTER
\ddl_constraint name COMMENT
```

<a id="9480ff4a85cd3c64"></a>
#### Description

It outputs the DDL statements for the current state of the constraint object.

> The objects stored in the recycle bin are not output.

**`\ddl_constraint` commands**

<a id="b632eacd70ffe86a"></a>
| Command | Description |
| --- | --- |
| `\ddl_constraint name` | It performs all options below. |
| `\ddl_constraint name ALTER` | It outputs the ALTER TABLE statement of the constraint object. |
| `\ddl_constraint name COMMENT` | It outputs the COMMENT ON CONSTRAINT statement corresponding to the comment on the constraint. |

<a id="801032efb29cd31c"></a>
#### Example

The following is an example of executing `\ddl_constraint ALTER`.

```
gSQL> \ddl_constraint h_user.lineitem_pk ALTER


SET SESSION AUTHORIZATION "H_USER"; 
ALTER TABLE "H_USER"."LINEITEM" 
    ADD CONSTRAINT "H_USER"."LINEITEM_PK" 
    PRIMARY KEY 
    ( 
        "L_ORDERKEY" ASC NULLS LAST
      , "L_LINENUMBER" ASC NULLS LAST
    ) 
    INDEX "LINEITEM_PK_INDEX" 
    PCTFREE  10 
    INITRANS 4 
    MAXTRANS 8 
    STORAGE 
    ( 
        INITIAL 524288 
        NEXT    262144 
        MINSIZE 524288 
        MAXSIZE 35184372088832 
    ) 
    TABLESPACE "TEMP_TBS" 
    NOT DEFERRABLE
    INITIALLY IMMEDIATE
;
```

<a id="61c711afa481b5c1"></a>
### `\ddl_index`

<a id="9442ff2494aa1fd5"></a>
#### Syntax

```
\ddl_index name
\ddl_index name CREATE
\ddl_index name COMMENT
```

<a id="5461b0e608c44f8c"></a>
#### Description

It outputs the DDL statements for the current state of the index object.

> The objects stored in the recycle bin are not output.

**`\ddl_index` commands**

<a id="de9d5fd6e1ab2c05"></a>
| Command | Description |
| --- | --- |
| `\ddl_index name` | It performs all options below. |
| `\ddl_index name CREATE` | It outputs the CREATE INDEX statement of the index object. |
| `\ddl_index name COMMENT` | It outputs the COMMENT ON INDEX statement corresponding to the comment on the index. |

<a id="75203314ce715aee"></a>
#### Example

The following is an example of executing `\ddl_index CREATE`.

```
gSQL> \ddl_index public.idx2 CREATE


SET SESSION AUTHORIZATION "TEST"; 
CREATE INDEX "PUBLIC"."IDX2" 
    ON "PUBLIC"."T1" 
    ( 
        "C3" ASC NULLS LAST
      , "C1" DESC NULLS FIRST
    ) 
    PCTFREE  10 
    INITRANS 4 
    MAXTRANS 8 
    STORAGE 
    ( 
        INITIAL 524288 
        NEXT    262144 
        MINSIZE 524288 
        MAXSIZE 35184372088832 
    ) 
    TABLESPACE "MEM_TEMP_TBS" 
;
```

<a id="0205fa731c743d17"></a>
### `\ddl_view`

<a id="b051a7d970c06033"></a>
#### Syntax

```
\ddl_view name
\ddl_view name CREATE
\ddl_view name GRANT
\ddl_view name COMMENT
```

<a id="8e5fc20e16f0b224"></a>
#### Description

It outputs the DDL statements for the current state of the view object.

**`\ddl_view` commands**

<a id="79861649b65fb4b2"></a>
| Command | Description |
| --- | --- |
| `\ddl_view name` | It performs all options below. |
| `\ddl_view name CREATE` | It outputs the CREATE VIEW statement of the view object. |
| `\ddl_view name GRANT` | It outputs the GRANT .. ON TABLE statement for the privilege information on the view. |
| `\ddl_view name COMMENT` | It outputs the COMMENT ON TABLE corresponding to the comment on the view. |

<a id="a2a16478b7ea2a00"></a>
#### Example

The following is an example of executing `\ddl_view CREATE`.

```
gSQL> \ddl_view h_user.revenue CREATE


SET SESSION AUTHORIZATION "H_USER"; 
CREATE OR REPLACE FORCE VIEW "H_USER"."REVENUE" 
    (supplier_no, total_revenue) 
    AS SELECT
    l_suppkey,
    ROUND( sum(l_extendedprice * (1 - l_discount)), 2)
FROM
    lineitem
WHERE
      l_shipdate >= date '1996-01-01'
  AND l_shipdate < date '1996-01-01' + interval '3' month
GROUP BY
    l_suppkey
;
```

<a id="7ca05c84662a43b5"></a>
### `\ddl_sequence`

<a id="f7008db931306a59"></a>
#### Syntax

```
\ddl_sequence name
\ddl_sequence name CREATE
\ddl_sequence name RESTART
\ddl_sequence name GRANT
\ddl_sequence name COMMENT
```

<a id="10d7b5b90dc7f6ff"></a>
#### Description

It outputs the DDL statements for the current state of the sequence object.

**`\ddl_sequence` commands**

<a id="cec2b8320d189058"></a>
| Command | Description |
| --- | --- |
| `\ddl_sequence name` | It performs all options below. |
| `\ddl_sequence name CREATE` | It outputs the CREATE SEQUENCE statement of the sequence object. |
| `\ddl_sequence name RESTART` | It outputs the ALTER SEQUENCE statement corresponding to the restart value of the sequence object. |
| `\ddl_sequence name GRANT` | It outputs the GRANT .. ON SEQUENCE statement for the privilege information on the sequence. |
| `\ddl_sequence name COMMENT` | It outputs the COMMENT ON SEQUENCE statement corresponding to the comment on the sequence. |

<a id="4228a5cb23b9670f"></a>
#### Examples

The following is an example of executing `\ddl_sequence CREATE`.

```
gSQL> \ddl_sequence h_user.h_seq CREATE


SET SESSION AUTHORIZATION "H_USER"; 
CREATE SEQUENCE "H_USER"."H_SEQ" 
    START WITH 1 
    INCREMENT BY 1 
    MAXVALUE 9223372036854775807 
    MINVALUE 1 
    NO CYCLE 
    CACHE 20 
;
```

The following is an example of executing `\ddl_sequence RESTART`.

```
gSQL> \ddl_sequence h_user.h_seq RESTART


SET SESSION AUTHORIZATION "H_USER"; 
ALTER SEQUENCE "H_USER"."H_SEQ" 
    RESTART WITH 21 
;
```

<a id="5d56473b41117e8d"></a>
### `\ddl_synonym`

<a id="5e834b5b8fbddcdc"></a>
#### Syntax

```
\ddl_synonym name
\ddl_synonym name CREATE
```

<a id="89c4f7f5f9e1b788"></a>
#### Description

It outputs the DDL statements for the current state of the synonym object.

**`\ddl_synonym` commands**

<a id="6adbda509999e2d7"></a>
| Command | Description |
| --- | --- |
| `\ddl_synonym` | It performs all options below. |
| `\ddl_synonym name CREATE` | It outputs the CREATE SYNONYM statement of the synonym object. |

<a id="de04dda0080a1481"></a>
#### Example

The following is an example of executing `\ddl_synonym CREATE`.

```
gSQL> \ddl_synonym syn CREATE

SET SESSION AUTHORIZATION "TEST"; 
CREATE SYNONYM "PUBLIC"."SYN" FOR "PUBLIC"."T1"
;
COMMIT;
```

<a id="6d70ed7500698e9b"></a>
### `\ddl_procedure`

<a id="5e6602634aa2ac07"></a>
#### Syntax

```
\ddl_procedure name
\ddl_procedure name CREATE
```

<a id="78619a863b1ce769"></a>
#### Description

It outputs the DDL statements for the current state of the stored procedure or the function object.

**`\ddl_procedure` commands**

<a id="f36cba251a1b1391"></a>
| Command | Description |
| --- | --- |
| `\ddl_procedure` | It performs all options below. |
| `\ddl_procedure name CREATE` | It outputs CREATE PROCEDURE/ FUNCTION statement of the stored procedure/ function object. |

<a id="b606aa3ad3ea5c59"></a>
#### Example

The following is an example of executing `\ddl_procedure CREATE`.

```
gSQL> \ddl_procedure proc1 CREATE


SET SESSION AUTHORIZATION "TEST"; 
CREATE OR REPLACE PROCEDURE "PUBLIC"."PROC1" 
is
begin
 null;
end;
/
COMMIT;
```

<a id="1af1e56ac5d40d3a"></a>
### `\ddl_package`

<a id="788c183f5827a21f"></a>
#### Syntax

```
\ddl_package name
\ddl_package name CREATE
```

<a id="64b01b5eb2e88064"></a>
#### Description

It outputs the DDL statements for the current state of the package spec or the package body object.

**`\ddl_package` commands**

<a id="a4c3fc8b9aad8318"></a>
| Command | Description |
| --- | --- |
| `\ddl_package` | It performs all options below. |
| `\ddl_package name CREATE` | It outputs CREATE PACKAGE/PACKAGE BODY statement of the package spec and the package body object. |

<a id="a54d1a79638937e5"></a>
#### Examples

The following is an example of executing `\ddl_package CREATE`.

```
gSQL> \ddl_package pkg1 CREATE


SET SESSION AUTHORIZATION "TEST";
CREATE OR REPLACE PACKAGE "PUBLIC"."PKG1"
is
  v1 integer;
  procedure proc1( a1 integer );
 end;
/
CREATE OR REPLACE PACKAGE BODY "PUBLIC"."PKG1"
is
  procedure proc1( a1 integer )
  is
  begin
    null;
  end;
end;
/
COMMIT;
```

<a id="37ddcc5f12fda169"></a>
### `\desc`

<a id="866a2f3217daa0cf"></a>
#### Syntax

```
\desc table_name
\desc schema_name.table_name
```

<a id="b30b13b27c1a0c9f"></a>
#### Description

It queries the structure information of the table.

A table may be described only with the table name as follows or described together with the schema name. If the schema name is not specified, the schema name of the table is determined by the [Schema Path](../part-03-sql-manual/13-sql-objects.md#025309f995bd075b) of the user.

- `\desc` t1
- `\desc` public.t1

If a table name is created by using [Identifiers](../part-03-sql-manual/11-sql-elements.md#ceb44fbf00a35273) when creating a table as follows, the double quotes (") is used to describe it.

- Creating a table 
    - CREATE TABLE "TaBle#@^*" ( id INTEGER );
- `\desc` "TaBle#@^*"
- `\desc` "PUBLIC"."TaBle#@^*"

The execution result includes the following information of the table.

- Column information
    - Column name
    - Data type
    - Whether NULL is allowed
- Index information
    - Index name
    - Storage space for index
    - Index type
    - Whether UNIQUE is allowed
    - Key column name
- Constraint information
    - Constraint name
    - Constraint type
    - The related index
    - Constraint column

<a id="015e6a85da6be25b"></a>
#### Examples

The following is an example of querying the information of the t1 table.

```
gSQL> \desc t1

COLUMN_NAME TYPE                    IS_NULLABLE
----------- ----------------------- -----------
ID          NUMBER(10,0)            FALSE      
NAME        CHARACTER VARYING(128)  TRUE       
ADDR        CHARACTER VARYING(1024) TRUE       

INDEX_NAME           TABLESPACE_NAME INDEX_TYPE IS_UNIQUE COLUMNS
-------------------- --------------- ---------- --------- -------
T1_PRIMARY_KEY_INDEX MEM_TEMP_TBS    BTREE      TRUE      ID     
T1_IDX_NAME          MEM_TEMP_TBS    BTREE      FALSE     NAME   

CONSTRAINT_NAME CONSTRAINT_TYPE ASSOCIATED_INDEX     COLUMNS
--------------- --------------- -------------------- -------
T1_PRIMARY_KEY  PRIMARY KEY     T1_PRIMARY_KEY_INDEX ID
```

The following is an example of querying the information of the t1 table by describing together with the schema name public.

```
gSQL> \desc public.t1

COLUMN_NAME TYPE                    IS_NULLABLE
----------- ----------------------- -----------
ID          NUMBER(10,0)            FALSE      
NAME        CHARACTER VARYING(128)  TRUE       
ADDR        CHARACTER VARYING(1024) TRUE       

INDEX_NAME           TABLESPACE_NAME INDEX_TYPE IS_UNIQUE COLUMNS
-------------------- --------------- ---------- --------- -------
T1_PRIMARY_KEY_INDEX MEM_TEMP_TBS    BTREE      TRUE      ID     
T1_IDX_NAME          MEM_TEMP_TBS    BTREE      FALSE     NAME   

CONSTRAINT_NAME CONSTRAINT_TYPE ASSOCIATED_INDEX     COLUMNS
--------------- --------------- -------------------- -------
T1_PRIMARY_KEY  PRIMARY KEY     T1_PRIMARY_KEY_INDEX ID
```

The following is an example of querying the information of the table created by using the delimited identifier.

```
gSQL> CREATE TABLE "TaBle#@^*" ( id INTEGER );

Table created.

gSQL> \desc "TaBle#@^*"

COLUMN_NAME TYPE         IS_NULLABLE
----------- ------------ -----------
ID          NUMBER(10,0) TRUE
```

If the delimited identifier is not used as follows, then an error occurs.

```
gSQL> \desc TaBle#@^*

ERR-42000(40000): syntax error 
\desc TaBle#@^*
...........^  ^
Error at line 1
```

<a id="0260325eb794a7de"></a>
### `\dynamic sql :var`

<a id="a814a4cc6f1654c5"></a>
#### Syntax

```
\dynamic sql :var
```

<a id="add79c0a8692b7ac"></a>
#### Description

It executes the SQL statement stored in the host variable var.  
It is similar in concept to [Embedded Dynamic SQL](../part-05-developer-manual/33-embedded-sql.md#67a684cfa2b6c7c3) which executes SQL statements that are not defined in an embedded SQL, but It is used when performing SQL statement which is not defined.

It is performed in the following order.

1. Declare a host variable. (Refer to [`\var`](#466b7f8794c4595b).)  
   `\var` var_stmt VARCHAR(1024)
2. Assign an SQL statement as the value of the host variable. (Refer to [`\exec :var := value`](#7b19e6e57e1e5fdd).)  
   `\exec` :var_stmt := 'SELECT # FROM t1'
3. Execute the dynamic SQL.  
   `\dynamic sql` :var_stmt

<a id="7651355f442a3cfe"></a>
#### Examples

The following is an example of declaring the var_stmt host variable and executing the dynamic SQL by assigning an SQL statement.

• Assigning the SELECT statement to the host variable

```
gSQL> \exec :var_stmt := 'SELECT * FROM t1'
```

• Executing the dynamic SQL

```
gSQL> \dynamic sql :var_stmt 

ID NAME   ADDR        
-- ------ ------------
 1 leekmo Seoul, Korea

1 row selected.
```

Two single quote (') are described like as the usage of the [`\exec :var := value`](#7b19e6e57e1e5fdd) command when a string exists in an SQL statement as the INSERT statement below.

• Declaring a host variable

```
gSQL> \var var_stmt VARCHAR(1024)
```

• Assigning the INSERT statement to the host variable

```
gSQL> \exec :var_stmt := 'INSERT INTO t1(id, name, addr) VALUES ( 1, ''leekmo'', ''Seoul, Korea'' )'
```

• Executing the dynamic SQL.

```
gSQL> \dynamic sql :var_stmt 

1 row created.
```

<a id="7b352f8446079c8a"></a>
### `\edit`

<a id="6254e915f83cc9a4"></a>
#### Description

It edits the SQL statement by using the text editor. The used text editor is specified in the EDITOR environment variable, and if the EDITOR environment variable does not exist, vi is used by default.

When using the editing feature, gsql hands over control by executing the editor. The user can freely edit the SQL statements with the editor. When the editor ends, the control is handed over to gsql, and its content will be added as the last history.

The SQL statement edited by the editor may be executed through the last history execution command `\\`.

> Only a single SQL statement can be edited with the SQL editor. An error occurs when executing multiple SQL statements.

The followings can be edited by using `\edit.`

- The most recently performed SQL statement
- the SQL statement stored in a file
- The SQL statement stored in the gsql history

The following chapter describes the usage.

<a id="bb904897fab5c700"></a>
#### `\edit`

<a id="b98d62369d85a822"></a>
##### Syntax

```
\edit
\ed
```

<a id="bffbaef70fff3fe5"></a>
##### Description

It edits the most recently executed SQL statement by using the text editor. If any SQL statement has not been executed, the text editor is run without any content.

<a id="eba66fd3a3d73692"></a>
##### Example

The following is an example of editing the most recently executed SQL statement.

- Editing the most recently executed SQL statement

```
gSQL> SELECT * FROM T1;
C1
--
 1
11
2 rows selected.
gSQL> \EDIT
SELECT * FROM T1 WHERE C1 < 10;
```

• Executing the edited SQL statement

```
gSQL> \\
C1
--
 1
1 row selected.
```

<a id="7e682ea69d7dcdf4"></a>
#### `\edit 'file_name'`

<a id="7665eb3913e9b963"></a>
##### Syntax

```
\edit 'file_name'
\ed   'file_name'
```

<a id="29b7d8783cc91b4e"></a>
##### Description

It edits the given file_name by using the text editor.  
The file_name is enclosed with the single quote (').  
file_name can use either an absolute path or a relative path as follows. When file_name uses a relative path, it searches for the file_name based on the path of gsql execution.

• Using the absolute path

```
gSQL> \edit '/home/goldilocks/sample.sql'
```

• Using the relative path

```
gSQL> \edit 'sample.sql'
```

<a id="f2750eeb5fc02f38"></a>
##### Example

The following is an example of editing the SQL statement stored in the file.

• Editing the most recently executed SQL statement

```
gSQL> SELECT * FROM T1;
C1
--
 1
11
2 rows selected.
gSQL> \EDIT 'sample.sql'
SELECT * FROM T1 WHERE C1 < 10;
```

• Executing the edited SQL statement

```
gSQL> \\
C1
--
 1
1 row selected.
```

<a id="4b7277c1a128cb1b"></a>
#### `\edit [history] {n}`

<a id="116611705471ee5c"></a>
##### Syntax

```
\edit [history] {n}
\ed   [history] {n}
```

<a id="1027d68107edc986"></a>
##### Description

It edits the SQL statement corresponding to the number from the SQL execution history which can be queried by using [`\history`](#abb530db4014a1ab).  
The value of number should be the ID value which is the result of executing [`\history`](#abb530db4014a1ab).

<a id="b2d4fb80132811cf"></a>
##### Example

The following is an example of editing the SQL statement stored in the gsql history.

```
gSQL> SELECT * FROM T1;
C1
--
 1
11
2 rows selected.
gSQL> \history
ID SQL             
-- ----------------
 1 SELECT * FROM T1
```

• Editing the SQL statement whose ID value is 1 from the stored history

```
gSQL> \edit 1
SELECT * FROM T1 WHERE C1 < 5;
```

• Executing the edited SQL statement

```
gSQL> \\
C1
--
 1
1 row selected.
```

<a id="6bf5fe8d586bd235"></a>
### `\exec`

<a id="86f9e10b6e3aca7d"></a>
#### Syntax

```
\exec
```

<a id="1deac50c90cabab5"></a>
#### Description

It executes the SQL statement which is prepared by [`\prepare sql`](#81d591bf1367796d).  
`\exec` operates similarly to the  [SQLExecute](../part-05-developer-manual/31-odbc.md#35c48ce37221b54d) function of ODBC and PreparedStatement::[execute](../part-05-developer-manual/32-jdbc.md#442c2df3c2025f3b) function of JDBC.  
The prepared SQL statements can be repeatedly executed by using `\exec`.

<a id="4184160010da5ab2"></a>
#### Examples

The following is an example of preparing an INSERT statement and repeatedly executing it.

• Preparing the INSERT statement

```
gSQL> \prepare sql INSERT INTO t1(id, addr) VALUES ( seq.NEXTVAL, 'N/A' );

SQL prepared.
```

• Executing the prepared statement

```
gSQL> \exec

1 row created.
```

• Executing the prepared statement

```
gSQL> \exec

1 row created.
```

• The results of querying the table are as follows.

```
gSQL> SELECT * FROM t1;

ID ADDR
-- ----
 1 N/A 
 2 N/A 

2 rows selected.
```

The following is an example of preparing the SELECT statement with the host variable and repeatedly executing it by changing the host variable value.

• Declaring the host variable

```
gSQL> \var v_id INTEGER
```

• Preparing the SELECT statement which used the host variable

```
gSQL> \prepare sql SELECT * FROM t1 WHERE ID = :v_id;

SQL prepared.
```

• Assigning the value 1 to the host variable

```
gSQL> \exec :v_id := 1
```

• Executing the prepared SELECT statement

```
gSQL> \exec

ID ADDR
-- ----
 1 N/A 

1 row selected.
```

• Assigning the value 2 to the host variable

```
gSQL> \exec :v_id := 2
```

• Executing the prepared SELECT statement

```
gSQL> \exec

ID ADDR
-- ----
 2 N/A 

1 row selected.
```

<a id="7b19e6e57e1e5fdd"></a>
### `\exec :var := value`

<a id="56b27d7151c72292"></a>
#### Syntax

```
\exec :variable := <value expression>
```

<a id="cbffc4d415a39c4b"></a>
#### Description

It assigns the value to the host variable.  
This command assigns a value to the host variable in the same way as executing [SELECT .. INTO](../part-03-sql-manual/20-sql-references-h-z.md#62c0547d8bd310b3) as follows.

```
gSQL> \exec :v_value := 1234
gSQL> SELECT 1234 INTO :v_value FROM DUAL;
```

The host variable must have been declared with [`\var`](#466b7f8794c4595b).

The host variable must be used together with colon (:), and the assignment operator (:=) is not allowed to omit (:). Simple values or operators may appear in &lt;value expression&gt; entered to the host variable. For more information, refer to [Expressions](../part-03-sql-manual/11-sql-elements.md#82a01b5b328b6d8d).

The value assigned to the host variable should be compatible with the data type of the host variable. For more information, refer to [Type Conversion](../part-03-sql-manual/11-sql-elements.md#935e2183d0c42aa6).

The value assigned to the host variable may be queried by using [`\print`](#40764010c6ea1a78).

```
\exec :v_value := 1234
\print v_value
```

The string should be enclosed in the single quote (') as follows when inserting the string into the host variable.

- Simple string
    - Value: abcd
    - `\exec` :v_value := 'abcd'
- The string which includes the single quote
    - Value: Tom's House
    - The single quote within the string is represented with the two single quotes ('') as follows.
    - `\exec` :v_value := 'Tom''s House'
- The SQL statement including the single quote
    - Value: INSERT INTO t1 VALUES (1, 'Tom''s House' )
    - The single quote within the string is represented with the two single quotes ('') as follows.
    - `\exec` :v_value := 'INSERT INTO t1 VALUES (1, ''Tom''s House'' )'

<a id="48aeecd4c69cca86"></a>
#### Examples

The following is an example of assigning the various types of string to the host variable.

• Declaring the host variable

```
gSQL> \var v_value VARCHAR(1024)
```

• Assigning the simple string

```
gSQL> \exec :v_value := 'abcd'
gSQL> \print v_value

V_VALUE
-------
abcd
```

• Assigning the string including the single quote (')

```
gSQL> \exec :v_value := 'Tom''s House'
gSQL> \print v_value

V_VALUE    
-----------
Tom's House
```

• Assigning the SQL statement including the single quote (')

```
gSQL> \exec :v_value := 'INSERT INTO t1 VALUES ( 1, ''Tom''s House'' )'
gSQL> \print v_value

V_VALUE                                   
------------------------------------------
INSERT INTO t1 VALUES ( 1, 'Tom's House' )
```

The following is an example of using the operation result when assigning the value to the host variable.

• Declaring the host variable

```
gSQL> \var v1 INTEGER
gSQL> \var v2 INTEGER
```

• Assigning the value to v1

```
gSQL> \exec :v1 := 100
```

• Assigning the result of operation with v1 to v2

```
gSQL> \exec :v2 := :v1 + 1000
```

• Querying the value of host variables v1 and v2

```
gSQL> \print v1

 V1
---
100

gSQL> \print v2

  V2
----
1100
```

The following is an example of assigning the value to the host variable and using the host variable in the SELECT statement.

• Declaring the host variable

```
gSQL> \var v_id INTEGER
```

• Assigning the value to the host variable

```
gSQL> \exec :v_id := 1
```

• Executing the SELECT statement by using the host variable

```
gSQL> SELECT * FROM t1 WHERE id = :v_id;

ID ADDR
-- ----
 1 N/A 

1 row selected.
```

The following is an example of obtaining the value to the host variable via [SELECT .. INTO](../part-03-sql-manual/20-sql-references-h-z.md#62c0547d8bd310b3).

• Declaring the host variable

```
gSQL> \var v_id INTEGER
```

• A value is not specified.

```
gSQL> \print v_id

V_ID
----
null
```

• Assigning the value to v_id by executing the SELECT INTO statement

```
gSQL> SELECT MAX(id) INTO :v_id FROM t1;

V_ID
----
   2

1 row selected.
```

• Checking the host variable value

```
gSQL> \print v_id

V_ID
----
   2
```

<a id="1f59b89b0868c63c"></a>
### `\exec sql`

<a id="043c0de311436384"></a>
#### Syntax

```
\exec sql <sql_statement>
```

<a id="803c5c36119cba76"></a>
#### Description

It executes the SQL statement described in &lt;sql_statement&gt;.  
It operates as same as the execution of the SQL statement at the prompt as follows.

```
gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.

gSQL> \exec sql SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.
```

The SQL statement is executed with the PREPARE/EXECUTE method using [`\prepare sql`](#81d591bf1367796d) and [`\exec`](#6bf5fe8d586bd235). On the other hand, `\exec sql` executes the SQL statement with the DIRECT EXECUTE method corresponding to [SQLExecDirect](../part-05-developer-manual/31-odbc.md#ac898c92a7f543f1) function of ODBC and to Statement::[execute](../part-05-developer-manual/32-jdbc.md#804bf080308a1857) function of JDBC.

<a id="13be934071868b89"></a>
#### Example

The following is an example of executing the SELECT statement.

```
gSQL> \exec sql SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.
```

<a id="619d085ddbb3b859"></a>
### `\explain plan`

<a id="de9f1c5100638ec4"></a>
#### Syntax

```
\explain plan <sql_statement>
\explain plan on <sql_statement>
\explain plan only <sql_statement>
```

<a id="cf3cc3e20036503a"></a>
#### Description

It outputs the execution plan of the SELECT statement described in &lt;sql_statement&gt;.

- `\explain plan on`
    - It executes the SQL statement and outputs the execution plan along with the query results.
- `\explain plan only`
    - It does not execute the SQL statement and outputs the execution plan without the query results.
- `\explain plan`
    - If on or only is not specified, the default value is on.

For more information about the execution plan, refer to [SQL Execution Plan](../part-03-sql-manual/15-sql-tuning.md#eb7fd3cec4fcfcc2).

<a id="e3e717d30a2ba196"></a>
#### Examples

If it is used together with ON as follows, it executes the SQL statement and outputs the execution plan with the query results.

```
gSQL> \explain plan on SELECT * FROM t1 WHERE id = 1;

ID NAME   ADDR        
-- ------ ------------
 1 leekmo Seoul, Korea

1 row selected.

>>>  start print plan

< Execution Plan >
==========================================================================
|  IDX  |  NODE DESCRIPTION                                 |       ROWS |
--------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                 |            |
|    1  |    TABLE ACCESS ("T1")                            |          1 |
==========================================================================

     1  -  READ COLUMNS : ID, NAME, ADDR
             PHYSICAL FILTER : ID = 1

<<<  end print plan
```

If it is used together with ONLY as follows, it does not execute the SQL statement and outputs the execution plan without the query results.

```
gSQL> \explain plan only SELECT * FROM t1 WHERE id = 1;


>>>  start print plan

< Execution Plan >
==========================================================================
|  IDX  |  NODE DESCRIPTION                                 |       ROWS |
--------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                 |            |
|    1  |    TABLE ACCESS ("T1")                            |          0 |
==========================================================================

     1  -  READ COLUMNS : ID, NAME, ADDR
             PHYSICAL FILTER : ID = 1

<<<  end print plan
```

<a id="1fc4a542f71f7089"></a>
### `\help`

<a id="a95fa451e4cad5ce"></a>
#### Syntax

```
\help
```

<a id="7e9a4388a056b02f"></a>
#### Description

It briefly displays the list of commands which begin with `(\)` in gsql interactive mode.

<a id="31d6d71be50ac67b"></a>
#### Examples

The following is an example of using `\help`.

```
gSQL> \help
\help                     
\q[uit]                   
\i[mport] {'FILE'}               Import SQL 
\ed[it] [{'FILE'|[HISTORY] num}] Edit SQL statement  
\\                               Executes the most recent history entry 
\{n}                             Executes n'th history entry 
\hi[story]                       Show history entries 
\desc     {[schema.]table_name}  Show table description 
\idesc    {[schema.]index_name}  Show index description 
\spo[ol]  ['filename' | OFF]     Stores query results in a file 
\ho[st]   [command]              Executes an operating system command 
\set vertical    {ON|OFF} 
\set time        {ON|OFF} 
\set timing      {ON|OFF} 
\set color       {ON|OFF} 
\set error       {ON|OFF} 
\set autocommit  {ON|OFF} 
\set autotrace   {ON|TRACEONLY|OFF}
\set serveroutput {ON|OFF} 
\set heading     {ON|OFF} 
\set linesize    {n}      0 < n <= 100000
\set pagesize    {n}      0 < n <= 100000
\set colsize     {n}      0 < n <= 104857600
\set numsize     {n}      0 < n <= 50
\set ddlsize     {n}      0 < n <= 100000
\set history     {n}      n <= 100000 ( if n < 0, clear history buffer ) 
\var             {host_var_name} {INTEGER|BIGINT|VARCHAR(n)} 
\exec            [{:host_var_name} := {constant}] 
\exec sql        {sql string}                   
\prepare sql     {sql string}                   
\dynamic sql     {host_var_name}                
\explain plan    [{ON|ONLY}] {sql string}       
\print           [{host_var_name}]              
\ddl_db                             
\ddl_tablespace    {name}           
\ddl_auth          {name}           
\ddl_schema        {name}           
\ddl_table         {[schema.]name}  
\ddl_constraint    {[schema.]name}  
\ddl_index         {[schema.]name}  
\ddl_view          {[schema.]name}  
\ddl_sequence      {[schema.]name}  
\ddl_synonym       {[schema.]name}  
\ddl_public_synonym {name}           
\startup         {[nomount|mount|open]}                   
\shutdown        {[abort|immediate|transactional|normal]} 
\cstartup        {[nomount|mount|open]}                   
\cshutdown       {[abort|normal]} 
\connect         [userid password] [as {sysdba|admin}]
```

<a id="19ec6ee64eb78c73"></a>
### `\host`

<a id="ee0e516b56076931"></a>
#### Syntax

```
\host [command]
\ho [command]
```

<a id="c79562e6630cf002"></a>
#### Description

It executes the command of the operational system without terminating gsql program.  
If HOST is input without command, then the prompt of the operational system is displayed and it is able to continuously input the command of the operational system.  
Instead of HOST, "$" is input in Windows, and "!" is input in UNIX.

<a id="d345a9c828692b61"></a>
#### Example

The following is an example of executing ls *.sql statement which is a command of UNIX operational system.

```
gSQL> \host ls *.sql
DictionarySchema.sql  InformationSchema.sql  PerformanceViewSchema.sql
```

<a id="abb530db4014a1ab"></a>
### `\history`

<a id="8f8fc0251f452944"></a>
#### Syntax

```
\history
\hi
```

<a id="8f28905c6429a909"></a>
#### Description

It displays the list of the SQL statements executed after executing gsql program.  
It manages only the successfully executed SQL statements and it does not include the failed SQL statement  nor the interactive command which begins with gsql`(\)`.  
The previously executed SQL statements can be executed again referring to the list through [`\\`](#e9fcaf4386815ef7)  or [`\{n}`](#cfaf01b3c6c630d9).  
The number of manageable SQL statements is controlled by using [`\set history`](#3ec7cb10d93a1a99).

<a id="e677c8ddbbaa99ae"></a>
#### Example

The following is an example of querying the SQL statement execution history and executing the SQL statement of number 8 again.

```
gSQL> \history

ID SQL                                                                  
-- ---------------------------------------------------------------------
 1 drop table t1                                                        
 2 create table t1 ( id integer, name varchar(128), addr varchar(1024) )
 3 create index t1_idx on t1(id)                                        
 4 insert into t1 values ( 1, 'leekmo', 'Seoul, Korea' )                
 5 insert into t1 values ( 2, 'mkkim', 'Seoul, Korea' )                 
 6 insert into t1 values ( 3, 'xcom73', 'Inchon, Korea' )               
 7 commit                                                               
 8 select * from dual                                                   

gSQL> \8

DUMMY
-----
X    

1 row selected.
```

<a id="1995ecbe7942efd3"></a>
### `\import`

<a id="b20ec9e33b4aff35"></a>
#### Syntax

```
\import 'file_name'
\i 'file_name'
```

<a id="c917dc92eb51aa0d"></a>
#### Description

It imports the SQL statement included in file_name.  
The file_name is enclosed with the single quote (').  
file_name can use either an absolute path or a relative path as follows. When file_name uses a relativepath, it searches for the file_name based on the path of gsql execution.

• Using the absolute path

```
gSQL> \import '/home/GOLDILOCKS/sample.sql'
```

• Using the relative path

```
gSQL> \import 'sample.sql'
```

<a id="d89de91b72ca42fd"></a>
#### Examples

The following is an example of importing the SQL statement from the file by using the absolute path.

```
gSQL> \import '/home/GOLDILOCKS/sample.sql'
DROP TABLE IF EXISTS t1;

Table dropped.

CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128),
    addr VARCHAR(128)
);

Table created.


INSERT INTO t1 
       VALUES ( 1, 'leekmo', 'Seoul, Korea'  ),
              ( 2, 'mkkim' , 'Seoul, Korea'  ),
              ( 3, 'xcom73', 'Inchon, Korea' );

3 rows created.

COMMIT;

Commit complete.
```

The following is an example of importing the SQL statement from the file by using the relative path.

```
gSQL> \import 'sample.sql'
DROP TABLE IF EXISTS t1;

Table dropped.

CREATE TABLE t1 
(
    id   INTEGER,
    name VARCHAR(128),
    addr VARCHAR(128)
);

Table created.


INSERT INTO t1 
       VALUES ( 1, 'leekmo', 'Seoul, Korea'  ),
              ( 2, 'mkkim' , 'Seoul, Korea'  ),
              ( 3, 'xcom73', 'Inchon, Korea' );

3 rows created.

COMMIT;

Commit complete.
```

<a id="104a85d31246002d"></a>
### `\idesc`

<a id="bbf05f0cd9f17fd8"></a>
#### Syntax

```
\idesc index_name
\idesc schema_name.index_name
```

<a id="93fb7c3c34288b5f"></a>
#### Description

It queries the structure information of the index.

An index can be described alone as follows or it can be described together with the schema name. If the schema name is not specified, the schema name of the index is determined by the user's [Schema Path](../part-03-sql-manual/13-sql-objects.md#025309f995bd075b).

- `\idesc` t1_idx_name
- `\idesc` public.t1_idx_name

The execution result includes the following key column information of the index.

- Key column name
- Key column location 
- Key column sort order (ascending/ descending)
- NULL position of the key column(FIRST/ LAST)

<a id="e17872a5fb5cb36c"></a>
#### Example

The following is an example of querying the information of the index t1_idx_name.

```
gSQL> \idesc t1_idx_name

COLUMN_NAME ORDINAL_POSITION IS_ASCENDING_ORDER IS_NULLS_FIRST
----------- ---------------- ------------------ --------------
NAME                       1 TRUE               FALSE
```

<a id="cfaf01b3c6c630d9"></a>
### `\{n}`

<a id="e4028a5374efd4b7"></a>
#### Syntax

```
\number
```

<a id="ca64892c74b84096"></a>
#### Description

It executes the SQL statement corresponding to the number from the SQL execution history which can be queried by using [`\history`](#abb530db4014a1ab).  
The value of number should be the ID value which is the result of executing [`\history`](#abb530db4014a1ab).

<a id="631c669635685363"></a>
#### Examples

The following is an example of executing SQL statement which used `\history`, then executing the DROP TABLE statement whose ID value is 1.

```
gSQL> \history

ID SQL                                            
-- -----------------------------------------------
 1 DROP TABLE IF EXISTS t1                        
 2 CREATE TABLE t1                                
   (                                              
       id   INTEGER PRIMARY KEY,                  
       name VARCHAR(128),                         
       addr VARCHAR(128)                          
   )                                              
 3 CREATE INDEX t1_idx_name ON t1(name)           
 4 INSERT INTO t1                                 
          VALUES ( 1, 'leekmo', 'Seoul, Korea'  ),
                 ( 2, 'mkkim' , 'Seoul, Korea'  ),
                 ( 3, 'xcom73', 'Inchon, Korea' ) 
 5 COMMIT                                         
 6 select * from t1                               

gSQL> \1   

Table dropped.
```

<a id="81d591bf1367796d"></a>
### `\prepare sql`

<a id="e16b0159ca64fddc"></a>
#### Syntax

```
\prepare sql <sql_statement>
```

<a id="a9138f7ad7517f2c"></a>
#### Description

It prepares the SQL statement described in &lt;sql_statement&gt;. The prepared SQL statement can be executed repeatedly with [`\exec`](#6bf5fe8d586bd235).

`\prepare sql` operates similarly to the [SQLPrepare](../part-05-developer-manual/31-odbc.md#9b7895881993baa4) functions of ODBC and Connection::[prepareStatement](../part-05-developer-manual/32-jdbc.md#52eb9f1a8fc7303b) function of JDBC.

<a id="7cac516cf64c11b4"></a>
#### Example

The following is an example of preparing the SELECT statement and repeatedly executing it.

• Preparing the SELECT statement

```
gSQL> \prepare sql SELECT * FROM t1 WHERE id > 2;

SQL prepared.
```

• Executing the prepared SQL statement

```
gSQL> \exec

ID NAME   ADDR         
-- ------ -------------
 3 xcom73 Inchon, Korea

1 row selected.

gSQL> INSERT INTO t1 VALUES ( 4, 'GOLDILOCKS', 'Better Place' );

1 row created.
```

• Executing the prepared SQL statement again

```
gSQL> \exec

ID NAME   ADDR         
-- ------ -------------
 3 xcom73 Inchon, Korea
 4 goldilocks  Better Place 

2 rows selected.
```

<a id="40764010c6ea1a78"></a>
### `\print`

<a id="895c5861b906fd28"></a>
#### Syntax

```
\print
\print variable
```

<a id="46f3dad2d95dfb26"></a>
#### Description

It queries the value of host variable declared with [`\var`](#466b7f8794c4595b) as follows. If the value of host variable is not set, it is NULL.

```
gSQL> \var v1 INTEGER
gSQL> \print v1

  V1
----
null
```

If the name of host variable is not specified as follows, it queries all declared host variables. VAR_ELAPSED_TIME_ is a built-in host variable which manages the execution time of SQL statement as follows.

```
gSQL> \print

NAME               VALUE
------------------ -----
VAR_ELAPSED_TIME__  null
V1                    21
V2                    10
```

<a id="faab25b636fcab99"></a>
#### Example

The following is an example of declaring the host variable, assigning the value to the host variable then querying it.

• Declaring the host variable

```
gSQL> \var v1 INTEGER
gSQL> \var v2 INTEGER
gSQL> \var v3 INTEGER
```

• Querying all host variables

```
gSQL> \print

NAME               VALUE
------------------ -----
VAR_ELAPSED_TIME__  null
V1                  null
V2                  null
V3                  null
```

• Assigning the value to the host variable

```
gSQL> \exec :v1 := 10
gSQL> \exec :v2 := 20
gSQL> \exec :v3 := :v1 + :v2
```

• Querying the host variable v3

```
gSQL> \print v3

V3
--
30
```

• Querying all host variables

```
gSQL> \print

NAME               VALUE
------------------ -----
VAR_ELAPSED_TIME__  null
V1                    10
V2                    20
V3                    30
```

<a id="2e2015c9e8b6a9bb"></a>
### `\quit`

<a id="1deedab69a23197e"></a>
#### Syntax

```
\quit
\q
```

<a id="eba6e7f354048b3d"></a>
#### Description

It quits gsql.  
When quitting gsql, all uncommitted transactions are committed.

<a id="47a7233bcb9c9a0b"></a>
#### Example

```
gSQL> \quit

%
```

<a id="538d21c1f6551b86"></a>
### `\set autocommit`

<a id="bcefb01cfd64b391"></a>
#### Syntax

```
\set autocommit on
\set autocommit off
```

<a id="e0c7c413d2c63fe7"></a>
#### Description

It sets whether to automatically commit after executing the SQL statement.

- `\set autocommit on`
    - It automatically commits after executing the SQL statement.
- `\set autocommit off`
    - It does not automatically commit after executing the SQL statement.
- The default value of autocommit is OFF.

<a id="378ed413943b8085"></a>
#### Examples

The following is a usage example when setting the AUTOCOMMIT value to ON.

• Setting the autocommit to on

```
gSQL> \set autocommit on
```

• The INSERT statement is automatically committed.

```
gSQL> INSERT INTO t1 ( id, name, addr ) VALUES ( 1, 'leekmo', 'Seoul, Korea' );

1 row created.
```

• It is not affected by rollback.

```
gSQL> ROLLBACK;

Rollback complete.

gSQL> SELECT * FROM t1;

ID NAME   ADDR        
-- ------ ------------
 1 leekmo Seoul, Korea

1 row selected.
```

The following is a usage example when setting the AUTOCOMMIT value to OFF.

• Setting the autocommit to off

```
gSQL> \set autocommit off
```

• The transaction in not committed after executing the INSERT statement.

```
gSQL> INSERT INTO t1 ( id, name, addr ) VALUES ( 1, 'leekmo', 'Seoul, Korea' );

1 row created.
```

• The transaction is rolled back.

```
gSQL> ROLLBACK;

Rollback complete.
```

• The INSERT statement is rolled back without any result.

```
gSQL> SELECT * FROM t1;

no rows selected.
```

<a id="e462737e3684880f"></a>
### `\set autotrace`

<a id="e479ce88acbd49a3"></a>
#### Syntax

```
\set autotrace on
\set autotrace traceonly
\set autotrace off
```

<a id="5cc65c6112617621"></a>
#### Description

It sets whether to output the execution plan.

- `\set autotrace on`
    - It executes SQL statement, and outputs the execution plan together with the query result.
- `\set autotrace traceonly`
    - It does not execute SQL statement, and outputs the execution plan without the query result.
- `\set autotrace off`
    - It does not output the execution plan.
    - The default value is off.

For more information, refer to [SQL execution plan](../part-03-sql-manual/15-sql-tuning.md#eb7fd3cec4fcfcc2).

<a id="efc3ade7c434c571"></a>
#### Example

When using ON as follows, it executes SQL statement and outputs the execution plan together with the query result.

```
gSQL> \set autotrace on
gSQL> SELECT * FROM t1 WHERE id = 1;

ID NAME   ADDR        
-- ------ ------------
 1 leekmo Seoul, Korea

1 row selected.

>>>  start print plan

< Execution Plan >
==========================================================================
|  IDX  |  NODE DESCRIPTION                                 |       ROWS |
--------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                 |            |
|    1  |    TABLE ACCESS ("T1")                            |          1 |
==========================================================================

     1  -  READ COLUMNS : ID, NAME, ADDR
             PHYSICAL FILTER : ID = 1

<<<  end print plan
```

When using TRACEONLY as follows, it does not execute SQL statement, and outputs the execution plan without the query result.

```
gSQL> \set autotrace traceonly
gSQL> SELECT * FROM t1 WHERE id = 1;


>>>  start print plan

< Execution Plan >
==========================================================================
|  IDX  |  NODE DESCRIPTION                                 |       ROWS |
--------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                 |            |
|    1  |    TABLE ACCESS ("T1")                            |          0 |
==========================================================================

     1  -  READ COLUMNS : ID, NAME, ADDR
             PHYSICAL FILTER : ID = 1

<<<  end print plan
```

<a id="a173748685f1d9f4"></a>
### `\set color`

<a id="f9a2c0d92a9fbd50"></a>
#### Syntax

```
\set color on
\set color off
```

<a id="b087367081cac9a4"></a>
#### Description

It sets whether to output each row of the query results in a different color on the terminal to distinguish them.

- `\set color on`
    - Each row is output in a different color.
- `\set color off`
    - Each row is output in the same color.
- The default value is OFF.

If the length of each row is too long so that it overflows the terminal window, then the row is output over multiple lines. In this case, each row is hard to be distinguished, so it reduces the readability It is used to distinguish between the rows and increase the readability on the terminal.

<a id="5d18fc08b3991e27"></a>
#### Example

The following is an example of setting the color to ON.

```
gSQL> \set color on
gSQL> SELECT id, addr FROM t1;

ID ADDR         
-- -------------
 1 Seoul, Korea 
 2 Seoul, Korea 
 3 Inchon, Korea

3 rows selected.
```

<a id="29513cfc2f8c8c50"></a>
### `\set colsize`

<a id="2001ce6a57d97c1e"></a>
#### Syntax

```
\set colsize number
```

<a id="a33cd6a8ebb46a39"></a>
#### Description

It sets the maximum length of the data when outputting LONG VARCHAR, LONG VARBINARY data.

- The colsize value is a positive integer between 1 and 104,857,600.(100M, the maximum length of LONG VARCHAR)
- The default value of colsize is 8,192.

The string length of the LONG VARCHAR column is too long, so the readability of the query execution is low as follows. In this case, the readability of LONG VARCHAR column can be increased by reducing the colsize, or it may be output as long as the desired length by enlarging the colsize.

```
gSQL> SELECT view_name, text FROM all_views WHERE view_name LIKE 'ALL_%' FETCH 3;

VIEW_NAME       
----------------
TEXT                                                                            
--------------------------------------------------------------------------------
ALL_ALL_TABLES  
SELECT                                                                          
       auth.AUTHORIZATION_NAME                ❶ OWNER                          
     , sch.SCHEMA_NAME                        ❷ TABLE_SCHEMA                   
     

... Ellipsis ...


                                                  WHERE      , pvcol.GRANTOR_ID                                                         
     , pvcol.GRANTEE_ID                                                         
     , pvcol.PRIVILEGE_TYPE_ID                                                  
                                                                                

3 rows selected.
```

<a id="75e6800fdcc8a492"></a>
#### Example

The following is an example of increasing the readability of the LONG VARCHAR column by reducing the colsize.

```
gSQL> \set colsize 200
gSQL> SELECT view_name, text FROM all_views WHERE view_name LIKE 'ALL_%' FETCH 3;

VIEW_NAME        TEXT                                                          
---------------- --------------------------------------------------------------
ALL_ALL_TABLES   SELECT                                                        
                        auth.AUTHORIZATION_NAME                ❶ OWNER        
                      , sch.SCHEMA_NAME                        ❷ TABLE_SCHEMA 
                      , tab.TABLE_NAME                         ❸ TABLE_NAME   
                      , spc.TAB                                                
ALL_COL_COMMENTS SELECT                                                        
                        auth.AUTHORIZATION_NAME                                
                      , sch.SCHEMA_NAME                                        
                      , tab.TABLE_NAME                                         
                      , col.COLUMN_NAME                                        
                      , col.COMMENTS                                           
                   FROM                                                        
                        DICTIONARY_SCHEMA.WHOLE_COLUMNS AS col                 
                      , DICTIONARY_S                                           
ALL_COL_PRIVS    SELECT                                                        
                        grantor.AUTHORIZATION_NAME                             
                      , grantee.AUTHORIZATION_NAME                             
                      , owner.AUTHORIZATION_NAME                               
                      , sch.SCHEMA_NAME                                        
                      , tab.TABLE_NAME                                         
                      , col.COLUMN_NAME                                        
                      , pvcol.PRIVILEGE_TY                                     

3 rows selected.
```

<a id="58135d3dceacd86f"></a>
### `\set ddlsize`

<a id="5415e56c0efb13f7"></a>
#### Syntax

```
\set ddlsize number
```

<a id="ec1c8ca443640bbf"></a>
#### Description

It sets the buffer size to output the statement when outputting the DDL statements by using the following commands.

- `\ddl_db`
- `\ddl_tablespace`
- `\ddl_auth`
- `\ddl_schema`
- `\ddl_table`
- `\ddl_constraint`
- `\ddl_index`
- `\ddl_view`
- `\ddl_sequence`
- `\ddl_synonym`
- `\ddl_public_synonym`
- `\ddl_procedure`
- `\ddl_package`

- The value of ddlsize is a positive integer between 1 and 1,0485,760 (10M).
- The default value of ddlsize is 10,000.

If an error occurs due to the lack of buffer space as follows, DDL statement may be output by increasing the value of ddlsize.

```
gSQL> \set ddlsize 1000
gSQL> \ddl_view dictionary_schema.all_tables

ERR-HY000(40052): not enough DDLSIZE. 
use command: \set ddlsize {n} 

gSQL> \set ddlsize 100000
gSQL> \ddl_view dictionary_schema.all_tables


SET SESSION AUTHORIZATION "SYS"; 
CREATE OR REPLACE FORCE VIEW "DICTIONARY_SCHEMA"."ALL_TABLES" 

... Ellipsis ...
```

<a id="6ae4189d2791e183"></a>
#### Example

The following is an example of changing the ddlsize.

```
gSQL> \set ddlsize 100000
gSQL>
```

<a id="96d9811f810ed53a"></a>
### `\set error`

<a id="32267be14c35e256"></a>
#### Syntax

```
\set error on
\set error off
```

<a id="4ae7680f33e3dc1e"></a>
#### Description

It sets whether to output the error message.

- `\set error on`
    - It outputs the error message. 
- `\set error off`
    - It does not output the error message. 
- The default value of error is ON.

If an error occurs during executing the SQL statement, gsql outputs the following information.

- SQLSTATE: SQL standard state code 
- Error code: GOLDILOCKS error code
- Error message

The following example describes that the error of the SQL statement occurs, the SQLSTATE value in ERR-42000(16040) is 42000, and the error code is 16040 within ().

```
gSQL> SELECT * FROM invalid_table;

ERR-42000(16040): table or view does not exist : 
SELECT * FROM invalid_table
              *
ERROR at line 1:
```

<a id="872a89154de762b7"></a>
#### Example

The following is an example of disabling the error message.

- Disabling the error message

```
gSQL> \set error off
```

- Outputting only the value of SQLSTATE and the error code

```
gSQL> SELECT * FROM invalid_table;

ERR-42000(16040)
```

<a id="47ca391ac7220527"></a>
### `\set heading`

<a id="411a4373073ea225"></a>
#### Syntax

```
\set heading {ON|OFF}
```

<a id="969ed01311f9391b"></a>
#### Description

It sets whether to output the header in the query result.

<a id="e9e6a190021b30a1"></a>
#### Example

- Set not to output the header message.

```
gSQL> \set heading off
```

- The following is an example of a query result in which the header message is not output.

```
gSQL> select * from dual;

X    

1 row selected.
```

<a id="3ec7cb10d93a1a99"></a>
### `\set history`

<a id="177131ec9aa746cb"></a>
#### Syntax

```
\set history number
```

<a id="0a4ae34441fde06c"></a>
#### Description

It sets the number of SQL statements to manage the history information.

- The history value is a positive integer between 1 and 100,000.
- If the history value is set to a negative value, all SQL history are removed.
- The default value of history is 128.

If the history value is reduced, the old SQL statement is removed.  
The history information is used when executing the previously executed SQL statement again through [`\\`](#e9fcaf4386815ef7) and [`\{n}`](#cfaf01b3c6c630d9).

<a id="a41f20ac1d8db035"></a>
#### Example

The following is an example of setting the number of history to 100.

```
gSQL> \set history 100
gSQL>
```

The following is an example of setting the number of history to smaller than the number of stored SQL statements.

- Five SQL statements are stored.

```
gSQL> \history

ID SQL                                            
-- -----------------------------------------------
 1 DROP TABLE IF EXISTS t1                        
 2 CREATE TABLE t1                                
   (                                              
       id   INTEGER PRIMARY KEY,                  
       name VARCHAR(128),                         
       addr VARCHAR(128)                          
   )                                              
 3 CREATE INDEX t1_idx_name ON t1(name)           
 4 INSERT INTO t1                                 
          VALUES ( 1, 'leekmo', 'Seoul, Korea'  ),
                 ( 2, 'mkkim' , 'Seoul, Korea'  ),
                 ( 3, 'xcom73', 'Inchon, Korea' ) 
 5 COMMIT
```

- The history value is reduced to 3.

```
gSQL> \set history 3
```

- Three SQL statements are stored.

```
gSQL> \history

ID SQL                                            
-- -----------------------------------------------
 3 CREATE INDEX t1_idx_name ON t1(name)           
 4 INSERT INTO t1                                 
          VALUES ( 1, 'leekmo', 'Seoul, Korea'  ),
                 ( 2, 'mkkim' , 'Seoul, Korea'  ),
                 ( 3, 'xcom73', 'Inchon, Korea' ) 
 5 COMMIT
```

The following is an example of removing all SQL statements stored in the history.

```
gSQL> \history

ID SQL                      
-- -------------------------
 1 SELECT * FROM dual       
 2 SELECT * FROM user_tables
```

- All SQL history are removed by using a negative value.

```
gSQL> \set history -1

gSQL> \history
gSQL>
```

<a id="42daf702d2eace6a"></a>
### `\set linesize`

<a id="f9562807728171b5"></a>
#### Syntax

```
\set linesize number
```

<a id="7b09884d434ba25e"></a>
#### Description

It sets the maximum size of a single line when outputting the query result.

- The value of linesize is a positive integer between 1 and 10,000.
- The default value of linesize is 80.

Each row of the query result is output on a single line basis. If there are many columns in a row or the row length is bigger than linesize, a row is output to the multiple lines so the readability is decreased.

```
gSQL> SELECT * FROM dict_columns WHERE table_name = 'USER_TABLES' FETCH 3;

TABLE_SCHEMA      TABLE_NAME  COLUMN_NAME    
----------------- ----------- ---------------
COMMENTS                                   
-------------------------------------------
DICTIONARY_SCHEMA USER_TABLES TABLE_SCHEMA   
Schema of the table                        
DICTIONARY_SCHEMA USER_TABLES TABLE_NAME     
Name of the table                          
DICTIONARY_SCHEMA USER_TABLES TABLESPACE_NAME
Name of the tablespace containing the table

3 rows selected.
```

In this case, a row may be controlled to be output in a single line by changing the linesize value.

<a id="0e498495255e6d90"></a>
#### Example

The following is an example of increasing the readability by setting the linesize larger.

```
gSQL> \set linesize 400
gSQL> SELECT * FROM dict_columns WHERE table_name = 'USER_TABLES' FETCH 3;

TABLE_SCHEMA      TABLE_NAME  COLUMN_NAME     COMMENTS                                   
----------------- ----------- --------------- -------------------------------------------
DICTIONARY_SCHEMA USER_TABLES TABLE_SCHEMA    Schema of the table                        
DICTIONARY_SCHEMA USER_TABLES TABLE_NAME      Name of the table                          
DICTIONARY_SCHEMA USER_TABLES TABLESPACE_NAME Name of the tablespace containing the table

3 rows selected.
```

<a id="c01ce4b4112a0598"></a>
### `\set numsize`

<a id="774a3aa56dd86e44"></a>
#### Syntax

```
\set numsize number
```

<a id="88cab569674406a2"></a>
#### Description

It sets the maximum number of digit for the output of a numeric value.

- The numsize value is a positive integer between 1 and 50. 
- The default value of numsize is 20.

If the number of digit of a numeric value exceeds the numsize range as follows, it is output in an exponential form.

```
gSQL> SELECT num, ( num * num ) AS result FROM t1;

          NUM               RESULT
------------- --------------------
1234567890123 1.52415787532276E+24

1 row selected.
```

By changing the value of numsize, these numeric value is output in a numeric form, not in an exponent form.

<a id="c86ef970b2b633d3"></a>
#### Example

The following is an example of outputting all digits of the numeric value by setting the numsize larger.

```
gSQL> \set numsize 50
gSQL> SELECT num, ( num * num ) AS result FROM t1;

          NUM                    RESULT
------------- -------------------------
1234567890123 1524157875322755800955129

1 row selected.
```

<a id="881be7eb5569cdac"></a>
### `\set pagesize`

<a id="dea786c54d70fc34"></a>
#### Syntax

```
\set pagesize number
```

<a id="b0f2c1b0567fc160"></a>
#### Description

It sets the number of the rows which is to be consisted in a single page.

- The value of pagesize is a positive integer between 1 and 10,000.
- The default value of pagesize is 20.

It is set when there are many rows of the query results or when a page should consist of a certain number of row.

<a id="20e16e7b31281cb0"></a>
#### Example

The following is an example of consisting a page in 10 rows unit.

```
gSQL> \set linesize 120
gSQL> \set pagesize 10
gSQL> SELECT column_name, comments FROM dict_columns  WHERE table_name = 'SEQUENCES';

COLUMN_NAME       COMMENTS                                                             
----------------- ---------------------------------------------------------------------
OWNER_ID          authorization identifier who owns the table of the sequence generator
SCHEMA_ID         schema identifier of the sequence generator                          
SEQUENCE_ID       sequence generator identifier                                        
SEQUENCE_TABLE_ID table id of sequence for naming resolution                           
TABLESPACE_ID     tablespace identifier of the sequence generator                       
PHYSICAL_ID       physical identifier of the sequence generator                        
SEQUENCE_NAME     sequence generator name                                              
DTD_IDENTIFIER    unsupported feature                                                  
START_VALUE       the start value of the sequence generator                            
MINIMUM_VALUE     the minimum value of the sequence generator                          

COLUMN_NAME      COMMENTS                                                         
---------------- -----------------------------------------------------------------
MAXIMUM_VALUE    the maximum value of the sequence generator                      
INCREMENT        the increment of the sequence generator                          
CYCLE_OPTION     The values of CYCLE_OPTION have the following meanings:          
                 - TRUE : The cycle option of the sequence generator is CYCLE.    
                 - FALSE : The cycle option of the sequence generator is NO CYCLE.
                                                                                  
CACHE_SIZE       number of sequence numbers to cache                              
CREATED_TIME     created time of the sequence generator                           
MODIFIED_TIME    last modified time of the sequence generator                     
COMMENTS         comments of the sequence generator                               
SEQUENCE_CATALOG catalog name of the sequence                                     
SEQUENCE_OWNER   owner name of the sequence                                       
SEQUENCE_SCHEMA  schema name of the sequence                                      

COLUMN_NAME             COMMENTS                                                         
----------------------- -----------------------------------------------------------------
SEQUENCE_NAME           sequence name                                                    
DATA_TYPE               the standard name of the data type                               
NUMERIC_PRECISION       the numeric precision of the numerical data type                 
NUMERIC_PRECISION_RADIX the radix ( 2 or 10 ) of the precision of the numerical data type
NUMERIC_SCALE           the numeric scale of the exact numerical data type               
START_VALUE             the start value of the sequence generator                        
MINIMUM_VALUE           the minimum value of the sequence generator                      
MAXIMUM_VALUE           the maximum value of the sequence generator                      
INCREMENT               the increment of the sequence generator                          
CYCLE_OPTION            cycle option                                                     

COLUMN_NAME                COMMENTS                                    
-------------------------- --------------------------------------------
CACHE_SIZE                 number of sequence numbers to cache         
DECLARED_DATA_TYPE         the data type name that a user declared     
DECLARED_NUMERIC_PRECISION the precision value that a user declared    
DECLARED_NUMERIC_SCALE     the scale value that a user declared        
CREATED_TIME               created time of the sequence generator      
MODIFIED_TIME              last modified time of the sequence generator
COMMENTS                   comments of the sequence generator          

37 rows selected.
```

<a id="6f38a748002b82ea"></a>
### `\set serveroutput`

<a id="b3cbc75f8e14150f"></a>
#### Syntax

```
\set serveroutput on
\set serveroutput off
```

<a id="1a5783817d3e7fca"></a>
#### Description

It controls automatic output feature for the message writeten by functions of which DBMS_OUTPUT package provides in gsql or gsqlnet

- `\set serveroutput on`
    - It automatically outputs messages accumulated in the server by DBMS_OUTPUT.PUT_LINE after executing SQL.
- `\set serveroutput off`
    - It does not use DBMS_OUTPUT package.
- The default value of serveroutput is OFF.

Basically, the maximum size of accumulated in the server is 20000 bytes.

<a id="bcf1360c6085bce1"></a>
#### Example

The following is an example of outputting the messages accumulated in a user defined function which was used in SQL statement.

```
gSQL> create or replace function my_msg( msg varchar(100) )
return integer
is
begin
  dbms_output.put_line( 'my message is : ' || msg );
  return length( msg );
end;
/
2 3 4 5 6 7 8 
Function created.

gSQL> commit;

Commit complete.

gSQL> \set serveroutput on
gSQL> select my_msg( 'Hello World!' ) from dual;

MY_MSG( 'Hello World!' )
------------------------
                      12

my message is : Hello World!
1 row selected.
```

<a id="7866de136f33ca55"></a>
### `\set sqlprompt`

<a id="60d55374f45e709f"></a>
#### Syntax

```
\set sqlprompt "prompt_sql"
```

<a id="ac6367a5ee850081"></a>
#### Description

It sets SQL for prompt of gsql or gsqlnet.

- Maximum 127 characters are allowed in SQL statement.
- Maximum 31 characters are allowed in the prompt returning to SQL statement.

Even when SQL is set, the prompt is not changed until connecting to the database.

If SQL statement is incorrect or the returning data is longer than 31 characters, then the user SQL statement is output following [SQLPROMPT ERROR] statement.

<a id="fcacd29747fa47d2"></a>
#### Example

The following is an example of outputting the user name and the cluster member name in the prompt.

```
gSQL> \set sqlprompt "current_user || '@' || cluster_member_name || '>'"
TEST@G1N1>
```

<a id="d3bd36d4c60a2bd6"></a>
### `\set time`

<a id="5a29f01412d4fa88"></a>
#### Syntax

```
\set time on
\set time off
```

<a id="f6dd5f9f5c7aae92"></a>
#### Description

It sets whether to output the current time.

- `\set time on`
    - It outputs the current time.
- `\set time off`
    - It does not output the current time.
- The default value of time is OFF.

<a id="fb4faf3447646f7a"></a>
#### Example

The following is an example of outputting the current time.

```
gSQL> \set time on
12:45:34 gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.

Elapsed time: 0.07600 ms
```

<a id="dacb5d2a2fc8e430"></a>
### `\set timing`

<a id="cd0c5896c3dcbc5a"></a>
#### Syntax

```
\set timing on
\set timing off
```

<a id="b06d93b1a6f00b1b"></a>
#### Description

It sets whether to output the execution time of SQL statement.

- `\set timing on`
    - The execution time is output. 
- `\set timing off`
    - The execution time is not output. 
- The default value of timing is OFF.

The unit of execution time is ms (millisecond).

<a id="9e748c2c0681293e"></a>
#### Example

The following is an example of outputting the execution time of SQL statement.

```
gSQL> \set timing on
gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.

Elapsed time: 0.07600 ms
```

<a id="969c6bd29ccd83a7"></a>
### `\set vertical`

<a id="1f456d1a969b8357"></a>
#### Syntax

```
\set vertical on
\set vertical off
```

<a id="43a040464cd7792f"></a>
#### Description

It sets whether to output the value of column in line unit.

- `\set vertical on`
    - A column is output in a line unit.
- `\set vertical off`
    - A row is output in a line unit.
- The default value of vertical is OFF.

If each row has an individual information, the readability can be increased by outputting the query result in a column unit.

If `\set vertical on` is set, then each row is separated by a blank line, and one line represents a single value, then it is consisted in the following form.

```
column name # data value
```

<a id="782c14f135c43068"></a>
#### Example

The following is an example of outputting a query result in a column unit.

```
gSQL> \set vertical on
gSQL> SELECT * FROM v$system_stat FETCH 10;

               STAT_NAME # SYSTEM_SAR
              STAT_VALUE # 3
                COMMENTS # system available resource( 0:none, 1:session 2:database )

               STAT_NAME # MAX_ENVIRONMENT_COUNT
              STAT_VALUE # 128
                COMMENTS # maximum environment count

               STAT_NAME # FREE_ENVIRONMENT_ID
              STAT_VALUE # 81
                COMMENTS # available environment identifier

               STAT_NAME # MAX_SESSION_COUNT
              STAT_VALUE # 128
                COMMENTS # maximum session count

               STAT_NAME # FREE_SESSION_ID
              STAT_VALUE # 82
                COMMENTS # available session identifier

               STAT_NAME # MAX_PROCESS_COUNT
              STAT_VALUE # 128
                COMMENTS # maximum process count

               STAT_NAME # FREE_PROCESS_ID
              STAT_VALUE # 1
                COMMENTS # available process identifier

               STAT_NAME # CACHE_ALIGNED_SIZE
              STAT_VALUE # 64
                COMMENTS # cache aligned size

               STAT_NAME # CPU_COUNT
              STAT_VALUE # 8
                COMMENTS # count of CPUs

               STAT_NAME # SYSTEM_TIME
              STAT_VALUE # 1408676900172925
                COMMENTS # system time


10 rows selected.
```

<a id="12d8dd68e6403350"></a>
### `\shutdown`

<a id="7713465ba595f8b5"></a>
#### Syntax

```
\shutdown
\shutdown abort
\shutdown immediate
\shutdown transactional
\shutdown normal
```

<a id="72d2d919b4b9311d"></a>
#### Description

It shuts down the GOLDILOCKS server.  
It should be connected as SYSDBA or ADMIN role to perform `\shutdown`. For more information about connecting as SYSDBA, refer to [Startup and Shutdown Server](#30a646b9d93b86a8).

- `\shutdown normal`
    - It blocks the connection from the new session and waits for all currently connected sessions to be terminated, then performs the checkpoint and shuts down the server.
- `\shutdown transactional`
    - It blocks the start of a new transaction and waits for all currently running transactions to be terminated, then performs the checkpoint and shuts down the server.
- `\shutdown immediate`
    - It blocks the execution of a new unit operation(ex FETCH or EXECUTE, etc.), waits for all currently running unit operations to be terminated, then rolls back all transactions and performs the checkpoint and shuts down the server.
- `\shutdown abort`
    - The server is forcibly shut down immediately regardless of the status of the currently connected session.
- `\shutdown`
    - It is as same as `\shutdown normal`.

In GOLDILOCKS cluster system, if the current phase is GLOBAL OPEN when using `\`shutdown to shut down a single node, then abort is the only option, but if the current phase is LOCAL OPEN or below, then all options are available.    
If using an option other than abort on GLOBAL OPEN phase, then the following error occurs.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \shutdown immediate

ERR-42000(16430): in the GLOBAL OPEN phase, the cluster database can be closed only with ABORT option :
ALTER SYSTEM CLOSE DATABASE IMMEDIATE
                            *
ERROR at line 1:
gSQL>
```

<a id="c8e5a66d27824745"></a>
#### Example

The following is an example of shutdowning GOLDILOCKS.

```
% gsql --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \shutdown

Shutdown success

gSQL>
```

<a id="b7d07f5598c0ed0c"></a>
### `\spool`

<a id="c29db5db4054e04b"></a>
#### Description

It sets all results output by using gsql to be stored in the terminal and file.

<a id="cc2f4d5766e16e0e"></a>
#### `\spool 'filename'`

<a id="64ebcdc2f37aa8e7"></a>
##### Syntax

```
\spool 'filename' [CREATE | REPLACE | APPEND]
\spo   'filename' [CREATE | REPLACE | APPEND]
```

<a id="755833f536d61330"></a>
##### Description

It starts the spool function. All output results performed by gsql are stored in the given filename since executing this statement.

The following options describe how to open the file.

- CREATE: It creates the file. If a file already exists, an error occurs. 
- REPLACE: It removes the contents of an existing file, and newly starts storing. If a file does not exist, it performs as same as CREATE.
- APPEND: It continues to store the contents from the end of an existing file. If a file does not exist, it performs as same as CREATE.

If these options are not given, it is operated in REPLACE mode by default.

> When starting a new spool during spooling, the existing spool stops and a new spool starts.

<a id="69e5250149342167"></a>
##### Example

The following is an example of starting spooling.

- Creating the result.txt file and storing the gsql execution result

```
gSQL> \SPOOL 'result.txt' CREATE
gSQL> SELECT * FROM T1 WHERE C1 < 10;
gSQL> \SPOOL OFF
```

- Continuing to store the result at the end of the existing result.txt file

```
gSQL> \SPOOL 'result.txt' APPEND
gSQL> SELECT * FROM T1 WHERE C1 >= 10;
gSQL> \SPOOL OFF
```

- Removing the contents of the existing result.txt file and storing a new result

```
gSQL> \SPOOL 'result.txt' REPLACE
gSQL> SELECT * FROM T1;
gSQL> \SPOOL OFF
```

<a id="044218139fe7146a"></a>
#### `\spool OFF`

<a id="e47f9d37f186c34c"></a>
##### Syntax

```
\spool OFF
\spo   OFF
```

<a id="b1672a93dd9acf40"></a>
##### Description

It ends the current spool. If the spool is not in use, it does not perform any transaction.

<a id="16038a9102731e94"></a>
##### Example

The following is an example of starting the spool then ending it.

```
gSQL> \SPOOL 'result.txt'
gSQL> SELECT * FROM T1;
```

- Ending spooling

```
gSQL> \SPOOL OFF
```

<a id="a83ded0fca072278"></a>
#### `\spool`

<a id="84e98e00ed3a6130"></a>
##### Syntax

```
\spool
\spo
```

<a id="ee7da55a2aa4c9bb"></a>
##### Description

It represents the current spool state. If the spool is in use, it informs which file is spooling. Otherwise, it informs that the spool is not in use.

<a id="0788abb46423a5dc"></a>
##### Example

The following is an example of editing the SQL statement stored in the gsql history.

```
gSQL> \SPOOL 'a.txt'
```

- It informs that it is spooling in a.txt.

```
gSQL> \SPOOL
 
currently spooling to a.txt
 
gSQL> \SPOOL OFF
```

- It informs that it is not spooling.

```
gSQL> \SPOOL
 
not spooling currently
```

<a id="b08fd63635320af0"></a>
### `\startup`

<a id="ecefe28da3d5647a"></a>
#### Syntax

```
\startup
\startup nomount
\startup mount
\startup open
```

<a id="8efc5f96e385c0c7"></a>
#### Description

It starts up the GOLDILOCKS server.  
It should be connected as SYSDBA or ADMIN role to perform `\startup`.   
For more information about connecting as SYSDBA, refer to [Startup and Shutdown Server](#30a646b9d93b86a8).

- `\startup nomount`
    - It starts up the server on the NOMOUNT phase.
- `\startup mount`
    - It starts up the server on the MOUNT phase.
- `\startup open`
    - It starts up the server on the OPEN phase.
- `\startup `
    - It is as same as `\startup open`.

The server start up is divided into NOMOUNT, MOUNT, OPEN phase. For more information, refer to [Multi-level Startup](../part-02-administration-manual/5-basic-management-of-goldilocks-database.md#83b0b11e83fe4d59).  
Execute [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references-a-b.md#6b3352cd0d97f557) statement to move on to the next phase after executing `\startup`.

<a id="ddc4e5de85809191"></a>
#### Example

The following is an example of starting up GOLDILOCKS.

```
% gsql --as SYSDBA

Connected to an idle instance.

gSQL> \startup

Startup success
```

<a id="466b7f8794c4595b"></a>
### `\var`

<a id="a0f9a500993db066"></a>
#### Syntax

```
\var variable_name data_type
```

<a id="72840024690e1f08"></a>
#### Description

It declares the host variable.  
When declaring the host variable which is as same as variable_name, the existing host variable is removed and a new one is declared. The maximum length of variable_name is 128 bytes.  
The data_type of host variable is as same as the data type of GOLDILOCKS.   
For more information, refer to [Data Type](../part-03-sql-manual/11-sql-elements.md#545971a2288a7b29).  
The host variable assigns the value by using [`\exec :var := value`](#7b19e6e57e1e5fdd) , and its value is queried by using [`\print`](#40764010c6ea1a78).

```
gSQL> \var v1 INTEGER
gSQL> \exec :v1 := 1
gSQL> \print v1

V1
--
 1
```

The host variable can be used as an input or output parameter in the SQL statement. When the host variable is used in the SQL statement or [`\exec :var := value`](#7b19e6e57e1e5fdd), a colon (:) sign should be put in front of the host variable to indicate that it is a host variable.

<a id="b0c818f6bb3c4c5e"></a>
#### Example

The following is an example of declaring the host variable and using it as an input argument of the SQL statement.

```
gSQL> \var v1 INTEGER
gSQL> \exec :v1 := 1
gSQL> SELECT * FROM t1 WHERE id = :v1;

ID NAME   ADDR        
-- ------ ------------
 1 leekmo Seoul, Korea

1 row selected.
```

The following is an example of using the host variable as an output argument of the SQL statement.

```
gSQL> \var v_name VARCHAR(128)
gSQL> SELECT name INTO :v_name FROM t1 WHERE id = 1;

V_NAME
------
leekmo

1 row selected.
```

The following is an example of declaring the host variable and using it as the input and output arguments of the SQL statement.

In the following [UPDATE name RETURNING .. INTO](../part-03-sql-manual/20-sql-references-h-z.md#fbacf0fb95b1411a) statement, the host variable of SET clause and WHERE clause, :v_id, is used as an input argument and :v_id of INTO clause is used as an output argument.

```
gSQL> \var v_name VARCHAR(128)
gSQL> \var v_id INTEGER             
gSQL> \exec :v_id := 1
gSQL> UPDATE t1 SET id = 100 + :v_id WHERE id = :v_id RETURNING id INTO :v_id;

V_ID
----
 101

1 row updated.

gSQL> \print v_id

V_ID
----
 101
```

---

[← 38. glsnr](38-glsnr.md) · [Table of contents](../README.md) · [40. gloader/gloadernet(Upload/download Tool) →](40-gloader-gloadernet-upload-download-tool.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
