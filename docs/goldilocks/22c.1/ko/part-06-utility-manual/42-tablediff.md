<a id="e793c00156e345ae"></a>

# 42. tablediff

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/e793c00156e345ae)  
> 태그: `22c.1_10_tag`

[← 41. gdump](41-gdump.md) · [전체 목차](../README.md) · [43. gsyncher →](43-gsyncher.md)

<a id="49d2f7fee381240a"></a>
## tablediff 개요

<a id="087d51f2b728bd1b"></a>
### 배경

GOLDILOCKS 시스템 운영자는 예상치 못한 장애로 인해 cyclone이나 LogMirror 툴로 동기화된 GOLDILOCKS의 두 테이블의 동기화가 어긋나는 경우에 대비할 필요가 있다. 동기화가 어긋났다는 것은 특정 row가 한 쪽 테이블에만 존재하거나 row의 column 내용 일부가 서로 다른 경우를 말한다. 혹은 이런식으로 동기화가 어긋나지 않았더라도 cyclone과 LogMirror는 테이블의 동기화 여부를 알려주지 않기 때문에 운영 시간을 피해서 테이블의 동기화 여부를 검증하고 비동기화된 row에 대한 동기화를 수행해야 한다.

<a id="a68ca5c6f9b67e7b"></a>
### 기능

tablediff는 CDC 등의 툴로 동기화된 GOLDILOCKS의 두 테이블을 row 단위로 비교하는 툴이다. 특정 row가 한 테이블에만 있거나 row의 내용이 다를 경우 리포팅하고 동기화 해준다. 각종 동작을 제어할 수 있는 설정 파일을 입력받고 비동기 row를 알리는 log 파일과 동기화 수행 결과를 알려주는 log 파일을 출력한다.

두 테이블의 스키마는 동일해야 하며 primary key를 반드시 포함하고 있어야 한다는 제약 조건이 있다. 실시간으로 테이블의 내용이 갱신될 수 있으므로 현재 트랜잭션이 발생하고 있는 테이블에 대해 이 툴을 수행하는 것은 권장하지 않는다. 다만 조회 (SELECT 구문)가 발생하고 있을 때는 문제가 되지 않는다. 이 툴은 GOLDILOCKS의 테이블에 대해서만 사용할 수 있다.

이 툴은 TableDiff와 TableSync라는 두 개의 실행 명령어를 가진다.

<a id="7cdedf0d9b7f8115"></a>
#### TableDiff

```
java sunje.goldilocks.tool.diff.TableDiff [configure file]
```

TableDiff 프로그램은 두 테이블의 비동기화 여부를 검증하고 옵션에 따라 비동기 row를 즉시 동기화하거나 동기화를 나중에 수행할 수 있도록 동기화 정보 (binary 파일)를 남기도록 할 수 있다. 즉시 동기화하는 thread는 다중으로 실행되도록 할 수 있다.

<a id="add523e99379df9d"></a>
#### TableSync

```
java sunje.goldilocks.tool.diff.TableSync [configure file]
```

TableSync 프로그램은 앞서 TableDiff가 남긴 동기화 정보를 이용하여 동기화를 수행한다. (Row 비교 작업은 하지 않는다.) 멀티 thread를 구동하여 동시에 진행할 수 있다.

> TableDiff에서 남긴 bin 파일에는 configure 파일이 적용되지 않은 두 table의 비동기화된 row가 저장되어 있는데 TableSync에서는 이 bin 파일을 이용하여 두 table을 강제로 동기화한다.

<a id="35396d60914de823"></a>
### 특징

이 툴은 Java 프로그램으로써 jar 파일 형태로 제공된다. 따라서 java(1.6)가 있어야 수행할 수 있다. 또한 GOLDILOCKS JDBC 드라이버를 사용하기 때문에 goldilocks6.jar가 필요하다. TCP/ IP로 GOLDILOCKS에 접속하기 때문에 원격으로 실행할 수 있고 독자적인 프로토콜을 사용하여 JDBC나 ODBC로 테이블을 검증하는 것보다 훨씬 빠르게 실행된다.

Row 비교 작업과 동기화 작업은 멀티 thread로 동시에 작업할 수 있다. Row 비교 작업을 다중화하기 위해서는 테이블의 key의 범위를 균등하게 나누는 작업을 수동으로 해줘야 한다. 사용자가 열 개의 범위로 나눠주면 (설정 파일에 정의할 수 있다.) 열 개의 thread가 테이블 비교 작업을 수행한다. 이에 반해 동기화 작업은 지정된 thread 개수만큼의 thread로 수행된다.

