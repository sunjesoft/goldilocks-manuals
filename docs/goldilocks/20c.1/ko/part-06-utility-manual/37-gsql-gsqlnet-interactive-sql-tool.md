<a id="35503e53d20c27eb"></a>

# 37. gsql/gsqlnet (Interactive SQL Tool)

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/35503e53d20c27eb)  
> 태그: `20c.1_30_tag`

[← 36. glsnr](36-glsnr.md) · [전체 목차](../README.md) · [38. gloader/gloadernet (Upload/download Tool) →](38-gloader-gloadernet-upload-download-tool.md)

<a id="f540f626c7838e92"></a>
## gsql 개요

다음은 실행파일이다.

**실행파일 구분**

<a id="0fac8c19b60cb1fb"></a>
| 실행파일 이름 | 구분 |
| --- | --- |
| gsql | Direct attach (D/A) 환경에서 사용된다. |
| gsqlnet | Client/ server (C/S) 환경에서 사용된다. |

> gsql에서 제공되는 모든 명령어는 gsqlnet에서도 동일하게 사용된다.

<a id="889705078ca51e2a"></a>
### 정의

gsql은 SQL 구문을 처리하기 위해 GOLDILOCKS에서 제공하는 대화형 유틸리티이다.

별도로 응용 프로그램을 작성하지 않아도 gsql 프로그램을 통해 SQL 구문을 수행할 뿐 아니라 SELECT 구문의 결과를 조회할 수도 있다.

gsql 프로그램은 SQL 구문을 수행할 뿐만 아니라 `(\)` 로 시작하는 gsql 고유의 명령어를 통해 테이블과 인덱스 등의 간략한 객체 정보를 조회할 수 있으며 서버의 구동과 종료, 출력 결과의 제어, SQL 구문의 실행 계획 정보 조회 등의 다양한 기능들을 제공한다.

<a id="f4e05c524828489b"></a>
### 사용 예

본 장에서는 gsql을 사용하여 테이블을 생성/ 제거하고 데이터를 조작하며 질의를 수행하는 예를 설명한다.

다음과 같이 gsql을 대화형 모드로 구동한다. 정상적으로 접속할 경우 *gSQL>* 프롬프트와 함께 SQL 구문이나 gsql 명령이 입력되기를 기다린다.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL>
```

다음과 같이 [CREATE TABLE](../part-03-sql-manual/18-sql-references.md#9b82da6d66aabe8c) 구문을 수행하여 테이블을 생성하고 트랜잭션을 COMMIT 한다.

```
gSQL> CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) );                 

Table created.

gSQL> COMMIT;

Commit complete.
```

생성한 테이블에 [INSERT INTO](../part-03-sql-manual/18-sql-references.md#f7aecaaad34d188f) 구문을 수행하여 데이터를 추가하고 트랜잭션을 COMMIT 한다. 두 번째 INSERT 구문은 두 개의 row를 추가하는 예이다.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'leekmo' );

1 row created.
```

- 두 개의 row가 추가된다.

```
gSQL> INSERT INTO t1 VALUES ( 2, 'mkkim' ), ( 3, 'xcom73' );

2 rows created.

gSQL> COMMIT;

Commit complete.
```

