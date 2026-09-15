<a id="25b0aff4ab5d3b8d"></a>

# 35. PyDBC

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/25b0aff4ab5d3b8d)  
> 태그: `22c.1_10_tag`

[← 34. PDO](34-pdo.md) · [전체 목차](../README.md) · [36. Hibernate →](36-hibernate.md)

<a id="68a38716f185fb73"></a>
## GOLDILOCKS PyDBC

<a id="6b80ae2abafb6654"></a>
### 개요

PyDBC는 [Python Database API Specification v2.0(PEP 249)](https://www.python.org/dev/peps/pep-0249/)를 준수하는 API를 사용하여 GOLDILOCKS 데이터베이스에 접속하는 Python을 프로그래밍한다.

PyDBC에는 Python 표준 라이브러리가 필요하고, GOLDILOCKS 데이터베이스를 연결하고 조작하는 내부 연산은 ODBC API를 호출하기 때문에 ODBC 라이브러리가 필요하다. PyDBC는 ODBC 라이브러리 $GOLDILOCKS_HOME/lib/에 있는 gdlcs를 기본으로 사용하는데 이는 사용자가 setup.py를 수정하여 변경할 수 있다.

PyDBC의 내부 연산은 ODBC 드라이버를 사용하기 때문에 [ODBC 구성요소 개요](31-odbc.md#97047ec0fa5f55be)와 동일하다. 응용 프로그램이 드라이버 관리자로 링크하는 아키텍처와 응용 프로그램이 GOLDILOCKS ODBC driver 라이브러리로 링크하는 아키텍처가 있다.

<a id="cc1ff03b0d809218"></a>
### 버전 체계

다음과 같이 pygoldilocks.so 파일을 실행하여 GOLDILOCKS PyDBC 버전 정보를 확인할 수 있다.

```
shell>python
>>> import pygoldilocks
>>> print pygoldilocks.version
3.2.0
```

현재 GOLDILOCKS PyDBC 드라이버 버전은 GOLDILOCKS 버전에 맞춘 3.2.0이며 이 드라이버는 표준 Python database API 2.0을 준수한다. PyDBC 드라이버는 Python 2.7, 3.4, 3.5, 3.6 버전을 지원하는데 PyDBC 드라이버 라이브러리는 각 Python 버전에 맞게 설치해야 한다.

<a id="7f80e6a1950407f4"></a>
### 설치

PyDBC를 설치하려면 소스를 구축해야 한다. PyDBC는 GOLDILOCKS_HOME/lib에 위치한 gdlcs 라이브러리를 링크하며 GOLDILOCKS_HOME/include에 위치한 goldilocks.h 헤더 파일을 포함하므로 환경 변수 GOLDILOCKS_HOME이 적절한 위치에 설정되어야 한다.

PyDBC를 설치하려면 Python과 GOLDILOCKS 라이브러리의 bit가 동일해야 한다. 따라서 GOLDILOCKS가 32 bit로 구축된 경우에는 Python도 32 bit를 사용하여 PyDBC를 설치해야 한다.

<a id="ce5482e425a1f8c5"></a>
#### Linux에서 설치하기

Linux에는 gcc 컴파일러가 필요하며 다음과 같이 구축한다.

```
shell> sudo python setup.py install
```

> HP-UX와 AIX 플랫폼은 지원하지 않는다.

<a id="8a261c4c516f2fe9"></a>
#### Windows에서 설치하기

Window에서는 다음과 같이 구축한다.

```
shell> python setup.py install
```

PyDBC를 컴파일 하려면 python 버전에 맞는 적절한 Microsoft Visual C++ 컴파일러를 사용해야 한다.  
자세한 내용은 [https://wiki.python.org/moin/WindowsCompilers](https://wiki.python.org/moin/WindowsCompilers)를 참조한다.

- Python 2.4 또는 2.5 버전을 구축하려면 Visual Studio 2003.NET 컴파일러가 필요하다. 이 컴파일러는 유료 버전만 있다.
- Python 2.6, 2.7, 3.0, 3.2 버전을 구축하려면 Visual C++ 2008 컴파일러가 필요하다. 이 컴파일러의 무료 버전은 Visual C++ 2008 Express이다.
- Python 3.3, 3.4 버전을 구축하려면 Visual C++ 2010 컴파일러가 필요하다. 이 컴파일러의 무료 버전은 Visual C++ 2010 Express이다.
- Python 3.5, 3.6 버전을 구축하려면 Visual C++ 2014 또는 VC 2017 컴파일러가 필요하다.
- Python 3.7 버전을 구축하려면 Visual C++ 2017 컴파일러가 필요하다.

<a id="17c01d546213e7ce"></a>
### 사용 예

<a id="63811f2a87e25a8d"></a>
#### connection 클래스 획득

PyDBC는 내부적으로 ODBC 라이브러리를 호출한다. 따라서 커넥션을 얻기 위해 [데이터 원본](31-odbc.md#38509fa109f62339)을 구성해야 한다.

- 커넥션을 얻기 위해 다음과 같이 작성한다.

```
import pygoldilocks
cnxn = pygoldilocks.connect( 'DSN=GOLDILOCKS;UID=test;PWD=test' )
```

PyDBC의 모듈인 pygoldilocks의 내장함수 connect를 호출하여 커넥션을 얻을 수 있다.

> DSN을 사용하기 위해서는 [데이터 원본](31-odbc.md#38509fa109f62339)이 사전에 구성되어 있어야 한다.

ODBC 라이브러리는 DSN에 CHARSET이 지정되지 않은 경우 이를 Console Character Set으로 설정한다. PyDBC는 내부에서 ODBC가 사용하는 character set을 기본 인코딩한다. GOLDILOCKS 서버가 사용하는 character set과 ODBC 라이브러리가 사용하는 character set이 다를 경우, 데이터 변환이 발생하는데 이 경우 성능이 저하될 수 있다. 예를 들어서 Windows에서는 기본 character set으로 CP949를 사용한다. 아무것도 설정되지 않은 경우 PyDBC는 내부에서 CP949(UHC)를 사용하여 encoding하고 ODBC 라이브러리 역시 UHC로 character set을 처리한다.

Client의 character set을 변경하는 방법은 다음과 같다.

- [데이터 원본 구성](31-odbc.md#38509fa109f62339)의 CHARSET 프로퍼티를 변경한다.
- 연결 문자열에 CHARSET 프로퍼티를 추가한다.
- pygoldilocks 모듈의 connect 메소드에 attrs_before 키워드를 사용한다.

위 세 가지 방법 모두 ODBC의 연결 프로퍼티 SQL_ATTR_CHARACTER_SET을 변경하고 PyDBC 라이브러리의 encoding도 설정한다.

<a id="c350ac7c0ef765ec"></a>
#### cursor와 row 클래스 사용하기

다음과 같이 cursor와 row 클래스를 사용할 수 있다.

```
cursor = cnxn.cursor()
cursor.execute( "SELECT NAME, ADDRESS FROM EMP" )

rows = cursor.fetchall()

for row in rows:
    print row.A, row.B

cursor.close()
cnxn.close()
```

<a id="5f21e66f29b99ae6"></a>
## API Reference

<a id="74e152ef395ad997"></a>
### pygoldilocks 모듈

pygoldilocks object는 [Python Database API Specification v2.0](https://www.python.org/dev/peps/pep-0249/)을 준수한다.  
자세한 내용은 [Python DB API 모듈](https://www.python.org/dev/peps/pep-0249/#module-interface)을 참조한다.

<a id="c62e21cbcf3cb572"></a>
#### 속성

- version
    - pygoldilocks 모듈의 버전은 GOLDILOCKS 데이터베이스의 버전을 따른다. 버전은 major.minor.patch 형식의 문자열이다.

- apilevel
    - DB API level 2.0을 가리키며 값은 "2.0" 문자열 상수이다.

- lowercase
    - 결과값으로 나온 row 객체에서 column 이름을 소문자로 할지 여부를 제어한다. 기본값은 false이다. 데이터베이스 column의 대소문자가 일치하지 않을 때 유용하다.

- threadsafety
    - 상수 1이며, thread가 모듈은 공유해도 연결은 공유하지 않는다.

- paramstyle
    - 매개 변수를 나타내며 그 값은 물음표를 의미하는 문자열 상수 "qmark"이다

<a id="5aa001393bbd399a"></a>
#### connect

데이터베이스와 새로운 연결을 만든다.

```
connect( *connectionstring, **kwargs )
```

ODBC 연결 문자열과 키워드를 입력한다. 키워드는 다음과 같다.

<a id="33fba64921a88f37"></a>
| 키워드 | 설명 | 기본값 |
| --- | --- | --- |
| attrs_before | Connection되기 전에 설정되어야 하는 속성을 지정한다. 값을 dictionary 타입으로 받는다. | - |
| autocommit | auto commit 여부를 설정한다. False인 경우, connection.commit을 호출해야 데이터베이스에 반영된다. | False |
| readonly | True인 경우, connection은 readonly로 설정된다. | False |
| timeout | Connection을 위한 timeout을 설정한다. SQL_ATTR_LOGIN_TIMEOUT이 설정된다. | - |

- attrs_before
    - 연결 전에 설정되는 옵션을 지정한다. 이 옵션들은 [SQLSetConnectAttr](31-odbc.md#a643d0267375e839)을 사용하여 설정한다. 속성과 값은 딕셔너리 타입으로 받는다. 설정에 대한 자세한 내용은 [ODBC 속성](31-odbc.md#2c7b29a5722e8858)을 참조한다.

```
cnxn =  pygoldilocks.connect( "DSN=GOLDILOCKS", attr_before={ pygoldilocks.SQL_ATTR_MAX_ROWS : 1000 })
```

<a id="f6059e5ac1fd43d7"></a>
#### Date

```
>>> print pygoldilocks.Date(1984,11,23),  type(pygoldilocks.Date(1984,11,23))
1984-11-23 <type 'datetime.date'>
```

주어진 값에 해당하는 date 객체를 생성한다.

<a id="07cfe8ea5ddcfce2"></a>
#### Time

```
>>> print pygoldilocks.Time(11,23,23), type(pygoldilocks.Time(11,23,23))
11:23:23 <type 'datetime.time'>
```

주어진 값에 해당하는 time 객체를 생성한다.

<a id="3fb7afecdc8aa590"></a>
#### Timestamp

```
>>> print pygoldilocks.Timestamp(1984,11,23,11,23,23), type(pygoldilocks.Timestamp(1984,11,23,11,23,23))
1984-11-23 11:23:23 <type 'datetime.datetime'>
```

주어진 값에 해당하는 datetime 객체를 생성한다.

<a id="81d9af87c58a2017"></a>
#### DATETIME

```
>>> print pygoldilocks.DATETIME(1984,11,23,11,23,23), type(pygoldilocks.DATETIME(1984,11,23,11,23,23))
1984-11-23 11:23:23 <type 'datetime.datetime'>
```

주어진 값에 해당하는 datetime 객체를 생성한다. [Timestamp](#3fb7afecdc8aa590)와 동일하다.

<a id="8f8a72b32f0eb069"></a>
#### Binary

```
>>> print pygoldilocks.Binary('binary'), type(pygoldilocks.Binary('binary'))
binary <type 'bytearray'>
```

주어진 값에 해당하는 bytearray 객체를 생성한다. [BINARY](#4a64f9edb488cf28)와 동일하다.

<a id="4a64f9edb488cf28"></a>
#### BINARY

```
>>> print pygoldilocks.BINARY('binary'), type(pygoldilocks.BINARY('binary'))
binary <type 'bytearray'>
```

주어진 값에 해당하는 bytearray 객체를 생성한다.

<a id="f13ed0457156e7a6"></a>
#### STRING

```
>>> print pygoldilocks.STRING('str'), type(pygoldilocks.STRING('str'))
str <type 'str'>
```

주어진 값에 해당하는 str 객체를 생성한다.

<a id="50ef6d6f4f711eeb"></a>
#### NUMBER

```
>>> print pygoldilocks.NUMBER(100.001), type(pygoldilocks.NUMBER(100.001))
100.001 <type 'float'>
```

주어진 값에 해당하는 float 객체를 생성한다.

<a id="a42c00f5c0bcb86b"></a>
#### ROWID

```
>>> print pygoldilocks.ROWID('AA'), type(pygoldilocks.ROWID('AA'))
AA <type 'str'>
```

데이터베이스의 row ID column을 기술하기 위해 사용되며 str 객체를 반환한다.

<a id="4286685d45fde11f"></a>
#### TimeFromTicks

```
>>> print pygoldilocks.TimeFromTicks( 10 )
09:00:10
```

인자값으로 설정된 datetime.time 객체를 반환한다.

<a id="b107ea00d55b1502"></a>
#### DateFromTicks

```
>>> print pygoldilocks.DateFromTicks( 360000 )
1970-01-05
```

인자값으로 설정된 datetime.date 객체를 반환한다.

<a id="e9b8c7cbfb6a0843"></a>
#### TimestampFromTicks

```
>>> print pygoldilocks.DateFromTicks( 360000 )
1970-01-05
```

인자값으로 설정된 datetime.timestamp 객체를 반환한다.

<a id="20d8b3aeaf135dd8"></a>
#### setDecimalSeparator

데이터베이스로부터 얻은 NUMERIC 타입의 소수점 구분 문자를 설정한다. 기본값은 .를 사용한다.

<a id="32b3eb90fd9dbc4a"></a>
#### getDecimalSeparator

설정된 NUMERIC 타입의 소수점 구분 문자를 얻는다.

<a id="ef45b5b678b32530"></a>
### Connection

데이터베이스와 연결을 관리하는 객체이며 pygoldilocks 모듈의 connect() 함수로 생성된다.

<a id="65bdc3d6f40c51db"></a>
#### 속성

- autocommit
    - Connection의 autocommit 모드를 설정할 수 있다.

- searchescape
    - ODBC의 Escape 문자를 얻는다. pygoldilocks는 '/'를 사용한다.

- timeout
    - SQL_ATTR_QUERY_TIMEOUT을 SQLSetConnectAttr 함수를 이용하여 설정한다.

<a id="c5abf7f6c8401fd3"></a>
#### 함수

- cursor()
    - 새로운 cursor 객체를 반환한다.

- commit()
    - 실행했던 SQL 구문을 commit 한다.

- rollback()
    - 실행했던 SQL 구문을 rollback 한다.

- close()
    - 연결을 닫는다. autocommit이 false인 경우, commit 되지 않았던 SQL 구문이 rollback 된다.

- getinfo( info )
    - ODBC의 SQLGetInfo 함수를 이용하여 연결 관련 속성을 얻을 수 있다. 자세한 내용은 [SQLGetInfo](31-odbc.md#ff70845becec3b11)를 참조한다.

```
dns_name = cnxn.getinfo( pygoldilocks.SQL_DATA_SOURCE_NAME )
```

- execute( sql, [*params] )
    - 새 cursor 객체를 생성하고 이 객체의 execute 함수를 실행한 후 cursor 객체를 반환한다.

```
cursor = cnxn.execute( "SELECT COUNT(*) FROM EMP" )
```

자세한 내용은 Cursor.execute() 함수를 참조한다. 이 함수는 Python API에는 없지만 편의를 위해 제공된다. 이 함수가 호출될 때마다 cursor 객체가 할당되기 때문에 하나 이상의 SQL 구문을 실행해야 하는 경우에는 사용을 권장하지 않는다.

- set_attr( attr_id, value )
    - [SQLSetConnectAttr](31-odbc.md#a643d0267375e839) 함수를 실행하여 연결 속성을 설정할 수 있다.
    - 다음은 set_attr 함수를 사용하여 데이터베이스의 트랜잭션 격리 단계를 조절하는 예이다.

```
connection.set_attr( pygoldilocks.SQL_ATTR_TXN_ISOLATION, pygoldilocks.SQL_TXN_SERIALIZABLE )
```

<a id="56ca493fa5303477"></a>
### Cursor

일반적으로 cursor 객체는 fetch 작업을 관리하는데 사용되는 데이터베이스 cursor를 의미한다. 데이터베이스 cursor는 ODBC statement handle (HSTMT)에 매핑된다. 동일한 connection이 생성한 cursor 객체는 서로 분리되지 않는다. 즉, 하나의 cursor가 데이터베이스에 수행한 모든 갱신 사항이 다른 cursor에도 적용된다.

> Cursor는 데이터베이스 트랜잭션을 관리하지 않고 connection이 트랜잭션을 commit 하거나 rollback 한다.

<a id="88fd09187a7a151f"></a>
#### 속성

<a id="c2802a400fac2012"></a>
##### Description

읽기 전용 속성이며 튜플 타입으로 마지막에 수행된 SELECT 구문이 반환한 각 column에 대한 내용이 들어있다. 각 튜플은 다음을 포함한다.

1. Column name (또는 alias)
2. Type code
3. Display size
4. Internal size
5. Precision
6. Scale
7. Nullable

SELECT 구문이 호출되지 않은 경우, descriptin은 none이다.

<a id="5292760cded81fb8"></a>
##### rowcount

마지막에 수행한 SQL 구문이 갱신한 row의 개수이다.

<a id="996c3b418da22b0d"></a>
##### arraysize

[fetchmany( [size = cursor.arraysize] )](#579e4e27d3920721) 함수를 사용하여 한 번에 가져올 수 있는 row의 개수이다. 기본값은 1이다.

<a id="66d4b3b4477b4a00"></a>
##### connection

읽기 전용 속성으로써 해당 cursor 객체를 생성한 connection 객체를 가리킨다.

<a id="6d8b334cc3421fa7"></a>
##### fast_executemany

True로 설정되면 [executemany( sql, [*params] )](#206b8bb1e3b8e1b2) 함수를 실행할 때 매개 변수를 배열로 구성하여 한 번의 execute로 처리한다. False로 설정되면 매개 변수마다 개별적으로 execute를 실행한다.

<a id="c91bf3ba99185efe"></a>
#### 함수

<a id="d2a17afd4e38c133"></a>
##### execute( sql, [*params] )

SQLPrepare와 SQLExecute 함수를 통해 SQL 구문을 수행하고 이 함수를 호출한 cursor를 반환한다.   
옵션인 매개 변수는 다음과 같이 사용할 수 있다.

```
cursor.execute( "SELECT A FROM TEST WHERE B=? AND C=?", x, y )
```

```
cursor.execute( "SELECT A FROM TEST WHERE B=? AND C=?", (x, y) )
```

<a id="206b8bb1e3b8e1b2"></a>
##### executemany( sql, [*params] )

각 매개 변수에 대한 SQL 구문을 실행하고 none을 반환한다. 매개 변수 params는 반드시 sequence의 sequence 타입이거나 sequence generator이어야 한다.

```
params = [ ( 1, 'A' ), ( 2, 'B' ) ]
cursor.executemany("INSERT INTO TEST( C1, C2 ) VALUES ( ?, ? )", params)
```

위 예에서 SQL 구문은 두 번 수행된다, 즉. ( 1, 'A' )와 ( 2, 'B' )에 대해 각각 실행된다. Cursor 객체의 fast_executemany가 true로 설정되었는지 false로 설정되었는지에 따라 executemany 동작이 달라진다.

위의 예는 다음과 동일하다.

```
params = [ ( 1, 'A' ), ( 2, 'B' ) ]
for p in params:
    cursor.execute( "INSERT INTO TEST( C1, C2 ) VALUES ( ?, ? )", p )
```

fast_executemany를 true로 설정하면 executemany는 한 번의 execute만으로 작업을 처리하려 한다. 이를 위해서는 매개 변수 params의 아이템에서 같은 인덱스 위치에 있는 데이터의 데이터 타입이 서로 동일해야 한다.

```
params = [ ( 1, 'A' ), ( '2', 'B' ) ]
cursor.executemany("INSERT INTO TEST( C1, C2 ) VALUES ( ?, ? )", params)
```

위의 예에서 매개 변수 params의 두 아이템 중 첫 번째 아이템의 데이터 타입이 다르다. 이처럼 아이템들 간에 동일한 인덱스 위치의 데이터 타입이 다르면 executemany가 SQL 구문을 한 번에 처리하지 않고 개별적으로 처리한다.

Connection 객체의 autocommit이 true일 경우, SQL 구문이 분할 처리되어 각각의 SQL 구문이 개별적으로 commit된다. 레코드를 순차적으로 처리하면서 오류가 발생하면 데이터베이스에 레코드의 일부만 commit 되고 일부는 commit 되지 못한 상태로 작업이 완료된다. 따라서 executemany()를 이용할 경우, 모든 레코드가 데이터베이스에 commit 되었는지 확인하기 위해 autocommit을 false로 먼저 설정하여 실행하는 것이 좋다.

<a id="4847dc355cfc326f"></a>
##### fetchone()

질의의 다음 row를 반환한다. 다음 데이터가 없을 경우에는 none이다.

<a id="f36310b04e0ccc70"></a>
##### fetchall()

질의에 남아 있는 모든 row를 반환한다. 모든 row를 메모리로 읽어들이기 때문에 사용 시 주의해야 한다.

<a id="579e4e27d3920721"></a>
##### fetchmany( [size = cursor.arraysize] )

size나 cursor.arraysize 만큼 남아있는 row를 반환한다. 다음 데이터는 빈 sequence 데이터를 반환한다. cursor.arraysize의 기본값은 1이다.

<a id="93753e65e3517f25"></a>
##### commit()

SQL 구문을 commit 한다. Cursor 객체를 생성한 connection 객체가 실행하는 함수로써 동일한 connection 객체에 생성된 모든 cursor에 적용된다. Connection 객체의 commit과 동일하다.

<a id="c79b443ff5941397"></a>
##### rollback()

SQL 구문을 rollback 한다. Cursor 객체를 생성한 connection 객체가 실행하는 함수로써 동일한 connection 객체에 생성된 모든 cursor에 적용된다. Connection 객체의 rollback과 동일하다.

<a id="b9a14e2ad250d1db"></a>
##### skip( count )

SQLFetchScroll과 SQL_FETCH_NEXT를 통해 count에 지정된 횟수만큼 레코드를 통과한다.

<a id="1896c19f1130bd75"></a>
##### nextset()

GOLDILOCKS ODBC에서 SQLMoreResults를 지원하지 않으므로 false를 반환한다.

<a id="69d94e5ad5876572"></a>
##### close()

Cursor 객체를 닫는다.

<a id="893fee68bb45febd"></a>
##### setinputsizes( size_list )

선택적 함수로써 sequence 타입을 매개 변수로 받는다. SQLBindParameter의 INPUT 매개 변수 크기를 설정한다.

<a id="1ec53ee2b4828789"></a>
##### setoutputsize( size )

선택적 함수로써 DB API와 다른 용도로 사용되어 OUTPUT 매개 변수에 대한 버퍼 크기를 할당한다.

<a id="559ee4d1a781f458"></a>
##### callproc( procname [, params] )

procname에 해당하는 저장 프로시저를 호출한다. 매개 변수는 sequence 타입이어야 하며 출력 매개 변수를 포함한다. 단, 입력할 때 출력 매개 변수에 위치한 데이터는 무의미하다. callproc 함수는 입력 매개 변수 데이터의 INOUT, OUT에 해당하는 데이터를 갱신하여 sequence 타입으로 반환한다.

```
create_proc = """CREATE OR REPLACE PROCEDURE PROC1( A1 INTEGER, A2 OUT CHAR(10) )
IS 
  V1 CHAR(10);
BEGIN
  SELECT T1.I1
    INTO V1
    FROM T1
    WHERE T1.I1 >= A1 AND T1.I1 <= A1;
  A2 := V1;
END;\
"""

cursor.execute( create_proc )

result = cursor.callproc( 'PROC1', ( 1, 0 ) )
```

<a id="808d8707e51b40f6"></a>
##### callfunc( funcname [, params] )

funcname에 해당하는 함수를 호출한다. callfunc()은 함수의 데이터를 반환한다.

```
create_func = """
CREATE OR REPLACE FUNCTION FUNC1( A1 INTEGER, A2 INTEGER )
  RETURN INTEGER
  IS
    V1 INTEGER;
  BEGIN

    SELECT COUNT(*)
      INTO V1
      FROM T1
      WHERE T1.I1 >= A1 AND T1.I1 <= A2;

    RETURN V1;
  END;\
"""

cursor.execute( create_func )
cursor.commit()

result = cussr.callfunc( 'FUNC1', ( 1,  4) )
```

<a id="9ff372a1c9c792fe"></a>
##### tables( table=None, catalog=None, schema=None, tableType=None )

지정된 조건을 만족하는 데이터베이스의 테이블 정보를 반환한다. 문자 '_'와 '%'는 와일드 카드로 해석된다. 각 row는 다음의 column 정보를 가지는데 자세한 내용은 [SQLTables](31-odbc.md#c5e194e88c5c7677)를 참조한다.

1. table_cat: 카탈로그 이름이다.
2. table_schem: 스키마 이름이다.
3. table_name: 테이블 이름이다.
4. table_type: 'TABLE', 'VIEW', 'SYSTEM TABLE', 'GLOBAL TEMPORARY', 'LOCAL TEMPORARY', 'IMMUTABLE TABLE', 'ALIAS', 'SYNONYM' 또는 특정 타입의 이름이 올 수 있다.
5. remarks: 테이블 명세이다.

```
print cursor.tables( table= 'TEST' ).fetchone()

#print table name
for row in cursor.tables():
 print row.table_name
```

> 매개 변수가 비어있을 경우 사용자에게 권한이 있는 모든 테이블의 정보를 반환한다.

<a id="5768117604a6bf32"></a>
##### columns( table=None, catalog=None, schema=None, tableType=None )

[SQLColumns](31-odbc.md#ef2fc0dda783516c) 함수를 통해 지정된 테이블의 column 정보를 얻는다. 각 row는 다음과 같은 column 정보를 포함한다.

1. table_cat
2. table_schem
3. table_name
4. column_name
5. data_type
6. type_name
7. column_size
8. buffer_length
9. decimal_digits
10. num_prec_radix
11. nullable
12. remarks
13. column_def
14. sql_data_type
15. sql_datetime_sub
16. char_octet_length
17. ordinal_position
18. is_nullable: SQL_NULLABLE, SQL_NO_NULLS 또는 SQL_NULLS_UNKNOWN.

```
#print column name of table TEST
for r in cursor.columns( table = 'TEST' ):
    print r.column_name
```

<a id="02c1445510b45e39"></a>
##### statistics( table, catalog=None, schema=None, unique=False, quick=True )

[SQLStatistics](31-odbc.md#963f950aca63eeb6) 함수를 통해 지정된 테이블과 관련된 정보를 얻는다.  
unique가 true일 경우, unique 인덱스만 반환하고, false일 경우, 모든 인덱스를 반환한다.  
quick이 true일 경우, CARDINALYTIY와 PAGES는 즉시 사용할 수 있는 경우에만 반환되고 그렇지 않으면 해당 열에는 NULL이 반환된다.

1. table_cat
2. table_schem
3. table_name
4. non_unique
5. index_qualifier
6. index_name
7. type
8. ordinal_position
9. column_name
10. asc_or_desc
11. cardinality
12. pages
13. filter_condition

> 와일드카드 문자는 허용되지 않는다.

<a id="62fc7cad572eb574"></a>
##### rowIdColumns( table, catalog=None, schema=None, nullable=True )

SQL_BEST_ROWID로 [SQLSpecialColumns](31-odbc.md#f56183f35ba8f64a)를 실행하여 row를 고유하게 식별하는 column의 결과 집합을 반환한다. 각 row는 다음과 같은 column 정보를 갖는다.

1. scope: SQL_SCOPE_CURROW, SQL_SCOPE_TRANSACTION, 또는 SQL_SCOPE_SESSION
2. column_name
3. data_type: ODBC의 SQL 타입 상수
4. type_name
5. column_size
6. buffer_length
7. decimal_digits
8. pseudo_column: SQL_PC_UNKNOWN, SQL_PC_NOT_PSEUDO 또는 SQL_PC_PSEUDO

<a id="5348c7758a63e458"></a>
##### rowVerColumns( table, catalog=None, schema=None, nullable=True )

SQL_ROWVER으로 [SQLSpecialColumns](31-odbc.md#f56183f35ba8f64a)를 실행하여 row가 업데이트 될 때 자동으로 업데이트 되는 column의 결과 집합을 반환한다. 각 row는 다음과 같은 column 정보를 갖는다.

1. scope: SQL_SCOPE_CURROW, SQL_SCOPE_TRANSACTION, 또는 SQL_SCOPE_SESSION
2. column_name
3. data_type: ODBC의 SQL 타입 상수
4. type_name
5. column_size
6. buffer_length
7. decimal_digits
8. pseudo_column: SQL_PC_UNKNOWN, SQL_PC_NOT_PSEUDO 또는, SQL_PC_PSEUDO

<a id="d5441c88d3c592c9"></a>
##### primaryKeys( table, catalog=None, schema=None )

[SQLPrimaryKeys](31-odbc.md#487e2f6112d08230) 함수를 실행하여 테이블의 주요 키를 구성하는 column의 결과 집합을 반환한다. 각 row는 다음과 같은 column 정보를 갖는다.

1. table_cat
2. table_schem
3. table_name
4. column_name
5. key_seq
6. pk_name

<a id="970388c7397602ba"></a>
##### foreignKeys( table=None, catalog=None, schema=None, foreignTable=None, foreignCatalog=None, foreignSchema=None )

[SQLForeignKeys](31-odbc.md#f489d57e96481820) 함수를 실행하여 지정된 테이블 또는 지정된 테이블의 기본 키를 참조하는 다른 테이블의 외래 키인 column 이름의 결과 집합을 만든다. 각 row는 다음과 같은 column 정보를 갖는다.

1. pktable_cat
2. pktable_schem
3. pktable_name
4. pkcolumn_name
5. fktable_cat
6. fktable_schem
7. fktable_name
8. fkcolumn_name
9. key_seq
10. update_rule
11. delete_rule
12. fk_name
13. pk_name
14. deferrability

<a id="71e45475521bf83e"></a>
##### procedures( procedure=None, catalog=None, schema=None )

[SQLProcedures](31-odbc.md#77cd8b42bb283b7f)를 실행하여 프로시저에 대한 정보의 결과 집합을 만든다. 각 row는 다음과 같은 column 정보를 갖는다.

1. procedure_cat
2. procedure_schem
3. procedure_name
4. num_input_params
5. num_output_params
6. num_result_sets
7. remarks
8. procedure_type

<a id="25b8615650218c3d"></a>
##### getTypeInfo( sqlType=None )

[SQLGetTypeInfo](31-odbc.md#bee8125193f5b247) 함수를 실행하여 지정된 데이터 타입 또는 GOLDILOCKS ODBC가 지원하는 모든 데이터 타입에 대한 정보의 결과 집합을 만든다. 각 row는 다음과 같은 column을 갖는다.

1. type_name
2. data_type
3. column_size
4. literal_prefix
5. literal_suffix
6. create_params
7. nullable
8. case_sensitive
9. searchable
10. unsigned_attribute
11. fixed_prec_scale
12. auto_unique_value
13. local_type_name
14. minimum_scale
15. maximum_scale
16. sql_data_type
17. sql_datetime_sub
18. num_prec_radix
19. interval_precision

<a id="956078a3583e7b71"></a>
### Row

Row 객체는 cursor 객체의 fetch 함수로 반환된다. DB API에 명시된 것처럼 튜플 타입처럼 처리된다.

```
row = cursor.fetchone()
for column in row:
    print column
```

다음과 같은 기능이 pygoldilocks에 추가되었다.

- Column 이름을 사용하여 데이터에 접근할 수 있다. 
- Cursor 객체가 닫힌 후에도 row를 통해 cursor.description 값에 접근할 수 있다. 
- Row의 값을 갱신할 수 있다.

Column 이름을 사용하여 row에 접근하면 편리할 뿐만 아니라 가독성도 높아진다. 그러나 column 이름에 Python 예약어나 공백이 포함되면 row.__getattribute__()를 통해 접근해야만 한다.

```
cursor.execute( "select c1 from test")
print cursor.description
row = cursor.fetchone()
print row.C1
```

```
(('C1', <type 'str'>, 10, 10, 10, 0, True),)
test
```

> GOLDILOCKS 데이터베이스의 식별자는 기본적으로 대문자이다. 하지만 소문자로 지정하는 경우도 있기 때문에 column 이름을 이용하여 row에 접근할 때는 대소문자 사용에 유의해야 한다.

<a id="a95943b50b51c5ab"></a>
#### 속성

- cursor_description

해당 row를 생성한 cursor 객체의 속성 description의 복사본이다. 자세한 내용은 [Cursor.description](#88fd09187a7a151f)을 참조한다.

<a id="085faae26ca53b7b"></a>
## Exception

Python 예외는 GOLDILOCKS ODBC에서 오류를 감지했을 때 pygoldilocks에 의해 발생한다. 예외 클래스는 다음과 같이 [Python DB API](https://www.python.org/dev/peps/pep-0249/#exceptions) 와 동일하다.

- Error
    - DatabaseError
        - DataError
        - OperationalError
        - IntegrityError
        - InternalError
        - ProgrammingError
        - NotSupportedError

오류가 발생할 경우, 일반적으로 예외 유형은 데이터베이스에서 제공하는 SQLSTATE 값을 기반으로 처리된다.

<a id="dfc3f6dcf6ad7349"></a>
| SQLSTATE | Exception |
| --- | --- |
| 0A000 | NotSupportedError |
| 01002 | OperationalError |
| 08001 | OperationalError |
| 08003 | OperationalError |
| 08004 | OperationalError |
| 08007 | OperationalError |
| 08S01 | OperationalError |
| 28000 | InterfaceError |
| 40002 | IntegrityError |
| 22*** | DataError |
| 23*** | IntegrityError |
| 24*** | ProgrammingError |
| 25*** | ProgrammingError |
| 42*** | ProgrammingError |

<a id="922234acadf99c43"></a>
## Data Type

<a id="3e5394cce92cbd6e"></a>
### Python 매개 변수를 GOLDILOCKS로 전달

Python 매개 변수를 GOLDILOCKS ODBC에 전달할 때는 다음과 같이 데이터가 변환된다.

**Python 3**

<a id="7944ca7aa3e02207"></a>
| Python datatype | 설명 | ODBC datatype |
| --- | --- | --- |
| None | - | SQL_VARCHAR |
| str | UTF-8 | SQL_VARCHAR or SQL_LONGVARCHAR |
| bytes, bytearray | binary | SQL_VARBINARY or SQL_LONGVARBINARY |
| bool | bit | SQL_BIT |
| datetime.date | date | SQL_TYPE_DATE |
| datetime.time | time | SQL_TYPE_TIME |
| datetime.datetime | timestamp | SQL_TYPE_TIMESTAMP |
| int | integer | SQL_BIGINT |
| float | floating point | SQL_DOUBLE |
| decimal | numeric | SQL_NUMERIC |

**Python 2**

<a id="244683cf796e17f3"></a>
| Python datatype | 설명 | ODBC datatype |
| --- | --- | --- |
| None | - | SQL_VARCHAR |
| str | UTF-8 | SQL_VARCHAR or SQL_LONGVARCHAR |
| bytearray | binary | SQL_VARBINARY or SQL_LONGVARBINARY |
| buffer | binary | SQL_VARBINARY or SQL_LONGVARBINARY |
| bool | bit | SQL_BIT |
| datetime.date | date | SQL_TYPE_DATE |
| datetime.time | time | SQL_TYPE_TIME |
| datetime.datetime | timestamp | SQL_TYPE_TIMESTAMP |
| int | integer | 32 bit: SQL_INTEGER, 64 bit: SQL_BIGINT |
| long | bigint | SQL_BIGINT |
| float | floating point | SQL_DOUBLE |
| decimal | numeric | SQL_NUMERIC |

<a id="5cbb3aa7b7062472"></a>
### GOLDILOCKS로부터 전달받는 SQL 값

GOLDILOCKS 데이터베이스의 데이터를 Python으로 전달할 때는 다음과 같이 데이터가 변환된다.

**Python 3**

<a id="785e648ec67c6a2b"></a>
| ODBC datatype | 설명 | Python datatype |
| --- | --- | --- |
| any | NULL | None |
| SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR | text | text |
| SQL_BINARY_SQL_VARBINARY, SQL_LONGVARBINARY | binary | bytes |
| SQL_NUMERIC | decimal, numeric | decimal.Decimal |
| SQL_BOOLEAN | bit, bool | bool |
| SQL_SMALLINT, SQL_INTEGER | integers | int |
| SQL_BIGINT | long | long |
| SQL_REAL, SQL_FLOAT, SQL_DOUBLE | floating point | float |
| SQL_TYPE_TIME | time | datetime.time |
| SQL_TYPE_DATE | date | datetime.date |
| SQL_TYPE_TIMESTAMP | timestamp | datetime.timestamp |
| SQL_TYPE_TIME_WITH_TIMEZONE | time with timezone | text |
| SQL_TYPE_TIMESTAMP_WITH_TIMEZONE | timestamp with timezone | text |
| SQL_C_INTERVAL_*** | interval | text |

**Python 2**

<a id="071d77c525e1ef01"></a>
| ODBC datatype | 설명 | Python datatype |
| --- | --- | --- |
| any | NULL | None |
| SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR | text | text |
| SQL_BINARY_SQL_VARBINARY, SQL_LONGVARBINARY | binary | bytes |
| SQL_NUMERIC | decimal, numeric | decimal.Decimal |
| SQL_BOOLEAN | bit, bool | bool |
| SQL_SMALLINT, SQL_INTEGER | integers | int |
| SQL_BIGINT | long | long |
| SQL_REAL, SQL_FLOAT, SQL_DOUBLE | floating point | float |
| SQL_TYPE_TIME | time | datetime.time |
| SQL_TYPE_DATE | date | datetime.date |
| SQL_TYPE_TIMESTAMP | timestamp | datetime.timestamp |
| SQL_TYPE_TIME_WITH_TIMEZONE | time with timezone | text |
| SQL_TYPE_TIMESTAMP_WITH_TIMEZONE | timestamp with timezone | text |
| SQL_C_INTERVAL_*** | interval | text |

Python 데이터 타입의 text는 Python 3에서는 unicode로 변환된다. Python 2에서는 데이터베이스의 character set에 따라 unicode나 string으로 변환된다.

**Python 2 text**

<a id="6993a28f50b47fb0"></a>
| DB character set | Python type |
| --- | --- |
| UTF-8 | str |
| SQL_ASCII | str |
| UHC | unicode |
| GB18030 | unicode |

---

[← 34. PDO](34-pdo.md) · [전체 목차](../README.md) · [36. Hibernate →](36-hibernate.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