<a id="0aac3e04790a6694"></a>
### 파일 구성

tablediff 프로그램은 $GOLDILOCKS_HOME/bin/tablediff.jar라는 단 하나의 파일로 구성된다. 실행하려면$GOLDILOCKS_HOME/lib/goldilocks6.jar 파일도 필요하다. 그리고 입력 인자로 설정 파일이 필요한데 $GOLDILOCKS_DATA/conf/tablediff.conf 샘플 파일을 참조하면 된다.

<a id="5c0d177fd018df00"></a>
## 사용법

<a id="44a6f62c0fbf3b65"></a>
### 커맨드 사용법

tablediff는 Java 프로그램이기 때문에 Java (JRE 1.6 또는 JDK1.6)가 필요하다. tablediff.jar 파일과 goldilocks6.jar 파일을 CLASSPATH에 포함시키거나 Java의 -classpath 옵션으로 지정해주면 된다. 다음과 같은 커맨드로 tablediff 프로그램을 구동할 수 있다.

```
export CLASSPATH=$CLASSPATH:$GOLDILOCKS_HOME/bin/tablediff.jar:$GOLDILOCKS_HOME/lib/goldilocks6.jar
java sunje.goldilocks.tool.diff.TableDiff [configure file]
```

또는

```
java -classpath $GOLDILOCKS_HOME/bin/tablediff.jar:$GOLDILOCKS_HOME/lib/goldilocks6.jar sunje.goldilocks.tool.diff.TableDiff [configure file]
```

다음은 간단한 샘플 테이블에 대해 TableDiff를 실행한 결과이다.

```
gSQL> create table tab1 ( c1 integer primary key, c2 char(10) );
gSQL> create table tab2 ( c1 integer primary key, c2 char(10) );
gSQL> insert into tab1 values ( 1, 'HELLO');
gSQL> insert into tab2 values ( 1, 'HELLO');
gSQL> insert into tab1 values ( 2, 'WORLD');
gSQL> insert into tab2 values ( 2, 'world');
gSQL> insert into tab1 values ( 3, 'good');
gSQL> insert into tab2 values ( 4, 'good');
gSQL> commit;


shell> java sunje.goldilocks.tool.diff.TableDiff tablediff.conf
Total 4 rows processed
  > row diff            : 1, update target(success/failure): 1/0
  > key diff source only: 1, insert into target(success/failure): 1/0
  > key diff target only: 1, delete from target(success/failure): 1/0
TableDiff completed
elapsed time = 0.229 sec
```

- tablediff.conf의 내용

```
SOURCE_URL      = jdbc:goldilocks://127.0.0.1:22581/test
SOURCE_USER     = TEST
SOURCE_PASSWORD = test
SOURCE_SCHEMA   = PUBLIC
SOURCE_TABLE    = TAB1

TARGET_URL      = jdbc:goldilocks://127.0.0.1:22581/test
TARGET_USER     = TEST
TARGET_PASSWORD = test
TARGET_SCHEMA   = PUBLIC
TARGET_TABLE    = TAB2

OPERATION       = SYNC
TARGET_INSERT = ON
TARGET_UPDATE = ON
TARGET_DELETE = ON
SOURCE_INSERT = OFF
```

<a id="6096c5d21cfb0a09"></a>
### Property Option

tablediff의 설정 파일에서 사용할 수 있는 옵션들을 설명한다.

<a id="69fb1f7eccbcb40d"></a>
#### SOURCE, TARGET 테이블 설정 옵션

이들은 source와 target 테이블을 정의하는 옵션들로써 반드시 정의되어야 한다. Source와 target은 각각 비교 대상이 되는 테이블을 지칭한다.

- SOURCE_URL: Source 테이블이 존재하는 GOLDILOCKS의 JDBC connection URL이다.
- SOURCE_USER: Source 테이블이 존재하는 GOLDILOCKS의 계정이다.
- SOURCE_PASSWORD: Source 테이블이 존재하는 GOLDILOCKS 계정의 password이다.
- SOURCE_SCHEMA: Source 테이블의 스키마이다.
- SOURCE_TABLE: Source 테이블 이름이다.
- TARGET_URL: Target 테이블이 존재하는 GOLDILOCKS의 JDBC connection URL이다.
- TARGET_USER: Target 테이블이 존재하는 GOLDILOCKS의 계정이다.
- TARGET_PASSWORD: Target 테이블이 존재하는 GOLDILOCKS 계정의 password이다.
- TARGET_SCHEMA: Target 테이블의 스키마이다.
- TARGET_TABLE: Target 테이블 이름이다.

