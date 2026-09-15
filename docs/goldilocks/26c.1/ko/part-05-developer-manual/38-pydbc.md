<a id="a088f981bef813f3"></a>

# 38. PyDBC

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/a088f981bef813f3)  
> 태그: `26c.1_0_tag`

[← 37. PDO](37-pdo.md) · [전체 목차](../README.md) · [39. aiogoldilocks →](39-aiogoldilocks.md)

<a id="e568ad84ee957437"></a>
## GOLDILOCKS PyDBC

<a id="f8ccd48763d9245a"></a>
### 개요

PyDBC는 [Python Database API Specification v2.0(PEP 249)](https://www.python.org/dev/peps/pep-0249/)를 준수하는 API를 사용하여 GOLDILOCKS 데이터베이스에 접속하는 Python을 프로그래밍한다.

PyDBC에는 Python 표준 라이브러리가 필요하고, GOLDILOCKS 데이터베이스를 연결하고 조작하는 내부 연산은 ODBC API를 호출하기 때문에 ODBC 라이브러리가 필요하다. PyDBC는 ODBC 라이브러리 $GOLDILOCKS_HOME/lib/에 있는 gdlcs를 기본으로 사용하는데 이는 사용자가 setup.py를 수정하여 변경할 수 있다.

PyDBC의 내부 연산은 ODBC 드라이버를 사용하기 때문에 [ODBC 구성요소 개요](34-odbc.md#4834a499a2bd6383)와 동일하다. 응용 프로그램이 드라이버 관리자로 링크하는 아키텍처와 응용 프로그램이 GOLDILOCKS ODBC driver 라이브러리로 링크하는 아키텍처가 있다.

<a id="571b073a87bebbc2"></a>
### 버전 체계

GOLDILOCKS PyDBC 드라이버 버전은 GOLDILOCKS 제품의 배포 버전에 맞춰 관리된다. 동일한 배포 버전에 포함된 PyDBC 라이브러리는 Python 버전이나 운영체제에 따라 파일 형식이 다를 수 있으나, 모두 동일한 드라이버 버전을 사용한다.

설치된 PyDBC 드라이버 버전은 pygoldilocks 모듈의 version 속성으로 확인할 수 있다.

```
shell>python
>>> import pygoldilocks
>>> print( pygoldilocks.version )
X.Y.Z (출력되는 X.Y.Z는 현재 Python 환경에 설치된 PyDBC 드라이버의 버전이다.)
```

PyDBC 드라이버 버전과 Python Database API 규격의 버전은 서로 다른 개념이다. PyDBC는 Python Database API Specification v2.0(PEP 249)을 준수하며, 여기서 2.0은 PyDBC 드라이버의 버전이 아니라 PyDBC가 준수하는 표준 API 규격의 버전을 의미한다.

PyDBC를 사용할 때는 GOLDILOCKS 서버와 함께 제공된 클라이언트 패키지의 드라이버를 사용하는 것을 권장한다. 서버와 다른 배포 버전의 PyDBC를 사용해야 하는 경우에는 해당 서버 버전과 PyDBC 드라이버의 호환성을 사전에 확인해야 한다.

PyDBC 라이브러리는 Python 버전과 운영체제 환경에 맞게 제공되므로, 다음 항목과 일치하는 라이브러리를 설치해야 한다.

- Python의 메이저 버전 및 마이너 버전
- 운영체제 및 CPU 아키텍처
- Python과 GOLDILOCKS 클라이언트 라이브러리의 비트 수 (32 비트 또는 64 비트)

<a id="bf2b2ea892a408ea"></a>
### 설치

PyDBC는 Python C 확장 모듈로 제공되며, GOLDILOCKS 클라이언트 패키지에 포함된 소스를 빌드하여 설치한다. PyDBC는 내부적으로 GOLDILOCKS ODBC 라이브러리인 gdlcs를 사용한다.

<a id="575412695131db85"></a>
#### 지원 환경

PyDBC는 HP-UX, AIX 및 macOS 플랫폼을 공식적으로 지원하지 않는다.

PyDBC가 지원하는 Python 버전은 다음과 같다.

- Python 2.4 이상
- Python 3.4 이상

Python 2는 Python 커뮤니티에서 더 이상 유지보수하지 않는 deprecated 버전이다. 기존 Python 2 응용 프로그램과의 호환성을 위해 Python 2.4 부터 2.7 까지 지원한다.

PyDBC는 Python C 확장 모듈이므로, 설치에 사용한 Python과 실제로 PyDBC를 실행하는 Python의 메이저 버전 및 마이너 버전이 일치해야 한다.

<a id="85cb69f63f6c6f27"></a>
#### 사전 요구 사항

PyDBC를 설치하기 전에 다음 사항을 확인한다.

- GOLDILOCKS 클라이언트 패키지가 설치되어 있어야 한다.
- GOLDILOCKS_HOME 환경 변수가 GOLDILOCKS 클라이언트 설치 디렉터리로 설정되어 있어야 한다.
- $GOLDILOCKS_HOME/include 에 goldilocks.h 헤더 파일이 있어야 한다.
- $GOLDILOCKS_HOME/lib 에 gdlcs 클라이언트 라이브러리가 있어야 한다.
- 설치할 Python 버전과 호환되는 C 컴파일러가 설치되어 있어야 한다.
- 사용하는 Python 버전의 개발 헤더가 설치되어 있어야 한다.
- Python과 GOLDILOCKS 클라이언트 라이브러리의 아키텍처가 일치해야 한다.

<a id="e634886659b9dbf2"></a>
#### Linux에서 설치하기

Linux에서 PyDBC를 빌드하려면 C 컴파일러와 사용하는 Python 버전의 개발 헤더가 필요하다.

먼저 GOLDILOCKS_HOME 환경 변수를 설정한다.

```
shell> export GOLDILOCKS_HOME=/path/to/goldilocks
```

필요에 따라 실행 시 gdlcs 공유 라이브러리를 찾을 수 있도록 라이브러리 검색 경로를 설정한다.

```
shell> export LD_LIBRARY_PATH=$GOLDILOCKS_HOME/lib:$LD_LIBRARY_PATH
```

<a id="23a261c4a393756b"></a>
##### Python 2

Python 2 소스 디렉터리로 이동한 후 설치한다.

```
shell> cd $GOLDILOCKS_HOME/app_dev/pygoldilocks/ver2
shell> python setup.py install
```

여러 버전의 Python 2 가 설치되어 있는 경우에는 설치 대상 Python의 실행 파일을 명시하여 설치한다.

```
shell> python2.7 setup.py install
```

Python 2.4부터 2.7까지는 해당 Python 버전과 호환되는 setuptools 또는 distutils를 사용하여 설치해야 한다.

<a id="3221528264061106"></a>
##### Python 3

Python 3 소스 디렉터리로 이동한 후 pip를 사용하여 설치한다.

```
shell> cd $GOLDILOCKS_HOME/app_dev/pygoldilocks/ver3
shell> python3 -m pip install .
```

여러 버전의 Python 3 가 설치되어 있는 경우에는 설치 대상 Python의 실행 파일을 명시하여 설치한다.

```
shell> python3.13 -m pip install .
```

PyDBC는 시스템 Python에 직접 설치하기보다는 Python 가상 환경에 설치하는 것을 권장한다. 또한 sudo python setup.py install 과 같이 관리자 권한으로 설치하는 방식은 권장하지 않는다

<a id="56d2d72eb27cdfe3"></a>
#### Windows에서 설치하기

Windows에서 PyDBC를 빌드하려면 사용하는 Python 버전과 호환되는 Microsoft C/C++ 컴파일러가 필요하다. 또한, Python, C/C++ 컴파일러 및 GOLDILOCKS 클라이언트 라이브러리는 동일한 아키텍처를 사용해야 한다.

Python 2에서 사용하는 컴파일러는 다음과 같다

- Python 2.4 ~ 2.5: Microsoft Visual Studio 2003.NET
- Python 2.6 ~ 2.7: Microsoft Visual C++ 2008

Python 3에서는 사용하는 Python 버전과 호환되는 Microsoft C/C++ Build Tools를 사용한다.  
자세한 내용은 [https://wiki.python.org/moin/WindowsCompilers](https://wiki.python.org/moin/WindowsCompilers)를 참조한다.

명령 프롬프트에서 GOLDILOCKS_HOME 환경 변수를 설정한다.

```
C:\> set GOLDILOCKS_HOME=C:\goldilocks
```

<a id="add8ba23d2f21b3d"></a>
##### Python 2

```
C:\> cd %GOLDILOCKS_HOME%\app_dev\pygoldilocks\ver2
C:\> python setup.py install
```

<a id="b9d81342db7aa344"></a>
##### Python 3

```
C:\> cd %GOLDILOCKS_HOME%\app_dev\pygoldilocks\ver3
C:\> python -m pip install .
```

<a id="60ac40bce62a20ef"></a>
#### 설치 확인

설치가 완료되면 다음 명령을 실행하여 pygoldilocks 모듈이 정상적으로 로드되는지 확인한다.

```
shell> python -c "import pygoldilocks; print(pygoldilocks.version)"
26.1.0
```

버전이 출력되면 PyDBC가 현재 Python 환경에 정상적으로 설치된 것이다.

pygoldilocks 모듈을 찾을 수 없다는 오류가 발생하면 설치에 사용한 Python과 확인에 사용한 Python이 동일한지 확인한다.

gdlcs 라이브러리를 찾을 수 없다는 오류가 발생하면 다음 사항을 확인한다.

- GOLDILOCKS_HOME 환경 변수
- GOLDILOCKS 클라이언트 라이브러리의 설치 경로
- 운영체제의 공유 라이브러리 검색 경로
- Python과 GOLDILOCKS 클라이언트 라이브러리의 아키텍처 일치 여부

<a id="464d7502d3c257ca"></a>
### 사용 예

<a id="fe734e31ad9cd906"></a>
#### connection 클래스 획득

PyDBC는 내부적으로 ODBC 라이브러리를 호출한다. 따라서 커넥션을 얻기 위해 [데이터 원본](34-odbc.md#69c211015508ccf1)을 구성해야 한다.

- 커넥션을 얻기 위해 다음과 같이 작성한다.

```
import pygoldilocks
cnxn = pygoldilocks.connect( 'DSN=GOLDILOCKS;UID=test;PWD=test' )
```

PyDBC의 모듈인 pygoldilocks의 내장함수 connect를 호출하여 커넥션을 얻을 수 있다.

> DSN을 사용하기 위해서는 [데이터 원본](34-odbc.md#69c211015508ccf1)이 사전에 구성되어 있어야 한다.

ODBC 라이브러리는 DSN에 CHARSET이 지정되지 않은 경우 이를 Console Character Set으로 설정한다. PyDBC는 내부에서 ODBC가 사용하는 character set을 기본 인코딩한다. GOLDILOCKS 서버가 사용하는 character set과 ODBC 라이브러리가 사용하는 character set이 다를 경우, 데이터 변환이 발생하는데 이 경우 성능이 저하될 수 있다. 예를 들어서 Windows에서는 기본 character set으로 CP949를 사용한다. 아무것도 설정되지 않은 경우 PyDBC는 내부에서 CP949(UHC)를 사용하여 encoding하고 ODBC 라이브러리 역시 UHC로 character set을 처리한다.

Client의 character set을 변경하는 방법은 다음과 같다.

- [데이터 원본 구성](34-odbc.md#69c211015508ccf1)의 CHARSET 프로퍼티를 변경한다.
- 연결 문자열에 CHARSET 프로퍼티를 추가한다.
- pygoldilocks 모듈의 connect 메소드에 attrs_before 키워드를 사용한다.

위 세 가지 방법 모두 ODBC의 연결 프로퍼티 SQL_ATTR_CHARACTER_SET을 변경하고 PyDBC 라이브러리의 encoding도 설정한다.

<a id="42401a27f8b8f208"></a>
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

<a id="2cfcb84a2d40c338"></a>
#### EXPLAIN PLAN 조회

SQL 실행 시 cursor 속성을 설정하여 실행 계획을 함께 생성할 수 있다. 실행 계획 기능을 활성화한 상태에서 SQL을 실행하면, 처리가 완료된 후 cursor 속성을 통해 해당 SQL의 실행 계획을 조회할 수 있다.

다음과 같이 SQL은 일반적인 cursor.execute() 방식으로 실행하며, 실행 계획은 cursor attribute 함수를 통해 별도로 조회한다.

```
import pygoldilocks


conn = pygoldilocks.connect("DSN=GOLDILOCKS;UID=test;PWD=test;")
cur = conn.cursor()
try:
    cur.setattr( pygoldilocks.SQL_ATTR_EXPLAIN_PLAN_OPTION,
        pygoldilocks.SQL_EXPLAIN_PLAN_ON )
<code>    cur.execute("select * from t1 where i1 = ?", 1)
    plan = cur.getattr(pygoldilocks.SQL_ATTR_EXPLAIN_PLAN_TEXT)
    print(plan)</code>
finally:
    try:
        cur.setattr( pygoldilocks.SQL_ATTR_EXPLAIN_PLAN_OPTION,
            pygoldilocks.SQL_EXPLAIN_PLAN_OFF )
    finally:
        cur.close()
        conn.close()
```

위 예제를 실행하면 다음과 같이 SQL 실행 계획이 출력된다.

```
$ python test.py

< Execution Plan >
=====================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                       ROWS |
-----------------------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                          1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                          1 |
|    2  |      TABLE ACCESS ("T1")                                     |                          1 |
=====================================================================================================

     1  -  TARGET : T1.I1
     2  -  READ COLUMN : T1.I1
             PHYSICAL FILTER : T1.I1 = ?
```

<a id="ec81d02775010902"></a>
## API Reference

<a id="3d127f211007f916"></a>
### pygoldilocks 모듈

pygoldilocks object는 [Python Database API Specification v2.0](https://www.python.org/dev/peps/pep-0249/)을 준수한다.  
자세한 내용은 [Python DB API 모듈](https://www.python.org/dev/peps/pep-0249/#module-interface)을 참조한다.

<a id="af0ba2040b5f8ae1"></a>
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

<a id="7134ebe17bf0c95b"></a>
#### connect

데이터베이스에 새로운 연결을 생성한다.

```
connect( [connection_str], **kwargs )
```

ODBC 연결 문자열과 키워드를 입력한다. 키워드는 다음과 같다.

<a id="6c97b2bd028cdb7e"></a>
| 키워드 | 설명 | 기본값 |
| --- | --- | --- |
| connection_str | 선택적인 positional 문자열 인자이다. 두 개 이상의 값이 지정되거나 문자열이 아닌 값이 지정되면 오류가 발생한다. | - |
| autocommit | auto commit 여부를 설정한다. False인 경우 connection.commit을 호출해야 데이터베이스에 변경 사항이 반영된다. | False |
| readonly | True 인 경우 connection을 readonly 로 설정한다. | False |
| timeout | Connection을 위한 timeout을 설정한다. SQL_ATTR_LOGIN_TIMEOUT 속성으로 설정한다. | - |
| attrs_before | Connection 전에 설정해야 하는 속성을 지정한다. Dictionary 타입의 값을 입력한다. | - |
| user, password | 각각 GOLDILOCKS connection keyword 인 'uid', 'pwd'로 변환한다. | - |
| 그 밖의 키워드 | 문자열로 변환하여 'key=value;' 형식으로 connection  string 에 추가한다. | - |

connect() 는 하나의 GOLDILOCKS connection string, keyword 인자 또는 두 방식을 조합하여 새로운 connection 을 생성한다.

다음은 하나의 문자열로 connection 속성을 전달하는 예이다.

```
cnxn = pygoldilocks.connect("dsn=GOLDILOCKS;host=127.0.0.1;port=22581;uid=test;pwd=test" )
```

다음은 문자열과 keyword을 조합하여 connection 속성을 전달하는 예이다.

```
cnxn = pygoldilocks.connect("dsn=GOLDILOCKS",user="test",password="test",autocommit=True)
```

다음은 keyword로 connection 속성을 전달하는 예이다.

```
cnxn = pygoldilocks.connect( dsn="GOLDILOCKS", port=22581, user="test", autocommit=True )
```

autocommit, readonly, timeout, attrs_before는 PyDBC가 직접 처리하며 connection string에 추가하지 않는다.

- attrs_before
    - 연결 전에 설정되는 옵션을 지정한다. 이 옵션들은 [SQLSetConnectAttr](34-odbc.md#651a81593f5d4eb4)을 사용하여 설정한다. 속성과 값은 딕셔너리 타입으로 지정한다. 설정 가능한 속성에 대한 자세한 내용은 [ODBC 속성](34-odbc.md#634d5985cb809379)을 참조한다.

```
cnxn =  pygoldilocks.connect( "DSN=GOLDILOCKS", attrs_before={ pygoldilocks.SQL_ATTR_MAX_ROWS : 1000 })
```

<a id="39f6e4c12575e9aa"></a>
#### Date

```
>>> print pygoldilocks.Date(1984,11,23),  type(pygoldilocks.Date(1984,11,23))
1984-11-23 <type 'datetime.date'>
```

주어진 값에 해당하는 date 객체를 생성한다.

<a id="f6ed80e2137f6db5"></a>
#### Time

```
>>> print pygoldilocks.Time(11,23,23), type(pygoldilocks.Time(11,23,23))
11:23:23 <type 'datetime.time'>
```

주어진 값에 해당하는 time 객체를 생성한다.

<a id="4fd3c2aee8fc3bbd"></a>
#### Timestamp

```
>>> print pygoldilocks.Timestamp(1984,11,23,11,23,23), type(pygoldilocks.Timestamp(1984,11,23,11,23,23))
1984-11-23 11:23:23 <type 'datetime.datetime'>
```

주어진 값에 해당하는 datetime.datetime 객체를 생성한다.

<a id="b3a43059f77215d7"></a>
#### DATETIME

```
>>> print pygoldilocks.DATETIME(1984,11,23,11,23,23), type(pygoldilocks.DATETIME(1984,11,23,11,23,23))
1984-11-23 11:23:23 <type 'datetime.datetime'>
```

주어진 값에 해당하는 datetime.datetime 객체를 생성한다. [Timestamp](#4fd3c2aee8fc3bbd)와 동일하다.

<a id="bc60ccedb148d8e0"></a>
#### Binary

```
>>> print pygoldilocks.Binary('binary'), type(pygoldilocks.Binary('binary'))
binary <type 'bytearray'>
```

주어진 값에 해당하는 bytearray 객체를 생성한다. [BINARY](#31482ce69958b7c1)와 동일하다.

<a id="31482ce69958b7c1"></a>
#### BINARY

```
>>> print pygoldilocks.BINARY('binary'), type(pygoldilocks.BINARY('binary'))
binary <type 'bytearray'>
```

주어진 값에 해당하는 bytearray 객체를 생성한다.

<a id="f0a2c41f2154c15f"></a>
#### STRING

```
>>> print pygoldilocks.STRING('str'), type(pygoldilocks.STRING('str'))
str <type 'str'>
```

주어진 값에 해당하는 str 객체를 생성한다.

<a id="c79d6f00b2b9eadd"></a>
#### NUMBER

```
>>> print pygoldilocks.NUMBER(100.001), type(pygoldilocks.NUMBER(100.001))
100.001 <type 'float'>
```

주어진 값에 해당하는 float 객체를 생성한다.

<a id="d0ca6b2f5d80240a"></a>
#### ROWID

```
>>> print pygoldilocks.ROWID('AA'), type(pygoldilocks.ROWID('AA'))
AA <type 'str'>
```

데이터베이스의 row ID column을 기술하기 위해 사용되며 str 객체를 반환한다.

<a id="b7e76efd5029d4be"></a>
#### TimeFromTicks

```
>>> pygoldilocks.TimeFromTicks(10)
datetime.time(9, 0, 10)
```

인자값으로 설정된 datetime.time 객체를 반환한다.

<a id="4271470008da343e"></a>
#### DateFromTicks

```
>>> pygoldilocks.DateFromTicks(360000)
datetime.date(1970, 1, 5)
```

인자값으로 설정된 datetime.date 객체를 반환한다.

<a id="427160d2a65a5137"></a>
#### TimestampFromTicks

```
>>> pygoldilocks.TimestampFromTicks(360000)
datetime.datetime(1970, 1, 5, 13, 0)
```

인자 값으로 설정된 datetime.datetime 객체를 반환한다.

<a id="d84f3096c200b9b8"></a>
#### setDecimalSeparator

데이터베이스로부터 얻은 NUMERIC 타입의 소수점 구분 문자를 설정한다. 기본값은 .를 사용한다.

<a id="c1ef3181e39a83ac"></a>
#### getDecimalSeparator

설정된 NUMERIC 타입의 소수점 구분 문자를 얻는다.

<a id="6caecbd19ce7a89c"></a>
### Connection

데이터베이스와 연결을 관리하는 객체이며 pygoldilocks 모듈의 connect() 함수로 생성된다.

<a id="04a321886192337c"></a>
#### 속성

<a id="316bb46202e23005"></a>
##### Python 2/3

- autocommit
    - Connection 의 autocommit 모드를 설정한다.

- searchescape
    - ODBC의 SQLGetInfo(SQL_SEARCH_PATTERN_ESCAPE) 가 반환한 패턴 escape 문자이다.

- timeout
    - 새 cursor의 기본 query timeout을 설정한다. 
    - SQLSetConnectAttr 함수를 사용하여 SQL_ATTR_QUERY_TIMEOUT 속성을 설정한다.

- maxwrite
    - 문자 및 바이너리 매개변수를 직접 bind 할지 SQLPutData 를 사용하여 전송할지 결정하는 기준이 되는 크기를 byte 단위로 지정한다.
    - 값이 0인 경우 드라이버와 데이터 타입에 따른 기본 기준을 사용한다. 사용자 지정 값은 255 이상이어야 한다. 
    - 이 값은 input 전송 방식만 변경할 뿐, 값을 자르거나 fetch 결과 크기를 제한하지 않는다.

<a id="e34548d7eca8de9c"></a>
##### Python 3

- closed
    - connection 핸들이 닫힌 경우에는 true 이고, 사용할 수 있는 경우에는 false 이다.

- messages
    - connection operation에서 발생한 DB-API warning 목록이다. 각 항목은 (Warning, warning instance) 형식이다.
    - connection method는 새로운 operation을 시작하기 전에 기존 목록을 삭제하므로 operation 직후 확인해야 한다.

<a id="27ca3b7d8b189859"></a>
#### 함수

<a id="fc66bdbba744d192"></a>
##### Python 2/3

- cursor()
    - 새로운 cursor 객체를 반환한다.

- commit()
    - 실행했던 SQL 구문을 commit 한다.

- rollback()
    - 실행했던 SQL 구문을 rollback 한다.

- close()
    - 연결을 닫는다. autocommit이 false인 경우, commit 되지 않았던 SQL 구문이 rollback 된다.

- getinfo( info )
    - ODBC의 SQLGetInfo 함수를 이용하여 연결 관련 속성을 얻을 수 있다. 자세한 내용은 [SQLGetInfo](34-odbc.md#0d999c9ecf635595)를 참조한다.

```
dsn_name = cnxn.getinfo( pygoldilocks.SQL_DATA_SOURCE_NAME )
```

- execute( sql, [*params] )
    - 새 cursor 객체를 생성하고 이 객체의 execute 함수를 실행한 후 cursor 객체를 반환한다.

```
cursor = cnxn.execute( "SELECT COUNT(*) FROM EMP" )
```

자세한 내용은 [Cursor.execute()](#2cfcb84a2d40c338) 함수를 참조한다. 이 함수는 Python DB-API 2.0 표준에는 없지만 편의를 위해 제공된다. 이 함수가 호출될 때마다 cursor 객체가 할당되기 때문에 하나 이상의 SQL 구문을 실행해야 하는 경우에는 사용을 권장하지 않는다.

- set_attr( attr_id, value )
    - [SQLSetConnectAttr](34-odbc.md#651a81593f5d4eb4) 함수를 실행하여 연결 속성을 설정할 수 있다.
    - 다음은 set_attr 함수를 사용하여 데이터베이스의 트랜잭션 격리 단계를 조절하는 예이다.

```
connection.set_attr( pygoldilocks.SQL_ATTR_TXN_ISOLATION, pygoldilocks.SQL_TXN_SERIALIZABLE )
```

- __enter__, __exit__
    - 사용자가 직접 호출하는 일반 메소드가 아니라 with connection 문에서 자동으로 호출되는 특수 메소드이다. autocommit이 비활성화된 경우 정상 종료 시 commit 을 수행하고, 예외 발생 시 rollback 을 수행한다. 발생한 예외는 호출자에게 그대로 전달하며, connection 도 닫지 않는다.

<a id="5402d943a773b580"></a>
##### Python 3

- character_set_name()
    - 현재 connection 에서 사용하는 GOLDILOCKS character set 이름을 문자열로 반환한다.

<a id="5645d68fe1c294ac"></a>
###### **Output Converter**

Output converter는 connection 별로 등록되며, 해당 connection에서 생성한 모든 cursor에 적용된다. 동일한 SQL 타입에 converter를 다시 등록하면 기존 converter를 교체한다. 등록 상태는 result set이 생성되는 execute 시점에 결정되며, 이후 registry 변경 사항은 다음 execute 부터 반영된다.

Output converter 는 database character set 을 Python 문자열로 자동 변환하기 전의 raw bytes를 입력값으로 받는다. 따라서 converter에서 사용하는 codec은 해당 connection에서 실제로 사용하는 character encoding과 일치해야 한다.

- get_output_converter( sqltype )
    - 지정한 SQL 타입에 등록된 output converter callable을 반환한다. 등록된 converter 가 없는 경우 None을 반환한다.

- add_output_converter(sqltype, func)
    - 지정한 SQL 타입의 결과를 변환하는 callable 을 등록한다. callable 은 raw bytes 또는 SQL NULL 인 None을 입력값으로 받고 반환되는 값은 fetched row의 값으로 사용된다.

- remove_output_converter(sqltype)
    - 지정한 SQL 타입에 등록된 converter를 제거한다. 등록된 converter가 없어도 오류 없이 완료된다.

- clear_output_converters()
    - connection에 등록된 모든 output converter를 제거한다.

다음은 UTF-8 connection을 기준으로 SQL_VARCHAR 타입의 converter 가 raw bytes 또는 SQL NULL에 해당하는 None을 입력받는 예이다.

```
def uppercase_varchar(raw_value):
    if raw_value is None:
        return None
    return raw_value.decode("utf-8").upper()

cnxn.add_output_converter(
    pygoldilocks.SQL_VARCHAR,
    uppercase_varchar,
)

try:
    registered_converter = cnxn.get_output_converter(
        pygoldilocks.SQL_VARCHAR
    )
    assert registered_converter is uppercase_varchar

    cursor.execute(
        "select cast('alpha' as varchar(20)) "
        "from fixed_table_schema.dual"
    )
    assert cursor.fetchone()[0] == "ALPHA"
finally:
    # 등록되지 않은 converter를 제거해도 오류가 발생하지 않는다.
    cnxn.remove_output_converter(
        pygoldilocks.SQL_VARCHAR
    )

assert (
    cnxn.get_output_converter(pygoldilocks.SQL_VARCHAR)
    is None
)

# 등록된 모든 converter를 제거한다.
cnxn.clear_output_converters()

# 제거 결과는 다음 execute()부터 적용된다.
cursor.execute(
    "select cast('alpha' as varchar(20)) "
    "from fixed_table_schema.dual"
)
assert cursor.fetchone()[0] == "alpha"
```

- setencoding( encoding, ctype=SQL_CHAR )
    - SQL text와 문자열 매개변수를 byte로 인코딩할 Python codec 을 설정한다. ctype 에는 SQL_CHAR 만 지정할 수 있으며, wide character 타입은 지원하지 않는다.

```
cnxn.setencoding("cp949", ctype=pygoldilocks.SQL_CHAR)
```

- setdecoding( sqltype, encoding, ctype=SQL_CHAR )
    - 문자 result data를 Python 문자열로 디코딩할 codec을 설정한다. sqltype에는 SQL_CHAR 만 지정할 수 있으며, wide character 타입은 지원하지 않는다.

```
cnxn.setdecoding( sqltype=pygoldilocks.SQL_CHAR, encoding="cp949", ctype=pygoldilocks.SQL_CHAR )
```


> 
> - setencoding()과 setdecoding() 설정은 해당 connection에 적용되며, 같은 함수를 다시 호출하거나 connection 객체가 소멸할 때까지 유지된다. SQL 실행, commit, rollback 또는 cursor 종료 시 자동으로 초기화되지 않는다. 
> - 자동으로 감지한 codec 으로 되돌리는 reset API와 현재 설정된 codec 이름을 조회하는 API는 제공하지 않는다.
> - character_set_name() 은 데이터베이스 character set 이름을 반환하며, 마지막으로 설정한 Python codec 이름은 반환하지 않는다.
> - SQL_VARCHAR, SQL_LONGVARCHAR는 SQL column/parameter 타입으로는 지원하지만, setencoding()과 setdecoding()의 ctype 인자로는 사용할 수 없다.
> 

<a id="a60115e5a5db45df"></a>
### Cursor

일반적으로 cursor 객체는 fetch 작업을 관리하는데 사용되는 데이터베이스 cursor를 의미한다. 데이터베이스 cursor는 ODBC statement handle (HSTMT)에 매핑된다. 동일한 connection에서 생성된 각 cursor는 별도의 statement handle을 사용하며, result set에서의 위치도 독립적으로 관리된다. 따라서 한 cursor의 fetch 위치는 다른 cursor에 영향을 주지 않는다.   
단, transaction은 connection 단위로 관리되므로 한 cursor에서 수행한 변경 사항과 해당 connection의 commit/rollback 결과는 같은 connection의 다른 cursor에도 적용된다.

<a id="cfd40eda3a441317"></a>
#### 속성

<a id="d81aa9222a56e1bd"></a>
##### Python 2/3

<a id="3afaf92de2d84b01"></a>
###### **description**

읽기 전용 속성이며 튜플 타입으로 마지막에 수행된 SELECT 구문이 반환한 각 column에 대한 내용이 들어있다. 각 튜플은 다음을 포함한다.

1. Column name (또는 alias)
2. Type code
3. Display size
4. Internal size
5. Precision
6. Scale
7. Nullable

SELECT 구문이 호출되지 않은 경우, description은 None이다.

<a id="49b4e9410938823e"></a>
###### **rowcount**

DML 또는 executemany()가 마지막으로 영향을 준 row의 개수이다. 정확한 값을 알 수 없거나 SELECT 문인 경우 그 값은 -1이다. 여러 execution의 값을 정확히 합산할 수 있는 경우 합산한 값을 반환한다.

<a id="afff5b9af8455dea"></a>
###### **arraysize**

[fetchmany( [size = cursor.arraysize] )](#40216c6f5d0164fe) 함수를 사용하여 한 번에 가져올 수 있는 row의 개수이다. 기본값은 1이다.

<a id="4ee2c7ba4da21a7e"></a>
###### **connection**

읽기 전용 속성으로써 해당 cursor 객체를 생성한 connection 객체를 가리킨다.

<a id="e76f58c8e948178e"></a>
###### **fast_executemany**

True로 설정되면 [executemany( sql, [*params] )](#1028218c5fb765b6) 함수를 실행할 때 매개 변수를 배열로 구성하여 한 번의 execute로 처리한다. False로 설정되면 매개 변수마다 개별적으로 execute를 실행한다.

<a id="885b7d573cebb0d0"></a>
###### **timeout**

해당 cursor의 query timeout을 초 단위로 설정한다. 0은 timeout 없음을 의미한다. 생성 시 connection.timeout 값을 기본값으로 사용하며, 이후에는 cursor 단위로 독립적인 값을 설정할 수 있다.

<a id="4d6d21f4da5a3ed8"></a>
##### Python 3

<a id="2398c596bc3a925a"></a>
###### **closed**

Cursor 자체 또는 부모 connection이 닫힌 경우 true 이다.

<a id="abaf0fbdd2a2543c"></a>
###### **messages**

Cursor warning 목록이며, 각 항목은 (Warning, warning_instance) 형식이다.   
새로운 non-fetch operation 을 수행하면 기존 목록이 삭제된다. 반면, fetch는 기존 항목을 유지하면서 warning을 추가할 수 있다.

<a id="6df21c80cfdea214"></a>
#### 함수

<a id="85c7ac6508c1a192"></a>
##### execute( sql, [*params] )

SQLPrepare와 SQLExecute 함수를 통해 SQL 구문을 수행하고 이 함수를 호출한 cursor를 반환한다.   
옵션인 매개 변수는 다음과 같이 사용할 수 있다.

```
cursor.execute( "SELECT A FROM TEST WHERE B=? AND C=?", x, y )
```

```
cursor.execute( "SELECT A FROM TEST WHERE B=? AND C=?", (x, y) )
```

<a id="1028218c5fb765b6"></a>
##### executemany( sql, [*params] )

각 매개 변수에 대한 SQL 구문을 실행하고, 이 메소드를 호출한 cursor 객체를 반환한다. 매개 변수 params는 매개변수 묶음의 시퀀스이거나, 매개변수 묶음을 차례대로 반환하는 iterator 또는 generator 여야 한다.

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

<a id="4a862d89ee4ee9fd"></a>
##### fetchone()

질의의 다음 row를 반환한다. 다음 데이터가 없을 경우에는 None이다.

<a id="ec48de7d43cbcca7"></a>
##### fetchall()

질의에 남아 있는 모든 row를 반환한다. 모든 row를 메모리로 읽어들이기 때문에 사용 시 주의해야 한다.

<a id="27eb8c1db9ab866c"></a>
##### fetchval()

질의 결과에서 다음 row의 첫 번째 column 값을 반환한다. 다음 row가 없으면 None을 반환한다.

<a id="40216c6f5d0164fe"></a>
##### fetchmany( [size = cursor.arraysize] )

size나 cursor.arraysize 만큼 남아있는 row를 반환한다. 다음 데이터는 빈 list 데이터를 반환한다. cursor.arraysize의 기본값은 1이다.

<a id="5398b80c6dc1c6f1"></a>
##### commit()

SQL 구문을 commit 한다. Cursor 객체를 생성한 connection 객체가 실행하는 함수로써 동일한 connection 객체에 생성된 모든 cursor에 적용된다. Connection 객체의 commit과 동일하다.

<a id="202fba6c5ec56f33"></a>
##### rollback()

SQL 구문을 rollback 한다. Cursor 객체를 생성한 connection 객체가 실행하는 함수로써 동일한 connection 객체에 생성된 모든 cursor에 적용된다. Connection 객체의 rollback과 동일하다.

<a id="751d55d618a10fd8"></a>
##### skip( count )

SQLFetchScroll과 SQL_FETCH_NEXT를 통해 count에 지정된 횟수만큼 레코드를 통과한다.

<a id="3da79da684bc42c6"></a>
##### nextset()

다음 result set이 있으면 해당 result set으로 이동한 후 true를 반환한다. 더 이상 result set이 없으면 None을 반환한다.

<a id="3e0454358fa5672c"></a>
##### close()

Cursor 객체를 닫는다.

<a id="ff9cd94d00b0c62b"></a>
##### setinputsizes( sizes )

SQL을 실행할 때 입력 매개변수를 바인딩하는 데 사용할 타입과 크기 metadata를 미리 지정한다. sizes 의 각 항목은 SQL에 나타나는 매개변수 marker (?)와 순서대로 대응한다. 이 메소드는 값을 반환하지 않는다.

sizes 에는 sequence, iterator 또는 generator를 전달할 수 있다. 전달된 iterator 와 generator는 호출 시 한 번만 sequence 로 변환되며, 변환된 설정은 다른 값으로 변경하거나 setinputsizes(None) 을 호출할 때까지 같은 cursor 의 후속 실행에도 사용된다.

setinputsizes() 의 크기는 데이터를 지정된 길이로 자르거나 채우는 옵션이 아니다. 문자열 또는 binary 데이터보다 작은 크기로 지정하면 bind 또는 실행 과정에서 오류가 발생할 수 있으며, 데이터 일부가 잘려서 저장되지는 않는다. 데이터보다 큰 크기로 지정해도 원래 데이터는 변경되지 않는다. 고정 크기 정수에 작은 column size를 지정해도 정수 값은 잘리지 않는다.

다음은 세 개의 입력 매개변수에 대한 column size를 각각 10, 100, 1000 으로 설정하는 예이다.

```
cursor.setinputsizes((10, 100, 1000))

cursor.execute(
      "insert into sample(code, name, description) values(?, ?, ?)",
      "A01",
      "Goldilocks",
      "Database description",
  )
```

설정 항목이 SQL 매개변수 개수보다 적으면 나머지 매개변수는 실행 시 자동으로 감지된다. 특정 위치만 지정하려면 앞선 위치에 None을 사용한다.

다음은 첫 번째와 세 번째 parameter를 자동으로 감지하고, 두 번째 parameter의 크기만 지정하는 예이다.

```
cursor.setinputsizes((None, 100, None))

cursor.execute(
    "insert into sample(id, name, amount) values(?, ?, ?)",
    1,
    "Goldilocks",
    12500,
)
```

다음은 저장된 설정을 모두 제거하는 예이다.

```
cursor.setinputsizes(None)
```

일시적으로 적용한 설정인 경우, 예외 발생 여부와 관계없이 초기화가 보장되도록 try/finally 사용을 권장한다.

```
try:
    cursor.setinputsizes((10, 100))
    cursor.execute(
        "insert into sample(code, name) values(?, ?)",
        "A01",
        "Goldilocks",
    )
finally:
    cursor.setinputsizes(None)
```

<a id="167c66e95bb74213"></a>
###### **Python 2**

Python 2 에서는 sizes 의 각 항목에 음수가 아닌 int 또는 long 타입의 column size 를 지정할 수 있다.

<a id="f7ba334cb9fe6834"></a>
###### **Python 3**

Python 3에서는 각 입력 매개변수에 다음 형식 중 하나를 사용할 수 있다.

- None: 자동 감지한 SQL 타입과 column size 및 decimal digits를 유지한다.
- 음수가 아닌 정수: 자동 감지된 SQL 타입은 유지하고 column size 만 변경한다.
- 지원하는 Python 타입 객체: 해당 Python 타입에 대응하는 SQL 타입을 사용한다.
- (sql_type, column_size, decimal_digits): SQL 타입, column size, precision, decimal digits 또는 scale을 지정한다. 자동 감지를 유지할 항목에는 None을 지정한다.

지원하는 Python 타입 객체는 다음과 같다.

- str: SQL_VARCHAR
- float: SQL_DOUBLE
- bytes, bytearray: SQL_VARBINARY
- datetime.date: SQL_TYPE_DATE
- datetime.time: SQL_TYPE_TIME
- datetime.datetime: SQL_TYPE_TIMESTAMP

setinputsizes()는 일부 Python 타입 객체를 해당 SQL 타입으로 자동 변환한다. int, bool, decimal.Decimal 타입 객체는 이러한 자동 변환을 지원하지 않는다. 이런 타입을 사용하려면 tuple descriptor 의 첫 번째 항목에 적절한 SQL 타입 상수를 지정해야 한다.

다음은 첫 번째 매개변수를 SQL_INTEGER, 두 번째 매개변수를 NUMERIC(12, 3) metadata로 설정하여 바인딩 하는 예이다.

```
from decimal import Decimal

cursor.setinputsizes(
    (
        # SQL_INTEGER 타입만 지정하고 나머지 metadata는 자동 감지
        (pygoldilocks.SQL_INTEGER, None, None),
        # NUMERIC(12, 3)의 precision과 scale 지정
        (pygoldilocks.SQL_NUMERIC, 12, 3),
    )
)

try:
    cursor.execute(
        "insert into sample(id, amount) values(?, ?)",
        1,
        Decimal("12345.678"),)
finally:
    cursor.setinputsizes(None)
```

다음은 Python 타입 객체를 직접 사용하는 예이다.

```
from datetime import date, datetime, time

cursor.setinputsizes((str, float, bytes, bytearray, date, time, datetime))
```

다음은 위 예제의 Python 타입 객체를 SQL 타입 상수로 대체하는 예이다. SQL 타입 상수를 직접 나열하면 column size 로 해석되므로 동일하게 동작하지 않는다.

```
cursor.setinputsizes( (
    (pygoldilocks.SQL_VARCHAR, None, None), # str
    (pygoldilocks.SQL_DOUBLE, None, None), # float
    (pygoldilocks.SQL_VARBINARY, None, None), # bytes
    (pygoldilocks.SQL_VARBINARY, None, None), # bytearray
    (pygoldilocks.SQL_TYPE_DATE, None, None),
    (pygoldilocks.SQL_TYPE_TIME, None, None),
    (pygoldilocks.SQL_TYPE_TIMESTAMP, None, None), ) )
```

<a id="690fa2d38526f3a8"></a>
##### setoutputsize( size, column=None )

<a id="7aeedb940f0f8151"></a>
###### **Python 2**

설정을 cursor 에 저장하여 callproc() 의 LONG variable OUT parameter buffer 크기에 적용한다. Column은 1-based OUT parameter index 이며, None 을 지정하면 저장된 global/index 설정을 초기화한다. 이 API 는 일반 SELECT 의 fetch 크기를 제한하기 위한 것이 아니다.

```
try:
    # callproc() 의 두 번째 LONG VARCHAR OUT parameter의 buffer 크기에 적용
    cursor.setoutputsize(4096, 2)
    values = cursor.callproc("PROC_WITH_LONG_OUT", ("", ""))
finally:
    cursor.setoutputsize(None)
```

<a id="edb4e0a575a7daaa"></a>
###### **Python 3**

인자를 검증하지만 출력 크기나 데이터 값에는 영향을 주지 않는 DB-API compatibility no-op 이다.

<a id="92222af8e64b9094"></a>
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

<a id="c6f631a93e193523"></a>
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

result = cursor.callfunc( 'FUNC1', ( 1,  4) )
```

<a id="0cdfeacd43e252ba"></a>
##### tables( table=None, catalog=None, schema=None, tableType=None )

지정된 조건을 만족하는 데이터베이스의 테이블 정보를 반환한다. 문자 '_'와 '%'는 와일드 카드로 해석된다. 각 row는 다음의 column 정보를 가지는데 자세한 내용은 [SQLTables](34-odbc.md#5f69ef61aa8c52f2)를 참조한다.

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

<a id="9db0f65f4adeb3ed"></a>
##### columns( table=None, catalog=None, schema=None, column=None )

[SQLColumns](34-odbc.md#070bf505d8cf7865) 함수를 통해 조건에 맞는 column의 metadata를 반환한다. 각 row 에는 다음과 같은 column 정보가 포함된다.

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

<a id="00a8ad785c1b5108"></a>
##### procedureColumns( procedure=None, catalog=None, schema=None )

[SQLProcedureColumns](34-odbc.md#1a3fc8906c28fb9b) 함수를 통해 procedure의 return value, result column 및 IN, OUT, INOUT parameter metadata 정보를 얻는다.

1. procedure_cat
2. procedure_schem
3. procedure_name
4. column_name
5. column_type
6. data_type
7. type_name
8. column_size
9. buffer_length
10. decimal_digits
11. num_prec_radix
12. nullable
13. remarks
14. column_def
15. sql_data_type
16. sql_datetime_sub
17. char_octet_length
18. ordinal_position
19. is_nullable

<a id="181f1d133a71fb15"></a>
##### statistics( table, catalog=None, schema=None, unique=False, quick=True )

[SQLStatistics](34-odbc.md#16beae805fd502f1) 함수를 통해 지정된 테이블과 관련된 정보를 얻는다.  
unique가 true일 경우, unique 인덱스만 반환하고, false일 경우, 모든 인덱스를 반환한다.  
quick이 true일 경우, CARDINALITY와 PAGES는 즉시 사용할 수 있는 경우에만 반환되고 그렇지 않으면 해당 열에는 NULL이 반환된다.

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

<a id="868fc4ffcae76b4a"></a>
##### rowIdColumns( table, catalog=None, schema=None, nullable=True )

SQL_BEST_ROWID로 [SQLSpecialColumns](34-odbc.md#27b7b9edf68d9933)를 실행하여 row를 고유하게 식별하는 column의 결과 집합을 반환한다. 각 row는 다음과 같은 column 정보를 갖는다.

1. scope: SQL_SCOPE_CURROW, SQL_SCOPE_TRANSACTION, 또는 SQL_SCOPE_SESSION
2. column_name
3. data_type: ODBC의 SQL 타입 상수
4. type_name
5. column_size
6. buffer_length
7. decimal_digits
8. pseudo_column: SQL_PC_UNKNOWN, SQL_PC_NOT_PSEUDO 또는 SQL_PC_PSEUDO

<a id="4edbae70f15bad0d"></a>
##### rowVerColumns( table, catalog=None, schema=None, nullable=True )

SQL_ROWVER으로 [SQLSpecialColumns](34-odbc.md#27b7b9edf68d9933)를 실행하여 row가 업데이트 될 때 자동으로 업데이트 되는 column의 결과 집합을 반환한다. 각 row는 다음과 같은 column 정보를 갖는다.

1. scope: SQL_SCOPE_CURROW, SQL_SCOPE_TRANSACTION, 또는 SQL_SCOPE_SESSION
2. column_name
3. data_type: ODBC의 SQL 타입 상수
4. type_name
5. column_size
6. buffer_length
7. decimal_digits
8. pseudo_column: SQL_PC_UNKNOWN, SQL_PC_NOT_PSEUDO 또는, SQL_PC_PSEUDO

<a id="b6737031ae73eee3"></a>
##### primaryKeys( table, catalog=None, schema=None )

[SQLPrimaryKeys](34-odbc.md#1e974efc8e812867) 함수를 실행하여 테이블의 주요 키를 구성하는 column의 결과 집합을 반환한다. 각 row는 다음과 같은 column 정보를 갖는다.

1. table_cat
2. table_schem
3. table_name
4. column_name
5. key_seq
6. pk_name

<a id="e809a537065da8c7"></a>
##### foreignKeys( table=None, catalog=None, schema=None, foreignTable=None, foreignCatalog=None, foreignSchema=None )

[SQLForeignKeys](34-odbc.md#5b186d3690419bf7) 함수를 실행하여 지정된 테이블 또는 지정된 테이블의 기본 키를 참조하는 다른 테이블의 외래 키인 column 이름의 결과 집합을 만든다. 각 row는 다음과 같은 column 정보를 갖는다.

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

<a id="f47787a949e1adce"></a>
##### procedures( procedure=None, catalog=None, schema=None )

[SQLProcedures](34-odbc.md#5386c500d404f82e)를 실행하여 프로시저에 대한 정보의 결과 집합을 만든다. 각 row는 다음과 같은 column 정보를 갖는다.

1. procedure_cat
2. procedure_schem
3. procedure_name
4. num_input_params
5. num_output_params
6. num_result_sets
7. remarks
8. procedure_type

<a id="3b270321fd5052f5"></a>
##### getTypeInfo( sqlType=None )

[SQLGetTypeInfo](34-odbc.md#2e63d37e8577cdaa) 함수를 실행하여 지정된 데이터 타입 또는 GOLDILOCKS ODBC가 지원하는 모든 데이터 타입에 대한 정보의 결과 집합을 만든다. 각 row는 다음과 같은 column을 갖는다.

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

<a id="147f07bf2dbe94c1"></a>
##### getattr( attr )

[SQLGetStmtAttr](34-odbc.md#abd83b43236a505f) 함수를 실행하여 지정된 statement 속성 정보를 반환한다. 반환되는 값의 타입은 statement 속성에 따라 달라진다.

<a id="a6f33d82c539573b"></a>
##### setattr( attr, attr_value )

[SQLSetStmtAttr](34-odbc.md#a8c84e0cefef8510) 함수를 실행하여 지정된 statement 속성에 attr_value 를 설정한다.

<a id="8d2e7ecf7507d431"></a>
##### cancel()

현재 cursor 에서 실행 중인 statement 의 취소를 요청한다.

cancel() 은 취소 요청만 수행하며, 실제 취소 결과는 CLI가 반환하는 진단 정보에 따라 exception 으로 보고될 수 있다. 취소 후 cursor를 다시 사용할 수 있는지는 응용 프로그램에서 exception 처리 완료 후 확인해야 한다.

```
import threading

def cancel_running_statement():
    cursor.cancel()

timer = threading.Timer(1.0, cancel_running_statement)
timer.start()
try:
    cursor.execute("CALL DBMS_LOCK.SLEEP(10)")
finally:
    timer.cancel()
```

<a id="1e83a198bf3bdbb2"></a>
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

<a id="16fbff5c308aefc6"></a>
#### 속성

- cursor_description

해당 row를 생성한 cursor 객체의 속성 description의 복사본이다. 자세한 내용은 [Cursor.description](#cfd40eda3a441317)을 참조한다.

<a id="eacccc93eb5b265e"></a>
## Exception

Python 예외는 GOLDILOCKS ODBC에서 오류를 감지했을 때 pygoldilocks에 의해 발생한다. 예외 클래스는 다음과 같이 [Python DB API](https://www.python.org/dev/peps/pep-0249/#exceptions) 와 동일하다.

```
Exception
├── Warning
└── Error
    ├── InterfaceError
    └── DatabaseError
        ├── DataError
        ├── OperationalError
        ├── IntegrityError
        ├── InternalError
        ├── ProgrammingError
        └── NotSupportedError
```

오류가 발생할 경우, 일반적으로 예외 유형은 데이터베이스에서 제공하는 SQLSTATE 값을 기반으로 처리된다.

<a id="dbd526b502bb9290"></a>
| SQLSTATE | Exception |
| --- | --- |
| 01002 | OperationalError |
| 08001, 08003, 08004, 08007, 08S01 | OperationalError |
| 0A000 | NotSupportedError |
| 28000 | InterfaceError |
| 40002 | IntegrityError |
| 22*** | DataError |
| 23*** | IntegrityError |
| 24***, 25***, 42*** | ProgrammingError |
| HY001, HY014, HYT00, HYT01 | OperationalError |
| IM001, IM002, IM003 | InterfaceError |

<a id="8ef02949fadcd9c4"></a>
## Data Type

<a id="67f9e2a854bb8d2c"></a>
### Python 매개 변수를 GOLDILOCKS로 전달

Python 매개 변수를 GOLDILOCKS ODBC에 전달할 때는 다음과 같이 데이터가 변환된다.

**Python 3**

<a id="737f5d061a761585"></a>
| Python datatype | 설명 | ODBC datatype |
| --- | --- | --- |
| None | - | SQL_VARCHAR |
| str | connection의 writing codec 으로 사용할 encoding | SQL_VARCHAR or SQL_LONGVARCHAR |
| bytes, bytearray | binary | SQL_VARBINARY or SQL_LONGVARBINARY |
| bool | boolean | SQL_BIT |
| datetime.date | date | SQL_TYPE_DATE |
| datetime.time | time | SQL_TYPE_TIME |
| datetime.time | time with time zone | SQL_TYPE_TIME_WITH_TIMEZONE |
| datetime.datetime | timestamp | SQL_TYPE_TIMESTAMP |
| datetime.datetime | timestamp with time zone | SQL_TYPE_TIMESTAMP_WITH_TIMEZONE |
| int | integer | SQL_BIGINT |
| float | floating point | SQL_DOUBLE |
| decimal | numeric | SQL_NUMERIC |

**Python 2**

<a id="69be97af2cd50b3e"></a>
| Python datatype | 설명 | ODBC datatype |
| --- | --- | --- |
| None | - | SQL_VARCHAR |
| str | byte string | SQL_VARCHAR or SQL_LONGVARCHAR |
| unicode | connection 의 character encoding 으로 변환 | SQL_VARCHAR or SQL_LONGVARCHAR |
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

<a id="7d29677601b07d8d"></a>
### GOLDILOCKS로부터 전달받는 SQL 값

GOLDILOCKS 데이터베이스의 데이터를 Python으로 전달할 때는 다음과 같이 데이터가 변환된다.

**Python 3**

<a id="5f671fd3b66827a7"></a>
| ODBC datatype | 설명 | Python datatype |
| --- | --- | --- |
| any | NULL | None |
| SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR | text | str |
| SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY | binary | bytes |
| SQL_NUMERIC | decimal, numeric | decimal.Decimal |
| SQL_BOOLEAN | bit, bool | bool |
| SQL_SMALLINT, SQL_INTEGER | integers | int |
| SQL_BIGINT | long | int |
| SQL_REAL, SQL_FLOAT, SQL_DOUBLE | floating point | float |
| SQL_TYPE_TIME | time | datetime.time |
| SQL_TYPE_DATE | date | datetime.date |
| SQL_TYPE_TIMESTAMP | timestamp | datetime.datetime |
| SQL_TYPE_TIME_WITH_TIMEZONE | time with timezone | datetime.time |
| SQL_TYPE_TIMESTAMP_WITH_TIMEZONE | timestamp with timezone | datetime.datetime |
| SQL_C_INTERVAL_*** | interval | str |
| SQL_ROWID | rowid | str |

**Python 2**

<a id="580bd8c319b93c95"></a>
| ODBC datatype | 설명 | Python datatype |
| --- | --- | --- |
| any | NULL | None |
| SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR | text | text |
| SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY | binary | bytearray |
| SQL_NUMERIC | decimal, numeric | decimal.Decimal |
| SQL_BOOLEAN | bit, bool | bool |
| SQL_SMALLINT, SQL_INTEGER | integers | int |
| SQL_BIGINT | long | long |
| SQL_REAL, SQL_FLOAT, SQL_DOUBLE | floating point | float |
| SQL_TYPE_TIME | time | datetime.time |
| SQL_TYPE_DATE | date | datetime.date |
| SQL_TYPE_TIMESTAMP | timestamp | datetime.datetime |
| SQL_TYPE_TIME_WITH_TIMEZONE | time with timezone | text |
| SQL_TYPE_TIMESTAMP_WITH_TIMEZONE | timestamp with timezone | text |
| SQL_C_INTERVAL_*** | interval | text |
| SQL_ROWID | rowid | text |

Python 데이터 타입의 text는 Python 3에서는 unicode로 변환된다. Python 2에서는 데이터베이스의 character set에 따라 unicode나 string으로 변환된다.

**Python 2 text**

<a id="477ecdda9826122d"></a>
| DB character set | Python type |
| --- | --- |
| UTF-8 | str |
| SQL_ASCII | str |
| UHC | unicode |
| GB18030 | unicode |

---

[← 37. PDO](37-pdo.md) · [전체 목차](../README.md) · [39. aiogoldilocks →](39-aiogoldilocks.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