다음은 테이블에 addr column을 추가하고 [UPDATE](../part-03-sql-manual/18-sql-references.md#43a8287f83dce60b) 구문을 수행하여 데이터를 갱신하는 예이다.

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

다음과 같이 입력된 데이터를 [SELECT](../part-03-sql-manual/18-sql-references.md#93101dc44f4e210d) 질의를 이용하여 조회한다. 질의 결과는 column 이름을 표현하는 header와 각 row를 하나의 line에 출력한 정보로 구성되어 있다. NULL 값은 소문자 null로 표현된다.

```
gSQL> SELECT * FROM t1 ORDER BY 1;

ID NAME   ADDR         
-- ------ -------------
 1 leekmo Seoul, Korea 
 2 mkkim  null         
 3 xcom73 Inchon, Korea

3 rows selected.
```

다음과 같이 호스트 변수를 선언하고 호스트 변수에 값을 대입하고 호스트 변수를 이용하여 질의를 수행할 수 있다.

```
gSQL> \var v_id INTEGER
gSQL> \exec :v_id := 1
gSQL> SELECT * FROM t1 WHERE id = :v_id;

ID NAME   ADDR        
-- ------ ------------
 1 leekmo Seoul, Korea

1 row selected.
```

[`\prepare sql`](#0a689bc4cd07f2fe) 명령을 이용해 SQL 구문을 준비하고 호스트 변수의 값을 바꿔가며 [`\exec`](#0f3949721f6b5ec3) 명령을 이용해 위의 SELECT 구문을 반복 수행한다. 다음과 같이 gsql 대화형 모드에서 ODBC와 JDBC의 prepare/ execute 동작을 simulation 할 수 있다.

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

다음은 embedded SQL, ODBC, JDBC에서 scrollable 커서를 선언하고 gsql을 통해 커서를 이용한 데이터 검색을 simulation 하는 예이다. [DECLARE cursor_name](../part-03-sql-manual/18-sql-references.md#45b9d98474d5f09d) 구문을 이용해 선언한 커서 cur1은 스크롤이 가능한 KEYSET 커서로써 [FETCH cursor_name](../part-03-sql-manual/18-sql-references.md#bafc38978b00122c) 구문을 이용해 다양한 fetch orientation을 사용할 수 있다.

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

다음은 생성한 테이블 t1을 제거하고 gsql 대화형 모드를 종료하는 예이다.

```
gSQL> DROP TABLE t1;

Table dropped.

gSQL> COMMIT;

Commit complete.

gSQL> \q
%
```

<a id="26f1a9e7fc256701"></a>
## gsql 실행

<a id="80a5f9bd2f310f5a"></a>
### gsql 정보

다음은 참조 옵션이다.

**참조 옵션**

<a id="1c9c4955fa879978"></a>
| 옵션 | 설명 |
| --- | --- |
| [--help](#e379aebc5348012d) | 옵션 목록 |
| [--version](#778446d7c5a93808) | gsql 버전 정보 |

Shell 프롬프트 상에서 수행할 수 있는 gsql의 command option은 다음과 같이 [--help](#e379aebc5348012d) 옵션을 통해 확인할 수 있다.

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

... 중략 ...

%
```

gsql 프로그램은 GOLDILOCKS 서버와 달리 별도의 version을 가지는데 다음과 같이 [--version](#778446d7c5a93808) 옵션을 사용하여 확인할 수 있다. GOLDILOCKS 서버의 version과 동일한 gsql 프로그램을 사용할 것을 권장한다.

```
% gsql --version

%
```

참고로 GOLDILOCKS 서버의 version은 다음과 같이 [VERSION](../part-03-sql-manual/17-built-in-function-references.md#38cde8c6fcd22905) 함수를 통해 확인할 수 있다.

```
gSQL> SELECT version() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="89e6a2ae339d700e"></a>
### 서버 접속

다음은 참조 옵션이다.

**참조 옵션**

<a id="33b14c20234e5562"></a>
| 옵션 | 설명 |
| --- | --- |
| [Username Password](#ffb66b3b6802a4dd) | 접속 사용자와 패스워드이다. |
| [--as {SYSDBA\|ADMIN}](#404a2449eaedab75) | 접속 role을 지정한다. |
| [--conn-string](#9f82c37b2b9ee3ed) | Connection string을 지정한다. |
| [--dsn](#084795786c7a0399) | Data Source Name (DSN)을 지정한다. |

<a id="0fe730d3ffb14441"></a>
#### 사용자 접속

gsql 프로그램을 이용하여 다양한 방법으로 GOLDILOCKS 서버에 접속할 수 있다.

다음과 같이 사용자 이름과 패스워드를 이용해 접속하는 것이 가장 단순한 사용 예이다. 다음 예는 test 사용자가 test 패스워드를 이용하여 접속하는 예이다. 접속에 성공할 경우, 대화형 모드로 동작하여 *gSQL>* 프롬프트가 사용자의 명령을 기다린다.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL>
```

다음은 잘못된 사용자 이름이나 잘못된 패스워드를 사용한 경우에 발생하는 에러이다. 로그인에 실패할 경우, 에러 메시지를 출력한 후에 gsql 프로그램을 종료한다.

```
% gsql test invalid_password

ERR-28000(16004): invalid username/password; logon denied

%
```

다음은 GOLDILOCKS 서버가 구동되지 않았을 경우에 에러가 발생하는 예이다. 다음과 같은 에러 메시지와 함께 gsql 프로그램이 종료된다.

```
% gsql test test

ERR-HY000(11031): Unable to attach the shared memory segment

%
```

이 외에도 다음과 같은 옵션을 통해 접속할 수 있는데 자세한 내용은 다음 옵션들을 참조한다.

- [--conn-string](#9f82c37b2b9ee3ed)
- [--dsn](#084795786c7a0399)

<a id="5abfd0232ede30fc"></a>
#### SYSDBA 접속

서버를 구동하거나 database에 대한 모든 권한을 가진 SYSDBA role 등에 접속하려면 [--as {SYSDBA|ADMIN}](#404a2449eaedab75) 옵션을 사용해야 한다.

다음은 GOLDILOCKS 서버를 구동하지 않은 상태에서 --as sysdba로 접속하는 예이다. *Connected to an idle instance* 메시지와 함께 *gSQL>* 프롬프트가 GOLDILOCKS를 구동할 수 있는 상태로 대기하고 있다.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL>
```

다음은 GOLDILOCKS 서버가 이미 구동되어 있는 경우 --as sysdba로 접속하는 예이다.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL>
```

서버 구동 및 종료에 대한 자세한 내용은 [서버 구동 및 종료](#1b5d02a17418ebcf)를 참조한다.

<a id="b92e7559d92dbf6e"></a>
#### gsql 종료

gsql은 다음과 같이 `\quit` 또는` \q` 명령을 이용하여 종료한다.   
자세한 내용은 [`\quit`](#9e3cc316e0e9f7fb)을 참조한다.

```
gSQL> \quit
%
```

<a id="5945635574e52670"></a>
### 대화형 모드 제어

다음은 참조 옵션이다.

**참조 옵션**

<a id="d7c83b5ceed75ca9"></a>
| 옵션 | 설명 |
| --- | --- |
| [--prompt](#a9c37b1d4e880db4) | 프롬프트를 지정한다. |
| [--no-prompt](#02067012a2a7f497) | 프롬프트를 제거한다. |
| [--import](#1e9ff833ceb05528) | 입력으로 SQL 파일을 수행한다. |
| [--silent](#ba57fa08b7eeadf7) | SQL 파일을 실행할 때 명령어와 실행 결과를 출력하지 않는다. |
| [--enable-color](#e48922af261f2aee) | 질의 결과를 row 별로 구분하여 출력한다. |

<a id="c81a08571d05b3f3"></a>
#### 프롬프트 제어

대화형 모드를 시작할 때 다음 예와 같이 --prompt 옵션을 이용하여 프롬프트를 변경할 수 있다. 다음은 *gSQL>* 프롬프트가 아닌 *GOLDILOCKS>* 프롬프트로 변경하는 예이다.

```
% gsql test test --prompt GOLDILOCKS

Connected to GOLDILOCKS Database.

GOLDILOCKS>
```

프롬프트 제어에 대한 자세한 내용은 다음 옵션들을 참조한다.

- [--prompt](#a9c37b1d4e880db4)
- [--no-prompt](#02067012a2a7f497)

<a id="83bcb12792e32363"></a>
#### 파일로부터 수행

gsql 프로그램을 이용하여 배치 작업 등을 수행할 때 --import 옵션을 이용하여 파일에 포함된 SQL 구문을 수행할 수 있다. 다음은 $GOLDILOCKS_HOME/admin 디렉토리에서 PerformanceViewSchema.sql 파일을 수행하는 예이다. 해당 예는 --silent 옵션을 이용하여 수행 결과를 출력하지 않도록 하였다.

```
% cd $GOLDILOCKS_HOME/admin
% gsql sys gliese --as sysdba --import 'PerformanceViewSchema.sql' --silent
%
```

파일로부터 gsql을 수행하는 방법에 대한 자세한 내용은 다음 옵션들을 참조한다.

- [--import](#1e9ff833ceb05528)
- [--silent](#ba57fa08b7eeadf7)
- [--enable-color](#e48922af261f2aee)

<a id="8a0fd27535b37eef"></a>
### gsql 설정 저장

<a id="5b0ef221326dd334"></a>
#### gsql 환경 파일 (gsql.ini)

gsql 환경 파일 (.gsql.ini)은 gsql을 구동할 때 자동으로 적용되는 옵션들로 구성된 파일이며 $HOME 디렉토리에 위치해야 한다.

환경 파일에 다수의 dsn을 설정할 수 있고 각 dsn마다 다른 옵션들을 지정할 수 있다. gsql을 구동할 때 dsn을 입력하지 않을 경우, GOLDILOCKS의 옵션들을 적용한다.

<a id="280aa2c05296e608"></a>
#### 사용 예

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

**옵션**

<a id="52aabde7ee44cf28"></a>
| 옵션 | 최소값 | 최대값 | 기본값 |
| --- | --- | --- | --- |
| [AUTOCOMMIT](#c5342131808a2378) | OFF | ON | OFF |
| [AUTOTRACE](#9114076e891ca168) | OFF | ON/TRACEONLY | OFF |
| [LINESIZE](#8654bfd6f1680424) | 1 | 10000 | 80 |
| [PAGESIZE](#72d51f9c7e68284b) | 1 | 10000 | 20 |
| [VERTICAL](#e88795a4ee13cd81) | OFF | ON | OFF |
| [TIME](#1505d55ddcb6ffa9) | OFF | ON | OFF |
| [TIMING](#ef371f8fc5832f3c) | OFF | ON | OFF |
| [ERROR](#c8ff78168c631446) | ON | OFF | ON |
| [COLSIZE](#b8a3227147bc77e2) | 1 | 10485760 | 8192 |
| [NUMSIZE](#fb05859baf125d50) | 1 | 50 | 20 |
| [DDLSIZE](#84305527a9268b5f) | 1 | 10485760 | 10000 |
| [HISTORY](#6b3b3355aea3daf4) | 0 | 100000 | 128 |

> .gsql.ini가 없거나 옵션값이 유효하지 않은 경우에는 이를 무시한다.

<a id="fac4abddc4fa47b6"></a>
#### glogin.sql

glogin.sql은 전역 설정 파일로써 $GOLDILOCKS_DATA/conf/glogin.sql에 위치한다. gsql을 구동할 때 glogin.sql 파일이 있으면 해당 파일을 읽고 포함된 명령문을 실행한다. 이렇게 하면 모든 gsql 세션을 설정 (예: 라인 크기) 할 수 있다.

<a id="1bd2f99974b0a268"></a>
#### login.sql

login.sql은 사용자 설정 파일이다. gsql을 구동할 때 현재 디렉토리에 login.sql 파일이 있으면 해당 파일을 읽고 포함된 명령문을 실행한다.  
login.sql의 설정이 glogin.sql의 설정보다 우선한다.

<a id="71359cc3c5d3c57f"></a>
## Interactive Command 사용

<a id="5bef9dd87dd5ca30"></a>
### gsql 대화형 모드 명령어

다음은 참조 명령어이다.

**참조 명령어**

<a id="50581388189e622f"></a>
| gsql 명령 | 설명 |
| --- | --- |
| [`\help`](#c88e9fafc5990cae) | gsql 명령어 목록 |

gsql 프로그램은 [서버 접속](#89e6a2ae339d700e)을 통해 다음과 같은 대화형 모드로 동작한다.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL>
```

사용자는 프롬프트 상에서 SQL 구문을 입력하여 수행하거나 gsql 대화형 모드에서 수행할 수 있는 고유 명령어를 입력하여 수행할 수 있다. gsql 고유 명령어는 SQL 구문과 구별하기 위하여 `back-slash(\)`로 시작한다. 즉, SQL 구문은 응용 프로그램에서 직접 사용할 수 있는 반면에 `back-slash(\)`로 시작하는 gsql 명령어는 응용 프로그램에서 사용할 수 없다.

> gsql 대화형 모드 명령어는 `\` 로 시작한다.

다음은 SQL 구문을 대화형 모드에서 수행하는 예이다.

```
gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.
```

다음은 gsql 명령어 [`\exec sql`](#937854e40d50d4a1)을 사용하여 동일한 SELECT 구문을 사용하는 예이다. `\exec sql` 명령은 [Embedded SQL](../part-05-developer-manual/31-embedded-sql.md#39245ca09c37e99b)의 SQL 구문 시작을 의미하는 EXEC SQL과 구문이 동일할 뿐 gsql 고유의 명령어이다.

```
gSQL> \exec sql SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.
```

[`\set time`](#1505d55ddcb6ffa9)을 통해 현재 시간을 프롬프트에 출력하도록 설정할 수 있다.

```
gSQL> \set time on
12:45:34 gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.

12:45:37 gSQL>
```

gsql 대화형 모드의 고유 명령어들은 다음과 같이 [`\help`](#c88e9fafc5990cae) 명령을 이용해 조회할 수 있다.

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
\cshutdown       {[abort|normal]} 
\connect         userid password [as {sysdba|admin}]
```

<a id="1b5d02a17418ebcf"></a>
### 서버 구동 및 종료

다음은 참조 명령어이다.

**참조 명령어**

<a id="0af9827314441e7b"></a>
| gsql 명령 | 설명 |
| --- | --- |
| [`\startup`](#6745e7877cd84787) | 서버를 구동한다. |
| [`\shutdown`](#ecc902a1a812dd0f) | 서버를 종료한다. |
| [`\cstartup`](#4d333be4c98ad8f3) | Cluster 환경을 위한 서버를 구동한다. |
| [`\cshutdown`](#5137f3c14b98733e) | Cluster 환경을 위한 서버를 종료한다. |

<a id="425da0b5cc52370e"></a>
#### Standalone

서버를 구동하거나 종료하려면 다음과 같이 SYSDBA 또는 ADMIN role로 접속해야 한다.

- SYSDBA role
    - 서버 구동 및 종료 등 DBA 관련 모든 권한을 가진다.
- ADMIN role
    - SYSDBA와 동일한 권한을 가지지만 한 session에만 접속할 수 있다.
    - 유효 session이 없거나 비정상적인 상황에서의 비상 접속을 위한 role 이다.

다음은 GOLDILOCKS 서버가 구동되지 않은 상태에서 SYSDBA role로 접속하는 예이다.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL>
```

gsql은 GOLDILOCKS 서버가 없는 상태에서 idle instance에 접속하고 [`\startup`](#6745e7877cd84787)명령을 통해 GOLDILOCKS 서버를 특정 단계로 구동하여 서버에 접속한다. 다음은 NOMOUNT 단계로 GOLDILOCKS 서버를 구동하는 예이다.

```
gSQL> \startup NOMOUNT

Startup success

gSQL>
```

GOLDILOCKS를 최초로 구동할 때만 [`\startup`](#6745e7877cd84787) 명령을 사용하며 GOLDILOCKS 서버를 구동하고 서버에 접속한 후에는 [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references.md#f9fc4d123ed9181c) 구문을 이용해 GOLDILOCKS 서버의 각 단계로 전환한다.

```
gSQL> ALTER SYSTEM MOUNT DATABASE;

System altered.

gSQL> ALTER SYSTEM OPEN DATABASE;

System altered.

gSQL>
```

GOLDILOCKS 서버를 별도의 단계 전환 없이 서비스가 가능한 OPEN 단계로 구동할 경우, 다음과 같이 별도의 옵션없이 `\startup` 명령을 수행한다.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL> \startup

Startup success

gSQL>
```

이미 서버가 특정 단계로 구동된 경우 `\startup` 명령은 다음과 같이 에러를 출력한다. 서버가 OPEN 단계까지 구동된 경우가 아니라면 다음과 같이 ALTER SYSTEM 구문을 이용하여 서버를 OPEN 단계로 구동할 수 있다.

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

서버 구동과 관련한 자세한 내용은 다음 링크를 참조한다.

- 서버 구동 단계: [다단계 시작](../part-02-administration-manual/5-goldilocks-데이터베이스-관리-기본.md#324d293a99dd4a23)
- 최초 서버 구동 명령: [`\startup`](#6745e7877cd84787)
- 서버 단계 변경: [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references.md#f9fc4d123ed9181c)

서버를 종료하려면 다음과 같이 `\shutdown` 명령을 사용한다. 서버 종료에 대한 자세한 내용은 [`\shutdown`](#ecc902a1a812dd0f) 명령을 참조한다.

```
gSQL> \shutdown

Shutdown success

gSQL>
```

<a id="17b5e36e441522e2"></a>
#### Cluster

`\cstartup` 명령어와 `\cshutdown` 명령어를 사용하여 서버를 구동하거나 종료하기 위해서는 odbc.ini 파일에 LOCATOR_DSN 속성이 정의되어야 하고, gsqlnet을 이용하여 SYSDBA 또는 ADMIN role 로 접속해야 한다.

다음은 GOLDILOCKS 서버가 구동되지 않은 상태에서 gsqlnet을 사용하여 SYSDBA role로 접속하는 예이다.

```
% gsqlnet sys gliese --as sysdba

Connected to an idle instance.

gSQL>
```

다음은 `\cstartup` 명령을 이용하여 GOLDILOCKS 서버를 LOCAL OPEN 단계로 구동하고 서버를 OPEN 단계로 전환하는 예이다.

```
gSQL> \cstartup LOCAL OPEN

Startup success

gSQL> ALTER SYSTEM OPEN GLOBAL DATABASE;

System altered.

gSQL>
```

`\cstartup` 명령어와 `\cshutdown` 명령어는 CS 환경에서 사용하기 때문에 서버를 구동하거나 종료하기 위해서 모든 서버에 glsnr가 서비스 중이어야 한다.

다음은 glsnr이 서비스하고 있지 않은 GOLDILOCKS 서버를 구동하려고 시도하는 예이다.

```
gSQL> \cstartup

ERR-HY000(58000): MEMBER(G1N1): the sender failed to connect to the member(1)
ERR-HY000(11067): MEMBER(G1N1): fail to connect to a host with a socket : connect() : stnConnect() returned errno(111)

gSQL>
```

다음은 [odbc.ini 파일](../part-05-developer-manual/29-odbc.md#f1a0bc8659eada10) 에 LOCATOR_DSN 속성과 LOCATOR DSN이 정의된 예이다.

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

다음은 odbc.ini 파일에 LOCATOR_DSN 속성이 정의되지 않은 상태에서 서버를 구동하려는 예이다.

```
gSQL> \cstartup

ERR-HY000(40057): not specified valid location information

gSQL>
```

`\CSTARTUP {LOCAL | GLOBAL} OPEN` 이외의 명령어는 해당 GOLDILOCKS 서버에만 적용된다. 따라서 `\CSTARTUP NOMOUNT, MOUNT` 명령어 이후 [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references.md#f9fc4d123ed9181c) 을 이용하여 단계별로 구동하기 위해서는 다른 서버들도 LOCAL OPEN 상태까지 직접 구동해야 한다.

다음은 `\CSTARTUP MOUNT` 이후 단계별 구동을 시도하는 예이다. 해당 서버는 MOUNT 단계로 구동 되지만 다른 서버는 LOCAL OPEN 단계까지 구동되지 않아 에러가 발생한다.

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

서버 구동과 관련한 자세한 내용은 아래의 링크를 참조한다.

- 서버 구동 단계: [다단계 시작](../part-02-administration-manual/5-goldilocks-데이터베이스-관리-기본.md#324d293a99dd4a23)
- 최초 서버 구동 명령: [`\cstartup`](#4d333be4c98ad8f3)
- 서버 단계 변경: [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references.md#f9fc4d123ed9181c)

전체 서버를 종료하려면 다음 예와 같이 `\cshutdown` 명령을 사용한다. 전체 서버 종료에 대한 자세한 내용은 [`\cshutdown`](#5137f3c14b98733e) 명령을 참조한다.

```
gSQL> \cshutdown

Shutdown success

gSQL>
```

<a id="a45f4e301c969527"></a>
### SQL 구문 수행

다음은 참조 명령어이다.

**참조 명령어**

<a id="8db3f5c20b7d6544"></a>
| gsql 명령 | 설명 |
| --- | --- |
| [`\import`](#43c841d979d82282) | SQL 파일을 실행한다. |
| [`\set autocommit`](#c5342131808a2378) | SQL 구문을 실행할 때마다 자동으로 COMMIT 한다. |
| [SQL References](../part-03-sql-manual/18-sql-references.md#f41b6aa6080197e3) | SQL 구문의 종류이다. |

<a id="e686599623d06524"></a>
#### SQL 구문 입력

대화형 모드에서 gsql은 대화형 모드 프롬프트인 gSQL>을 출력하고 사용자의 입력을 기다린다. 사용자가 SQL 구문 입력을 완료하면 gsql은 SQL 구문을 서버로 전달하여 수행한다. 대화형 모드에서 SQL 구문을 종료하려면 semi-colon (;) 다음에 <kbd>enter</kbd>를 입력한다. SQL 구문을 처리한 후에는 수행 결과를 출력하고 프롬프트 gSQL>이 다시 출력된 후 사용자의 입력을 기다린다.

다음은 한 개 라인에 SQL 구문을 입력하고 실행하는 예이다.

```
gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.

gSQL>
```

다음은 여러 라인에 걸쳐 SQL 구문을 입력하고 수행하는 예이다. SQL 구문이 완료되지 않은 상태에서 <kbd>enter</kbd>를 입력할 경우 다음 라인으로 이동하여 라인번호를 출력하고 사용자의 입력을 기다린다.

```
gSQL> SELECT id, name
2
```

계속해서 다음과 같이 SQL 구문을 모두 입력하고 semi-colon (;)과 <kbd>enter</kbd>를 입력할 경우, SQL 구문을 실행하고 *gSQL>* 프롬프트가 다음 명령을 기다린다.

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

다음과 같이 single-quote (') 안에 포함된 semi-colon (;)은 문자열로 인식되어 SQL 구문 입력이 완료된 것으로 인식하지 않는다.

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

<a id="b1dde197a788b304"></a>
#### 파일로부터 SQL 구문 입력

대화형 모드에서 SQL 구문을 직접 입력하지 않고 파일로부터 수행할 경우, `\import` 명령을 사용한다. 다음은 sample.sql 파일을 읽어 다수의 SQL 구문들을 수행하는 예이다. 자세한 내용은 [`\import`](#43c841d979d82282) 명령을 참조한다.

```
gSQL> \import 'sample.sql'
```

• Drop table

```
DROP TABLE IF EXISTS t1;

Table dropped.
```

• Create table

```
CREATE TABLE t1 
(
    id   INTEGER PRIMARY KEY,
    name VARCHAR(128),
    addr VARCHAR(128)
);

Table created.
```

• Create index

```
CREATE INDEX t1_idx_name ON t1(name);

Index created.
```

• Insert three rows

```
INSERT INTO t1 
       VALUES ( 1, 'leekmo', 'Seoul, Korea'  ),
              ( 2, 'mkkim' , 'Seoul, Korea'  ),
              ( 3, 'xcom73', 'Inchon, Korea' );

3 rows created.
```

• Commit transaction

```
COMMIT;

Commit complete.

gSQL>
```

<a id="9822bb9994aa77dd"></a>
#### gsql 주석

대화형 모드에서 사용되는 주석은 SQL 구문의 주석과 동일하다. [--import](#1e9ff833ceb05528) 옵션을 통해 파일로부터 입력되는 주석도 SQL 구문의 주석과 동일하다. SQL 구문의 주석에 대한 자세한 내용은 [Comments](../part-03-sql-manual/11-sql-elements.md#2f026740093827c1)를 참조한다.

다음은 대화형 모드에서 line comment를 사용하는 예이다.

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

다음은 `\import` 명령을 이용해 파일의 내용을 수행하는 예이다. 대화형 모드에서의 주석과 동일하게 처리되며 파일의 내용이 모두 실행된 후에 *gSQL>* 프롬프트가 다음 SQL 구문을 기다린다.

```
gSQL> \import 'sample.sql'
```

• Drop table

```
DROP TABLE IF EXISTS t1;

Table dropped.
```

• Create table

```
CREATE TABLE t1 
(
    id   INTEGER PRIMARY KEY,
    name VARCHAR(128),
    addr VARCHAR(128)
);

Table created.
```

• Create index

```
CREATE INDEX t1_idx_name ON t1(name);

Index created.
```

• Insert three rows

```
INSERT INTO t1 
       VALUES ( 1, 'leekmo', 'Seoul, Korea'  ),
              ( 2, 'mkkim' , 'Seoul, Korea'  ),
              ( 3, 'xcom73', 'Inchon, Korea' );

3 rows created.
```

• Commit transaction

```
COMMIT;

Commit complete.

gSQL>
```

다음은 대화형 모드에서 multi-line comment를 사용하는 예이다.

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

gsql 대화형 모드에서 사용할 수 있는 주석은 SQL 구문의 주석과 동일하며 주석에 대한 자세한 내용은 SQL 구문의 [Comments](../part-03-sql-manual/11-sql-elements.md#2f026740093827c1)를 참조한다.

<a id="97dcdc08b2986def"></a>
#### SQL 수행 결과

대화형 모드에서 SELECT 구문 등의 질의를 수행하면 gsql은 질의 결과를 출력한다. 출력 결과는 column 이름으로 구성된 상단부, 질의 결과에 해당하는 데이터들, 질의 결과의 요약인 하단부로 구성된다.

다음은 SELECT 구문을 수행하는 예이다.

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

위의 예에서 출력 결과의 상단부는 column 이름과 함께 데이터와 구분하기 위한 hyphen (-)으로 구성된다. 출력 결과의 중앙에는 질의 결과가 출력되며 하나의 row는 한 line을 기준으로 출력되며 각 데이터 값은 공백으로 구분된다. 출력 결과의 하단부는 질의 결과의 요약으로써 세 개의 row가 검색되었음을 출력한다.

SQL 질의 이외의 [Data Definition Language](../part-03-sql-manual/12-sql-languages.md#dcad2080e7c66bcc), [Data Manipulation Language](../part-03-sql-manual/12-sql-languages.md#a4e4077c2c349ac2), [Control Language](../part-03-sql-manual/12-sql-languages.md#3365410f5d2cd7ef) 등의 구문은 각 SQL 구문의 특성에 맞는 수행 결과를 요약한 정보를 출력한다.

다음은 DDL, DML, control language를 각각 수행하고 그 결과를 출력하는 예이다.

• DDL 구문

```
gSQL> CREATE TABLE t1 ( id INTEGER, name VARCHAR(128) );

Table created.
```

• DML 구문

```
gSQL> INSERT INTO t1 VALUES ( 1, 'leekmo' );

1 row created.
```

• Transaction control 구문

```
gSQL> COMMIT;

Commit complete.

gSQL>
```

<a id="1743b2de0b175eeb"></a>
#### SQL 수행 에러

SQL 구문을 수행할 때 발생하는 에러는 다음과 같은 정보로 구성된다.

- SQLSTATE 정보: SQL 표준의 SQLSTATE 값
- Error code: GOLDILOCKS 고유의 error code 값
- Error message: 에러 발생 원인을 기술하는 에러 메시지

다음은 SELECT 구문을 수행할 때 에러가 발생하는 예이다. ERR-42000 값이 SQLSTATE에 해당하며, (16040) 값이 GOLDILOCKS 고유의 error code 이고 두 번째 라인에서 invalid_table에 해당하는 테이블이나 view가 존재하지 않는다는 에러 메시지로 구성되어 있다.

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

<a id="3cd59b448f18ac54"></a>
#### 대화형 명령어의 수행 결과

SQL 구문과 함께 사용하는 대화형 명령어들은 SQL 구문을 수행한 것과 동일한 결과와 에러를 출력한다.

다음은 [`\prepare sql`](#0a689bc4cd07f2fe) 명령을 이용해 SQL 구문을 준비하고 [`\exec`](#0f3949721f6b5ec3) 명령을 이용해 준비된 SQL 구문을 수행하는 예이다.

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

다음은 [`\prepare sql`](#0a689bc4cd07f2fe) 명령을 사용할 때 SQL 구문에 에러가 존재하는 경우로써 SQL 구문을 수행한 것과 동일한 에러를 출력한다.

• `\prepare sql` 명령의 에러

```
gSQL> \prepare sql SELECT * FROM invalid_table;

ERR-42000(16040): table or view does not exist : 
SELECT * FROM invalid_table
              *
ERROR at line 1:
```

• 동일한 SQL 구문의 에러

```
gSQL> SELECT * FROM invalid_table;

ERR-42000(16040): table or view does not exist : 
SELECT * FROM invalid_table
              *
ERROR at line 1:

gSQL>
```

대화형 모드의 gsql 명령어들 중에 SQL 구문을 포함하지 않거나 출력할 내용이 없는 명령어의 경우, 해당 명령이 성공할 때 별도의 메시지 없이 *gSQL>* 프롬프트만 출력한다.

다음은 별도의 성공 메시지 없이 대화형 명령어를 수행하는 예이다. 에러가 발생할 경우 에러 메시지를 출력한다.

- 대화형 gsql 명령어가 정상적으로 수행되는 경우

```
gSQL> \var v1 INTEGER
gSQL> \exec :v1 := 1
```

- 대화형 gsql 명령어가 에러를 발생시키는 경우

```
gSQL> \var v2 INVALID TYPE

ERR-42000(40000): syntax error 
\var v2 INVALID TYPE
........^     ^
Error at line 1

gSQL>
```

대화형 명령어의 수행 결과는 [Interactive Command References](#25c23aa77d38bf77)의 각 명령어 설명과 사용 예를 참조한다.

<a id="95e72475132262e0"></a>
#### SQL 구문의 자동 COMMIT

gsql의 대화형 모드에서 수행하는 SQL 구문은 [COMMIT](../part-03-sql-manual/18-sql-references.md#4d322680eba93c4a) 또는 [ROLLBACK](../part-03-sql-manual/18-sql-references.md#eaa6143895b543a3) 구문을 통해 트랜잭션을 완료하거나 철회할 수 있다.

다음은 다수의 INSERT 구문을 수행하고 COMMIT 또는 ROLLBACK을 수행하는 예이다. 다음 예에서 첫 번째 INSERT 구문은 COMMIT에 의해 정상적으로 완료된 반면에 두 번째와 세 번째 INSERT 구문은 ROLLBACK에 의해 수행이 철회되었다.

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

SQL 구문을 수행할 때마다 자동으로 트랜잭션을 COMMIT 하려면 다음과 같이 [`\set autocommit`](#c5342131808a2378) 명령을 이용하여 제어할 수 있다. 위의 예와 동일한 SQL 구문을 수행한 경우, 각 SQL 구문이 자동으로 COMMIT 되어 두 번째, 세 번째 INSERT 구문의 수행 결과도 ROLLBACK과 관계없이 완료되었음을 알 수 있다.

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

자동 COMMIT 제어에 대한 자세한 내용은 [`\set autocommit`](#c5342131808a2378) 명령어를 참조한다.

<a id="79fbf65249506ab2"></a>
#### 수행 중인 SQL 구문의 강제종료

대화형 모드에서 실행 중인 SQL 구문을 강제로 종료하려면 <kbd>Ctrl</kbd>+<kbd>C</kbd>를 입력한다.

다음은 오래 수행되는 SELECT 구문을 강제 종료하는 예이다. SQL 구문을 수행하는 중에 키보드를 이용해 <kbd>Ctrl</kbd>+<kbd>C</kbd>를 입력할 경우 *operation canceled* 에러 메시지를 출력하고 수행 중이던 SQL 구문이 강제 종료된다.

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

<a id="017542ed4963efdc"></a>
### 출력 결과 제어

다음은 참조 명령어이다.

**참조 명령어**

<a id="141815b1e1c05ca2"></a>
| gsql 명령 | 설명 |
| --- | --- |
| [`\set color`](#28ac515c7426a0ea) | 각 row를 다른 색깔로 구별한다. |
| [`\set colsize`](#b8a3227147bc77e2) | Column 결과의 최대 크기를 제어한다. |
| [`\set error`](#c8ff78168c631446) | 에러 메시지 출력 여부를 제어한다. |
| [`\set linesize`](#8654bfd6f1680424) | Row의 최대 출력 길이를 제어한다. |
| [`\set numsize`](#fb05859baf125d50) | 숫자값의 최대 digit 개수를 제어한다. |
| [`\set pagesize`](#72d51f9c7e68284b) | Page에 포함할 row의 개수를 제어한다. |
| [`\set timing`](#ef371f8fc5832f3c) | SQL 구문 수행 시간을 출력한다. |
| [`\set vertical`](#e88795a4ee13cd81) | 각 column을 한 line에 출력한다. |

<a id="029efbe5382fed30"></a>
#### Page 구성 제어

앞서 [SQL 수행 결과](#97dcdc08b2986def)에 기술한대로 질의 결과의 상단부에는 column 이름을 출력하고 데이터를 출력한 후, 하단부에 요약 결과를 출력한다.

질의 결과가 많을 경우 pagesize (기본값 20) 단위로 나누어 각 page마다 column 이름과 데이터를 출력하고 모든 page의 출력이 완료된 후 하단부에 요약 결과를 출력한다.

다음은 pagesize를 5로 변경하여 질의 결과를 출력한 예이다. Pagesize 제어에 대한 자세한 내용은 [`\set pagesize`](#72d51f9c7e68284b)명령을 참조한다.

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

질의 결과의 각 row는 linesize (기본값 80) 단위로 출력되는데 한 row의 길이가 linesize를 넘어갈 경우 다음 line에 결과를 출력한다.

다음은 linesize를 200으로 조정하기 전과 후의 질의 결과이다. Linesize 제어에 대한 자세한 내용은 [`\set linesize`](#8654bfd6f1680424) 명령을 참조한다.

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

- Linesize를 200으로 설정한다.

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

터미널 상에서 각 row를 구별하여 가독성을 높이고 싶은 경우 [`\set color`](#28ac515c7426a0ea) 명령을 통해 다음과 같이 row 마다 색깔을 달리하여 출력할 수 있다. 자세한 내용은 [`\set color`](#28ac515c7426a0ea) 명령을 참조한다.

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

질의 결과를 출력할 때 row를 line 단위가 아닌 column 단위로 하나의 line에 출력하려면 `\set vertical on` 명령을 사용한다. 다음 예와 같이 column 단위로 출력 결과가 생성되는데 자세한 내용은 [`\set vertical`](#e88795a4ee13cd81) 명령을 참조한다.

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

<a id="3a41501bdbb2801a"></a>
#### 데이터 값의 출력 제어

gsql은 질의 결과에 포함되는 모든 데이터를 문자열로 변환하여 출력한다.

숫자형은 numsize (기본값 20)를 digit 단위로 출력하며 numsize 보다 큰 숫자값은 exponent 형태로 표현한다. 다음은 numsize를 이용해 출력값을 제어하는 예이며 자세한 내용은 [`\set numsize`](#fb05859baf125d50) 명령을 참조한다.

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

숫자값 출력에 대한 다양한 제어가 필요한 경우, 다음과 같이 [TO_CHAR( number )](../part-03-sql-manual/17-built-in-function-references.md#3b3cd1288d7889b5) 함수를 이용해 출력을 제어할 수 있다.

```
gSQL> SELECT num, TO_CHAR( num * num, '$999,999,999,999,999,999,999,999,999' ) AS result FROM t1;

          NUM RESULT                               
------------- -------------------------------------
1234567890123    $1,524,157,875,322,755,800,955,129

1 row selected.

gSQL>
```

DATE/ TIME/ TIMESTAMP와 같은 날짜/ 시간 타입의 경우, gsql은 다음과 같은 프로퍼티 정보를 이용해 출력 형태를 결정한다.

- [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#ec78df636da07fb6)
- [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#15c05b1b42192d13)
- [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#7dad2bb0bce4c28d)
- [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#1793ce4c56053b95)
- [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#0a90eef2149e893a)

해당 프로퍼티는 TO_CHAR(), TO_DATE() 등의 함수에서 format 정보를 입력하지 않았을 때 사용되는 프로퍼티이다. ODBC나 JDBC를 이용한 응용 프로그램이 SQL 구문에서 TO_CHAR(), TO_DATE() 등의 함수를 사용할 때만 위의 프로퍼티를 사용하는 반면에, gsql은 날짜/ 시간 데이터 값을 출력하기 위해 최초로 접속할 때 해당 프로퍼티 정보를 획득하여 이를 이용한다. 대화형 모드에서 다음과 같은 SQL 구문으로 프로퍼티를 변경할 경우, gsql은 갱신된 프로퍼티 정보를 사용한다.

- [ALTER SESSION SET property_name](../part-03-sql-manual/18-sql-references.md#4b18743f121b279d)
- [ALTER SYSTEM SET property_name](../part-03-sql-manual/18-sql-references.md#daca16c30923690a)

다음은 DATE column에 대한 출력을 제어하는 예이다.

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

프로퍼티를 변경하지 않고 날짜/ 시간 출력값을 제어하려면 다음과 같이 [TO_CHAR( datetime )](../part-03-sql-manual/17-built-in-function-references.md#6a95099dcd5efb32) 함수를 사용한다.

```
gSQL> SELECT TO_CHAR( enter_date, 'YYYY"년" MM"월" DD"일"' ) as result FROM t1;

RESULT          
----------------
2014년 08월 26일

1 row selected.

gSQL>
```

BINARY나 VARBINARY와 같은 이진 문자열의 경우, 다음과 같이 hex 값으로 결과를 출력한다.

```
gSQL> select * from t1;

BINARY_VALUE        
--------------------
A010002F370000000000

1 row selected.

gSQL>
```

LONG VARCHAR, LONG VARBINARY 타입의 데이터는 아주 긴 문자열을 포함할 수 있어 colsize (기본값 8192) 만큼만 데이터를 출력한다. 다음은 colsize를 줄여 LONG VARCHAR 타입인 TEXT column의 일부 데이터를 출력한 예인데 colsize 값을 늘려 데이터를 모두 출력할 수 있다. 자세한 내용은 [`\set colsize`](#b8a3227147bc77e2)  명령을 참조한다.

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

<a id="b1d8185c36a1758d"></a>
#### SQL 구문 수행시간

SQL 구문을 수행할 때 수행 시간을 출력하려면 다음과 같이 `\set timing on` 명령을 사용한다. 자세한 내용은 [`\set timing`](#ef371f8fc5832f3c) 명령을 참조한다.

```
gSQL> \set timing on
gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.

Elapsed time: 0.08500 ms
```

<a id="7538b19e21a9f40b"></a>
### 출력 결과 저장

Terminal 출력과 동시에 gsql에서 수행되는 모든 결과를 file에 기록한다.

**참조 명령어**

<a id="3aa155d3bbc29483"></a>
| gsql 명령 | 설명 |
| --- | --- |
| `\spool` | 출력 결과를 file에 저장한다. |

출력 결과 저장과 관련된 기능들은 [`\spool`](#ab855d85ea887c89)의 명령어들을 참조한다.

출력 결과는 다음과 같이 저장할 수 있다.

- result.txt 파일에 실행 결과를 저장하기 시작

```
gSQL> \SPOOL 'result.txt'
```

- Spool 상태 확인

```
gSQL> \SPOOL
 
currently spooling to result.txt

gSQL> SELECT * FROM T1 WHERE C1 < 10;
```

- Spool 기능 종료

```
gSQL> \SPOOL OFF
```

<a id="46ae013f47c1c8a7"></a>
### SQL 객체 정보 조회

SQL 객체에 대한 정보는 [DICTIONARY_SCHEMA](../part-02-administration-manual/9-database-information.md#26ad9a84eb1934b9), [INFORMATION_SCHEMA](../part-02-administration-manual/9-database-information.md#76e69304f31f4796)의 각종 view들로 조회할 수 있다.

**참조 명령어**

<a id="5ab939259aa2bec6"></a>
| gsql 명령 | 설명 |
| --- | --- |
| [`\desc`](#b4d1178aec2889c2) | 테이블 정보를 조회한다. |
| [`\idesc`](#3cc6adb4e775dc1c) | 인덱스 정보를 조회한다. |

예를 들어 다음과 같이 생성된 테이블과 인덱스가 있을 경우,

```
CREATE TABLE t1 
(
    id   INTEGER PRIMARY KEY,
    name VARCHAR(128),
    addr VARCHAR(128)
);

CREATE INDEX t1_idx_name ON t1(name);
```

사용자는 다음과 같이 일련의 SQL 구문들을 수행하여 테이블과 관련된 정보를 조회할 수 있다.

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
NAME        VARCHAR           Y       
ADDR        VARCHAR           Y       

3 rows selected.

gSQL> SELECT index_name FROM user_indexes WHERE table_schema = 'PUBLIC' AND table_name = 'T1';

INDEX_NAME          
--------------------
T1_PRIMARY_KEY_INDEX
T1_IDX_NAME         

2 rows selected.

gSQL>
```

gsql 은 다음과 같이 `\desc` 명령어를 이용해 테이블과 관련된 정보를 쉽게 조회할 수 있다. 출력 결과 및 자세한 내용은 [`\desc`](#b4d1178aec2889c2) 명령을 참조한다.

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

명령어 `\idesc`는 다음 예와 같이 인덱스와 관련된 정보를 보여준다. 자세한 내용은 [`\idesc`](#3cc6adb4e775dc1c)명령을 참조한다.

```
gSQL> \idesc t1_idx_name

COLUMN_NAME ORDINAL_POSITION IS_ASCENDING_ORDER IS_NULLS_FIRST
----------- ---------------- ------------------ --------------
NAME                       1 TRUE               FALSE         

gSQL>
```

<a id="a74d40c0fa3c906c"></a>
### SQL 객체의 DDL 구문 출력

다음과 같은 gsql 명령어들은 SQL 객체의 현재 상태에 해당하는 DDL 구문을 출력한다. SQL 객체를 생성하는 CREATE 구문 뿐만 아니라 다양한 옵션을 통해 관련 객체의 DDL 구문을 출력할 수 있다.

> 휴지통에 보관된 객체들은 출력되지 않는다.

**참조 명령어**

<a id="1f6eb4f087ce116a"></a>
| gsql 명령 | 설명 |
| --- | --- |
| [`\ddl_cluster`](#a3198ba56660ca0b) | 클러스터와 관련된 DDL을 출력한다. |
| [`\ddl_db`](#f814ed0276f7c927) | 데이터베이스와 관련된 DDL을 출력한다. |
| [`\ddl_tablespace`](#a1f5b03d15830a32) | 테이블스페이스와 관련된 DDL을 출력한다. |
| [`\ddl_profile`](#720e0ea1294f39c9) | Profile과 관련된 DDL을 출력한다. |
| [`\ddl_audit_policy`](#9ed3153ad8b48405) | Audit policy와 관련된 DDL을 출력한다. |
| [`\ddl_auth`](#95b90195ea61225e) | 계정과 관련된 DDL을 출력한다. |
| [`\ddl_schema`](#22b7662f8bed9731) | 스키마와 관련된 DDL을 출력한다. |
| [`\ddl_public_synonym`](#154bcff6b21654f2) | Public synonym과 관련된 DDL을 출력한다. |
| [`\ddl_table`](#dce7524a3b40f576) | 테이블과 관련된 DDL을 출력한다. |
| [`\ddl_constraint`](#6b2d013b24cb2a83) | 제약 조건과 관련된 DDL을 출력한다. |
| [`\ddl_index`](#db8a3ad0620424ee) | 인덱스와 관련된 DDL을 출력한다. |
| [`\ddl_view`](#c1e543751777c6fa) | View와 관련된 DDL을 출력한다. |
| [`\ddl_sequence`](#154929446753c11d) | 시퀀스와 관련된 DDL을 출력한다. |
| [`\ddl_synonym`](#975cd121d4ade13c) | Synonym과 관련된 DDL을 출력한다. |
| [`\ddl_procedure`](#bfdd1dc3f6b95efc) | Procedure와 관련된 DDL을 출력한다. |
| [`\ddl_package`](#b3e38d648d9ce661) | Package과 관련된 DDL을 출력한다. |
| [`\set ddlsize`](#84305527a9268b5f) | DDL 출력 버퍼의 크기를 제어한다. |

다음은 orders 테이블을 생성하는 예이다.

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

위에서 orders 테이블을 생성한 CREATE TABLE 구문은 다음과 같이 `\ddl_table` 명령을 통해 출력한다.

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
        MAXSIZE 562949953159168 
    ) 
    TABLESPACE "MEM_DATA_TBS" 
;
```

위의 결과에서 SET AUTHORIZATION 구문은 CREATE TABLE 구문을 수행한 소유자를 의미한다. 출력한 CREATE TABLE 구문에는 사용자가 입력하지 않은 정보, 즉 테이블이 속한 스키마 이름, 테이블이 저장된 테이블스페이스 이름 및 테이블의 물리적 정보도 함께 출력된다.

테이블에 생성된 제약 조건에 해당하는 DDL은 다음과 같이 `\ddl_table`의 CONSTRAINT 옵션을 사용해 출력한다.

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
        MAXSIZE 562949953159168 
    ) 
    TABLESPACE "MEM_TEMP_TBS" 
    NOT DEFERRABLE
    INITIALLY IMMEDIATE
;
```

자세한 내용은 각 SQL 객체에 대응하는 gsql 명령어를 참조한다.

> `\ddl_table` 등의 명령어를 사용하는 동시에 관련 SQL 객체에 DDL을 수행하면 서로 다른 결과를 출력할 수도 있으므로 동시에 DDL을 수행하지 않도록 한다.

<a id="28949315f1b31fc3"></a>
### History 제어

gsql은 대화형 모드에서 수행된 SQL 구문에 대한 이력을 관리한다.

**참조 명령어**

<a id="2ae170b3945281f3"></a>
| gsql 명령 | 설명 |
| --- | --- |
| [`\\`](#4c1575265582051a) | 이전 SQL을 수행한다. |
| [`\{n}`](#c2ebdddcf744e75d) | SQL 이력 번호에 해당하는 구문을 실행한다. |
| [`\history`](#ad141bbb20a37ce0) | SQL 수행 이력을 조회한다. |
| [`\set history`](#6b3b3355aea3daf4) | History 버퍼 개수를 제어한다. |

다음은 이미 실행했던 SQL 구문을 다시 실행하는 예이다.

- 가장 최근에 성공적으로 실행한 SQL 구문을 실행한다.

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

- 이력에 존재하는 1번 SQL을 실행한다.

```
gSQL> \1   

Table dropped.
```

gsql의 history 관련 기능들은 [참조 명령어 ](#2ae170b3945281f3)의 명령어들을 참조한다.

<a id="10278add001b8074"></a>
### SQL 편집

Text editor를 사용하여 SQL 구문을 편집한다. 이 때 사용할 text editor는 환경 변수 EDITOR에 지정할 수 있으며 환경 변수 EDITOR가 존재하지 않을 경우에는 기본적으로 vi를 사용한다.

**참조 명령어**

<a id="417090a3f5ad3100"></a>
| gsql 명령 | 설명 |
| --- | --- |
| `\edit` | Text editor를 사용하여 SQL 구문을 편집한다. |

편집 기능을 사용하면 gsql은 편집기를 실행하여 제어권을 넘긴다. 사용자는 편집기에서 SQL 구문 내용을 자유롭게 편집할 수 있으며 편집기를 종료하면 gsql에서 제어권을 돌려 받은 후 해당 내용을 마지막 이력으로 추가한다.

이렇게 편집기를 통해서 편집된 SQL 구문은 가장 마지막 이력 실행 명령인 `\\`를 통해서 실행할 수 있다.

> SQL 편집 기능은 단일 SQL 문장만 편집할 수 있다. 다중 SQL 구문을 실행할 경우, 오류가 발생한다.

`\edit` 명령을 사용하여 편집할 수 있는 내용은 다음과 같다.

- 가장 최근에 수행한 SQL 구문
- File에 저장된 SQL 구문
- gsql의 이력에 저장된 SQL 구문

gsql 편집 관련 기능에 대한 자세한 내용은 [`\edit`](#a18be4b967d5bb7f)의 명령어들을 참조한다.

다음은 SQL 구문을 편집하는 예이다.

- 가장 최근에 실행한 SQL 구문을 편집한다.

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

- 편집된 SQL 구문을 실행한다.

```
gSQL> \\
C1
--
 1
1 row selected.
```

<a id="c4157a40c0c198de"></a>
### 연결 제어

다음은 참조 명령어이다.

**참조 명령어**

<a id="df084ef8d73778cf"></a>
| gsql 명령 | 설명 |
| --- | --- |
| [`\connect`](#e3e9cd0a2e7b2922) | 새로운 사용자로 접속한다. |
| [`\quit`](#9e3cc316e0e9f7fb) | 접속을 종료한다. |

대화형 모드에서 `\connect` 명령을 이용해 다음과 같이 새로운 사용자로 접속할 수 있다. `\connect ` 명령은 기존의 session을 종료하고 새로운 session을 생성한다. 자세한 내용은 [`\connect`](#e3e9cd0a2e7b2922) 명령을 참조한다.

```
gSQL> \connect test test
gSQL>
```

다음과 같이 [SET SESSION AUTHORIZATION user_identifier](../part-03-sql-manual/18-sql-references.md#f764bc65dcc3237c) 구문을 이용해 사용자를 변경할 수 있다. `\connect` 명령이 수행 중인 트랜잭션을 모두 COMMIT 하고 새로운 session을 생성하는 반면에 SET SESSION AUTHORIZATION 구문은 기존의 session을 그대로 유지한 채 사용자를 변경한다.

```
gSQL> SET SESSION AUTHORIZATION test;

Session set.

gSQL>
```

대화형 모드를 종료하려면 다음과 같이 `\quit` 명령을 사용한다. 자세한 내용은 [`\quit`](#9e3cc316e0e9f7fb) 명령을 참조한다.

```
gSQL> \quit
%
```

<a id="335b41df53dea500"></a>
### 호스트 변수 사용

gsql은 대화형 모드에서 호스트 변수를 선언하고 호스트 변수에 값을 대입하며 SQL 구문에 호스트 변수를 함께 사용할 수 있다.

**참조 명령어**

<a id="83213372c93231e7"></a>
| gsql 명령 | 설명 |
| --- | --- |
|  [`\var`](#5bdd58614174a2b3) | 호스트 변수를 선언한다. |
|  [`\exec :var := value`](#374539d536d0872d) | 호스트 변수에 값을 할당한다. |
|  [`\print`](#828c84fc4aea1dd3) | 호스트 변수의 값을 출력한다. |
|  [`\dynamic sql :var`](#45a31fc296ced749) | 호스트 변수에 저장된 SQL 문장을 수행한다. |

다음은 [`\var`](#5bdd58614174a2b3) 명령을 이용하여 호스트 변수를 선언하고 [`\exec :var := value`](#374539d536d0872d) 명령을 이용해 호스트 변수에 값을 대입하고 [`\print`](#828c84fc4aea1dd3) 명령을 이용해 호스트 변수의 값을 조회하는 예이다. 자세한 내용은 각 명령을 참조한다.

```
gSQL> \var v_id INTEGER
gSQL> \exec :v_id := 1
gSQL> \print v_id

V_ID
----
   1

gSQL>
```

대화형 모드에서 선언한 변수는 다음과 같이 SQL 구문 내에서 입력 인자로 사용할 수 있다.

```
gSQL> SELECT * FROM t1 WHERE id = :v_id;

ID NAME   ADDR        
-- ------ ------------
 1 leekmo Seoul, Korea

1 row selected.

gSQL>
```

대화형 모드에서 선언한 변수는 다음과 같이 SQL 구문 내에서 출력 인자로 사용할 수 있다.

```
gSQL> SELECT id INTO :v_id FROM t1 WHERE name = 'mkkim';

V_ID
----
   2

1 row selected.

gSQL>
```

<a id="28e4114f86fceec9"></a>
### SQL 구문 처리 방식 제어

응용 프로그램을 작성하기 전에 gsql 대화형 모드의 명령어를 이용하여 SQL을 처리할 경우, 응용 프로그램에서 자주 사용하는 prepare/ execute 수행, cursor를 이용한 검색 등의 SQL 구문 처리 방식을 simulation 할 수 있다.

**참조 명령어**

<a id="835b850f30c7b3cb"></a>
| gsql 명령 | 설명 |
| --- | --- |
| [`\exec sql`](#937854e40d50d4a1) | SQL 문장을 바로 실행한다. |
| [`\prepare sql`](#0a689bc4cd07f2fe) | SQL 문장을 준비한다. |
| [`\exec`](#0f3949721f6b5ec3) | 준비된 SQL 문장을 수행한다. |
| [`\dynamic sql :var`](#45a31fc296ced749) | 호스트 변수에 저장된 SQL 문장을 수행한다. |

다음 Java 응용 프로그램은 $GOLDILOCKS_HOME/sample/JDBC/JdbcSample.java의 일부 코드 내용이다.

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

다음과 같이 [`\prepare sql`](#0a689bc4cd07f2fe) 명령과 [`\exec`](#0f3949721f6b5ec3) 명령을 이용하여 위에서 Java 코드의 PreparedStatement class를 이용하여 구현한 것을 simulation 할 수 있다.

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

다음 embedded SQL 프로그램은 $GOLDILOCKS_HOME/sample/EmbeddedSQL/sample2.gc의 일부 코드 내용이다.

```
int main(int argc, char **argv)
{

    EXEC SQL BEGIN DECLARE SECTION;
    int          sEmpNo;
    varchar      sEName[20 + 1];
    char         sJob[20];
    long         sSalary;
    EXEC SQL END DECLARE SECTION;

    ... 중략 ...
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
    
    ... 중략 ...

}
```

위의 embedded SQL 프로그램의 커서를 이용한 질의 처리 과정은 다음과 같이 gsql의 대화형 모드에서 simulation 할 수 있다.

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

> 다른 DBMS에서는 다음과 같은 SQL 구문을 embedded SQL에서만 제한적으로 사용할 수 있는 반면에 GOLDILOCKS에서는 embedded SQL 뿐만 아니라 ODBC나 JDBC를 이용한 응용 프로그램을 작성할 때 SQL 처리 함수들의 인자로 사용할 수 있다.  
> 
> 
> - [SELECT .. INTO](../part-03-sql-manual/18-sql-references.md#a345298536f40392)
> - [DECLARE cursor_name](../part-03-sql-manual/18-sql-references.md#45b9d98474d5f09d)
> - [OPEN cursor_name](../part-03-sql-manual/18-sql-references.md#ee8cdd33c43f9c76)
> - [FETCH cursor_name](../part-03-sql-manual/18-sql-references.md#bafc38978b00122c)
> - [CLOSE cursor_name](../part-03-sql-manual/18-sql-references.md#38584f03f4e1823e)
> 

<a id="0a89a7547f22a6ec"></a>
### SQL 실행 계획 정보

다음은 참조 명령어이다.

**참조 명령어**

<a id="b27f5c488a93671c"></a>
| gsql 명령 | 설명 |
| --- | --- |
| [`\explain plan`](#6160cfd32df70014) | SQL 문장의 실행 계획을 출력한다. |
| [`\set autotrace`](#9114076e891ca168) | 실행 계획 출력 여부를 설정한다. |

대화형 모드에서 다음과 같이 `\explain plan` 명령이나 `\set autotrace` 명령을 이용하여 SQL 구문의 실행 계획을 조회할 수 있다. 명령에 대한 자세한 내용은 [`\explain plan`](#6160cfd32df70014), [`\set autotrace`](#9114076e891ca168)를 참조하고 실행 계획에 대한 해석은 [SQL 실행 계획](../part-03-sql-manual/15-sql-tuning.md#f6556ce75bce767e)을 참조한다.

다음은 `\explain plan` 명령을 이용하여 TPC-H 벤치마크의 4번 질의를 수행하는 예이다.

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

<a id="fc6b477741876799"></a>
## Command Option References

본 장에서는 쉘 프롬프트 상에서 gsql 명령을 수행할 때 사용하는 option에 대해 설명한다.

<a id="ffb66b3b6802a4dd"></a>
### Username Password

<a id="aaf9202bfe4ad3c5"></a>
#### 설명

사용자 이름과 password를 이용하여 GOLDILOCKS에 접속한다.

<a id="d7f207fb1bec2220"></a>
#### 사용 예

다음은 사용자 test로 접속하는 예이다.

```
% gsql test test

Connected to GOLDILOCKS Database.

gSQL>
```

다음은 사용자 정보나 password가 잘못되어 GOLDILOCKS 접속에 실패하는 예이다.

```
% gsql invalid_user invalid_password

ERR-28000(16004): invalid username/password; logon denied

%
```

<a id="404a2449eaedab75"></a>
### --as {SYSDBA|ADMIN}

<a id="56dc527ad8f97398"></a>
#### 설명

SYSDBA role이나 ADMIN role로 GOLDILOCKS에 접속한다.  
해당 role에 대한 자세한 내용은 [서버 구동 및 종료](#1b5d02a17418ebcf)를 참조한다.

```
% gsql sys gliese --as sysdba
```

<a id="f0fdf027ee116203"></a>
#### 사용 예

다음은 SYSDBA role로 접속하는 예이다.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL>
```

<a id="9f82c37b2b9ee3ed"></a>
### --conn-string

<a id="8dc4bc97eacb5c5c"></a>
#### 설명

Connection string을 통해 GOLDILOCKS에 접속한다.  
기술할 connection string의 내용은 ODBC 함수 [SQLDriverConnect](../part-05-developer-manual/29-odbc.md#b4ff09d176e96152)의 input string과 동일한 형태로 사용해야 한다. Connection string에 대한 자세한 내용은 [SQLDriverConnect](../part-05-developer-manual/29-odbc.md#b4ff09d176e96152) 함수를 참조한다.

<a id="e2064748e66b7e0b"></a>
#### 사용 예

다음은 --conn-string을 이용하여 접속하는 예이다.

```
% gsql --conn-string 'DSN=GOLDILOCKS;UID=test;PWD=test'

Connected to GOLDILOCKS Database.

gSQL>
```

<a id="084795786c7a0399"></a>
### --dsn

<a id="215ed4d5ea5d7a51"></a>
#### 설명

odbc.ini 파일에 정의된 Data Source Name (DSN)을 이용하여 접속한다.  
DSN 이름은 odbc.ini 파일에 정의된 이름이어야 한다. odbc.ini 파일에 대한 자세한 내용은 [UNIX에서 DSN 구성](../part-05-developer-manual/29-odbc.md#86bcad9e50f97988) 을 참조한다.  
DSN이 생략된 경우 기본값은 GOLDILOCKS이다.

<a id="2a54f9b93c63981c"></a>
#### 사용 예

다음은 DSN을 이용해 접속하는 예이다.

```
% gsql test test --dsn GOLDILOCKS

Connected to GOLDILOCKS Database.

gSQL>
```

위의 예에서 사용한 odbc.ini 파일의 내용은 다음과 같다.

```
[GOLDILOCKS]
DATE_FORMAT = SYYYY-MM-DD
TIME_FORMAT = HH24:MI:SS.FF6
```

> gsql은 odbc.ini 속성 중에 HOST, PORT를 인식하지 않는다.

<a id="e48922af261f2aee"></a>
### --enable-color

<a id="3dbef379c8d0d2d0"></a>
#### 설명

터미널 상에서 질의 결과의 각 row를 다른 색깔로 출력하여 쉽게 구분할 수 있도록 한다.  
대화형 모드로 질의를 수행할 경우 질의 결과를 row 마다 다른 색깔로 출력하며 이는 [--import](#1e9ff833ceb05528) 옵션을 이용해 파일에 포함된 SELECT 구문의 결과에도 적용된다.

<a id="1d77aaef25f49279"></a>
#### 사용 예

다음은 --enable-color 옵션을 이용하여 gsql을 수행하고 대화형 모드에서 질의 결과를 출력하는 예이다.

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

다음은 --import 옵션을 이용하여 파일 내에 포함된 SELECT 질의를 수행하는 예이다.

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

<a id="e379aebc5348012d"></a>
### --help

<a id="427d7edf196a1104"></a>
#### 설명

gsql 프로그램의 옵션 목록을 간략히 보여준다.

<a id="9ca3d176f6b2009c"></a>
#### 사용 예

다음은 --help 옵션을 사용하는 예이다.

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

<a id="1e9ff833ceb05528"></a>
### --import

<a id="482fb0c49959c248"></a>
#### 설명

대화형 모드가 아닌 파일 내의 SQL 구문을 배치로 수행한다.   
기술할 파일 이름은 single-quote (')로 묶어서 기술하며 절대 경로 또는 상대 경로를 사용할 수 있다.

<a id="4312e919d6a482ab"></a>
#### 사용 예

다음은 파일의 절대 경로를 이용하여 SQL 구문을 수행하는 예이다.

```
% gsql test test --import '/home/GOLDILOCKS/sample.sql'
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

다음은 파일의 상대 경로를 이용하여 SQL 구문을 수행하는 예이다.

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

<a id="02067012a2a7f497"></a>
### --no-prompt

<a id="4f955d1cfac9620a"></a>
#### 설명

대화형 모드를 수행할 때 프롬프트를 출력하지 않는다.

<a id="fb5ac357a5ac4eaa"></a>
#### 사용 예

다음은 --no-prompt를 사용하는 예이다.

```
% gsql test test --no-prompt
SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.
```

<a id="a9c37b1d4e880db4"></a>
### --prompt

<a id="6b166d6024612d54"></a>
#### 설명

대화형 모드를 수행할 때 gsql의 프롬프트를 설정한다.   
기본값은 gSQL이다.   
특수문자나 공백을 포함할 경우, 다음과 같이 double-qoute (")로 묶어서 기술한다.

```
% gsql test test --prompt "GOLDILOCKS Mercury.2.1"
```

<a id="4445a2b089f9c4bd"></a>
#### 사용 예

다음은 --prompt 옵션을 이용하여 대화형 모드의 프롬프트를 GOLDILOCKS로 변경하는 예이다.

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

<a id="ba57fa08b7eeadf7"></a>
### --silent

<a id="1e43ef6afca2b2aa"></a>
#### 설명

SQL 구문의 수행 결과를 출력하지 않는다.  
[--import](#1e9ff833ceb05528) 명령을 이용해 파일을 읽어 대량의 SQL 구문을 수행할 경우에 유용하다.  
--silent 옵션은 대화형 모드로 동작할 때도 적용된다.

<a id="115185dc994446c0"></a>
#### 사용 예

다음은 $GOLDILOCKS_HOME/admin 디렉토리에서 --silent 옵션을 이용하여 DictionarySchema.sql 파일을 수행하는 예이다.

```
% gsql sys gliese --as sysdba --import 'DictionarySchema.sql' --silent
%
```

<a id="778446d7c5a93808"></a>
### --version

<a id="7f9fc0002c864090"></a>
#### 설명

gsql 프로그램의 version 정보를 출력한다.  
GOLDILOCKS와 동일한 version의 gsql 프로그램을 사용할 것을 권장한다. GOLDILOCKS의 version은 다음과 같이 SQL 함수 [VERSION](../part-03-sql-manual/17-built-in-function-references.md#38cde8c6fcd22905)을 통해 확인할 수 있다.

```
gSQL> SELECT version() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="cefe66afb71d229c"></a>
#### 사용 예

다음은 --version 옵션을 사용하는 예이다.

```
% gsql --version

 Release Name.X.X.X revision(XXXXX)

%
```

<a id="25c23aa77d38bf77"></a>
## Interactive Command References

대화형 모드에서 사용하는 gsql 고유 명령어는 모두 backslash`(\)` 로 시작한다.

<a id="4c1575265582051a"></a>
### `\\`

<a id="fe3cd5ac146a2882"></a>
#### 구문

```
\\
```

<a id="9b6dd63394652baf"></a>
#### 설명

가장 최근에 성공한 SQL 구문을 실행한다.

<a id="537cc2c5059659bb"></a>
#### 사용 예

```
gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.
```

- 가장 최근에 성공한 SQL 구문을 실행한다.

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

- 실패한 SQL 구문이 아닌 가장 최근에 성공한 SQL 구문을 실행한다.

```
gSQL> \\

DUMMY
-----
X    

1 row selected.
```

<a id="e3e9cd0a2e7b2922"></a>
### `\connect`

<a id="417ef76cda81e5ac"></a>
#### 구문

```
\connect username password [as sysdba]
```

<a id="974f0256fe4a42f9"></a>
#### 설명

입력된 username과 password로 새로 접속한다.   
종료되지 않은 트랜잭션이 존재하는 경우 COMMIT을 수행한다.

<a id="1eba22ea13b3393d"></a>
#### 사용 예

다음은 test 계정으로 접속한 예이다.

```
gSQL> \connect test test
gSQL>
```

다음과 같이 password가 잘못된 경우, 에러가 발생한다.

```
gSQL> \connect test invalid_password

ERR-28000(16004): invalid username/password; logon denied

gSQL> SELECT * FROM dual;

ERR-08003(40044): connection does not exist
```

다음은 SYSDBA role로 접속하는 예이다.

```
gSQL> \connect sys gliese as sysdba
gSQL>
```

<a id="4d333be4c98ad8f3"></a>
### `\cstartup`

<a id="d45162c8e0332c56"></a>
#### 구문

```
\cstartup
\cstartup nomount
\cstartup mount
\cstartup open
\cstartup local open
\cstartup global open
```

<a id="6a89586d4914bae7"></a>
#### 설명

Cluster 환경에서 GOLDILOCKS 서버를 구동한다.

`\cstartup` 명령을 수행하려면 SYSDBA 또는 ADMIN role로 접속해야 한다. SYSDBA로 접속하는 방법은 [서버 구동 및 종료](#1b5d02a17418ebcf)를 참조한다.

- `\cstartup nomount`
    - 해당 서버를 NOMOUNT 단계로 시작한다.
- `\cstartup mount`
    - 해당 서버를 MOUNT 단계로 시작한다.
- `\cstartup local open`
    - 해당 서버 및 다른 서버를 LOCAL OPEN 단계로 시작한다.
- `\cstartup global open`
    - 모든 서버를 GLOBAL OPEN 단계로 시작한다.
- `\cstartup open`
    - `\cstartup global open`과 동일하다.
- `\cstartup`
    - `\cstartup global open`과 동일하다.

`\cstartup local open` 명령어와 `\cstartup global open` 명령어는 해당 서버와 다른 서버들도 해당 단계까지 구동 시킨다. 이 외의 명령어는 해당 서버에만 적용되므로 [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references.md#f9fc4d123ed9181c)를 이용하여 단계별로 구동하려면 직접 서버를 LOCAL OPEN 단계까지 구동해야 한다.

서버의 구동 단계는 NOMOUNT, MOUNT, LOCAL OPEN, GLOBAL OPEN 단계로 구분되며 자세한 내용은 [다단계 시작](../part-02-administration-manual/5-goldilocks-데이터베이스-관리-기본.md#324d293a99dd4a23)을 참조한다.

`\cstartup` 명령을 수행한 후에 다음 단계로 넘어가기 위해서는 [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references.md#f9fc4d123ed9181c) 구문을 수행해야 한다.

glocator를 이용한 `\cstartup`은 [CSTARTUP과 CSHUTDOWN](44-glocator.md#13ef0422121ec448)을 통해 확인할 수 있다.


> 
> - CS 환경에서만 사용하는 명령어로써 gsqlnet에서만 사용할 수 있다.
> - `\cstartup nomount/mount` 이외의 명령은 해당 서버와 함께 다른 서버에까지 영향을 미치는 명령어이다. 따라서 [odbc.ini 파일](../part-05-developer-manual/29-odbc.md#f1a0bc8659eada10)에 LOCATOR_DSN 속성이 기술되지 않았을 경우, 에러가 반환된다.
> 

<a id="455d252e85b1eea0"></a>
#### 사용 예

다음은 GOLDILOCKS를 구동하는 예이다.

```
% gsqlnet sys gliese --as sysdba

Connected to an idle instance.

gSQL> \cstartup

Startup success
```

<a id="5137f3c14b98733e"></a>
### `\cshutdown`

<a id="df9b00e347405abd"></a>
#### 구문

```
\cshutdown
\cshutdown abort
\cshutdown normal
```

<a id="43ccf234b2957c3e"></a>
#### 설명

Cluster 환경에서 GOLDILOCKS 서버를 종료한다.

`\cshutdown` 명령을 수행하려면 SYSDBA 또는 ADMIN role로 접속해야 한다. SYSDBA로 접속하는 방법은 [서버 구동 및 종료](#1b5d02a17418ebcf)를 참조한다.

- `\cshutdown normal`
    - 새로운 session의 접속을 차단하고 현재 접속된 모든 session의 종료를 기다린 후, checkpoint를 수행하고 서버를 종료한다.
- `\cshutdown abort`
    - 접속 중인 session들의 상태와 무관하게 바로 서버를 강제 종료한다.
- `\cshutdown`
    - `\cshutdown normal` 과 동일하다.

glocator를 이용한 `\cshutdown`은 [CSTARTUP과 CSHUTDOWN](44-glocator.md#13ef0422121ec448)을 통해 확인할 수 있다.

> • CS 환경에서만 사용하는 명령어로써 gsqlnet에서만 사용할 수 있다.  
> • `\cshutdown` 명령은 해당 서버와 함께 다른 서버에까지 영향을 미치는 명령어이다. 따라서 [odbc.ini 파일](../part-05-developer-manual/29-odbc.md#f1a0bc8659eada10) LOCATOR_DSN 속성이 기술되지 않았을 경우, 에러가 반환된다.

<a id="201e203070ac0bfb"></a>
#### 사용 예

다음은 GOLDILOCKS를 종료하는 예이다.

```
% gsqlnet sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \cshutdown

Shutdown success

gSQL>
```

<a id="a3198ba56660ca0b"></a>
### `\ddl_cluster`

<a id="763d84625105ef58"></a>
#### 구문

```
\ddl_cluster
```

<a id="0ae11c76c158f5a6"></a>
#### 설명

Cluster system의 현재 상태에 해당하는 cluster DDL 구문을 출력한다.   
Cluster system에서 유효한 구문이다.

<a id="8efcc554da5734ed"></a>
#### 사용 예

다음은 3 x 2로 구성된 cluster system에 대해 `\ddl_cluster` 명령을 수행하는 예이다.

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

<a id="f814ed0276f7c927"></a>
### `\ddl_db`

<a id="a9d1f2246b25da8f"></a>
#### 구문

```
\ddl_db 
\ddl_db GRANT
\ddl_db COMMENT
```

<a id="448020c5665fa164"></a>
#### 설명

데이터베이스 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

> 휴지통에 보관된 객체들은 출력되지 않는다.

**`\ddl_db` 명령**

<a id="e3ef59e9ac8ba66a"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_db` | 데이터베이스에 생성된 모든 객체의 DDL 구문을 출력한다. |
| `\ddl_db GRANT` | 데이터베이스 객체의 권한 정보에 해당하는 GRANT .. ON DATABASE 구문을 출력한다. |
| `\ddl_db COMMENT` | 데이터베이스 객체의 주석 정보에 해당하는 COMMENT ON DATABASE 구문을 출력한다. |

옵션이 없는 `\ddl_db` 명령을 수행하면 다음과 같은 순서로 DDL 구문을 출력한다.

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

단, dictionary 정보를 포함하고 있는 다음 스키마와 관련된 정보는 출력하지 않는다.

- DICTIONARY_SCHEMA
- INFORMATION_SCHEMA
- PERFORMANCE_VIEW_SCHEMA
- DEFINITION_SCHEMA
- FIXED_TABLE_SCHEMA

위의 dictionary 정보를 포함하는 schema에 대한 DDL 구문은 [`\ddl_schema`](#22b7662f8bed9731) 명령을 이용해 출력할 수 있다.

<a id="da6473f58a8565da"></a>
#### 사용 예

다음은 `\ddl_db` 명령을 수행하는 예이다.

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

... 중략 ...
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

다음은 `\ddl_db GRANT` 명령을 수행하는 예이다.

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

... 중략 ...
```

<a id="a1f5b03d15830a32"></a>
### `\ddl_tablespace`

<a id="f17ec4737eec2952"></a>
#### 구문

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

<a id="8a814d0f93b467da"></a>
#### 설명

테이블스페이스 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

> 휴지통에 보관된 객체들은 출력되지 않는다.

**`\ddl_tablespace` 명령**

<a id="7a3b67557f721f50"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_tablespace name` | 아래의 모든 옵션을 수행한다. |
| `\ddl_tablespace name CREATE` | 테이블스페이스의 CREATE TABLESPACE 구문을 출력한다. |
| `\ddl_tablespace name ALTER` | 테이블스페이스에 추가된 datafile 또는 memory에 대한 ALTER TABLESPACE 구문을 출력한다. |
| `\ddl_tablespace name TABLE` | 테이블스페이스에 저장된 table들의 CREATE TABLE 구문을 출력한다. |
| `\ddl_tablespace name CONSTRAINT` | 테이블스페이스에 저장된 constraint들의 ALTER TABLE 구문을 출력한다. |
| `\ddl_tablespace name INDEX` | 테이블스페이스에 저장된 index들의 CREATE INDEX 구문을 출력한다. |
| `\ddl_tablespace name GRANT` | 테이블스페이스의 권한 정보에 대한 GRANT .. ON TABLESPACE 구문을 출력한다. |
| `\ddl_tablespace name COMMENT` | 테이블스페이스의 주석에 해당하는 COMMENT ON TABLESPACE 구문을 출력한다. |

<a id="b04a504729fce5d1"></a>
#### 사용 예

다음은 `\ddl_tablespace CREATE` 명령을 수행하는 예이다.

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

다음은 `\ddl_tablespace ALTER` 명령을 수행하는 예이다.

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

<a id="720e0ea1294f39c9"></a>
### `\ddl_profile`

<a id="723a17e354af521b"></a>
#### 구문

```
\ddl_profile name
\ddl_profile name CREATE
\ddl_profile name COMMENT
```

<a id="9a9814685f1c17d8"></a>
#### 설명

Profile 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

**`\ddl_profile` 명령**

<a id="b5c9e5b46c7fb7b7"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_profile name` | 아래의 모든 옵션을 수행한다. |
| `\ddl_profile name CREATE` | Profile 객체의 CREATE PROFILE 구문을 출력한다. |
| `\ddl_profile name COMMENT` | Profile의 주석에 해당하는 COMMENT ON PROFILE 구문을 출력한다. |

<a id="8a51ea587f8509f3"></a>
#### 사용 예

다음은 `\ddl_profile CREATE` 명령을 수행하는 예이다.

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

<a id="9ed3153ad8b48405"></a>
### `\ddl_audit_policy`

<a id="839b3fea3c941a6d"></a>
#### 구문

```
\ddl_audit_policy name
\ddl_audit_policy name CREATE
\ddl_audit_policy name AUDIT
\ddl_audit_policy name COMMENT
```

<a id="5d3dffe2a0f11035"></a>
#### 설명

Audit policy 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

> 휴지통에 보관된 객체들의 AUDIT ACTION은 출력되지 않는다.

**`\ddl_audit_policy` 명령**

<a id="89677834774df707"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_audit_policy name` | 아래의 모든 옵션을 수행한다. |
| `\ddl_audit_policy name CREATE` | Audit policy 객체의 CREATE AUDIT POLICY 구문을 출력한다. |
| `\ddl_audit_policy name AUDIT` | Audit policy 객체의 AUDIT POLICY 구문을 출력한다. |
| `\ddl_audit_policy name COMMENT` | Audit policy의 주석에 해당하는 COMMENT ON AUDIT POLICY 구문을 출력한다. |

<a id="875026c91ba09fd7"></a>
#### 사용 예

다음은 `\ddl_audit_policy CREATE` 명령을 수행하는 예이다.

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

<a id="95b90195ea61225e"></a>
### `\ddl_auth`

<a id="6168fe44f98d7ae4"></a>
#### 구문

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

<a id="8ab2ff945ef6df99"></a>
#### 설명

계정 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

> 휴지통에 보관된 객체들은 출력되지 않는다.

**`\ddl_auth` 명령**

<a id="8cc5bbf6f30d8782"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_auth name` | 아래의 모든 옵션을 수행한다. |
| `\ddl_auth name CREATE` | 사용자 객체의 CREATE USER 구문을 출력한다. |
| `\ddl_auth name SCHEMA` | 사용자가 소유한 schema들의 CREATE SCHEMA 구문을 출력한다. |
| `\ddl_auth name SCHEMA PATH` | 계정의 schema path에 해당하는 ALTER USER 구문을 출력한다. |
| `\ddl_auth name TABLE` | 사용자가 소유한 table들의 CREATE TABLE 구문을 출력한다. |
| `\ddl_auth name CONSTRAINT` | 사용자가 소유한 constraint들의 ALTER TABLE 구문을 출력한다. |
| `\ddl_auth name INDEX` | 사용자가 소유한 index들의 CREATE INDEX 구문을 출력한다. |
| `\ddl_auth name VIEW` | 사용자가 소유한 view들의 CREATE VIEW 구문을 출력한다. |
| `\ddl_auth name SEQUENCE` | 사용자가 소유한 sequence들의 CREATE SEQUENCE 구문을 출력한다. |
| `\ddl_auth name SYNONYM` | 사용자가 소유한 synonym들의 CREATE SYNONYM 구문을 출력한다. |
| `\ddl_auth name PROCEDURE` | 사용자가 소유한 procedure와 function들의 CREATE PROCEDURE/FUNCTION 구문을 출력한다. |
| `\ddl_auth name PACKAGE` | 사용자가 소유한 package들의 CREATE PACKAGE/PACKAGE BODY 구문을 출력한다. |
| `\ddl_auth name COMMENT` | 계정의 주석에 해당하는 COMMENT ON AUTHORIZATION 구문을 출력한다. |

<a id="58caece59b8894f7"></a>
#### 사용 예

다음은 `\ddl_auth CREATE` 명령을 수행하는 예이다.

```
gSQL> \ddl_auth h_user CREATE


SET SESSION AUTHORIZATION "SYS"; 
CREATE USER "H_USER" 
    IDENTIFIED BY H_USER 
    DEFAULT TABLESPACE "TEST_TBS" 
    TEMPORARY TABLESPACE "TEMP_TBS" 
    INDEX TABLESPACE NULL
    WITHOUT SCHEMA 
;
```

다음은 `\ddl_auth SCHEMA` 명령을 수행하는 예이다.

```
gSQL> \ddl_auth h_user SCHEMA


SET SESSION AUTHORIZATION "SYS"; 
CREATE SCHEMA "H_USER" 
    AUTHORIZATION "H_USER" 
;
```

다음은 `\ddl_auth TABLE` 명령을 수행하는 예이다.

```
gSQL> \ddl_auth h_user TABLE

SET SESSION AUTHORIZATION "H_USER"; 
CREATE TABLE "H_USER"."REGION" 
    ( 
        "R_REGIONKEY" NUMBER( 10, 0 )
      , "R_NAME" CHAR( 25 OCTETS )
      , "R_COMMENT" VARCHAR( 152 OCTETS )
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
        MAXSIZE 562949953159168 
    ) 
    TABLESPACE "TEST_TBS" 
;

SET SESSION AUTHORIZATION "H_USER"; 
CREATE TABLE "H_USER"."NATION" 
    ( 
        "N_NATIONKEY" NUMBER( 10, 0 )
      , "N_NAME" CHAR( 25 OCTETS )
      , "N_REGIONKEY" NUMBER( 10, 0 )
      , "N_COMMENT" VARCHAR( 152 OCTETS )
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
        MAXSIZE 562949953159168 
    ) 
    TABLESPACE "TEST_TBS" 
;
```

<a id="22b7662f8bed9731"></a>
### `\ddl_schema`

<a id="e8079e0ef1277229"></a>
#### 구문

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

<a id="d788afc9d2addd77"></a>
#### 설명

스키마 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

> 휴지통에 보관된 객체들은 출력되지 않는다.

**`\ddl_schema` 명령**

<a id="68850fdafb3a7d51"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_schema name` | 아래의 모든 옵션을 수행한다. |
| `\ddl_schema name CREATE` | 스키마 객체의 CREATE SCHEMA 구문을 출력한다. |
| `\ddl_schema name TABLE` | 스키마에 속한 table들의 CREATE TABLE 구문을 출력한다. |
| `\ddl_schema name CONSTRAINT` | 스키마에 속한 constraint들의 ALTER TABLE 구문을 출력한다. |
| `\ddl_schema name INDEX` | 스키마에 속한 index들의 CREATE INDEX 구문을 출력한다. |
| `\ddl_schema name VIEW` | 스키마에 속한 view들의 CREATE VIEW 구문을 출력한다. |
| `\ddl_schema name SEQUENCE` | 스키마에 속한 sequence들의 CREATE SEQUENCE 구문을 출력한다. |
| `\ddl_schema name SYNONYM` | 스키마에 속한 synonym들의 CREATE SYNONYM 구문을 출력한다. |
| `\ddl_schema name PROCEDURE` | 스키마에 속한 procedure와 function들의 CREATE PROCEDURE/ FUNCTION 구문을 출력한다. |
| `\ddl_schema name PACKAGE` | 스키마에 속한 package들의 CREATE PACKAGE/PACKAGE BODY 구문을 출력한다. |
| `\ddl_schema name GRANT` | 스키마의 권한 정보에 대한 GRANT .. ON SCHEMA 구문을 출력한다. |
| `\ddl_schema name COMMENT` | 스키마의 주석에 해당하는 COMMENT ON SCHEMA 구문을 출력한다. |

<a id="5eecb3693e37a2f1"></a>
#### 사용 예

다음은 `\ddl_schema CREATE` 명령을 수행하는 예이다.

```
gSQL> \ddl_schema h_user CREATE


SET SESSION AUTHORIZATION "SYS"; 
CREATE SCHEMA "H_USER" 
    AUTHORIZATION "H_USER" 
;
```

다음은 `\ddl_schema CONSTRAINT` 명령을 수행하는 예이다.

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
        MAXSIZE 562949953159168 
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
        MAXSIZE 562949953159168 
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
        MAXSIZE 562949953159168 
    ) 
    TABLESPACE "TEMP_TBS" 
    NOT DEFERRABLE
    INITIALLY IMMEDIATE
;
```

<a id="154bcff6b21654f2"></a>
### `\ddl_public_synonym`

<a id="c77d0ab30ed431ef"></a>
#### 구문

```
\ddl_public_synonym name
\ddl_public_synonym name CREATE
```

<a id="4cf908113758d617"></a>
#### 설명

Public synonym 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

**`\ddl_public_synonym` 명령**

<a id="8925ed03c19c6de5"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_public_synonym` | 아래의 모든 옵션을 수행한다. |
| `\ddl_public_synonym name CREATE` | Public synonym 객체의 CREATE PUBLIC SYNONYM 구문을 출력한다. |

<a id="02aedfea93d50492"></a>
#### 사용 예

다음은 `\ddl_public_synonym CREATE` 명령을 수행하는 예이다.

```
gSQL> \ddl_public_synonym pubsyn CREATE

SET SESSION AUTHORIZATION "SYS"; 
CREATE PUBLIC SYNONYM "PUBSYN" FOR "PUBLIC"."T1"
;
COMMIT;
```

<a id="dce7524a3b40f576"></a>
### `\ddl_table`

<a id="a2935dabdc7697be"></a>
#### 구문

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

<a id="57c31f5c3826359b"></a>
#### 설명

테이블 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

> 휴지통에 보관된 객체들은 출력되지 않는다.

**`\ddl_table` 명령**

<a id="287594f8e9bf1528"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_table name` | 아래의 모든 옵션을 수행한다. |
| `\ddl_table name CREATE` | 테이블 객체의 CREATE TABLE 구문을 출력한다. |
| `\ddl_table name CONSTRAINT ` | 테이블에 생성된 constraint들의 ALTER TABLE 구문을 출력한다. |
| `\ddl_table name INDEX` | 테이블에 생성된 index들의 CREATE INDEX 구문을 출력한다. |
| `\ddl_table name IDENTITY` | 테이블이 identity column을 가질 경우 restart 값에 대한 ALTER TABLE 구문을 출력한다. |
| `\ddl_table name SUPPLEMENTAL` | 테이블에 supplemental log 옵션이 설정된 경우 ALTER TABLE 구문을 출력한다. |
| `\ddl_table name GRANT` | 테이블의 권한 정보에 대한 GRANT .. ON TABLE 구문을 출력한다. |
| `\ddl_table name COMMENT` | 테이블의 주석에 해당하는 COMMENT ON TABLE 구문을 출력한다. |

<a id="be39c88b874632de"></a>
#### 사용 예

다음은 `\ddl_table CREATE` 명령을 수행하는 예이다.

```
gSQL> \ddl_table h_user.orders CREATE

SET SESSION AUTHORIZATION "H_USER"; 
CREATE TABLE "H_USER"."ORDERS" 
    ( 
        "O_ORDERKEY" NUMBER( 10, 0 )
      , "O_CUSTKEY" NUMBER( 10, 0 )
      , "O_ORDERSTATUS" CHAR( 1 OCTETS )
      , "O_TOTALPRICE" NUMBER( 12, 2 )
      , "O_ORDERDATE" DATE
      , "O_ORDERPRIORITY" CHAR( 15 OCTETS )
      , "O_CLERK" CHAR( 15 OCTETS )
      , "O_SHIPPRIORITY" NUMBER( 10, 0 )
      , "O_COMMENT" VARCHAR( 79 OCTETS )
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
        MAXSIZE 562949953159168 
    ) 
    TABLESPACE "TEST_TBS" 
;
```

다음은 `\ddl_table GRANT` 명령을 수행하는 예이다.

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

<a id="6b2d013b24cb2a83"></a>
### `\ddl_constraint`

<a id="fda630826843e37b"></a>
#### 구문

```
\ddl_constraint name
\ddl_constraint name ALTER
\ddl_constraint name COMMENT
```

<a id="73823a7da1736104"></a>
#### 설명

제약 조건 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

> 휴지통에 보관된 객체들은 출력되지 않는다.

**`\ddl_constraint` 명령**

<a id="4482c433448eebf1"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_constraint name` | 아래의 모든 옵션들을 수행한다. |
| `\ddl_constraint name ALTER` | 제약 조건 객체의 ALTER TABLE 구문을 출력한다. |
| `\ddl_constraint name COMMENT` | 제약 조건의 주석에 해당하는 COMMENT ON CONSTRAINT 구문을 출력한다. |

<a id="b603e2d9acc55ddf"></a>
#### 사용 예

다음은 `\ddl_constraint ALTER` 명령을 수행하는 예이다.

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
        MAXSIZE 562949953159168 
    ) 
    TABLESPACE "TEMP_TBS" 
    NOT DEFERRABLE
    INITIALLY IMMEDIATE
;
```

<a id="db8a3ad0620424ee"></a>
### `\ddl_index`

<a id="49cf0f7ce6a88b63"></a>
#### 구문

```
\ddl_index name
\ddl_index name CREATE
\ddl_index name COMMENT
```

<a id="a929c96151212f5d"></a>
#### 설명

인덱스 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

> 휴지통에 보관된 객체들은 출력되지 않는다.

**`\ddl_index` 명령**

<a id="1cb9e1acabb9a64d"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_index name` | 아래의 모든 옵션을 수행한다. |
| `\ddl_index name CREATE` | 인덱스 객체의 CREATE INDEX 구문을 출력한다. |
| `\ddl_index name COMMENT` | 인덱스의 주석에 해당하는 COMMENT ON INDEX 구문을 출력한다. |

<a id="ef193d236f11a7e9"></a>
#### 사용 예

다음은 `\ddl_index CREATE` 명령을 수행하는 예이다.

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
        MAXSIZE 562949953159168 
    ) 
    TABLESPACE "MEM_TEMP_TBS" 
;
```

<a id="c1e543751777c6fa"></a>
### `\ddl_view`

<a id="13ef860dffc37bcb"></a>
#### 구문

```
\ddl_view name
\ddl_view name CREATE
\ddl_view name GRANT
\ddl_view name COMMENT
```

<a id="6371c4158e305418"></a>
#### 설명

View 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

**`\ddl_view` 명령**

<a id="39ef66b8167afd1f"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_view name` | 아래의 모든 옵션을 수행한다. |
| `\ddl_view name CREATE` | View 객체의 CREATE VIEW 구문을 출력한다. |
| `\ddl_view name GRANT` | View의 권한 정보에 대한 GRANT .. ON TABLE 구문을 출력한다. |
| `\ddl_view name COMMENT` | View의 주석에 해당하는 COMMENT ON TABLE 구문을 출력한다. |

<a id="f24c4fb89368c545"></a>
#### 사용 예

다음은 `\ddl_view CREATE` 명령을 수행하는 예이다.

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

<a id="154929446753c11d"></a>
### `\ddl_sequence`

<a id="e14086a77b3b6aa4"></a>
#### 구문

```
\ddl_sequence name
\ddl_sequence name CREATE
\ddl_sequence name RESTART
\ddl_sequence name GRANT
\ddl_sequence name COMMENT
```

<a id="c114ece9542a9aef"></a>
#### 설명

시퀀스 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

**`\ddl_sequence` 명령**

<a id="0f043230eb62569f"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_sequence name` | 아래의 모든 옵션을 수행한다. |
| `\ddl_sequence name CREATE` | 시퀀스 객체의 CREATE SEQUENCE 구문을 출력한다. |
| `\ddl_sequence name RESTART` | 시퀀스 객체의 restart 값에 해당하는 ALTER SEQUENCE 구문을 출력한다. |
| `\ddl_sequence name GRANT` | 시퀀스의 권한 정보에 대한 GRANT .. ON SEQUENCE 구문을 출력한다. |
| `\ddl_sequence name COMMENT` | 시퀀스의 주석에 해당하는 COMMENT ON SEQUENCE 구문을 출력한다. |

<a id="b37ff03af77e60b3"></a>
#### 사용 예

다음은 `\ddl_sequence CREATE` 명령을 수행하는 예이다.

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

다음은 `\ddl_sequence RESTART` 명령을 수행하는 예이다.

```
gSQL> \ddl_sequence h_user.h_seq RESTART


SET SESSION AUTHORIZATION "H_USER"; 
ALTER SEQUENCE "H_USER"."H_SEQ" 
    RESTART WITH 21 
;
```

<a id="975cd121d4ade13c"></a>
### `\ddl_synonym`

<a id="0154686906af7867"></a>
#### 구문

```
\ddl_synonym name
\ddl_synonym name CREATE
```

<a id="74e22a795b277ab2"></a>
#### 설명

Synonym 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

**`\ddl_synonym` 명령**

<a id="c5229c6b0fdf8504"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_synonym` | 아래의 모든 옵션을 수행한다. |
| `\ddl_synonym name CREATE` | Synonym 객체의 CREATE SYNONYM 구문을 출력한다. |

<a id="7488c62b481e259a"></a>
#### 사용 예

다음은 `\ddl_synonym CREATE` 명령을 수행하는 예이다.

```
gSQL> \ddl_synonym syn CREATE

SET SESSION AUTHORIZATION "TEST"; 
CREATE SYNONYM "PUBLIC"."SYN" FOR "PUBLIC"."T1"
;
COMMIT;
```

<a id="bfdd1dc3f6b95efc"></a>
### `\ddl_procedure`

<a id="7483724f9473fd5a"></a>
#### 구문

```
\ddl_procedure name
\ddl_procedure name CREATE
```

<a id="508f4421ed88aa82"></a>
#### 설명

Stored procedure나 function 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

**`\ddl_procedure` 명령**

<a id="e00fcbabc62d6966"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_procedure` | 아래의 모든 옵션을 수행한다. |
| `\ddl_procedure name CREATE` | Stored procedure/ function 객체의 CREATE PROCEDURE/FUCNTION 구문을 출력한다. |

<a id="4837c7f7187490d4"></a>
#### 사용 예

다음은 `\ddl_procedure CREATE` 명령을 수행하는 예이다.

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

<a id="b3e38d648d9ce661"></a>
### `\ddl_package`

<a id="7a3d7e2fd6ec7678"></a>
#### 구문

```
\ddl_package name
\ddl_package name CREATE
```

<a id="067a3e92b8075ed6"></a>
#### 설명

package spec이나 package body 객체의 현재 상태에 해당하는 DDL 구문을 출력한다.

**`\ddl_package` 명령**

<a id="1b26eee782010e1f"></a>
| 명령어 | 설명 |
| --- | --- |
| `\ddl_package` | 아래의 모든 옵션을 수행한다. |
| `\ddl_package name CREATE` | Package Spec 및 package body 객체의 CREATE PACKAGE/PACKAGE BODY 구문을 출력한다. |

<a id="4d8e604286d8d742"></a>
#### 사용 예

다음은 `\ddl_package CREATE` 명령을 수행하는 예이다.

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

<a id="b4d1178aec2889c2"></a>
### `\desc`

<a id="6c8df35fb49d1f72"></a>
#### 구문

```
\desc table_name
\desc schema_name.table_name
```

<a id="c9adf8fc129ad174"></a>
#### 설명

테이블의 구조 정보를 조회한다.

테이블은 다음과 같이 테이블 이름만 기술하거나 테이블 이름을 스키마 이름과 함께 기술할 수 있다. 스키마 이름을 명시하지 않은 경우 테이블의 스키마 이름은 사용자의 [Schema Path](../part-03-sql-manual/13-sql-objects.md#af5f5168830f70fb)에 의해 결정된다.

- `\desc` t1
- `\desc` public.t1

테이블을 생성할 때 다음과 같이 [delimited identifier](../part-03-sql-manual/11-sql-elements.md#bf797922265f9c61)를 이용해 테이블 이름을 생성한 경우, double-quote (")를 사용해 기술한다.

- 테이블 생성 
    - CREATE TABLE "TaBle#@^*" ( id INTEGER );
- `\desc` "TaBle#@^*"
- `\desc` "PUBLIC"."TaBle#@^*"

수행 결과는 해당 테이블의 다음과 같은 정보를 포함한다.

- Column 정보
    - Column 이름
    - 데이터 타입
    - NULL 가능 여부
- 인덱스 정보
    - 인덱스 이름
    - 인덱스 저장 공간
    - 인덱스 타입
    - UNIQUE 여부
    - Key column 이름
- 제약 조건 정보
    - 제약 조건 이름
    - 제약 조건 유형
    - 관련 인덱스
    - 제약 조건 column

<a id="46e0e64889c3bd9b"></a>
#### 사용 예

다음은 t1 테이블의 정보를 조회하는 예이다.

```
gSQL> \desc t1

COLUMN_NAME TYPE                    IS_NULLABLE
----------- ----------------------- -----------
ID          NUMBER(10,0)            FALSE      
NAME        VARCHAR(128)            TRUE       
ADDR        VARCHAR(1024)           TRUE       

INDEX_NAME           TABLESPACE_NAME INDEX_TYPE IS_UNIQUE COLUMNS
-------------------- --------------- ---------- --------- -------
T1_PRIMARY_KEY_INDEX MEM_TEMP_TBS    BTREE      TRUE      ID     
T1_IDX_NAME          MEM_TEMP_TBS    BTREE      FALSE     NAME   

CONSTRAINT_NAME CONSTRAINT_TYPE ASSOCIATED_INDEX     COLUMNS
--------------- --------------- -------------------- -------
T1_PRIMARY_KEY  PRIMARY KEY     T1_PRIMARY_KEY_INDEX ID
```

다음은 스키마 이름 public과 함께 기술하여 t1 테이블의 정보를 조회하는 예이다.

```
gSQL> \desc public.t1

COLUMN_NAME TYPE                    IS_NULLABLE
----------- ----------------------- -----------
ID          NUMBER(10,0)            FALSE      
NAME        VARCHAR(128)            TRUE       
ADDR        VARCHAR(1024)           TRUE       

INDEX_NAME           TABLESPACE_NAME INDEX_TYPE IS_UNIQUE COLUMNS
-------------------- --------------- ---------- --------- -------
T1_PRIMARY_KEY_INDEX MEM_TEMP_TBS    BTREE      TRUE      ID     
T1_IDX_NAME          MEM_TEMP_TBS    BTREE      FALSE     NAME   

CONSTRAINT_NAME CONSTRAINT_TYPE ASSOCIATED_INDEX     COLUMNS
--------------- --------------- -------------------- -------
T1_PRIMARY_KEY  PRIMARY KEY     T1_PRIMARY_KEY_INDEX ID
```

다음은 delimited identifier를 사용하여 생성한 테이블의 정보를 조회하는 예이다.

```
gSQL> CREATE TABLE "TaBle#@^*" ( id INTEGER );

Table created.

gSQL> \desc "TaBle#@^*"

COLUMN_NAME TYPE         IS_NULLABLE
----------- ------------ -----------
ID          NUMBER(10,0) TRUE
```

다음과 같이 delimited identifier를 사용하지 않은 경우, 에러가 발생한다.

```
gSQL> \desc TaBle#@^*

ERR-42000(40000): syntax error 
\desc TaBle#@^*
...........^  ^
Error at line 1
```

<a id="45a31fc296ced749"></a>
### `\dynamic sql :var`

<a id="edbd911faaff0cfa"></a>
#### 구문

```
\dynamic sql :var
```

<a id="3f0f6fd7eddf6c11"></a>
#### 설명

호스트 변수 var에 저장된 SQL 문장을 수행한다.  
Embedded SQL의 정의되지 않은 SQL 문장을 수행하는 [Embedded Dynamic SQL](../part-05-developer-manual/31-embedded-sql.md#bab9699b12f1bf0c)과 유사한 개념으로써 정의되지 않은 SQL 문장을 수행할 때 사용한다.

다음과 같은 절차로 수행한다.

1. 호스트 변수를 선언한다. ([`\var`](#5bdd58614174a2b3)를 참조한다.)  
   `\var` var_stmt VARCHAR(1024)
2. 호스트 변수의 값으로 SQL 문장을 대입한다. ([`\exec :var := value`](#374539d536d0872d)를 참조한다.)  
   `\exec` :var_stmt := 'SELECT # FROM t1'
3. Dynamic SQL을 수행한다.  
   `\dynamic sql` :var_stmt

<a id="56433ec3ffeb470d"></a>
#### 사용 예

다음은 var_stmt 호스트 변수를 선언하고 SQL 문장을 대입하여 dynamic SQL을 실행하는 예이다.

- 호스트 변수에 SELECT 문장을 대입한다.

```
gSQL> \exec :var_stmt := 'SELECT * FROM t1'
```

- Dynamic SQL을 수행한다.

```
gSQL> \dynamic sql :var_stmt 

ID NAME   ADDR        
-- ------ ------------
 1 leekmo Seoul, Korea

1 row selected.
```

다음 INSERT 문장과 같이 SQL 문장에 문자열이 존재할 경우 명령어 [`\exec :var := value`](#374539d536d0872d)를 사용할 때와 같이 single-quote (')를 두 번 기술한다.

- 호스트 변수를 선언한다.

```
gSQL> \var var_stmt VARCHAR(1024)
```

- 호스트 변수에 INSERT 문장을 대입한다.

```
gSQL> \exec :var_stmt := 'INSERT INTO t1(id, name, addr) VALUES ( 1, ''leekmo'', ''Seoul, Korea'' )'
```

- Dynamic SQL을 수행한다.

```
gSQL> \dynamic sql :var_stmt 

1 row created.
```

<a id="a18be4b967d5bb7f"></a>
### `\edit`

<a id="67a92cc1addfe9f9"></a>
#### 설명

Text editor를 사용하여 SQL 구문을 편집한다. 이 때 사용할 text editor는 환경 변수 EDITOR에 지정할 수 있으며 환경 변수 EDITOR가 존재하지 않을 경우에는 기본적으로 vi를 사용한다.

편집 기능을 사용하게 되면, gsql은 편집기를 실행하여 제어권을 넘긴다. 사용자는 편집기에서 SQL 구문 내용을 자유롭게 편집할 수 있고 편집기를 종료하게 되면 gsql에서 제어권을 돌려 받은 후에 해당 내용을 마지막 이력으로 추가한다.

이렇게 편집기를 통해서 편집된 SQL 구문은 가장 마지막 이력 실행 명령인 `\\`를 통해서 실행할 수 있다.

> 단일 SQL 구문만 SQL 편집 기능을 사용하여 편집할 수 있다. 다중 SQL 구문을 실행할 경우 오류가 발생한다.

`\edit` 명령을 사용하여 편집할 수 있는 내용은 다음과 같다.

- 가장 최근에 수행한 SQL 구문
- File에 저장된 SQL 구문
- gsql 이력에 저장된 SQL 구문

다음 절에서 각각에 대한 사용 방법을 설명한다.

<a id="732b611986b8b2b7"></a>
#### `\edit`

<a id="1da74e2b826c9cd9"></a>
##### 구문

```
\edit
\ed
```

<a id="32530dc2066223f5"></a>
##### 설명

Text editor를 사용하여 가장 마지막에 수행한 SQL 구문을 편집한다. 만약 아무런 SQL도 수행한 적이 없다면 아무 내용도 없는 상태로 text editor가 실행된다.

<a id="a68baea731aa977e"></a>
##### 사용 예

다음은 가장 최근에 수행한 SQL 구문을 편집하는 예이다.

- 가장 최근에 수행한 SQL 구문을 편집한다.

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

- 편집된 SQL 구문을 실행한다.

```
gSQL> \\
C1
--
 1
1 row selected.
```

<a id="e1c9503c0442448a"></a>
#### `\edit 'file_name'`

<a id="cbc33035ddd076ca"></a>
##### 구문

```
\edit 'file_name'
\ed   'file_name'
```

<a id="1d03650ebd21bf53"></a>
##### 설명

Text editor를 사용하여 주어진 file_name을 편집한다.  
file_name은 single quote (') 내에 기술한다.  
file_name은 다음과 같이 절대 경로 또는 상대 경로를 사용할 수 있으며 상대 경로를 사용할 경우 gsql을 수행한 경로를 기준으로 file_name을 찾는다.

- 절대 경로 사용

```
gSQL> \edit '/home/GOLDILOCKS/sample.sql'
```

- 상대 경로 사용

```
gSQL> \edit 'sample.sql'
```

<a id="03fd0fbdae96464e"></a>
##### 사용 예

다음은 file에 저장된 SQL 구문을 편집하는 예이다.

- 가장 최근에 수행한 SQL 구문을 편집한다.

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

- 편집된 SQL 구문을 실행한다.

```
gSQL> \\
C1
--
 1
1 row selected.
```

<a id="a8d117e3d86aa0c8"></a>
#### `\edit [history] {n}`

<a id="1ab9077ec1795825"></a>
##### 구문

```
\edit [history] {n}
\ed   [history] {n}
```

<a id="1015dfdcfa16a485"></a>
##### 설명

[`\history`](#ad141bbb20a37ce0) 명령으로 조회할 수 있는 SQL 수행 이력 중에서 number에 해당하는 구문을 편집한다.  
number 값은 [`\history`](#ad141bbb20a37ce0) 수행 결과의 ID 값이어야 한다.

<a id="8130653de6b324c0"></a>
##### 사용 예

다음은 gsql의 이력에 저장된 SQL 구문을 편집하는 예이다.

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

- 저장된 이력 중 ID가 1인 내용을 편집한다.

```
gSQL> \edit 1
SELECT * FROM T1 WHERE C1 < 5;
```

- 편집된 SQL 구문을 실행한다.

```
gSQL> \\
C1
--
 1
1 row selected.
```

<a id="0f3949721f6b5ec3"></a>
### `\exec`

<a id="0d85c7c3206c8ea9"></a>
#### 구문

```
\exec
```

<a id="8253fe486e53a277"></a>
#### 설명

[`\prepare sql`](#0a689bc4cd07f2fe) 명령에 의해 준비된 SQL 구문을 수행한다.  
`\exec` 명령은 ODBC의 [SQLExecute](../part-05-developer-manual/29-odbc.md#6d328906d0f53989) 함수와 JDBC의 PreparedStatement::[execute](../part-05-developer-manual/30-jdbc.md#434400ad9308cd8f) 함수와 유사하게 동작한다.  
준비된 SQL 구문은 `\exec` 명령을 통해 반복적으로 수행할 수 있다.

<a id="e5714ea2715e945c"></a>
#### 사용 예

다음은 INSERT 구문을 준비하고 반복적으로 수행하는 예이다.

- INSERT 구문을 prepare 한다.

```
gSQL> \prepare sql INSERT INTO t1(id, addr) VALUES ( seq.NEXTVAL, 'N/A' );

SQL prepared.
```

- Prepare 된 구문을 수행한다.

```
gSQL> \exec

1 row created.
```

- Prepare 된 구문을 수행한다.

```
gSQL> \exec

1 row created.
```

- 테이블 조회 결과는 다음과 같다.

```
gSQL> SELECT * FROM t1;

ID ADDR
-- ----
 1 N/A 
 2 N/A 

2 rows selected.
```

다음은 호스트 변수와 함께 SELECT 구문을 prepare 하고 호스트 변수의 값을 바꿔가며 반복 수행하는 예이다.

- 호스트 변수를 선언한다.

```
gSQL> \var v_id INTEGER
```

- 호스트 변수를 사용한 SELECT 구문을 prepare 한다.

```
gSQL> \prepare sql SELECT * FROM t1 WHERE ID = :v_id;

SQL prepared.
```

- 호스트 변수에 1 값을 대입한다.

```
gSQL> \exec :v_id := 1
```

- 준비된 SELECT 구문을 수행한다.

```
gSQL> \exec

ID ADDR
-- ----
 1 N/A 

1 row selected.
```

- 호스트 변수에 2 값을 대입한다.

```
gSQL> \exec :v_id := 2
```

- 준비된 SELECT 구문을 수행한다.

```
gSQL> \exec

ID ADDR
-- ----
 2 N/A 

1 row selected.
```

<a id="374539d536d0872d"></a>
### `\exec :var := value`

<a id="3cd243a6bf196953"></a>
#### 구문

```
\exec :variable := <value expression>
```

<a id="4ed101ddb68d49ce"></a>
#### 설명

호스트 변수에 값을 대입한다.  
해당 명령은 다음과 같은 [SELECT .. INTO](../part-03-sql-manual/18-sql-references.md#a345298536f40392) 구문을 수행한 것과 동일한 방식으로 호스트 변수에 값을 대입한다.

```
gSQL> \exec :v_value := 1234
gSQL> SELECT 1234 INTO :v_value FROM DUAL;
```

호스트 변수는 [`\var`](#5bdd58614174a2b3) 명령을 통해 선언되어 있어야 한다.

호스트 변수는 colon (:)과 함께 사용하여야 하며, 대입 연산자 (:=)에서 (:)을 생략하면 안된다. 호스트 변수에 입력되는 &lt;value expression&gt;에는 단순한 값이나 연산을 사용할 수 있다. 자세한 내용은 [Expressions](../part-03-sql-manual/11-sql-elements.md#7762cb83a82d78cc)를 참조한다.

호스트 변수에 입력되는 값은 호스트 변수의 데이터 타입에 입력 가능한 값이어야 한다. 자세한 내용은 [타입간 변환](../part-03-sql-manual/11-sql-elements.md#07646aa9949781c3)을 참조한다.

입력된 호스트 변수의 값은 [`\print`](#828c84fc4aea1dd3) 명령을 이용해 조회할 수 있다.

```
\exec :v_value := 1234
\print v_value
```

호스트 변수에 문자열을 대입할 경우 다음과 같이 문자열을 single quote (')로 묶어서 입력한다.

- 단순 문자열
    - 값: abcd
    - `\exec` :v_value := 'abcd'
- Single quote가 포함된 문자열
    - 값: Tom's House
    - 문자열 안의 single-quote (')는 다음과 같이 single quote (')를 두 번 사용한다.
    - `\exec` :v_value := 'Tom''s House'
- Single quote가 포함된 SQL 문장
    - 값: INSERT INTO t1 VALUES ( 1, 'Tom''s House' )
    - 문자열 안의 single quote (')는 다음과 같이 single quote (')를 두 번 사용한다.
    - `\exec` :v_value := 'INSERT INTO t1 VALUES ( 1, ''Tom''s House'' )'

<a id="d17d5491c2209cc0"></a>
#### 사용 예

다음은 다양한 형태의 문자열을 호스트 변수에 대입하는 예이다.

- 호스트 변수를 선언한다.

```
gSQL> \var v_value VARCHAR(1024)
```

- 단순 문자열을 대입한다.

```
gSQL> \exec :v_value := 'abcd'
gSQL> \print v_value

V_VALUE
-------
abcd
```

- Single quote (')가 포함된 문자열을 대입한다.

```
gSQL> \exec :v_value := 'Tom''s House'
gSQL> \print v_value

V_VALUE    
-----------
Tom's House
```

- Single quote (')가 포함된 SQL 문장을 대입한다.

```
gSQL> \exec :v_value := 'INSERT INTO t1 VALUES ( 1, ''Tom''s House'' )'
gSQL> \print v_value

V_VALUE                                   
------------------------------------------
INSERT INTO t1 VALUES ( 1, 'Tom's House' )
```

다음은 호스트 변수에 값을 할당할 때 연산결과를 사용하는 예이다.

- 호스트 변수를 선언한다.

```
gSQL> \var v1 INTEGER
gSQL> \var v2 INTEGER
```

- v1에 값을 할당한다.

```
gSQL> \exec :v1 := 100
```

- v1과의 연산을 수행한 값을 v2에 할당한다.

```
gSQL> \exec :v2 := :v1 + 1000
```

- 호스트 변수 v1과 v2의 값을 조회한다.

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

다음은 호스트 변수에 값을 할당하고 호스트 변수를 SELECT 구문에 사용하는 예이다.

- 호스트 변수를 선언한다.

```
gSQL> \var v_id INTEGER
```

- 호스트 변수에 값을 할당한다.

```
gSQL> \exec :v_id := 1
```

- 호스트 변수를 이용하여 SELECT 구문을 수행한다.

```
gSQL> SELECT * FROM t1 WHERE id = :v_id;

ID ADDR
-- ----
 1 N/A 

1 row selected.
```

다음은 [SELECT .. INTO](../part-03-sql-manual/18-sql-references.md#a345298536f40392) 구문을 통해 호스트 변수에 값을 얻어오는 예이다.

- 호스트 변수를 선언한다.

```
gSQL> \var v_id INTEGER
```

- 어떠한 값도 설정되어 있지 않다.

```
gSQL> \print v_id

V_ID
----
null
```

- SELECT INTO 구문 수행을 통해 v_id에 값을 할당한다.

```
gSQL> SELECT MAX(id) INTO :v_id FROM t1;

V_ID
----
   2

1 row selected.
```

- 호스트 변수의 값을 확인한다.

```
gSQL> \print v_id

V_ID
----
   2
```

<a id="937854e40d50d4a1"></a>
### `\exec sql`

<a id="749d108ef6132266"></a>
#### 구문

```
\exec sql <sql_statement>
```

<a id="7cadf835c0db2a52"></a>
#### 설명

&lt;sql_statement&gt;에 기술된 SQL 구문을 실행한다.   
다음과 같이 프롬프트 상에서 SQL 구문을 수행한 것과 동일하게 동작한다.

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

SQL 구문을 수행할 때 [`\prepare sql`](#0a689bc4cd07f2fe) 명령과 [`\exec`](#0f3949721f6b5ec3) 명령을 이용하여 PREPARE/EXECUTE 방식으로 실행하는 것과 달리, `\exec sql` 명령은 ODBC의 [SQLExecDirect](../part-05-developer-manual/29-odbc.md#63026bcefa261dda) 함수와 JDBC의 Statement::[execute](../part-05-developer-manual/30-jdbc.md#831bf7c80862de67) 함수에 대응하는 DIRECT EXECUTE 방식으로 SQL 구문을 수행한다.

<a id="e8226663dc6d69e5"></a>
#### 사용 예

다음은 SELECT 구문을 수행하는 간단한 예이다.

```
gSQL> \exec sql SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.
```

<a id="6160cfd32df70014"></a>
### `\explain plan`

<a id="22aadd913a644e9a"></a>
#### 구문

```
\explain plan <sql_statement>
\explain plan on <sql_statement>
\explain plan only <sql_statement>
```

<a id="aa426cb0756b6657"></a>
#### 설명

&lt;sql_statement&gt;에 기술된 SELECT 구문 등의 실행 계획을 출력한다.

- `\explain plan on`
    - SQL 구문을 수행하고 질의 결과와 함께 실행 계획을 출력한다.
- `\explain plan only`
    - SQL 구문을 수행하지 않고 질의 결과 없이 실행 계획을 출력한다.
- `\explain plan`
    - on이나 only를 명시하지 않은 경우, 기본값은 on 이다.

실행 계획에 대한 자세한 설명은 [SQL 실행 계획](../part-03-sql-manual/15-sql-tuning.md#f6556ce75bce767e)을 참조한다.

<a id="bf52558beaa2bb2f"></a>
#### 사용 예

다음과 같이 ON과 함께 사용할 경우 SQL 구문을 수행하고 질의 결과와 함께 실행 계획을 출력한다.

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

다음과 같이 ONLY를 사용할 경우 SQL 구문을 수행하지 않고 질의 결과 없이 실행 계획만 출력한다.

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

<a id="c88e9fafc5990cae"></a>
### `\help`

<a id="0160ce7967c88d7f"></a>
#### 구문

```
\help
```

<a id="89a0edf9d08a4c2e"></a>
#### 설명

gsql 대화형 모드에서 `(\)`로 시작하는 명령어 목록을 간략히 보여준다.

<a id="9449352f5d5954d8"></a>
#### 사용 예

다음은 `\help` 명령을 사용하는 예이다.

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

<a id="54cca2c486a10dd1"></a>
### `\host`

<a id="013babedb4eadc55"></a>
#### 구문

```
\host [command]
\ho [command]
```

<a id="878ac54e551e8cc8"></a>
#### 설명

gsql 프로그램을 종료하지 않은 채 운영 체제 명령을 실행한다.   
command 없이 HOST를 입력하면 운영 체제 프롬프트가 표시되며 운영 체제 명령어를 계속 입력할 수 있다.   
HOST 대신 Windows에서는 "$"를, UNIX에서는 "!" 문자를 사용할 수 있다.

<a id="2f613d7bd4ec519a"></a>
#### 사용 예

다음은 UNIX 운영 체제 명령인 `ls *.sql` 구문을 수행하는 예이다.

```
gSQL> \host ls *.sql
DictionarySchema.sql  InformationSchema.sql  PerformanceViewSchema.sql
```

<a id="ad141bbb20a37ce0"></a>
### `\history`

<a id="ec30d4fda6245093"></a>
#### 구문

```
\history
\hi
```

<a id="8d04f555df29cd7c"></a>
#### 설명

gsql 프로그램을 수행한 이후의 SQL 구문 수행 목록을 보여준다.  
수행에 성공한 SQL 구문만 관리하며, gsql (`\`)로 시작하는 대화형 명령어로 수행한 명령어나 실패한 SQL 구문은 포함하지 않는다.  
해당 목록을 참조하여 [`\\`](#4c1575265582051a) 명령이나 [`\{n}`](#c2ebdddcf744e75d) 명령을 통해 이전에 수행한 SQL 구문을 다시 수행할 수 있다.  
관리할 수 있는 SQL 구문의 개수는 [`\set history`](#4686267060d45f6d) 명령을 통해 제어한다.

<a id="4c6966607ad5bdf4"></a>
#### 사용 예

다음은 SQL 구문 수행 이력를 조회하고 8번 SQL 구문을 다시 수행하는 예이다.

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

<a id="43c841d979d82282"></a>
### `\import`

<a id="f0b7a60aaeff4554"></a>
#### 구문

```
\import 'file_name'
\i 'file_name'
```

<a id="a67ed8678762a348"></a>
#### 설명

file_name에 포함된 SQL 구문들을 수행한다.  
file_name은 single quote (') 안에 기술한다.  
file_name은 다음과 같이 절대 경로 또는 상대 경로를 사용할 수 있으며 상대 경로를 사용할 경우 gsql을 수행한 경로를 기준으로 file_name을 찾는다.

- 절대 경로 사용

```
gSQL> \import '/home/GOLDILOCKS/sample.sql'
```

- 상대 경로 사용

```
gSQL> \import 'sample.sql'
```

<a id="755ea28d7867a1a7"></a>
#### 사용 예

다음은 절대 경로를 사용하여 file 내의 SQL 구문을 사용하는 예이다.

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

다음은 상대 경로를 사용하여 file 내의 SQL 구문을 사용하는 예이다.

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

<a id="3cc6adb4e775dc1c"></a>
### `\idesc`

<a id="1a8d781b49f219cc"></a>
#### 구문

```
\idesc index_name
\idesc schema_name.index_name
```

<a id="c1135894b395b751"></a>
#### 설명

인덱스의 구조 정보를 조회한다.

인덱스 이름은 다음과 같이 인덱스 이름만 기술하거나 스키마 이름과 함께 기술할 수 있다. 스키마 이름을 명시하지 않은 경우, 인덱스의 스키마 이름은 사용자의 [Schema Path](../part-03-sql-manual/13-sql-objects.md#af5f5168830f70fb)에 의해 결정된다.

- `\idesc` t1_idx_name
- `\idesc` public.t1_idx_name

수행 결과는 다음과 같이 인덱스의 key column 정보를 포함한다.

- Key column의 이름
- Key column의 위치 
- Key column의 정렬 순서 (오름차순/ 내림차순)
- Key column의 NULL 값 위치 (FIRST/ LAST)

<a id="59c3465f968b451a"></a>
#### 사용 예

다음은 t1_idx_name 인덱스의 정보를 조회하는 예이다.

```
gSQL> \idesc t1_idx_name

COLUMN_NAME ORDINAL_POSITION IS_ASCENDING_ORDER IS_NULLS_FIRST
----------- ---------------- ------------------ --------------
NAME                       1 TRUE               FALSE
```

<a id="c2ebdddcf744e75d"></a>
### `\{n}`

<a id="bd548562d6a85a3f"></a>
#### 구문

```
\number
```

<a id="7caee57b68bcf36b"></a>
#### 설명

[`\history`](#ad141bbb20a37ce0) 명령으로 조회할 수 있는 SQL 수행 이력 중에 number에 해당하는 구문을 수행한다.  
number 값은 [`\history`](#ad141bbb20a37ce0) 수행 결과의 ID 값이어야 한다.

<a id="cd8f5c619a77d847"></a>
#### 사용 예

다음은 `\history` 명령으로 수행한 SQL 구문을 수행하고 ID 값 1에 해당하는 DROP TABLE 구문을 수행하는 예이다.

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

<a id="0a689bc4cd07f2fe"></a>
### `\prepare sql`

<a id="d1ebb9906915c558"></a>
#### 구문

```
\prepare sql <sql_statement>
```

<a id="4eec8bc9564fd01e"></a>
#### 설명

&lt;sql_statement&gt;에 기술된 SQL 구문을 준비한다. 준비된 SQL 구문은 [`\exec`](#0f3949721f6b5ec3) 명령을 통해 반복적으로 수행할 수 있다.

`\prepare sql` 명령은 ODBC의 [SQLPrepare](../part-05-developer-manual/29-odbc.md#08f366baa3432305) 함수와 JDBC의 Connection::[prepareStatement](../part-05-developer-manual/30-jdbc.md#4040e7f9614cf855) 함수와 유사하게 동작한다.

<a id="70473aa0bc1ab9e7"></a>
#### 사용 예

다음은 SELECT 구문을 준비하고 반복적으로 수행하는 예이다.

- SELECT 구문을 준비한다.

```
gSQL> \prepare sql SELECT * FROM t1 WHERE id > 2;

SQL prepared.
```

- 준비된 SQL을 수행한다.

```
gSQL> \exec

ID NAME   ADDR         
-- ------ -------------
 3 xcom73 Inchon, Korea

1 row selected.

gSQL> INSERT INTO t1 VALUES ( 4, 'GOLDILOCKS', 'Better Place' );

1 row created.
```

- 준비된 SQL을 다시 수행한다.

```
gSQL> \exec

ID NAME   ADDR         
-- ------ -------------
 3 xcom73 Inchon, Korea
 4 goldilocks  Better Place 

2 rows selected.
```

<a id="828c84fc4aea1dd3"></a>
### `\print`

<a id="478ce82f8b3fe075"></a>
#### 구문

```
\print
\print variable
```

<a id="ab4d8d0a529e4fb0"></a>
#### 설명

다음과 같이 [`\var`](#5bdd58614174a2b3) 명령으로 선언한 호스트 변수 값을 조회한다. 호스트 변수 값이 설정되지 않은 경우 NULL 값을 가진다.

```
gSQL> \var v1 INTEGER
gSQL> \print v1

  V1
----
null
```

다음과 같이 호스트 변수 이름을 기술하지 않을 경우, 선언한 모든 호스트 변수의 값을 조회한다. 다음 예에서 VAR_ELAPSED_TIME_ 호스트 변수는 구문 수행시간을 관리하는 built-in 호스트 변수이다.

```
gSQL> \print

NAME               VALUE
------------------ -----
VAR_ELAPSED_TIME__  null
V1                    21
V2                    10
```

<a id="2edd1ee7b315e097"></a>
#### 사용 예

다음은 호스트 변수를 선언하고 호스트 변수에 값을 할당하고 이를 조회하는 예이다.

- 호스트 변수를 선언한다.

```
gSQL> \var v1 INTEGER
gSQL> \var v2 INTEGER
gSQL> \var v3 INTEGER
```

- 모든 호스트 변수를 조회한다.

```
gSQL> \print

NAME               VALUE
------------------ -----
VAR_ELAPSED_TIME__  null
V1                  null
V2                  null
V3                  null
```

- 호스트 변수에 값을 할당한다.

```
gSQL> \exec :v1 := 10
gSQL> \exec :v2 := 20
gSQL> \exec :v3 := :v1 + :v2
```

- v3 호스트 변수를 조회한다.

```
gSQL> \print v3

V3
--
30
```

- 모든 호스트 변수를 조회한다.

```
gSQL> \print

NAME               VALUE
------------------ -----
VAR_ELAPSED_TIME__  null
V1                    10
V2                    20
V3                    30
```

<a id="9e3cc316e0e9f7fb"></a>
### `\quit`

<a id="9e1516c380ea6594"></a>
#### 구문

```
\quit
\q
```

<a id="45e628b41383ead8"></a>
#### 설명

gsql을 종료한다.   
종료할 때 COMMIT 되지 않은 트랜잭션을 모두 COMMIT 한다.

<a id="ea671c47cc635539"></a>
#### 사용 예

```
gSQL> \quit

%
```

<a id="c5342131808a2378"></a>
### `\set autocommit`

<a id="ee238f77e2edd467"></a>
#### 구문

```
\set autocommit on
\set autocommit off
```

<a id="6c18c1a3193121c3"></a>
#### 설명

SQL 구문을 수행한 후에 자동으로 COMMIT 할지 여부를 설정한다.

- `\set autocommit on`
    - SQL 구문을 수행한 후에 자동으로 COMMIT 한다.
- `\set autocommit off`
    - SQL 구문을 수행한 후에 자동으로 COMMIT 하지 않는다.
- autocommit의 기본값은 OFF 이다.

<a id="be8d0e0324aaf0fc"></a>
#### 사용 예

다음은 AUTOCOMMIT 값을 ON으로 설정했을 때의 사용 예이다.

- autocommit을 on으로 설정한다.

```
gSQL> \set autocommit on
```

- INSERT 구문이 자동으로 COMMIT 된다.

```
gSQL> INSERT INTO t1 ( id, name, addr ) VALUES ( 1, 'leekmo', 'Seoul, Korea' );

1 row created.
```

- Rollback의 영향을 받지 않는다.

```
gSQL> ROLLBACK;

Rollback complete.

gSQL> SELECT * FROM t1;

ID NAME   ADDR        
-- ------ ------------
 1 leekmo Seoul, Korea

1 row selected.
```

다음은 AUTOCOMMIT 값을 OFF로 설정했을 때의 사용 예이다.

- autocommit을 off로 설정한다.

```
gSQL> \set autocommit off
```

- INSERT 구문을 수행한 후에 트랜잭션이 종료되지 않는다.

```
gSQL> INSERT INTO t1 ( id, name, addr ) VALUES ( 1, 'leekmo', 'Seoul, Korea' );

1 row created.
```

- 트랜잭션을 철회한다.

```
gSQL> ROLLBACK;

Rollback complete.
```

- INSERT 구문이 철회되어 결과가 없다.

```
gSQL> SELECT * FROM t1;

no rows selected.
```

<a id="9114076e891ca168"></a>
### `\set autotrace`

<a id="bf80ebc1957a664c"></a>
#### 구문

```
\set autotrace on
\set autotrace traceonly
\set autotrace off
```

<a id="1dd8f287a43d4187"></a>
#### 설명

실행 계획 출력 여부를 설정한다.

- `\set autotrace on`
    - SQL 구문을 수행하고 질의 결과와 함께 실행 계획을 출력한다.
- `\set autotrace traceonly`
    - SQL 구문을 수행하지 않고 질의 결과 없이 실행 계획을 출력한다.
- `\set autotrace off`
    - 실행 계획을 출력하지 않는다.
    - 기본값은 off 이다.

실행 계획에 대한 자세한 내용은 [SQL 실행 계획](../part-03-sql-manual/15-sql-tuning.md#f6556ce75bce767e)을 참조한다.

<a id="47b06896be4dba40"></a>
#### 사용 예

다음과 같이 ON과 함께 사용할 경우 SQL 구문을 수행하고 질의 결과와 함께 실행 계획을 출력한다.

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

다음과 같이 TRACEONLY를 사용할 경우 SQL 구문을 수행하지 않고 질의 결과 없이 실행 계획만 출력한다.

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

<a id="28ac515c7426a0ea"></a>
### `\set color`

<a id="43248432f2adb9e4"></a>
#### 구문

```
\set color on
\set color off
```

<a id="1239d485050d3d96"></a>
#### 설명

터미널 상에서 질의 결과의 각 row를 구별할 수 있도록 출력 결과의 색깔을 다르게 할지 여부를 설정한다.

- `\set color on`
    - Row 별로 출력 색깔을 다르게 한다.
- `\set color off`
    - Row 별 출력 색깔이 동일하다.
- color의 기본값은 OFF 이다.

각 row의 길이가 너무 길어서 터미널의 창을 넘어갈 경우 여러 줄에 걸쳐 출력된다. 이 경우, row와 row 를 구별하기 어려워서 가독성이 떨어지기 때문에 터미널에서의 가독성을 높이기 위해 이 구문을 사용한다.

<a id="93647e2d4d01d262"></a>
#### 사용 예

다음은 color 값을 ON으로 설정한 예이다.

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

<a id="b8a3227147bc77e2"></a>
### `\set colsize`

<a id="75efc3323ed715bb"></a>
#### 구문

```
\set colsize number
```

<a id="2d995c68e407277a"></a>
#### 설명

LONG VARCHAR, LONG VARBINARY 타입 데이터의 최대 출력 크기를 설정한다.

- colsize의 값은 1 ~ 104857600 (100M, LONG VARCHAR의 최대 크기) 범위의 양의 정수값이다.
- colsize의 기본값은 8192이다.

LONG VARCHAR column은 문자열 길이가 길기 때문에 다음과 같은 질의 수행 결과의 가독성이 떨어진다. 이 때, colsize를 줄여 LONG VARCHAR column의 가독성을 높이거나, colsize를 크게 하여 원하는 길이만큼 출력할 수 있다.

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
     

... 중략 ...


                                                  WHERE      , pvcol.GRANTOR_ID                                                         
     , pvcol.GRANTEE_ID                                                         
     , pvcol.PRIVILEGE_TYPE_ID                                                  
                                                                                

3 rows selected.
```

<a id="475c32a02d023379"></a>
#### 사용 예

다음은 colsize를 줄여 LONG VARCHAR column의 출력 가독성을 높이는 예이다.

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

<a id="84305527a9268b5f"></a>
### `\set ddlsize`

<a id="0c00e3b3a7aced25"></a>
#### 구문

```
\set ddlsize number
```

<a id="1a407a4db1c692fe"></a>
#### 설명

다음 명령을 통해 DDL을 출력할 때 구문을 출력할 버퍼의 크기를 설정한다.

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

- ddlsize 값은 1 ~ 10485760 (10M) 범위의 양의 정수값이다.
- ddlsize의 기본값은 10000 이다.

다음과 같이 버퍼 공간 부족으로 인한 에러가 발생할 경우, ddlsize 값을 증가시켜 DDL 구문을 출력할 수 있다.

```
gSQL> \set ddlsize 1000
gSQL> \ddl_view dictionary_schema.all_tables

ERR-HY000(40052): not enough DDLSIZE. 
use command: \set ddlsize {n} 

gSQL> \set ddlsize 100000
gSQL> \ddl_view dictionary_schema.all_tables


SET SESSION AUTHORIZATION "SYS"; 
CREATE OR REPLACE FORCE VIEW "DICTIONARY_SCHEMA"."ALL_TABLES" 

... 중략 ...
```

<a id="78aee42dbe6bccfe"></a>
#### 사용 예

다음은 ddlsize를 변경하는 예이다.

```
gSQL> \set ddlsize 100000
gSQL>
```

<a id="c8ff78168c631446"></a>
### `\set error`

<a id="8a476e0c2d39eca2"></a>
#### 구문

```
\set error on
\set error off
```

<a id="e61d9d19c4f6812f"></a>
#### 설명

에러 메시지 출력 여부를 설정한다.

- `\set error on`
    - 에러 메시지를 출력한다.
- `\set error off`
    - 에러 메시지를 출력하지 않는다.
- error의 기본값은 ON 이다.

SQL 구문을 수행할 때 에러가 발생하면 gsql은 다음과 같은 정보를 출력한다.

- SQLSTATE: SQL 표준 상태 코드
- 에러 코드: GOLDILOCKS 에러 코드
- 에러 메시지

다음 예에서 SQL 구문에 에러가 발생하였고 ERR-42000(16040)에서 42000이 SQLSTATE 값이며 에러 코드는 ( ) 안의 16040 이다.

```
gSQL> SELECT * FROM invalid_table;

ERR-42000(16040): table or view does not exist : 
SELECT * FROM invalid_table
              *
ERROR at line 1:
```

<a id="ae9e789395e50c6c"></a>
#### 사용 예

다음은 에러 메시지를 출력하지 않도록 설정하는 예이다.

- 에러 메시지를 출력하지 않도록 한다.

```
gSQL> \set error off
```

- SQLSTATE 값과 에러 코드만 출력한다.

```
gSQL> SELECT * FROM invalid_table;

ERR-42000(16040)
```

<a id="4686267060d45f6d"></a>
### `\set heading`

<a id="7271b27ab4d57ab8"></a>
#### 구문

```
\set heading {ON|OFF}
```

<a id="6c8a94a4eb9ae2b9"></a>
#### 설명

질의 결과에 헤더를 출력할지 여부를 결정한다.

<a id="07155e94718de4ae"></a>
#### 사용 예

- 헤더 메시지를 출력하지 않도록 한다.

```
gSQL> \set heading off
```

- 다음은 질의 결과에 헤더 메시지를 출력하지 않는 예이다.

```
gSQL> select * from dual;

X    

1 row selected.
```

<a id="6b3b3355aea3daf4"></a>
### `\set history`

<a id="6499614076bb899b"></a>
#### 구문

```
\set history number
```

<a id="b75b8b0972edf047"></a>
#### 설명

이력 정보를 관리할 SQL 구문의 개수를 설정한다.

- history 값은 1 ~ 100000 범위의 양의 정수값이다.
- history 값을 음수로 설정하면 모든 SQL 이력을 제거한다.
- history의 기본값은 128이다.

history 값이 줄어들면 오래된 SQL 구문을 제거한다.  
history 정보는 [`\\`](#4c1575265582051a) 명령이나 [`\{n}`](#c2ebdddcf744e75d) 명령을 통해 이전에 수행한 SQL 구문을 다시 수행하려 할 때 사용한다.

<a id="d4a25c53180dbde8"></a>
#### 사용 예

다음은 history 개수를 100으로 설정하는 예이다.

```
gSQL> \set history 100
gSQL>
```

다음은 저장되어 있는 SQL 구문의 개수보다 history 개수를 작게 설정하는 예이다.

- 다섯 개의 SQL 구문이 저장되어 있다.

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

- history 값을 3으로 줄인다.

```
gSQL> \set history 3
```

- 세 개의 SQL 구문이 저장되어 있다.

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

다음은 history에 저장된 모든 SQL 이력을 제거하는 예이다.

```
gSQL> \history

ID SQL                      
-- -------------------------
 1 SELECT * FROM dual       
 2 SELECT * FROM user_tables
```

- 음수값을 이용해 모든 SQL 이력을 제거한다.

```
gSQL> \set history -1

gSQL> \history
gSQL>
```

<a id="8654bfd6f1680424"></a>
### `\set linesize`

<a id="afe76330f4479fe6"></a>
#### 구문

```
\set linesize number
```

<a id="549d724cd25be3bf"></a>
#### 설명

질의 결과 출력할 때 한 line의 최대 크기를 설정한다.

- linesize 값은 1 ~ 10000 범위의 양의 정수값이다.
- linesize의 기본값은 80 이다.

질의 결과를 출력할 때 한 row는 하나의 line을 기준으로 출력된다. Row의 column 개수가 많거나 출력 길이가 linsize 보다 클 경우 다음 예와 같이 여러 line에 걸쳐 출력되기 때문에 가독성이 떨어진다.

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

이 경우, linesize 값을 변경하여 하나의 row가 하나의 line에 출력되도록 제어할 수 있다.

<a id="05a001b978d3b284"></a>
#### 사용 예

다음은 linesize를 크게 설정하여 가독성을 높이는 예이다.

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

<a id="fb05859baf125d50"></a>
### `\set numsize`

<a id="aeead70f5ff259b4"></a>
#### 구문

```
\set numsize number
```

<a id="a03f406926a54f8d"></a>
#### 설명

숫자값 출력을 위한 최대 digit 개수를 설정한다.

- numsize 값은 1 ~ 50 범위의 양의 정수값이다.
- numsize의 기본값은 20 이다.

다음과 같이 숫자값의 digit 개수가 numsize의 범위를 벗어나는 경우 exponent 형태로 출력된다.

```
gSQL> SELECT num, ( num * num ) AS result FROM t1;

          NUM               RESULT
------------- --------------------
1234567890123 1.52415787532276E+24

1 row selected.
```

이런 숫자값을 exponent 형태가 아닌 숫자로 모두 표현하고자 할 때 numsize 값을 변경하여 출력할 수 있다.

<a id="c1cf843af4050851"></a>
#### 사용 예

다음은 numsize를 크게 설정하여 숫자의 모든 digit를 출력하는 예이다.

```
gSQL> \set numsize 50
gSQL> SELECT num, ( num * num ) AS result FROM t1;

          NUM                    RESULT
------------- -------------------------
1234567890123 1524157875322755800955129

1 row selected.
```

<a id="72d51f9c7e68284b"></a>
### `\set pagesize`

<a id="8cf28fe7c0184e41"></a>
#### 구문

```
\set pagesize number
```

<a id="ef4a1fb536997384"></a>
#### 설명

한 page 단위로 구성할 row의 개수를 설정한다.

- pagesize 값은 1 ~ 10000 범위의 양의 정수값이다.
- pagesize의 기본값은 20 이다.

질의 결과로 출력되는 row의 개수가 많거나 특정 개수 단위로 page를 구성하고자 할 때 설정한다.

<a id="1ee378a5c362dc7b"></a>
#### 사용 예

다음은 10 개의 row 단위로 하나의 page를 구성하는 예이다.

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

<a id="1d087da5cc539621"></a>
### `\set serveroutput`

<a id="f2cc99badd31f5c9"></a>
#### 구문

```
\set serveroutput on
\set serveroutput off
```

<a id="130a9bf40cc33b71"></a>
#### 설명

gsql이나 gsqlnet에서 DBMS_OUTPUT Package에서 제공하는 함수들에 의해 씌여진 메시지들을 자동으로 출력하는 기능을 제어한다.

- `\set serveroutput on`
    - SQL을 수행한 후에 DBMS_OUTPUT.PUT_LINE이 서버에 축적한 메시지를 자동으로 출력한다.
- `\set serveroutput off`
    - DBMS_OUTPUT package를 사용하지 않는다.
- serveroutput의 기본값은 OFF 이다.

기본적으로 서버에 축적할 수 있는 메시지의 최대 크기는 20000 byte 이다.

<a id="8d781db675e7a5e5"></a>
#### 사용 예

다음은 SQL 구문에서 사용된 user-defined function에서 축적한 메시지를 출력하는 예이다.

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

<a id="1505d55ddcb6ffa9"></a>
### `\set time`

<a id="8f7b8d645ab2d4f4"></a>
#### 구문

```
\set time on
\set time off
```

<a id="6b7c078792122a79"></a>
#### 설명

현재 시간의 출력 여부를 설정한다.

- `\set time on`
    - 현재 시간을 출력한다.
- `\set time off`
    - 현재 시간을 출력하지 않는다.
- time의 기본값은 OFF 이다.

<a id="f38b49388284840c"></a>
#### 사용 예

다음은 현재 시간을 출력하는 예이다.

```
gSQL> \set time on
12:45:34 gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.

Elapsed time: 0.07600 ms
```

<a id="ef371f8fc5832f3c"></a>
### `\set timing`

<a id="32c1e4c655ab1f39"></a>
#### 구문

```
\set timing on
\set timing off
```

<a id="3c674e342c4aadaf"></a>
#### 설명

SQL 구문 수행시간의 출력 여부를 설정한다.

- `\set timing on`
    - 수행시간을 출력한다.
- `\set timing off`
    - 수행시간을 출력하지 않는다.
- timing의 기본값은 OFF 이다.

수행시간의 단위는 ms (millisecond) 이다.

<a id="21683cc6268e185d"></a>
#### 사용 예

다음은 SQL 구문의 수행 시간을 출력하는 예이다.

```
gSQL> \set timing on
gSQL> SELECT * FROM dual;

DUMMY
-----
X    

1 row selected.

Elapsed time: 0.07600 ms
```

<a id="e88795a4ee13cd81"></a>
### `\set vertical`

<a id="0713d10d29a2e8e4"></a>
#### 구문

```
\set vertical on
\set vertical off
```

<a id="31714758d5d76dd5"></a>
#### 설명

Column 값을 line 단위로 출력할지 여부를 설정한다.

- `\set vertical on`
    - Column을 line 단위로 출력한다.
- `\set vertical off`
    - Row를 line 단위로 출력한다.
- vertical의 기본값은 OFF 이다.

각 row가 개별적인 정보를 가지고 있는 경우, 질의 출력 결과를 column 단위로 출력하여 가독성을 높일 수 있다.

`\set vertical on`으로 설정할 경우, 각 row는 빈 줄로 구분되며 하나의 line은 하나의 값을 표현하고 다음과 같은 형태로 구성된다.

```
column 이름 # 데이터 값
```

<a id="530ba2f3e951afee"></a>
#### 사용 예

다음은 질의 결과를 column 단위로 출력하는 예이다.

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

<a id="ecc902a1a812dd0f"></a>
### `\shutdown`

<a id="a662e52d1bec3e89"></a>
#### 구문

```
\shutdown
\shutdown abort
\shutdown immediate
\shutdown transactional
\shutdown normal
```

<a id="8a6025d8e7811a1e"></a>
#### 설명

GOLDILOCKS 서버를 종료한다.  
`\shutdown` 명령을 수행하려면 SYSDBA 또는 ADMIN role로 접속해야 한다. SYSDBA로 접속하는 방법은 [서버 구동 및 종료](#1b5d02a17418ebcf)를 참조한다.

- `\shutdown normal`
    - 새로운 session의 접속을 차단하고 현재 접속된 모든 session이 종료될 때까지 기다린 후, checkpoint를 수행하고 서버를 종료한다.
- `\shutdown transactional`
    - 새로운 transaction의 시작을 차단하고 현재 수행 중인 transaction들이 종료될 때까지 기다린 후, checkpoint를 수행하고 서버를 종료한다.
- `\shutdown immediate`
    - 새로운 단위 연산 (예: FETCH, EXECUTE)의 수행을 차단하고 현재 수행 중인 모든 단위 연산이 종료될 때까지 기다린 후, 모든 transaction들을 rollback 하고, checkpoint를 수행하고 서버를 종료한다.
- `\shutdown abort`
    - 접속 중인 session들의 상태와 관계없이 바로 서버를 강제 종료한다.
- `\shutdown`
    - `\shutdown normal`과 동일하다.

<a id="659944d53417f6a7"></a>
#### 사용 예

다음은 GOLDILOCKS를 종료하는 예이다.

```
% gsql sys gliese --as sysdba

Connected to GOLDILOCKS Database.

gSQL> \shutdown

Shutdown success

gSQL>
```

<a id="ab855d85ea887c89"></a>
### `\spool`

<a id="1ef8a7fb648b048d"></a>
#### 설명

gsql을 사용하여 출력되는 모든 결과를 terminal과 file에 기록한다.

<a id="e997ee5f64c30ab0"></a>
#### `\spool 'filename'`

<a id="17248e183893cbf3"></a>
##### 구문

```
\spool 'filename' [CREATE | REPLACE | APPEND]
\spo   'filename' [CREATE | REPLACE | APPEND]
```

<a id="8ba7f51d8d6746b4"></a>
##### 설명

Spool 기능을 시작한다. 이 구문이 실행된 이후부터 gsql에서 수행된 모든 출력 결과가 주어진 *filename*에 기록된다.

다음 option들은 file을 open하는 방법을 기술한다.

- CREATE: File을 새로 생성한다. 기존 file이 있을 경우, 에러가 발생한다.
- REPLACE: 기존 file의 내용을 삭제하고 새로 기록을 시작한다. 만약 기존 file이 없을 경우, CREATE와 동일하게 동작한다.
- APPEND: 기존 file의 가장 뒷부분에 이어서 내용을 기록한다. 만약 기존 file이 없을 경우, CREATE와 동일하게 동작한다.

만약 이런 option이 주어지지 않았을 경우, 기본적으로 REPLACE 모드로 동작한다.

> Spool 기능이 동작하는 도중에 새로운 spool이 시작되면 기존의 spool은 종료되고 새 spool이 시작된다.

<a id="e6f0d3106003c47d"></a>
##### 사용 예

다음은 spool 기능을 시작하는 예이다.

- result.txt file을 생성하여 gsql 실행 결과를 기록한다.

```
gSQL> \SPOOL 'result.txt' CREATE
gSQL> SELECT * FROM T1 WHERE C1 < 10;
gSQL> \SPOOL OFF
```

- 기존 result.txt file의 뒷부분에 결과를 이어서 기록한다.

```
gSQL> \SPOOL 'result.txt' APPEND
gSQL> SELECT * FROM T1 WHERE C1 >= 10;
gSQL> \SPOOL OFF
```

- 기존 result.txt file의 내용을 삭제하고 새로 결과를 기록한다.

```
gSQL> \SPOOL 'result.txt' REPLACE
gSQL> SELECT * FROM T1;
gSQL> \SPOOL OFF
```

<a id="7f7b8058d3739681"></a>
#### `\spool OFF`

<a id="2225ab1df395e2c0"></a>
##### 구문

```
\spool OFF
\spo   OFF
```

<a id="f886081e67014524"></a>
##### 설명

현재 spool을 종료한다. 만약 spool을 사용하고 있는 중이 아니라면 아무런 동작도 일어나지 않는다.

<a id="209b49f1f34e697b"></a>
##### 사용 예

다음은 spool을 시작한 뒤에 종료하는 예이다.

```
gSQL> \SPOOL 'result.txt'
gSQL> SELECT * FROM T1;
```

- Spool 종료

```
gSQL> \SPOOL OFF
```

<a id="250af8e5107c1e77"></a>
#### `\spool`

<a id="3cf2bb8ea3153ab8"></a>
##### 구문

```
\spool
\spo
```

<a id="1b3d6be66aef538b"></a>
##### 설명

현재 spool 상태를 나타낸다. Spool을 사용하는 중이라면 어떤 file이 spool 중인지 알려주고, spool을 사용하고 있지 않은 경우에는 spool을 사용하고 있지 않다는 사실을 알린다.

<a id="0a44430669fbd10c"></a>
##### 사용 예

다음은 gsql 이력에 저장된 SQL 구문을 편집하는 예이다.

```
gSQL> \SPOOL 'a.txt'
```

- a.txt에 spool 중이라는 사실을 알린다.

```
gSQL> \SPOOL
 
currently spooling to a.txt
 
gSQL> \SPOOL OFF
```

- 현재 spool을 사용하고 있지 않다는 사실을 알린다.

```
gSQL> \SPOOL
 
not spooling currently
```

<a id="6745e7877cd84787"></a>
### `\startup`

<a id="356311b72593ebe8"></a>
#### 구문

```
\startup
\startup nomount
\startup mount
\startup open
```

<a id="f6c2ef6143f9e3f8"></a>
#### 설명

GOLDILOCKS 서버를 구동한다.  
`\startup` 명령을 수행하려면 SYSDBA 또는 ADMIN role로 접속해야 한다. SYSDBA로 접속 방법은 [서버 구동 및 종료](#1b5d02a17418ebcf)를 참조한다.

- `\startup nomount`
    - 서버를 NOMOUNT 단계로 시작한다.
- `\startup mount`
    - 서버를 MOUNT 단계로 시작한다.
- `\startup open`
    - 서버를 OPEN 단계로 시작한다.
- `\startup `
    - `\startup open`과 동일하다.

서버의 구동 단계는 NOMOUNT, MOUNT, OPEN 단계로 구분되며 자세한 내용은 [다단계 시작](../part-02-administration-manual/5-goldilocks-데이터베이스-관리-기본.md#324d293a99dd4a23)을 참조한다.   
`\startup` 명령을 수행한 후에 다음 단계로 전이하려면 [ALTER SYSTEM {MOUNT | OPEN} DATABASE](../part-03-sql-manual/18-sql-references.md#f9fc4d123ed9181c)를 참조한다.

<a id="b40820316997b201"></a>
#### 사용 예

다음은 GOLDILOCKS를 구동하는 예이다.

```
% gsql sys gliese --as sysdba

Connected to an idle instance.

gSQL> \startup

Startup success
```

<a id="5bdd58614174a2b3"></a>
### `\var`

<a id="7013e6f4dedf0bdc"></a>
#### 구문

```
\var variable_name data_type
```

<a id="9fb298552eec8a3c"></a>
#### 설명

호스트 변수를 선언한다.  
variable_name과 동일한 호스트 변수가 선언되어 있을 경우, 기존의 호스트 변수를 삭제하고 새로 선언한다. variable_name의 최대 길이는 128 byte 이다.  
호스트 변수의 data_type은 GOLDILOCKS의 데이터 타입과 동일한데 자세한 내용은 [Data Type](../part-03-sql-manual/11-sql-elements.md#2ec7b2e6f23b520c)을 참조한다.  
호스트 변수는 [`\exec :var := value`](#374539d536d0872d) 명령을 이용하여 값을 대입하며, [`\print`](#828c84fc4aea1dd3) 명령을 통해 값을 조회할 수 있다.

```
gSQL> \var v1 INTEGER
gSQL> \exec :v1 := 1
gSQL> \print v1

V1
--
 1
```

호스트 변수는 SQL 구문의 입력 또는 출력 인자로 사용할 수 있으며 SQL 구문이나 [`\exec :var := value`](#374539d536d0872d) 명령에서 사용할 때는 colon (:) 기호를 호스트 변수 앞에 붙여 호스트 변수임을 명시해야 한다.

<a id="2f15fb44e809b9f8"></a>
#### 사용 예

다음은 호스트 변수를 선언하고 SQL 구문의 입력 인자로 사용하는 예이다.

```
gSQL> \var v1 INTEGER
gSQL> \exec :v1 := 1
gSQL> SELECT * FROM t1 WHERE id = :v1;

ID NAME   ADDR        
-- ------ ------------
 1 leekmo Seoul, Korea

1 row selected.
```

다음은 호스트 변수를 SQL 구문의 출력 인자로 사용하는 예이다.

```
gSQL> \var v_name VARCHAR(128)
gSQL> SELECT name INTO :v_name FROM t1 WHERE id = 1;

V_NAME
------
leekmo

1 row selected.
```

다음은 호스트 변수를 선언하고 SQL 구문의 입력과 출력 인자로 사용하는 예이다.

[UPDATE name RETURNING .. INTO](../part-03-sql-manual/18-sql-references.md#422b753d8ea6394c) 구문을 수행하는 다음 예에서 SET 절과 WHERE 절의 호스트 변수 :v_id 는 입력 인자로 사용되었으며 INTO 절의 :v_id는 출력 인자로 사용되었다.

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

[← 36. glsnr](36-glsnr.md) · [전체 목차](../README.md) · [38. gloader/gloadernet (Upload/download Tool) →](38-gloader-gloadernet-upload-download-tool.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