다음 예제를 참조한다.

```
SOURCE_URL      = jdbc:goldilocks://192.168.0.100:22581/test
SOURCE_USER     = TEST
SOURCE_PASSWORD = test
SOURCE_SCHEMA   = PUBLIC
SOURCE_TABLE    = T1

TARGET_URL      = jdbc:goldilocks://192.168.0.101:22581/test
TARGET_USER     = TEST
TARGET_PASSWORD = test
TARGET_SCHEMA   = PUBLIC
TARGET_TABLE    = T2
```

<a id="51fa682980512761"></a>
#### Operation

TableDiff의 동작을 결정한다. DIFF로 동작하면 동기화 정합성 검증만 수행하여 결과를 알리고, SYNC로 동작하면 정합성을 검증하면서 동기화 작업을 함께 수행한다.

DIFF로 동작하면 (DIFF_BIN_FILE 속성으로 명시한 파일명으로) 정합성 결과 파일이 생성되는데 이 파일을 가지고 TableSync를 수행할 수 있다.

<a id="33850f23bd55c1f4"></a>
#### 동기화 정책 설정

다음과 같이 동기화 정책을 제어하는 네 가지 속성이 있다. 모두 ON이나 OFF 값을 가질 수 있다.

- TARGET_INSERT: Source에 있는 key가 target에 없으면 target에 그 key를 삽입한다.
- TARGET_UPDATE: Key가 아닌 column의 내용이 다르면 target의 row를 갱신한다.
- TARGET_DELETE: Source에 없는 key가 target에 있으면 target의 row를 삭제한다.
- SOURCE_INSERT: Source에 없는 key가 target에 있으면 source에 그 row를 삽입한다.

> TARGET_DELETE와 SOURCE_INSERT가 모두 ON일 수는 없다.

<a id="3118aaa6cf044e54"></a>
#### EXCLUDED_COLUMNS

비교 대상에서 제외할 column을 명시한다. 콤마 (,)를 구분자로 사용하여 column 이름을 명시하면 된다. Key column은 제외할 수 없다.

<a id="20594cd448652c43"></a>
#### WHERE_CLAUSE

테이블의 비교 대상 row에 대한 조건을 설정할 수 있다. 예를 들어 WHERE_CLAUSE = SALARY >= 1000000 이라고 명시하면 테이블의 row 중에 SALARY column 값이 1,000,000 이상인 row들에 대해서만 정합성 검사가 이루어진다.

<a id="80027a534dd052c3"></a>
#### DISPLAY_ROW_UNIT

TableDiff 프로그램은 테이블 비교 작업의 진행 상황을 표시하는데 특정 개수의 row를 처리할 때마다 콘솔로 몇 개의 row가 처리되었는지 출력한다. 이 속성은 몇 개의 row마다 출력할 것인지를 설정한다. 기본값은 100,000인데 생략할 수 있다.

<a id="751cc926b34c2c52"></a>
#### SYNC_OUT_FILE

동기화 결과를 기록할 파일 이름을 설정한다. 정의되지 않으면 tablesync.log에 기록한다. 만일 동기화 thread가 여러 개인 경우, 파일 이름 뒤에 숫자가 붙는다.

<a id="f378ba9977185d52"></a>
#### DIFF_OUT_FILE

Row 불일치 결과를 기록할 파일 이름을 설정한다. 정의되지 않으면 tablediff.log에 기록한다. 이 파일은 사람이 읽을 수 있는 텍스트 파일 형태이다.

<a id="e8b6f3ac39882c64"></a>
#### DIFF_BIN_FILE

OPERATION 속성을 DIFF로 설정하면 TableDiff는 동기화 정보 파일을 남기는데 이 속성이 정의한 파일명으로 남긴다. TableSync는 이 파일을 입력 인자로 사용한다.

<a id="9ab9c3d4428f6184"></a>
#### PROPAGATE_REDO_LOG

Row 동기화 작업 로그를 다른 복제 서버에 전파할지 여부를 결정한다. 기본값은 OFF 이다.

<a id="332332ce1be6e1cb"></a>
#### LOGGING_ON_SUCCESS

Row 동기화 작업을 할 때 사용한 DML (INSERT, UPDATE, DELETE)이 성공했을 경우에도 기록을 남길 것인지 여부를 설정한다. 기본값은 OFF 이며 이 값이 설정되어 있으면 동기화 작업 속도가 떨어진다. DML이 실패할 경우에는 이 속성과 관계없이 로깅 정보를 남긴다.

<a id="1d3e4c33bb5ae62e"></a>
#### LOGGING_ON_DIFF

Row 정합성을 비교하여 불일치가 발생했을 때 로깅을 남길 것인지 여부를 설정한다. 기본값은 OFF 이다.

<a id="ac1fe6148e17e389"></a>
#### JOB_QUEUE_SIZE

Row 동기화 작업은 작업 thread들에 의해 이루어지는데 동기화 작업 thread들은 JOB QUEUE에 들어온 작업들을 하나씩 가져가서 작업을 수행한다. JOB QUEUE에 작업을 넣는 thread는 TableDiff나 TableSync의 메인 thread인데 동기화 thread의 작업 속도가 더디면 JOB QUEUE가 가득차게 된다.   
JOB_QUEUE_SIZE 속성은 JOB QUEUE의 크기를 결정하는데 이 값이 크면 queue가 가득차는 경우는 자주 발생하지 않겠지만 메모리를 많이 사용하게 된다. 기본값은 100인데 100 정도면 queue가 가득차지 않은 상태로 사용할 수 있다.  
이 속성은 특별한 경우가 아니면 바꾸지 않는 것이 좋다.

<a id="50338f0899449f48"></a>
#### JOB_THREAD

동기화 작업 thread 수를 지정한다. 정의하지 않을 경우, 기본값은 1이다. 동기화 할 row가 많을 경우 CPU의 개수를 고려하여 이 값을 적당한 수로 지정하는게 좋다. 당연히 이 값이 클수록 동기화 속도가 빨라진다.

<a id="68d7493288087ea1"></a>
#### JOB_UNIT_SIZE

동기화 작업은 이 속성이 명시한 크기만큼 batch job으로 수행한다. 기본값은 100이다.

<a id="a1d393ec25a83444"></a>
#### DISPLAY_CALL_STACK

에러가 발생할 경우, call stack을 표시할 것인지 여부를 설정한다. 기본값은 OFF 이다.

<a id="8a7aa72f645b1d5a"></a>
#### 테이블 비교의 다중화 설정

일반적으로 TableDiff의 row 비교 작업은 단일 thread로 수행된다. 하지만 조건절을 명시하면 여러 thread로 비교 작업을 수행할 수 있다. 속성 이름을 PARTITION_RANGE[n]으로 하여 n 개의 속성에 대해 WHERE 조건절처럼 범위를 설정하면 n 개의 thread가 각각 비교 검사를 수행한다.

예를 들어 테이블에 월별 데이터가 들어 있는 경우에 12 개의 thread가 각각 비교 검사를 수행하도록 하려면 다음 속성들을 정의하면 된다.

```
PARTITION_RANGE1 = MONTH=1
PARTITION_RANGE2 = MONTH=2
PARTITION_RANGE3 = MONTH=3
PARTITION_RANGE4 = MONTH=4
PARTITION_RANGE5 = MONTH=5
PARTITION_RANGE6 = MONTH=6
PARTITION_RANGE7 = MONTH=7
PARTITION_RANGE8 = MONTH=8
PARTITION_RANGE9 = MONTH=9
PARTITION_RANGE10 = MONTH=10
PARTITION_RANGE11 = MONTH=11
PARTITION_RANGE12 = MONTH=12
```

모든 조건들은 서로 중복되지 않아야 하며 (disjoint해야 하며) union한 것은 전체 set와 동일해야 한다. 또한 조건에 사용되는 column은 반드시 primary key의 앞부분이어야 한다. (즉, 명시한 조건이 primary index를 사용할 수 있어야 한다.)   
TableDiff에만 적용되는 속성으로써 TableSync는 이 속성을 무시한다.

---

[← 41. gdump](41-gdump.md) · [전체 목차](../README.md) · [43. gsyncher →](43-gsyncher.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
