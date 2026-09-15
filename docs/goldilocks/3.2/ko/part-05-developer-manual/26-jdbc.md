<a id="68d137984549bd4d"></a>

# 26. JDBC

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/68d137984549bd4d)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 25. ODBC](25-odbc.md) · [전체 목차](../README.md) · [27. Embedded SQL →](27-embedded-sql.md)

<a id="0b0bffb3cbbfdb61"></a>
## GOLDILOCKS JDBC 개요

<a id="6ff65f612e3a2aba"></a>
### GOLDILOCKS JDBC 소개

GOLDILOCKS는 TCP/ IP 연결을 기반으로 한 표준 JDBC 4.0을 준수 (일부 기능 제외)하는 GOLDILOCKS JDBC 드라이버를 제공한다. 사용자는 GOLDILOCKS JDBC 드라이버를 이용하여 Java 프로그램 내에서 GOLDILOCKS와 접속하여 각종 트랜잭션 기능 및 데이터 조회 기능을 사용할 수 있다. GOLDILOCKS JDBC 드라이버는 JDK 1.6 기반으로 작성되고 구축되었기 때문에 JDBC 4.0의 기능을 지원한다. $GOLDILOCKS_HOME/lib/goldilocks6.jar 파일을 class path에 추가하여 드라이버를 사용할 수 있다.

뿐만 아니라 하위 버전의 Java (JDK 1.4, JDK 1.5)를 사용하는 사용자를 위해 JDBC 3.0을 구현한 goldilocks4, goldilocks5.jar도 함께 지원한다. goldilocks 다음의 숫자는 JDK 버전을 의미한다. 자세한 내용은 [버전 및 지원 여부](#d0bf1a5a538a9715)를 참조한다.

GOLDILOCKS JDBC는 JDBC 표준 스펙을 대부분 준수하고 있으며 일부 고유한 기능을 제공하기 위해 표준 API가 아닌 method와 클래스도 지원한다. 비표준 method에 대해서는 [JDBC API References](#18ec3add277117c4)의 각 클래스 API나 [추가 타입 사용](#94b4ca2893aa3371)을 참조한다.

<a id="d7defb0365cbe340"></a>
### 특징

- Type-4 JDBC 드라이버

GOLDILOCKS JDBC는 순수 Java로만 구현된 JDBC Type-4 유형이다. 추가적인 라이브러리 없이 jar 파일만으로 JDBC 드라이버를 사용할 수 있다. 뿐만 아니라 JDBC-ODBC bridge 유형보다 빠르고 안정적이며 native API를 사용한 Type-2보다 이식성 (portability)이 좋다.

- JDBC 표준 준수

GOLDILOCKS JDBC는 JDBC 표준을 준수하므로 여타의 JDBC 프로그램을 거의 변경하지 않고 재활용할 수 있다. Connection을 얻는 방법부터 각종 statement, ResultSet 기능들을 수정없이 사용할 수 있다. 단, connection URL과 프로퍼티 이름, 로딩할 드라이버 클래스 이름은 GOLDILOCKS에 맞게 변경해야 한다. 그리고 표준에 없는 기능과 타입들은 별도의 클래스와 method API로 사용할 수 있다.

- 다양한 Java 버전 지원

GOLDILOCKS JDBC 드라이버는 네 개의 파일 (goldilocks7.jar, goldilocks6.jar, goldilocks5.jar, goldilocks4.jar)를 지원하므로 사용자는 Java 실행 환경에 맞는 파일을 선택하여 사용할 수 있다. 각각의 jar 파일은 JDK 1.7, JDK 1.6, JDK 1.5, JDK 1.4를 기반으로 제작, 구축되었기 때문에 JDBC 4.1, JDBC 4.0, JDBC 3.0, JDBC 3.0 스펙을 따른다.

- 서버와의 유연한 버전 호환성

서버와 JDBC 드라이버와의 호환성은 프로토콜 버전을 참조한다. 서버가 JDBC 드라이버보다 프로토콜 버전이 높을 경우에 접속할 수 있다.

- Connection pooling을 위한 API 지원

JDBC connection 객체는 생성 비용이 비싼 자원이다. 따라서 JDBC 표준에는 이를 풀링할 수 있는 체계를 정의했으며 그것을 인터페이스로 만든 것이 ConnectionPoolDataSource와 PooledConnection이다. GOLDILOCKS JDBC는 이 인터페이스를 구현하여 제3자의 미들웨어 제품에서 풀링 기능을 사용할 수 있도록 하는 기반을 제공한다.

- XA API 지원

글로벌 트랜잭션 표준인 XA 인터페이스를 구현하여 사용자가 글로벌 트랜잭션 작업을 할 수 있도록 한다. JDBC 인터페이스인 XAResource를 사용하여 각종 XA 기능을 표준에 맞게 수행할 수 있다.

- GOLDILOCKS 고유 데이터 타입

GOLDILOCKS는 JDBC 표준에서 제공하지 않는 데이터 타입을 사용한다. 예를 들어 interval 관련 타입과 timestamp with time zone과 같이 time zone 정보를 가지는 타입들이 있다. 이들 타입들을 데이터베이스에 삽입하거나 가져올 수 있는 방법들을 드라이버가 제공한다.

- 서버 기반의 강력한 커서 스크롤 기능

타 JDBC 드라이버들은 ResultSet 스크롤을 위해 row set을 드라이버 내에서 캐싱하는 방법을 취하여, client 응용 프로그램이 과도하게 메모리를 많이 사용하는 경우가 있다. 예를 들어 scroll insensitive로 커서를 열어 마지막 row까지 fetch하게 되면 모든 row들을 드라이버 내에 캐싱하게 되는데 이 때 전체 테이블이 client 메모리에 상주하게 되므로 out of memory 에러가 발생할 수도 있고, 과도하게 client 메모리 리소스를 소모하게 된다.

하지만 GOLDILOCKS는 서버 내에 커서 스크롤 기능이 있기 때문에 client가 가볍고, 빠르고 안정적인 성능을 낼 수 있다.

- 효율적인 자원 사용

타 JDBC 드라이버들에 비해 row 정보를 유지하는 메모리를 최소화하고, 되도록 Java 객체를 사용하지 않기 때문에 많은 row들을 탐색할 경우에도 garbage collection 작업을 피할 수 있으며 적은 메모리를 사용하도록 하여 빠르고 안정적으로 테이블을 스캔할 수 있다.

- 정확하고 방대한 메타 데이터

JDBC 표준의 DatabaseMetaData 인터페이스를 충실하고 정확하게 구현했기 때문에 다양한 데이터베이스 툴과 쉽게 연계할 수 있다. 뿐만 아니라 각종 시스템 view를 통해 데이터베이스 메타 정보들을 조회할 수 있어 사용성이 높아졌다.

- 강력한 로깅 기능

문제가 발생했을 때 뿐만 아니라 평상시에도 JDBC API 콜이나 네트워크 사용 상황을 모니터링 할 수 있도록 각종 logging 기능을 제공한다. Connection URL에 로깅 관련 기능을 명세하면 콘솔이나 파일 등으로 해당 내용의 기록을 남길 수 있다. 로깅에는 JDBC method call 기록에 대한 로깅, 프로토콜 송수신에 대한 로깅, 사용한 SQL 문에 대한 로깅, 이 세 가지가 있다.

- Connection failover

GOLDILOCKS 서버와의 연결에 실패하거나 execution 할 때 연결이 끊어지면 미리 등록된 대체 서버에 자동으로 다시 접속하여 기존 connection을 계속해서 사용할 수 있도록 JDBC driver 레벨의 connection failover를 지원한다. 사용자는 connection이 끊겼을 때를 대비한 별도의 예외 처리없이 기존의 JDBC 프로그램으로 connection failover 기능을 사용할 수 있다.

- 서버와 direct attach 연결 가능

TCP/ IP 기반의 연결 이외에 서버와 같은 프로세스로 연동할 수 있는 Direct Attach 방식의 연결도 할 수 있다. ODBC 연결이 Direct Attach, Client/ Server 방식을 모두 지원하듯이 GOLDILOCKS JDBC driver도 두 가지 연결 방법을 모두 제공한다. Direct attach로 연결된 JDBC 프로그램은 TCP/ IP 통신을 하지 않고 직접 서버 프로세스에 연동되어 jvm 안에서 서버 기능을 사용할 수 있다. TCP/ IP로 연결한 JDBC 프로그램보다 두 배 이상의 성능을 낼 수 있다.

<a id="d0bf1a5a538a9715"></a>
### 버전 및 지원 여부

<a id="b22f98f161f5c72a"></a>
#### GOLDILOCKS JDBC 버전 체계

goldilocks6.jar 파일에 대해 다음과 같이 실행하면 GOLDILOCKS JDBC 버전 정보를 볼 수 있다.

```
shell>java -jar goldilocks6.jar

 GOLDILOCKS JDBC Driver 1.1 Procotol-1.3.1, JDBC4.0 compiled with JDK1.6
```

위 예제는 현재 GOLDILOCKS JDBC의 드라이버 버전이 1.0이고, 프로토콜 버전은 1.3.1, 그리고 이 드라이버가 준수하는 JDBC 표준 버전은 4.0이며 JDK 1.6에서 구축되었다는 정보를 담고 있다. 드라이버 버전은 GOLDILOCKS 제품 버전과는 별개인 드라이버의 버전을 나타내고 기능이 보강될 때마다 올라간다. JDBC 드라이버 버전에 대한 자세한 내용은 DatabaseMetaData의 [getDriverMajorVersion](#7ef8b5503e1ed230), [getDriverMinorVersion](#bf5cdf346b811809), [getDriverVersion](#58056f8238b068e0)을 참조한다.

프로토콜 버전은 서버와의 호환성 여부를 결정하며 드라이버는 서버의 프로토콜 버전과 같거나 더 낮을 때 서버에 연동될 수 있다. 즉, 서버는 하위 프로토콜 버전의 모든 client API를 지원한다.

goldilocks6.jar는 JDBC 4.0 표준을 준수하며 JDK 1.6에서 구축되었다. 따라서 사용자 Java 환경이 JDK 1.6이상일 경우에는 goldilocks6.jar를 사용하면 된다. 만일 JDK 1.7 이상의 Java를 사용할 경우, goldilocks6.jar는 사용할 수 있지만 JDBC 5.0의 API나 클래스들은 사용할 수 없다.

JDK 1.5나 1.4 환경의 Java를 사용할 경우, goldilocks5.jar나 goldilocks4.jar를 사용해야 한다. 이 둘은 모두 JDBC 3.0 표준을 준수한다.

<a id="9f43f358d5575a1a"></a>
### 사용 예

<a id="bf7c706043251a53"></a>
#### Class Path 설정

GOLDILOCKS JDBC 드라이버를 사용하려면 CLASSPATH를 설정해야 한다.

```
export CLASSPATH=.:$GOLDILOCKS_HOME/lib/goldilocks6.jar
```

또는 사용자의 Java 실행환경에 맞는 jar 파일을 path에 추가해도 된다.

<a id="008f16a906a978c7"></a>
#### 드라이버 클래스 로딩

드라이버 클래스는 다음과 같이 로딩할 수 있다.

```
Class.forName("sunje.goldilocks.jdbc.GoldilocksDriver");
```

위 예는 전통적인 JDBC 사용 방법으로써 해당 드라이버 클래스를 동적으로 로딩하여 DriverManager에 등록하게 한 다음 연결을 얻는다. 요즘은 DataSource를 통해 연결을 얻는 방법을 더 많이 사용하는데 이에 대해서는 [JDBC API References](#18ec3add277117c4)의 해당 클래스를 참조한다.

<a id="8176075ce720dbad"></a>
#### Connection 얻기

Connection을 얻으려면 다음과 같이 코드를 작성한다.

```
Connection con = DriverManager.getConnection(
    "jdbc:goldilocks://127.0.0.1:22581/test", "TEST", "test");
```

GOLDILOCKS JDBC를 사용하기 위한 접속 URL은 "jdbc:goldilocks:"로 시작해야 한다. 그 다음은 서버의 IP와 port 번호이며 URL의 마지막 부분 "/test"는 DB 이름이다. 현재 GOLDILOCKS는 다중 DB를 지원하지 않으므로 DB 이름을 특별히 체크하지는 않는다. 사용자가 접속한 URL은 DatabaseMetaData.getURL()을 통해서 다시 얻을 수 있다.

IP를 0.0.0.0으로, 포트를 0으로 설정하면 Direct Attach (D/A) 모드로 접속한다. 혹은 ip:port 대신 da라는 접속 프로토콜을 사용해도 된다. 즉 다음 두 URL 모두 D/A 모드로 접속하게 한다.

```
"jdbc:goldilocks://0.0.0.0:0/test"
"jdbc:goldilocks:da/test"
```

Username과 password는 각각 데이터베이스의 계정과 암호를 사용해야 한다.

<a id="d3b9326357fe93a8"></a>
#### Statement와 ResultSet 사용

Statement와 ResultSet은 다른 JDBC 프로그램과 동일하게 사용하면 된다.

```
Statement stmt = con.createStatement();
ResultSet rs = stmt.executeQuery("SELECT NAME, ADDRESS FROM EMP");
while (rs.next())
{
    System.out.println("name = " + rs.getString(1));
    System.out.println("address = " + rs.getString(2));
}
rs.close();
stmt.close();
```

<a id="b12f4689eb75f2f3"></a>
## 기능 명세

<a id="d9172ae65a8ca8dc"></a>
### 연결

<a id="8d3582227d16c5e1"></a>
#### DriverManager를 이용한 연결

Connection을 얻는 전통적인 방법은 DriverManager를 사용하는 것이다.

```
Connection con = DriverManager.getConnection(url_string, user_name, password);
```

url_string에는 다음과 같은 세가지 유형이 있다.

```
jdbc:goldilocks://[ip address]:[port_no]/[db_name]
```

```
jdbc:goldilocks:da/[db_name]
```

```
jdbc:goldilocks:locator//[ip address]:[port_no][, [ip address]:[port_no] ]*/[db_name]
```

IP address에는 IPv4, IPv6 모두 사용 가능하며, port_no에는 설정된 포트 번호를 명시하면 된다. db_name은 현재 접속에 사용되지 않기 때문에 어떤 이름이든 설정할 수 있지만 생략할 수는 없다. 다음은 예제 URL이다.

```
String url_string = "jdbc:goldilocks://127.0.0.1:22581/test";
```

IP "0.0.0.0"과 포트 0은 D/A 접속을 위한 특별한 주소로 사용된다. D/A 모드에 대한 자세한 내용은 [Direct Attach 모드 접속](#5531ea2737958fa0)을 참조한다.

user_name과 password는 GOLDILOCKS 계정을 의미한다.

위의 getConnection() method 외에 각종 property를 설정하기 위해 다음 method를 사용한다.

```
Properties prop = new Properties();
prop.setProperty("user", user_name);
prop.setProperty("password", password);
Connection con = DriverManager.getConnection(url_string, prop);
```

glocator로부터 서버의 접속 정보를 얻기 위해 연결 프로퍼티를 대신하여 url_string에 locator 키워드를 추가하여 사용할 수 있다. 이 때 ip address와 port_no는 glocator의 접속 정보로 간주한다. 다음은 연결 구문에 locator 키워드를 사용하는 예이다.

```
String url_string = "jdbc:goldilocks:locator//127.0.0.1:42581,127.0.0.1:42582/test?locator_service=S1";
```

처음 접속 정보 127.0.0.1:42581은 glocator의 접속 정보이고 이후의 접속 정보는 127.0.0.1:42582처럼ALTERNATE_LOCATORS 프로퍼티로 처리된다.

다음은 위의 url_string과 같은 의미의 프로퍼티 설정이다.

```
String url_strng = "jdbc:goldilocks://0.0.0.0:0/test";
Properties prop = new Properties();
prop.setProperty("locator_host", "127.0.0.1");
prop.setProperty("locator_port", "42581");
prop.setProperty("alternate_locators", "127.0.0.1:42582");
prop.setProperty("locator_service", "S1");
Connection con = DriverManager.getConnection(url_string, prop);
```

접속에 사용할 수 있는 프로퍼티 목록은 GOLDILOCKSDriver의 getPropertyInfo() method를 통해 확인할 수 있다. 자세한 내용은 [연결 프로퍼티](#2081c33a3f3f0333)를 참조한다.

DriverManager를 사용하면 생성되는 connection 객체의 login timeout과 logger는 DriverManager에 등록된 값을 사용한다. 즉, 이 connection 객체로부터 생성되는 모든 JDBC 인터페이스들이 사용하는 logger는 저 logger이다. 따라서 connection 객체마다 개별 logger를 가질 수 없다.

<a id="4732f956814f8ad6"></a>
#### DataSource를 이용한 연결

JDBC 표준은 과거의 DriverManager보다는 DataSource를 사용할 것을 더 권장한다. DataSource는 어떤 data source에 접근할 수 있도록 하는 단일한 인터페이스이며, 각종 data source에 관계되는 설정 값들을 개별적으로 설정할 수 있으며, DataSource 객체 자체를 원격으로 전송할 수도 있기 때문이다.

다음과 같이 DataSource를 통해 connection 객체를 얻을 수 있다.

```
import sunje.goldilocks.jdbc.GoldilocksDataSource;

GoldilocksDataSource ds = new GoldilocksDataSource();
ds.setServerName("127.0.0.1");
ds.setPortNumber(22581);
ds.setDatabaseName("test");
ds.setUser("TEST");
ds.setPassword("test");
Connection con = ds.getConnection();
```

이처럼 DataSource 객체를 생성하기 위해서는 GoldilocksDataSource 클래스를 사용해야 한다.

그 다음 각종 연결 정보는 DataSource 표준 API가 아닌 setter method를 사용해야 하는데, 자세한 내용은 [DataSource](#c0867ea7d7189a10)를 참조한다.

DriverManager를 이용할 때는 login timeout과 logger를 글로벌하게 설정했어야 했지만, DataSource는 login timeout과 logger를 개별적으로 설정할 수 있다.

```
ds.setLoginTimeout(10);
ds.setLogWriter(out);
```

<a id="4aba0f5264d1e44c"></a>
#### 미들웨어 연동

Weblogic, JBoss와 같은 미들웨어와 연동하려면 XADataSource, ConnectionPoolDataSource 인터페이스를 구현한 클래스 이름을 알아야 한다. GOLDILOCKS에서는 sunje.goldilocks.jdbc 패키지에 GoldilocksXADataSource, GoldilocksConnectionPoolDataSource를 제공한다. 이 두 클래스 모두 GoldilocksDataSource와 마찬가지로 각종 setter method를 제공한다.

```
import sunje.goldilocks.jdbc.GoldilocksXADataSource;

GoldilocksXADataSource ds = new GoldilocksXADataSource();
ds.setServerName("127.0.0.1");
ds.setPortNumber(22581);
ds.setDatabaseName("test");
ds.setUser("TEST");
ds.setPassword("test");
XAConnection con = ds.getXAConnection();
```

<a id="2e3a6037193b88a9"></a>
#### 연결 프로퍼티

**연결 프로퍼티**

<a id="2081c33a3f3f0333"></a>
| 이름 | 필수/선택 | 유효값 | 설명 |
| --- | --- | --- | --- |
| alternate_servers | 선택 | IP:PORT[,IP:PORT]+ | Failover를 위한 대체 서버 목록이다. 콤마 (,)로 구분한다. |
| batch_count | 선택 | Any integer | 한 번의 프로토콜 송수신으로 처리할 수 있는 batch job 개수이다. 기본값은 1000이다. 이 값이 너무 작으면 배치를 처리할 때 네트워크 송수신이 잦아져 성능이 저하될 수 있고, 너무 크면 세션이 execution result들을 쌓아놔야 하기 때문에 서버 메모리가 증가될 수 있다. |
| connection_retry_count | 선택 | Any integer | 연결할 때의 재시도 횟수를 저장한다. 기본값은 0이고 재시도하지 않는다. |
| connection_retry_delay | 선택 | Any integer | 연결을 재시도할 때 재시도 하기 전의 delay를 초 단위로 지정한다. 기본값은 3이다. |
| date_format | 선택 | Any string | 드라이버 내부에서 date와 string 사이의 변환 작업에 사용되는 문자 포맷이다. |
| da_buffer_size | 선택 | Any integer | Direct attach 모드로 접속했을 경우 fetch, bind 할 때 데이터를 주고 받는 버퍼의 크기를 지정한다. 기본값은 100000이다. |
| decoding_replacement | 선택 | Any string | 바이트 배열을 string으로 decoding 할 때, decoding할 수 없는 바이트 값을 대체할 문자이다. 기본값은 ?이다. |
| failover_granularity | 선택 | {"0", "1", "2"} | Failover 성공 여부를 판단한다. non-atomic(0), atomic(1), 2는 아직 지원하지 않는다. Failover 도중에 기존 prepared statement들에 대해 prepare 과정에서 에러가 발생할 경우 0은 failover를 계속 수행하고 1은 failover 실패를 결정한다. 기본값은 0이다. |
| failover_type | 선택 | {"connection", "session"} | Failover 유형을 결정한다.  * Connection: 서버에 접속할 때만 failover를 사용한다.  * Session: 서버에 접속할 때 뿐만 아니라 execution 등 서버와 통신하는 모든 경우에 failover를 사용한다. 기본값은 connection이다. |
| format_grammar | 선택 | {"db", "java"} | date_format과 같은 속성 문자열이 GOLDILOCKS 문법인지, Java의 SimpleDateFormat에 사용되는 문법인지를 결정한다. 기본값은 db이다. |
| global_logger | 선택 | {"console"} | 로깅 대상을 지정한다. 현재는 console만 가능한다. 가장 먼저 지정한 것만 유효하다. |
| home_dir | 선택 | Any string | Cluster server의 home directory를 지정한다. 기본값은 null이다. |
| keep_alive | 선택 | {"on", any} | Connection의 socket 속성을 keep_alive로 설정할지 여부이다. 이 속성을 부여하면 TCP socket 내부에서 주기적으로 ack를 주고받으며 서로 연결된 상태를 유지한다. 즉, 랜선 에러를 감지하여 연결을 강제로 끊기게 할 수 있다. |
| locator_connection_timeout | 선택 | Any integer | glocator로부터 패킷을 받을 때까지 대기하는 시간이다. |
| locator_file | 선택 | Any string | Location file이다. |
| locator_host | 선택 | IP address | glocator의 host address이다. |
| locator_port | 선택 | Port no | glocator의 port이다. |
| locator_service | 선택 | Any string | 서버 접속 정보를 얻기 위한 service 이름이다. |
| lzeros | 선택 | Any integer | Numeric을 문자열로 표현할 때 소수점 다음 0의 개수가 이 값을 넘어가면 exponent 표기법으로 표현된다. 기본값은 15이다. |
| new_password | 선택 | Any string | old_password 속성과 함께 사용하여 계정 암호를 바꿀 수 있다. |
| old_password | 선택 | Any string | new_password 속성과 함께 사용하여 계정 암호를 바꿀 수 있다. |
| packet_compression_threshold | 선택 | Any integer | 서버로 보낼 통신 데이터의 크기가 packet_compression_threshold 보다 클 경우, 통신 데이터를 압축한다. 속성값의 범위는 32 ~ 2113929216 이다. |
| password | 필수 | Any string | 사용자 계정 암호이다. |
| program | 선택 | Any string | 프로그램에 대한 설명이다. |
| protocol_log | 선택 | {"on", any} | 프로토콜 송수신 로깅을 할 것인지 여부이다. 기본값은 "" (안함)이다. |
| query_log | 선택 | {"on", any} | 쿼리 로깅을 할 것인지 여부이다. 기본값은 "" (안함)이다. |
| role | 선택 | {"", "SYSDBA", "ADMIN"} | 계정 롤을 지정한다. 기본값은 ""이다. |
| session_type | 선택 | {"1", "2", "3"} 또는 {"dedicate", "shared", "default"} | Dedicated/ shared/ default 중 하나이다. (Default를 선택할 경우, DB에서 선택된다.) |
| time_format | 선택 | Any string | 드라이버 내부에서 time과 string 사이의 변환 작업에 사용되는 문자 포맷이다. |
| timestamp_format | 선택 | Any string | 드라이버 내부에서 timestamp와 string 사이의 변환 작업에 사용되는 문자 포맷이다. |
| timetz_format | 선택 | Any string | 드라이버 내부에서 time with timezone와 string 사이의 변환 작업에 사용되는 문자 포맷이다. |
| timestamptz_format | 선택 | Any string | 드라이버 내부에서 timestamp with timezone과 string 사이의 변환 작업에 사용되는 문자 포맷이다. |
| trace_log | 선택 | {"on", any} | 트레이스 로깅을 할 것인지 여부이다. 기본값은 "" (안함)이다. |
| tzeros | 선택 | Any integer | Numeric을 문자열로 표현할 때 자릿수 0의 개수가 이 값을 넘어가면 exponent 표기법으로 표현된다. 기본값은 15이다. |
| user | 필수 | Any string | 사용자 계정 이름이다. |
| use_targettype | 선택 | {"0", "1", "2"} | 통신을 통해 column 타입을 수신할 경우, 같이 수신할 정보이다. * 0: none * 1: name * 2: all |


> 
> - locator_file은 locator_host와 locator_port 보다 우선적으로 적용된다. locator_file에 대한 자세한 내용은 [Location File](../part-06-utility-manual/42-gloctl.md#e85c8553b0240431)을 참조한다.
> - locator_service 속성은 locator_service에 속한 서버에 접속할 수 있게 한다. 자세한 내용은 [glocator](../part-06-utility-manual/40-glocator.md#a88d7ba491121954)와 [gloctl](../part-06-utility-manual/42-gloctl.md#6d8244ec8b476667)를 참조한다.
> 

<a id="e8382a8d56573234"></a>
### 데이터 조작

<a id="972fb21085dc7cb2"></a>
#### Statement를 이용한 데이터 조작

Statement 객체를 사용하여 각종 SQL 문을 실행할 수 있다. 다음과 같이 connection 객체로부터 statement 객체를 얻을 수 있다.

```
Connection con = DriverManager.getConnection(...);
Statement stmt = con.createStatement();
```

이렇게 생성된 statement 객체의 execute method와 executeUpdate method를 사용하여 각종 DML 문이나 DDL 문을 수행할 수 있다.

```
stmt.executeUpdate("create table emp ( id varchar(20), name varchar(30), age integer )");
stmt.executeUpdate("insert into emp values ('1234560000', '김연아', 24)");
int updated = stmt.executeUpdate("delete from emp where age > " + age);
```

execute와 executeUpdate의 차이점은 오직 반환값 뿐이다. execute는 수행한 SQL 문이 ResultSet을 반환하는지 여부를, executeUpdate는 갱신이 반영된 row의 개수를 각각 반환한다. execute는 DML이나 SELECT 구문에 모두 사용할 수 있지만 executeUpdate를 SELECT 문에 사용하면 SQLException이 발생한다.

> Statement로 SQL 문을 실행하는 것을 direct-execution이라고 한다. Direct-execution은 SQL 문에 대한 prepare 작업 (파싱, 검증 (validation), 최적화 (optimization) 작업)과 실행 (execution)을 한 번에 수행하는 방법이다. 이에 반해 prepare-execution은 prepare 작업을 한 번 해두고, execution을 반복 수행하는 방법이다. Direct-execution을 한 번 수행할 때마다 prepare, execution 작업이 발생하기 때문에 동일한 SQL 문을 반복적으로 수행해야 할 경우 prepare-execution이 더 효율적이다.

<a id="94092bbc14eca337"></a>
#### PreparedStatement를 이용한 데이터 조작

JDBC 표준은 데이터 조작을 위해 parameter를 사용할 수 있는 PreparedStatement 인터페이스를 제공하여 사용자가 보다 효율적으로 실행할 수 있도록 한다. 뿐만 아니라 PreparedStatement는 반복적인 실행에 대해 SQL 문 prepare 작업을 한 번만 하기 때문에 빠르게 수행할 수 있다.

```
Connection con = DriverManager.getConnection(...);
PreparedStatement pstmt = con.prepareStatement(
  "insert into emp values (?, ?, ?)");
pstmt.setString(1, "55544123000");
pstmt.setString(2, "김길동");
pstmt.setInt(3, 32);
pstmt.executeUpdate();
pstmt.setString(1, "1357924680");
pstmt.setString(2, "고둘리");
pstmt.setInt(3, 41);
pstmt.executeUpdate();
```

라인 2 ~ 3처럼 SQL 문을 prepare 해놓은 후에 데이터를 바인딩하고 실행한다. 한 번 prepare된 PreparedStatement는 계속해서 바인딩과 실행을 반복 수행할 수 있다.

만약 바인딩을 생략하고 execute()를 수행하면 이전에 바인딩 했던 값들이 사용된다.

```
pstmt.setString(1, "333555777000");
pstmt.setString(2, "강철규");
pstmt.setInt(3, 55);
pstmt.executeUpdate();
pstmt.setString(1, "245778884440");
pstmt.executeUpdate();
```

이와 같이 라인 6에서 2, 3 번째 parameter에 값을 바인딩하지 않고 바로 실행하면 이전에 바인딩 된 값인 "강철규"와 55가 사용된다. 만약 이전에 바인딩 된 값이 없을 경우 SQLException이 발생한다.

바인딩 된 값들을 모두 제거하려면 clearParameters()를 사용한다.

```
pstmt.setString(1, "333555777000");
pstmt.setString(2, "강철규");
pstmt.setInt(3, 55);
pstmt.executeUpdate();
pstmt.clearParameters();
pstmt.setString(1, "245778884440");
pstmt.executeUpdate();
```

이와 같이 라인 5에서 parameter들을 제거한 후, 첫 번째 parameter에만 값을 바인딩하고 실행하면 (라인 7) SQLException이 발생한다.

PreparedStatement를 사용하는 주된 이유는 다양한 타입의 데이터를 바인딩 할 수 있기 때문이다. Statement로는 값을 문자열로 표현할 수 밖에 없기 때문에 binary나 timestamp 같은 타입의 데이터를 입력하기에는 불편하다. 하지만 PreparedStatement로는 모든 타입으로 바인딩 할 수 있기 때문에 더 편리하다.

```
pstmt.setTimestamp(1,
  new Timestamp(Calendar.getInstance().getTimeInMillis()));
pstmt.setCharacterStream(2, new StringReader(BIG_STRING));
pstmt.setObject(3, someObj, Types.LONGVARCHAR);
pstmt.setObject(4, otherObj);
```

위의 예에서 1 ~ 2번 라인은 java.sql.Timestamp 객체를 바인딩한다. 바인딩 타입 (서버에 데이터가 전해질 때, 그 데이터의 GOLDILOCKS 타입)은 TIMESTAMP이다. 각종 setter method에 의해 결정되는 바인딩 타입에 대한 자세한 내용은 [PreparedStatement](#7bbc3faf505d0c2b)의 해당 API를 참조한다.

라인 3은 reader 객체를 바인딩하는데, 내부적으로 LONG VARCHAR 타입으로 바인딩하게 된다.

라인 4는 Java object 타입의 객체를 바인딩하는데, 타입이 LONG VARCHAR라는 것을 명시적으로 알려준다. Types의 타입에 매핑되는 GOLDILOCKS 타입에 대한 자세한 내용은 [SQL 타입 → GOLDILOCKS 타입](#e234a5c29f761940)을 참조한다.

라인 5는 Java object 타입을 그대로 바인딩하는데, 클래스 타입에 따라 해당되는 GOLDILOCKS 데이터 타입으로 바인딩된다. 클래스 타입과 GOLDILOCKS 데이터 타입 사이의 매핑에 대한 자세한 내용은 [Java 객체 → GOLDILOCKS 타입](#ccfa76b095a87789)을 참조한다.

<a id="86049146e4de34de"></a>
#### Statement를 이용한 배치 실행

Statement의 addBatch()와 executeBatch()를 사용하여 서로 다른 SQL 문을 batch job 형태로 실행할 수 있다.

```
stmt.addBatch("insert into emp values ("12345", "Jake", 22)");
stmt.addBatch("insert into salary values ("12345", 5000)");
stmt.addBatch("update members set total_count=total_count+1 where age=22");
stmt.executeBatch();
```

이처럼 서로 다른 SQL 문을 하나의 executeBatch() method를 통해 수행할 수 있다. 하지만 이 method 호출을 통해 세 개의 구문 모두가 서버에서 수행된 결과를 모아 한 번의 프로토콜로 JDBC 드라이버에 전달하는 것은 아니다. 내부적으로 세 번의 프로토콜 전송과 서버에서의 실행, 결과 전송이라는 작업이 수행되는 것이다. 즉, 성능상 큰 이점을 가질 수 있는 것은 아니라는 점에 주의해야 한다.

executeBatch를 실행한 후 등록된 job들은 모두 지워진다.

실행 도중 에러가 발생해도 끝까지 등록된 job을 모두 수행한다. 에러 발생 유무는 반환된 int[] 형의 값을 참고하면 알 수 있다. 즉, int[]이 EXECUTE_FAILED 값을 가지면 그 job은 실패했다는 의미이다.

<a id="dfdb082aef2e73d8"></a>
#### PreparedStatement를 이용한 배치 실행

PreparedStatement의 addBatch()와 executeBatch() method를 이용하여 좀 더 강력한 배치 실행을 수행할 수 있다.

```
PreparedStatement pstmt = con.prepareStatement("insert into emp values (?, ?, ?)");
pstmt.setString(1, "12345000");
pstmt.setString(2, "John");
pstmt.setInt(3, 33);
pstmt.addBatch();

pstmt.setString(1, "222333555");
pstmt.setString(2, "Henry");
pstmt.setInt(3, 24);
pstmt.addBatch();
int[] inserted = pstmt.executeBatch();
```

위의 예는 두 개의 row를 추가하는 과정이다. 두 개의 row를 구성할 값들을 addBatch()를 통해 바인드하고, 이후 executeBatch()를 호출하면 바인드 한 값과 execute에 대한 프로토콜이 서버로 전송되어 실행된다. 즉, executeBatch() 할 때만 통신하기 때문에 statement의 배치 실행보다 효율적이고 성능이 빠르다.

executeBatch()를 수행한 후엔 바인딩된 값들이 모두 삭제되기 때문에 executeBatch()을 다시 수행하려면 새로운 값을 다시 바인드 해야 한다. 실행한 후에 등록된 job들을 지우기 위해 clearBatch()를 명시적으로 호출하지 않아도 된다.

실행하는 도중에 에러가 발생해도 등록된 job 모두를 끝까지 수행한다. 에러 발생 유무는 반환된 int[] 형의 값을 참고하여 확인할 수 있다. 즉, int[]이 EXECUTE_FAILED 값을 가지면 그 job은 실패했다는 의미이다.

GOLDILOCKS JDBC는 executeBatch() 외에 executeBatchAtomic() 이라는 별도의 method를 제공한다. executeBatch()는 서버에서 등록된 job의 개수만큼 실행하지만, executeBatchAtomic()은 등록된 job (바인딩된 값들)을 한 번에 실행하기 때문에 응답시간이 더 빠르다. 다만 atomic이라는 이름에서 알 수 있듯이 하나라도 실패하게 되면 전부 실패하게 된다. 따라서 반환되는 유형은 int[]형이 아니라 int이다.

```
...
int inserted = ((GoldilocksPreparedStatement)pstmt).executeBatchAtomic();
```

<a id="a43324411630c3dc"></a>
### 데이터 조회

<a id="82625d65a147af68"></a>
#### Column 값 조회

Statement나 PreparedStatement의 executeQuery()를 통해서 얻은 ResultSet 객체를 통해 데이터를 조회할 수 있다.

```
...
ResultSet rs = pstmt.executeQuery();
while(rs.next())
{
    String id = rs.getString(1);
    String name = rs.getString(2);
    int age = rs.getInt(3);
    ...
}
```

테이블의 데이터를 조회한 후 ResultSet의 각종 getter method를 통해 해당 column의 내용을 얻을 수 있다. 테이블의 데이터는 GOLDILOCKS 데이터 타입의 원래 형태로 JDBC 드라이버에 전달되며, 사용자가 호출한 getter method 종류에 따라 적절한 Java 데이터 타입으로 변환되어 사용자에게 전달된다. GOLDILOCKS 데이터 타입과 getter method와의 타입 변환 매핑은 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.

GOLDILOCKS 데이터 타입을 해당 getter의 타입으로 변환할 수 없으면 SQLException이 발생한다.

<a id="ed3f7304b6c84967"></a>
#### Closing ResultSet

사용을 마친 ResultSet의 자원은 close()를 통해 해제할 수 있다. 사용자가 명시적으로 close()를 호출하지 않아도 다음과 같은 경우에는 ResultSet의 close()를 호출한 것과 동일한 결과를 가져온다.

- 상위 statement가 close되었을 때
- 상위 connection이 close되었을 때
- Statement의 executeQuery()가 다시 호출되었을 때
- Fetch하는 도중 에러가 발생했을 때

위의 세 번째 경우에 하나의 statement로부터 생성되는 ResultSet의 경우 동시에 두 개가 유지될 수 없다. 마지막 executeQuery()를 통해 생성된 ResultSet 객체만 유효하다.

<a id="c5930fd8a3d19830"></a>
#### Fetch Size

JDBC는 statement의 setFetchSize(int rows)를 통해 서버로부터 한 번에 fetch해오는 row 개수를 지정할 수 있다. GOLDILOCKS의 ResultSet은 이 속성의 기본값이 0이다. 0은 서버가 fetch 할 row의 개수를 자동으로 정하는데, forward only인 경우 한 통신 패킷에 담을 수 있는 최대 row 개수이고, scrollable인 경우 100개로 고정된다. 이 값이 크면 JDBC ResultSet이 차지하는 메모리 양이 많아지고, 너무 작으면 통신이 자주 발생한다.

이 값은 주로 scrollable ResultSet에 많이 사용하는데, 왜냐하면 scroll sensitive라 할지라도 ResultSet의 row 캐시 내에서 이동할 때는 sensitive하지 않기 때문에 이 값을 너무 크게 잡으면 row에 대한 최신 갱신 정보를 가질 수 없기 때문이다.

<a id="27746c80d6a7d89d"></a>
#### 필드 크기 제한

JDBC는 statement의 setMaxFieldSize(int size)를 통해 한 column의 최대 길이를 제한할 수 있다. 이 설정에 의해 CHAR, VARCHAR, LONG VARCHAR, BINARY, VARBINARY, LONG VARBINARY 타입의 최대 길이를 제한할 수 있다. 이 길이를 넘는 데이터는 잘라버린다. 기본값은 0이고 이 경우 최대 길이를 제한하지 않는다.

INTEGER, DATE와 같은 다른 타입에 대해서는 이 속성이 무시된다.

<a id="30fcf1c31b181796"></a>
### ResultSet 스크롤

<a id="efba8fcc7417fbcf"></a>
#### Scrollable ResultSet 획득

Scrollable ResultSet은 scroll sensitive와 scroll insensitive 두 가지이다. Scroll sensitive는 ResultSet을 순회하는 동안 자기 트랜잭션에 의해서든, 타 트랜잭션에 의해서든 갱신된 값들을 볼 수 있는 커서 유형이고, scroll insensitive는 그렇지 못한 커서이다. GOLDILOCKS 서버는 두 가지 스크롤 유형을 모두 지원하며, JDBC를 통해서도 그 기능을 자유롭게 사용할 수 있다.

```
Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE,
                                     ResultSet.CONCUR_READ_ONLY);
ResultSet rs = stmt.executeQuery("select id, name, age from emp");
```

라인 1처럼 statement를 생성할 때 ResultSet 타입을 TYPE_SCROLL_SENSITIVE로 설정하면 이 statement 객체로부터 생성되는 ResultSet은 모두 scroll sensitive 커서가 된다. 단, 현재 GOLDILOCKS는 updatable ResultSet은 지원하지 않는다.

Scroll insensitive인 ResultSet을 얻으려면 타입을 TYPE_SCROLL_INSENSITIVE로 설정해야 한다. 기본값은 TYPE_FORWARD_ONLY이다.

단, scroll sensitive ResultSet이라 하더라도 ResultSet의 row 캐시 내에서 이동할 때는 최신값을 볼 수 없고 갱신 유무도 알 수 없다. Row를 서버로부터 다시 fetch 해와야만 알 수 있다.

<a id="64f8f1b30c93cadb"></a>
#### 스크롤

JDBC API는 커서를 스크롤 하기 위해 다음과 같은 method를 제공한다.

```
public boolean next() throws SQLException;
public boolean previous() throws SQLException;
public boolean first() throws SQLException;
public boolean last() throws SQLException;
public boolean absolute(int rows) throws SQLException;
public boolean relative(int rows) throws SQLException;
public void beforeFirst() throws SQLException;
public void afterLast() throws SQLException;
```

next()는 forward only나 scrollable ResultSet에 모두 사용할 수 있는 method이며, 커서 위치를 다음 row로 이동시킨다. 이동한 위치에서 row를 읽을 수 있으면 true를, 그렇지 않을 경우에는 false를 반환한다. 그 외의 method들은 scrollable ResultSet에만 사용할 수 있다.

previous()는 이전 row로, first()는 첫 번째 row로, last()는 마지막 row로, absolute()는 절대 위치로, relative()는 현재 위치로부터 상대 위치로 이동시킨다. beforeFirst()는 첫 번째 row 이전으로 위치시키며, afterLast()는 마지막 row의 다음에 위치시킨다.

```
rs.afterLast();
while (rs.previous())
{
    String id = rs.getString(1);
    String name = rs.getString(2);
    int age = rs.getInt(3);
    ...
}
```

위 코드는 마지막 row부터 첫 번째 row까지 거꾸로 조회한다.

현재 커서의 위치는 다음 method를 통해 알 수 있다.

```
public int getRow() throws SQLException;
```

<a id="9453aa5601d54bbb"></a>
#### 스크롤 원리

ResultSet 스크롤은 사용하기 간단한 편이지만, 내부 동작 원리를 알지 못하면 성능이 크게 저하될 수도 있어 주의해서 사용해야 한다. 스크롤은 JDBC 드라이버의 ResultSet 내의 result cache에서 수행되지만, cache를 벗어난 범위에 대해서는 서버에서 스크롤이 수행되며 이에 따라 통신이 발생하면 성능이 저하될 수 있다.

Scrollable ResultSet의 fetch size는 내부 (internal) 기본값이 100이다. (외부 기본값은 0이며, 이 값은 setFetchSize() method를 통해 변경할 수 있다.) 즉, 한 번에 JDBC 드라이버로 가져오는 row 개수가 100개라는 뜻이다. ResultSet의 row 캐시는 100개의 row로 구성되는데, 이동시키려는 row 위치가 캐시 내에 있을 경우, ResultSet의 커서 위치만 바꾸면 된다. 하지만 캐시 내에 없을 경우에는 이동시키려는 위치의 row를 다시 서버로부터 가져와야 한다. 이 때 이동시키려는 row를 포함한 row set을 가져오는 방식을 알아야 한다.

예를 들어, ResultSet이 1번부터 100번의 row를 가지고 있고 현재 커서 위치가 100번에 있을 경우에 next()를 호출하게 되면 다음 row가 캐시 내에 없기 때문에 101번부터 200번까지의 row를 서버로부터 fetch해 와야 한다. 반면에 101번부터 200번까지의 row가 ResultSet 캐시 내에 있고, 현재 위치가 101번 row에 있을 때 previous()를 호출한 경우, 서버로부터 100번부터 199번 row를 fetch 해온다면 이는 적절하지 못하다. 만약 이렇게 구현한다면 previous()를 호출할 때마다 서버에서 매번 fetch 해와야 하기 때문이다. GOLDILOCKS는 이런 비효율을 방지하기 위해 previous()를 호출하여 해당 row를 서버로부터 가져와야 하는 상황이 되면 해당 row를 마지막으로 하는 row set을 서버로부터 가져온다. 즉, previous()에 의해 100번 row를 fetch 해와야 하는 상황이라면 1번부터 100번까지의 row를 fetch 해온다. 그러면 previous()에 유리하도록 fetch하게 된다.

이 규칙을 일반화하면 다음과 같다.

- 이동시키려는 위치가 현재 위치 이후일 경우, 그 위치로부터 100개 (설정한 fetch size)의 row를 fetch한다.
- 이동시키려는 위치가 현재 위치 이전이면 그 위치 앞쪽의 100개 row를 fetch한다.
- first()로 이동할 때는 첫 100개를 가져온다.
- last()로 이동할 때는 마지막 100개를 가져온다.

즉, 뒤로 이동할 때는 next()에 유리하도록, 앞으로 이동할 때는 previous()에 유리하도록 fetch한다. 이는 absolute(), relative()로 이동할 때도 마찬가지이다.

<a id="94b4ca2893aa3371"></a>
### 추가 타입 사용

<a id="7e4a7dcd3ed695f6"></a>
#### Interval 타입

GOLDILOCKS는 interval과 관련하여 다음과 같은 13가지 타입을 지원한다.

- interval year
- interval month
- interval year to month
- interval day
- interval hour
- interval minute
- interval second
- interval minute to second
- interval hour to minute
- interval hour to second
- interval day to hour
- interval day to minute
- interval day to second

JDBC를 이용하여 sunje.goldilocks.jdbc.GoldilocksInterval 객체를 생성하면 PreparedStatement의 setObject()를 통해 interval 데이터를 테이블에 추가할 수 있다.

GoldilocksInterval 객체는 GoldilocksInterval의 static method인 createIntervalXXX를 사용하여 생성할 수 있다.

```
import sunje.goldilocks.jdbc.GoldilocksInterval;

...
GoldilocksInterval interval = GoldilocksInterval.createIntervalDayToSecond(2, 6, "2 08:23:54.560843");
PreparedStatement pstmt = con.prepareStatement("insert into interval_table values (?,?)");
pstmt.setString(1, someId);
pstmt.setObject(2, interval);
pstmt.executeUpdate();
```

createIntervalXXX method에 대한 자세한 내용은 [GoldilocksInterval](#8db3c186cf434146)을 참조한다. 이와 같이 GoldilocksInterval을 생성하여 setObject를 통해 바인딩 할 수 있다. 또는 타입을 명시하기 위해 다음과 같이 실행해도 된다.

```
import sunje.goldilocks.jdbc.GoldilocksTypes;
...
pstmt.setObject(2, interval, GoldilocksTypes.INTERVAL_DAY_TO_SECOND);
```

GoldilocksInterval 객체없이 string 문자열로 데이터를 추가할 수 있다.

```
pstmt.setObject(2, "2 08:23:54.560843", GoldilocksTypes.INTERVAL_DAY_TO_SECOND);
```

이 경우, JDBC 드라이버 내에서 GoldilocksInterval 객체를 생성하여 호스트 변수에 바인딩한다. 또는setString() method를 통해 문자열로 바인딩 할 수도 있다.

```
pstmt.setString(2, "2 08:23:54.560843");
```

이렇게 하면 서버에 문자열 그대로 전송되며 서버에서 문자열을 interval day to second 타입으로 변환하여 추가한다.

데이터베이스로부터 interval 타입을 조회하려면 ResultSet의 getObject()나 getString()을 이용한다.

```
import sunje.goldilocks.jdbc.GoldilocksInterval;

ResultSet rs = stmt.executeQuery("select interval_value from some_table");
while (rs.next())
{
    GoldilocksInterval interval = (GoldilocksInterval)rs.getObject(1);
    System.out.println("type = " + interval.getTypeName() + 
                       ", value = " + interval.toString());
}
```

ResultSet의 getObject()를 통해 GoldilocksInterval 타입의 데이터를 얻을 수 있다. GoldilocksInterval 클래스는 각종 시간 데이터를 얻을 수 있는 getYear(), getHour() 등의 getter를 제공한다. getter API에 대한 자세한 내용은 [GoldilocksInterval](#8db3c186cf434146)을 참조한다.

<a id="cc1221c70cf04c60"></a>
#### Time with time zone과 Timestamp with time zone 타입

GOLDILOCKS는 시간과 관련하여 date, time, timestamp와 같은 SQL 표준 타입 뿐만 아니라 time with time zone과 timestamp with time zone 타입도 제공한다.

```
CREATE TABLE SAMPLE_TABLE ( C1 TIME WITH TIME ZONE,
                            C2 TIMESTAMP WITH TIME ZONE );
```

GOLDILOCKS JDBC는 time with time zone과 timestamp with time zone 타입의 데이터를 추가하기 위해 GoldilocksPreparedStatement 클래스에 setTimeTimeZone (int colIndex, time time, calendar timezone) method와 setTimestampTimeZone (int colIndex, timestamp time, calendar timezone) method를 제공한다. 자세한 내용은 [setTimeTimeZone](#3f3067d1b8c5bd6c)과 [setTimestampTimeZone](#fedba2580ddc3692)을 참조한다.

물론 기존의 setTime()과 setTimestamp() method로도 추가할 수 있지만, 이 column의 time zone 값은 무조건 Java 실행 환경의 local time zone으로 설정된다. 따라서 다양한 time zone 정보를 추가하기 위해서는 setTimeTimeZone()이나 setTimestampTimeZone을 사용해야 한다.

setTimeTimeZone과 setTimestampTimeZone으로 주어진 time, timestamp 데이터를 주어진 time zone 값과 함께 추가할 수 있다.

```
import sunje.goldilocks.jdbc.GoldilocksPreparedStatement;

PreparedStatement pstmt = con.prepareStatement(
    "INSERT INTO SAMPLE_TABLE VALUES (?,?,?,?)");
Calendar now = Calendar.getInstance();
Calendar usNow = Calendar.getInstance(TimeZone.getTimeZone("GMT-8"));

Time t = new Time(now.getTimeInMillis());
Timestamp ts = new Timestamp(now.getTimeInMillis());

pstmt.setTime(1, t);
pstmt.setTimestamp(2, ts);
pstmt.executeUpdate();

((GoldilocksPreparedStatement)pstmt).setTimeTimeZone(1, t, now);
((GoldilocksPreparedStatement)pstmt).setTimestampTimeZone(2, ts, now);
pstmt.executeUpdate();

((GoldilocksPreparedStatement)pstmt).setTimeTimeZone(1, t, usNow);
((GoldilocksPreparedStatement)pstmt).setTimestampTimeZone(2, ts, usNow);
pstmt.executeUpdate();
```

11, 12 라인은 해당 column에 time 타입과 timestamp 타입으로 바인딩한다. t와 ts 값이 각각 서버로 전달되어 서버에서 기본 time zone 값이 DB column에 추가된다.

이에 반해 15, 16 라인은 해당 column에 time with time zone 타입과 timestamp with time zone 타입으로 바인딩하여, time zone 정보도 함께 서버로 전달한다. 결과적으로 서버와 client의 time zone 설정이 동일할 경우, 11 ~ 13 라인에 의해 추가되는 row와 15 ~ 17 라인에 의해 추가되는 row는 동일하다.

19, 20 라인은 GMT-8 시간대의 time zone 정보를 추가한다.

Time with time zone과 timestamp with time zone의 데이터를 조회하는 방법은 크게 두 가지이다. 서버로부터 char로 얻는 방법과 JDBC로 해당 타입의 데이터를 가져와서 time이나 timestamp 객체로 얻는 방법이 있다.

```
ResultSet rs = stmt.executeQuery("select c1, cast(c1 as char(33)), c2, cast(c2 as char(33)) from sample_table");
while (rs.next())
{
    System.out.println("c1 = " + rs.getTime(1).toString());
    System.out.println("c1 as char = " + rs.getString(2));

    System.out.println("c2 = " + rs.getTimestamp(3).toString());
    System.out.println("c2 as char = " + rs.getString(4));
}
```

위 코드를 실행하면 다음과 같은 결과를 확인할 수 있다.

```
c1 = 12:35:26
c1 as char = 12:35:26.052000 +09:00           
c2 = 2014-03-27 12:35:26.052
c2 as char = 2014-03-27 12:35:26.052000 +09:00
c1 = 12:35:26
c1 as char = 12:35:26.052000 +09:00           
c2 = 2014-03-27 12:35:26.052
c2 as char = 2014-03-27 12:35:26.052000 +09:00
c1 = 12:35:26
c1 as char = 19:35:26.052000 -08:00           
c2 = 2014-03-27 12:35:26.052
c2 as char = 2014-03-26 19:35:26.052000 -08:00
```

<a id="d8e7c4d84358a1fe"></a>
### 로깅

<a id="efdb2227ab3f4bff"></a>
#### 로깅 종류

JDBC를 이용하는 프로젝트를 개발할 때, JDBC 드라이버가 각종 로그를 남길 수 있으면 여러가지로 도움이 된다. GOLDILOCKS는 프로젝트를 개발할 때만이 아니라 운용할 때도 유용한 정보를 로깅할 수 있는 기능을 제공한다.   
로깅의 종류는 세 가지인데 trace log, protocol log, query log 이다.

Trace log는 JDBC API가 호출될 때마다 정보를 남긴다. 어떤 JDBC API가 호출되는 지를 알 수 있다. Protocol log는 JDBC 드라이버와 GOLDILOCKS 서버 사이에 통신 패킷을 주고 받는 상황을 보여준다. Query log는 PreparedStatement나 statement가 실행될 때, 실행할 SQL 문을 기록한다.

<a id="3bc568e53ef75cf1"></a>
#### DriverManager를 이용한 로깅

먼저 DriverManager를 이용하여 로깅을 남길 수 있다. DriverManager에 setLogWriter() method를 이용하여 로깅할 매체를 결정할 수 있고, connection url에 남길 로깅의 종류를 명시한다.

```
DriverManager.setLogWriter(new PrintWriter(System.out));
String url = "jdbc:goldilocks://localhost:22581/test?trace_log=on&query_log=on";
Connection con = DriverManager.getConnection(url, "TEST", "test");
```

1번 라인은 로깅 매체를 정의하는 것이다. 모든 로깅을 콘솔로 출력하게 한다. 2번 라인은 connection URL을 정의하는 것인데, ? 문자 뒤에 프로퍼티를 정의할 수 있다. trace_log, query_log를 사용하겠다는 의미이다.

이와 같이 이 프로퍼티들은 URL에 명시할 수도 있고, properties 객체로 정의할 수도 있다.

```
Properties prop = new Properties();
prop.put("trace_log", "on");
prop.put("query_log", "on");
prop.put("protocol_log", "on");
prop.put("user", "TEST");
prop.put("password", test");
Connection con = DriverManager.getConnection(url, prop);
```

GOLDILOCKS에서 사용할 수 있는 connection property들은 [연결 프로퍼티](#2081c33a3f3f0333)에 정의되어 있다.

간혹 DriverManager의 setLogWriter()를 호출하기 어려운 경우가 있다. 예를 들어, 미들웨어를 사용하는 경우 저런 코드를 추가할 수 없다. 그런 경우에 대비해 GOLDILOCKS JDBC는 global_logger라는 전역 프로퍼티를 제공한다. 다른 일반적인 프로퍼티들은 하나의 connection에만 적용되지만, 이 속성은 전역적으로 적용된다. 즉, 이 프로퍼티를 설정하면 DriverManager.setLogWriter()를 호출하지 않아도 된다.

```
String url = "jdbc:goldilocks://localhost:22581/test?" +            
             "global_logger=console&trace_log=on&query_log=on";
Connection con = DriverManager.getConnection(url, "TEST", "test");
```

global_logger 속성은 처음 한 번만 적용되는데 만약 DriverManager에 이미 log writer가 설정되어 있으면 이 속성은 무시된다. 이 속성의 값으로는 현재 console만 지원된다. 다른 값인 경우에는 아무런 동작을 하지 않는다.

<a id="edbf16dd6766583e"></a>
#### DataSource를 이용한 로깅

DriverManager와는 다르게 DataSource는 객체별로 log writer를 설정할 수 있다. 하나의 DataSource 객체에 log writer를 세팅하면 그 DataSource로부터 생성되는 모든 connection은 그 log writer로 로깅된다. DataSource에 로깅을 설정하는 방법은 다음과 같다.

```
import sunje.goldilocks.jdbc.GoldilocksDataSource;
...
GoldilocksDataSource ds = new sunje.goldilocks.jdbc.GoldilocksDataSource();
ds.setServerName("localhost");
ds.setDatabaseName("test");
ds.setUser("TEST");
ds.setPassword("test");
ds.setPortNumber(22581);
ds.setLogTarget("console");
ds.setTraceLog("on");
ds.setQueryLog("on");
ds.setProtocolLog("on");
Connection con = ds.getConnection();
```

이와 같이 setLogTarget(), setTraceLog(), setQueryLog(), setProtocolLog() method를 사용하여 로깅 기능을 설정할 수 있다. setLogTarget() 대신 DataSource의 setLogWriter()를 호출해도 된다. 다만 미들웨어를 사용하는 경우에는 setLogWriter()와 같은 method를 직접 호출할 수 없기 때문에 property로 제어해야 하는데, 이 때 logTarget, traceLog, queryLog, protocolLog 속성을 정의하면 미들웨어가 자동으로 이 method들을 호출한다.

<a id="373c97263781c47e"></a>
### Plan Text 조회

<a id="3d47b3d88549245d"></a>
#### 사용법

GOLDILOCKS ODBC를 사용하면 실행된 statement의 plan text를 얻어올 수 있는 것처럼 GOLDILOCKS JDBC를 사용해서도 plan text를 얻어올 수 있다. GoldilocksStatement 클래스에 비 표준 API method를 사용하여 plan text를 생성하도록 설정할 수 있고, 만들어진 plan text를 얻어올 수도 있다.

```
Connection con = ...
GoldilocksStatement stmt = (GoldilocksStatement)con.createStatement();
stmt.setExplainPlanOption(GoldilocksStatement.EXPLAIN_PLAN_OPTION_ON);
ResultSet rs = stmt.executeQuery("select * from t1");
System.out.println(stmt.getExplainPlan());
```

예를 들어 간단한 테이블을 조회했을 때의 plan text는 다음과 같이 출력된다.

```
< Execution Plan >
==========================================================================
|  IDX  |  NODE DESCRIPTION                                |       ROWS |
--------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                |            |
|    1  |    TABLE ACCESS ("T1")                           |          0 |
==========================================================================
     1  -  READ COLUMNS : A
```

<a id="1eacc3e83b18fa7a"></a>
#### 옵션 종류

GOLDILOCKS는 다음과 같이 plan text 생성과 관련된 네가지 속성을 제공한다.

- EXPLAIN_PLAN_OPTION_OFF: Statement의 plan text 관련 속성의 기본값으로써 plan text를 생성하지 않는다.
- EXPLAIN_PLAN_OPTION_ON: 실행할 때나 fetch 할 때 plan text를 생성한다.
- EXPLAIN_PLAN_OPTION_ON_VERBOSE: 실행할 때나 fetch 할 때 실행 시간과 같이 보다 자세한 plan text를 생성한다.
- EXPLAIN_PLAN_OPTION_ONLY: 실행할 때나 fetch 할 때 EXPLAIN_PLAN_OPTION_ON처럼 plan text를 생성하지만 실제로 실행은 하지 않는다.

이 속성들은 GoldilocksStatement.setExplainPlanOption(int) method를 사용하여 설정할 수 있으며 한 번 설정하면 계속해서 이 속성이 유지된다. 속성의 상수값은 GoldilocksStatement에 정의되어 있다.

> SELECT 구문이 아닌 DML이나 기타 SQL 구문은 실행할 때 plan text가 생성되지만 SELECT 구문은 fetch되고 서버 내에서 커서가 끝까지 갔을 때 plan text가 생성된다. 따라서 SELECT 구문일 경우 ResultSet으로 모든 row를 순회한 다음에 plan text를 얻어야 한다. 단, 테이블에 row가 적을 경우에는 끝까지 fetch하지 않아도 서버 커서의 끝까지 순회할 수 있으므로 이 경우 plan text를 얻을 수 있다.

<a id="eabf5f15a1a83244"></a>
### Connection Failover

GOLDILOCKS는 client 레벨 (JDBC, ODBC)의 connection failover를 지원한다. GOLDILOCKS에 JDBC 또는 ODBC를 이용하여 client/ server 모드로 접속한 응용 프로그램은 연결에 실패하거나 연결이 끊길 경우, 자동으로 대체 서버로 연결할 수 있다. 이를 통해 여러 대의 서버를 활용한 고가용성 응용 프로그램을 작성할 수 있도록 해준다. 특히 웹 서버와 연동된 환경에서 연결 속성 (connection property)을 통해 주 서버 URL과 대체 서버 URL을 등록하면 connection pool로부터 가져온 connection 객체를 끊길 걱정없이 안정적으로 사용할 수 있다. Failover는 전적으로 드라이버 내부에서 자동 진행되며 사용자는 재접속에 대한 로직을 고민할 필요없다.

Failover 기능을 사용하려면 alternate_servers 속성을 부여해야 한다. 이 속성값으로 대체 서버의 IP와 port를 부여할 수 있다. 콤마 (,)를 사용하여 여러 개의 대체 서버를 명시할 수도 있다.

```
Class.forName("sunje.goldilocks.jdbc.GoldilocksDriver");

String url = "jdbc:goldilocks://192.168.0.101:22581/test";
Property prop = new Properties();
prop.setProperty("user", "TEST");
prop.setProperty("password", "test");
prop.setProperty("alternate_servers", "192.168.0.201:22581");
Connection con = DriverManager.getConnection(url, prop); ❶
Statement stmt = con.createStatement();
stmt.executeUpdate("insert into time_tab values (sysdate)"); ❷
...
```

예를 들어, 1에서 주 서버 (192.168.0.101)의 연결이 실패하면 자동으로 대체 서버 (192.168.0.201)로 접속한 후 connection 객체를 반환한다. 사용자에게는 별다른 에러가 반환되지 않는다. 만약 2에서 executeUpdate() 하는 도중에 연결이 끊기거나 그 전에 끊어져서 서버와 통신을 할 수 없을 경우 드라이버 내부에서 자동으로 대체 서버로 접속하여 기존 connection 객체를 계속해서 사용할 수 있도록 조치한 후 SQLException이 발생한다. 사용자는 SQLException을 처리한 후에 기존 connection 객체를 계속해서 사용할 수 있다.

Connection 객체의 getWarnings()를 통해 failover 여부를 알 수 있다.

GOLDILOCKS JDBC의 failover 특징 중에 하나는 connection 객체로부터 생성된 statement 객체나 PreparedStatement 객체를 계속해서 사용할 수 있다는 점이다. (ResultSet은 계속해서 사용할 수 없다)

특히 PreparedStatement들은 failover가 발생하면 내부적으로 대체 서버에서 다시 prepare 작업을 수행하므로 사용자가 계속해서 이 객체를 사용할 수 있다.

```
Connection con = DriverManager.getConnection(url, prop);
PreparedStatement pstmt = 
    con.prepareStatement("insert into t1 values (?,?)");
...
try
{
    pstmt.setInt(1, 100);
    pstmt.setString(2, "John");
    pstmt.executeUpdate();
}
catch (SQLException sException)
{
    if (sException.getErrorCode() == 21012)
    {
```

- Communication link failure 에러가 발생하여 failover가 발생했다.
- 계속해서 pstmt 객체를 사용할 수 있다.

```
pstmt.executeUpdate(); 
    }
    else
    {
        ...
    }
}
```

GOLDILOCKS JDBC 드라이버는 failover와 관련해 몇 가지 속성을 제공한다. 이를 통해 failover 유형, 접속 순서 및 failover시 사용되는 간단한 정책 등을 결정할 수 있다.

<a id="65d14b0e53a70186"></a>
#### failover_type

이 속성으로 failover 유형을 선택할 수 있다. 위 예제 코드 1에서 발생하는 failover를 connection failover라 하고 2에서 발생하는 failover를 session failover라 부른다. 이 속성값으로 connection을 부여하면 connection failover만 수행하게 하며, session을 부여하면 connection failover와 session failover를 모두 수행하게 한다. 기본값은 connection이다.

<a id="81be8619d614ac0e"></a>
#### failover_granularity

Failover가 발생하면 현재의 connection 객체로부터 생성된 PreparedStatement 객체들에 대체 서버로 접속한 후 prepare 작업을 다시 수행하는데 이 때 대체 서버에서 prepare가 실패했을 경우 (서버 환경이 달라서 에러가 발생할 수 있음) failover 자체를 실패로 처리할지 또는 prepare 에러를 무시할지 여부를 이 속성이 결정한다. 현재 이 속성값으로 0과 1을 부여할 수 있는데, 0을 부여하면 prepare 에러를 무시한 채 failover를 계속해서 수행할 수 있게하고, 1을 주면 failover가 실패하도록 한다. 기본값은 0이다. 만약 0을 부여하고 prepare에 실패하면 PreparedStatement 객체를 계속해서 사용할 수 없고 사용자가 다시 직접 PreparedStatement 객체를 생성해야 한다.

<a id="5531ea2737958fa0"></a>
### Direct Attach 모드 접속

GOLDILOCKS JDBC 1.1부터 기존 TCP/ IP 기반의 Client/ Server 모드 (C/S 모드) 외에 direct attach 모드 (D/A 모드) 연결을 제공한다. 이 연결 방식은 ODBC D/A 모드 접속과 마찬가지로 서버 프로세스와 직접 연동하여 하나의 프로세스 안에 (jvm과 같은 프로세스 안에) 서버 모듈이 연동되어 작동한다. 그렇기 때문에 원격 호스트에서는 D/A 모드로 접속할 수 없다.

D/A 모드는 in-memory 데이터베이스인 GOLDILOCKS의 빠른 처리라는 장점을 살리기 위해 고안된 특별한 연결 방식이다. TCP/ IP 기반의 접속으로는 GOLDILOCKS의 빠른 트랜잭션 처리 효과가 값비싼 네트워크 비용으로 상쇄되기 때문에 빠른 처리를 요구하는 상황에서는 다른 대안이 필요하다. 비록 GOLDILOCKS 서버와 같은 호스트 내에서 실행해야 한다는 제약이 있지만 빠른 처리를 필요로 하는 경우 D/A 모드 접속은 좋은 대안이 될 수 있다.

D/A 모드로 접속한 JDBC 프로그램은 jvm 내에서 DB connection이 처음 생성되면 GOLDILOCKS jni 라이브러리가 로딩되어 서버의 기능을 직접 호출할 수 있다. 네트워크 비용없이 jvm에서 native interface를 통해 서버 모듈을 직접 호출할 수 있기 때문에 기존의 C/S 모드보다 빠른 처리가 가능하다.

<a id="0fee09e6205020f1"></a>
#### 접속 방법

D/A 모드로 접속하기 위해 connection URL에 기존 ip:port 대신 0.0.0.0:0을 사용한다. 기존의 URL 방식을 그대로 사용할 수 있으며 0.0.0.0:0이라는 특별한 ip:port 주소를 사용하여 기존 응용 프로그램의 수정을 최소화할 수 있다. 또는 da라는 특수 프로토콜을 URL에 사용하면 D/A 모드로 접속할 수 있다.

```
Connection con =
 DriverManager.getConnection("jdbc:goldilocks://0.0.0.0:0/test","TEST","test");
```

또는

```
Connection con =
 DriverManager.getConnection("jdbc:goldilocks:da/test", "TEST", "test");
```

<a id="e730b8ebd60ccec9"></a>
#### D/A 접속의 특징

D/A 모드로 접속하면 jvm 안에서 GOLDILOCKS server 모듈을 직접 호출할 수 있다. JDBC 프로그램과 GOLDILOCKS server 모듈 사이에는 Java Native Interface (JNI)를 통해 호출한다. JNI 호출 비용이 비싼 것을 고려하여 최소 호출 비용으로 서버 모듈을 사용하기 때문에 기존 TCP/ IP 기반의 JDBC보다 두 배 이상성능이 빨라진다.

기존 TCP/ IP 기반의 접속을 사용할 때는 goldilocks6.jar 파일만 사용하지만 D/A 모드로 접속할 때는 $GOLDILOCKS_HOME/lib에 있는 libgoldilocksjni.so와 libgoldilocksas.so 파일을 동적으로 로딩해서 사용한다. 따라서 두 라이브러리 파일이 없으면 연결할 때 에러가 발생한다. 하지만 Java 프로그램을 구동할 때 라이브러리 파일의 위치를 별도로 명시할 필요는 없다. goldilocks6.jar 파일과 같은 디렉토리에 있는 한 현재 디렉토리부터 이 두 개의 라이브러리 파일을 찾아서 로딩하기 때문이다.

<a id="18ec3add277117c4"></a>
## JDBC API References

<a id="ed4d918cd104144f"></a>
### Array

클래스가 구현되지 않았다.

<a id="e3e0e2de647186f8"></a>
#### free

```
void free() throws SQLException
```

<a id="d80bf21fb99b6df6"></a>
#### getArray

```
Object getArray() throws SQLException
```

```
Object getArray(Map<String,Class<?>> map) throws SQLException
```

```
Object getArray(long index, int count) throws SQLException
```

```
Object getArray(long index, int count, Map<String,Class<?>> map) throws SQLException
```

<a id="ea121e2c18d8bea6"></a>
#### getBaseType

```
int getBaseType() throws SQLException
```

<a id="aba800df7d7218fa"></a>
#### getBaseTypeName

```
String getBaseTypeName() throws SQLException
```

<a id="74cef4e321f4ee4c"></a>
#### getResultSet

```
ResultSet getResultSet() throws SQLException
```

```
ResultSet getResultSet(Map<String,Class<?>> map) throws SQLException
```

```
ResultSet getResultSet(long index, int count) throws SQLException
```

```
ResultSet getResultSet(long index, int count, Map<String,Class<?>> map) throws SQLException
```

<a id="c9f5aa2023262f6d"></a>
### Blob

클래스가 구현되지 않았다.

<a id="7dab0ce2fe262526"></a>
#### free

```
void free() throws SQLException
```

<a id="3c851b6ea1083a1b"></a>
#### getBinaryStream

```
InputStream getBinaryStream() throws SQLException
```

```
InputStream getBinaryStream(long pos, long length) throws SQLException
```

<a id="003d1d9855071cc2"></a>
#### getBytes

```
byte[] getBytes(long pos, int length) throws SQLException
```

<a id="f5cfb1d01c90ca44"></a>
#### length

```
long length() throws SQLException
```

<a id="fe2aa49e81c14b33"></a>
#### position

```
long position(byte[] pattern, long start) throws SQLException
```

```
long position(Blob pattern, long start) throws SQLException
```

<a id="2d639b1720be17ac"></a>
#### setBinaryStream

```
OutputStream setBinaryStream(long pos) throws SQLException
```

<a id="879f109c144c74f5"></a>
#### setBytes

```
int setBytes(long pos, byte[] bytes) throws SQLException
```

```
int setBytes(long pos, byte[] bytes, int offset, int len) throws SQLException
```

<a id="183e4320d072c233"></a>
#### truncate

```
void truncate(long len) throws SQLException
```

<a id="9065b7c6bbdb2bf7"></a>
### CallableStatement

<a id="377eed1b522752fb"></a>
#### getArray

```
Array getArray(int parameterIndex) throws SQLException
```

- 동작: Array 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
Array getArray(String parameterName) throws SQLException
```

- 동작: Array 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="ede23d0cd0691de4"></a>
#### getBigDecimal

```
BigDecimal getBigDecimal(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 BigDecimal 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
BigDecimal getBigDecimal(int parameterIndex, int scale) throws SQLException
```

- 동작: 구현되어 있지 않다. (Deprecated 된 method이다.)
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
BigDecimal getBigDecimal(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="cd7ca83025bfdb2d"></a>
#### getBlob

```
Blob getBlob(int parameterIndex) throws SQLException
```

- 동작: Blob 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
Blob getBlob(String parameterName) throws SQLException
```

- 동작: Blob 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="2bbe77d984276307"></a>
#### getBoolean

```
boolean getBoolean(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 boolean 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
boolean getBoolean(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="ddc6fbe550c1df18"></a>
#### getByte

```
byte getByte(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 byte 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조하기 바란다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있다면 SQLException이 발생한다.

```
byte getByte(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="17e87deda0d4e593"></a>
#### getBytes

```
byte[] getBytes(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 byte[] 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
byte[] getBytes(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="5c19d49046be2c21"></a>
#### getCharacterStream

```
Reader getCharacterStream(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 reader 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
Reader getCharacterStream(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="605bd2abb0e43038"></a>
#### getClob

```
Clob getClob(int parameterIndex) throws SQLException
```

- 동작: Clob 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
Clob getClob(String parameterName) throws SQLException
```

- 동작: Clob 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="c6497cd4d0d99683"></a>
#### getDate

```
Date getDate(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 date 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Date 객체를 만들 때 local timezone과 locale을 사용한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
Date getDate(int parameterIndex, Calendar cal) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 date 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Date 객체를 만들 때 cal의 timezone과 locale을 사용한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
Date getDate(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
Date getDate(String parameterName, Calendar cal) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="b3ca8d201bfb5c71"></a>
#### getDouble

```
double getDouble(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 double 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
double getDouble(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="4b94ab585779b8e0"></a>
#### getFloat

```
float getFloat(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 float 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
float getFloat(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="f40e1ae64371ff2a"></a>
#### getInt

```
int getInt(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 int 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
int getInt(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="d88233906bc58332"></a>
#### getLong

```
long getLong(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 long 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
long getLong(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="824ecbbff2782fa2"></a>
#### getNCharacterStream

```
Reader getNCharacterStream(int parameterIndex) throws SQLException
```

- 동작: NCHAR 계열 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
Reader getNCharacterStream(String parameterName) throws SQLException
```

- 동작: NCHAR 계열 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="b2417107c02924e6"></a>
#### getNClob

```
NClob getNClob(int parameterIndex) throws SQLException
```

- 동작: NClob 계열 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
NClob getNClob(String parameterName) throws SQLException
```

- 동작: NClob 계열 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="d0af20700f6c2406"></a>
#### getNString

```
String getNString(int parameterIndex) throws SQLException
```

- 동작: NCHAR 계열 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
String getNString(String parameterName) throws SQLException
```

- 동작: NCHAR 계열 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="b6ab8302edf145e9"></a>
#### getObject

```
Object getObject(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 Java 객체 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
Object getObject(int parameterIndex, Map<String,Class<?>> map) throws SQLException
```

- 동작: 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
Object getObject(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
Object getObject(String parameterName, Map<String,Class<?>> map) throws SQLException
```

- 동작: 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="75d02fb408992172"></a>
#### getRef

```
Ref getRef(int parameterIndex) throws SQLException
```

- 동작: Ref 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
Ref getRef(String parameterName) throws SQLException
```

- 동작: Ref 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="2c16df0a4ae2b332"></a>
#### getRowId

```
RowId getRowId(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 rowId 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.\
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
RowId getRowId(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="8209f004b16e7da0"></a>
#### getShort

```
short getShort(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 short 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
short getShort(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="288a670eef744b8b"></a>
#### getSQLXML

```
SQLXML getSQLXML(int parameterIndex) throws SQLException
```

- 동작: SQLXML 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
SQLXML getSQLXML(String parameterName) throws SQLException
```

- 동작: SQLXML 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="4f43e6481453ae2c"></a>
#### getString

```
String getString(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 string 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
String getString(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="87ab123207033113"></a>
#### getTime

```
Time getTime(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 time 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Time 객체를 만들 때, local timezone을 사용한다.
- parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
Time getTime(int parameterIndex, Calendar cal) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 time 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Time 객체를 만들 때, cal의 timezone을 사용한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
Time getTime(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
Time getTime(String parameterName, Calendar cal) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="6025e8ebb19a3b04"></a>
#### getTimestamp

```
Timestamp getTimestamp(int parameterIndex) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 timestamp 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Timestamp 객체를 만들 때, local timezone을 사용한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
Timestamp getTimestamp(int parameterIndex, Calendar cal) throws SQLException
```

- 동작: parameterIndex 번째 column의 데이터를 timestamp 타입으로 얻는다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Timestamp 객체를 만들 때, cal의 timezone을 사용한다.
- 예외: parameterIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우, SQLException이 발생한다.

```
Timestamp getTimestamp(String parameterName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
Timestamp getTimestamp(String parameterName, Calendar cal) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="960dc4fe35ba287f"></a>
#### getURL

```
URL getURL(int parameterIndex) throws SQLException
```

- 동작: URL 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
URL getURL(String parameterName) throws SQLException
```

- 동작: URL 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="9b21c93b3caf80eb"></a>
#### registerOutParameter

```
void registerOutParameter(int parameterIndex, int sqlType) throws SQLException
```

- 동작: parameterIndex 위치에 있는 OUT 매개 변수를 sqlType으로 등록한다. 모든 out 매개 변수는 stored procedure가 실행되기 전에 등록되어야 한다. sqlType으로 지정된 out 매개 변수의 JDBC 타입은 매개 변수 값을 읽기 위해 get method에 사용되는 Java 타입을 결정한다. GOLDILOCKS 타입별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: parametrIndex가 유효하지 않거나, database에 접근할 수 없거나 CallableStatement가 이미 닫혀 있을 경우 SQLException이 발생한다. GOLDILOCKS가 지원하지 않는 타입에 대해서는 SQLFeatureNotSupprtedException이 발생한다.

```
void registerOutParameter(int parameterIndex, int sqlType, int scale) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void registerOutParameter(int parameterIndex, int sqlType, String typeName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void registerOutParameter(String parameterName, int sqlType) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void registerOutParameter(String parameterName, int sqlType, int scale) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void registerOutParameter(String parameterName, int sqlType, String typeName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="6ad629f1eece5580"></a>
#### setAsciiStream

```
void setAsciiStream(String parameterName, InputStream x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setAsciiStream(String parameterName, InputStream x, int length) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setAsciiStream(String parameterName, InputStream x, long length) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="313e4bb55851f520"></a>
#### setBigDecimal

```
void setBigDecimal(String parameterName, BigDecimal x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="7537799c4343bfb5"></a>
#### setBinaryStream

```
void setBinaryStream(String parameterName, InputStream x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setBinaryStream(String parameterName, InputStream x, int length) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setBinaryStream(String parameterName, InputStream x, long length) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="92769cc9ad1894a3"></a>
#### setBlob

```
void setBlob(String parameterName, Blob x) throws SQLException
```

- 동작: Blob 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
void setBlob(String parameterName, InputStream inputStream) throws SQLException
```

- 동작: Blob 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
void setBlob(String parameterName, InputStream inputStream, long length) throws SQLException
```

- 동작: Blob 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="ac3caaa8ab78ffba"></a>
#### setBoolean

```
void setBoolean(String parameterName, boolean x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="3eb186bc721643de"></a>
#### setByte

```
void setByte(String parameterName, byte x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="471cef83a6b28805"></a>
#### setBytes

```
void setBytes(String parameterName, byte[] x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="7acb1e1d74cb7676"></a>
#### setCharacterStream

```
void setCharacterStream(String parameterName, Reader reader) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setCharacterStream(String parameterName, Reader reader, int length) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setCharacterStream(String parameterName, Reader reader, long length) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="00b56f8936bfa0a5"></a>
#### setClob

```
void setClob(String parameterName, Clob x) throws SQLException
```

- 동작: Clob 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
void setClob(String parameterName, Reader reader) throws SQLException
```

- 동작: Clob 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
void setClob(String parameterName, Reader reader, long length) throws SQLException
```

- 동작: Clob 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="9c8e0b40c90ec601"></a>
#### setDate

```
void setDate(String parameterName, Date x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setDate(String parameterName, Date x, Calendar cal) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="6e090d7ad17c37fe"></a>
#### setDouble

```
void setDouble(String parameterName, double x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="a9a671d9693431bb"></a>
#### setFloat

```
void setFloat(String parameterName, float x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="f3b76d9c7cf3ea95"></a>
#### setInt

```
void setInt(String parameterName, int x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="d61baeafb1728941"></a>
#### setLong

```
void setLong(String parameterName, long x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="514466fb6b23f5fb"></a>
#### setNCharacterStream

```
void setNCharacterStream(String parameterName, Reader value) throws SQLException
```

- 동작: NChar는 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setNCharacterStream(String parameterName, Reader value, long length) throws SQLException
```

- 동작: NChar는 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="7787e0f0971f6d79"></a>
#### setNClob

```
void setNClob(String parameterName, NClob value) throws SQLException
```

- 동작: NClob은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setNClob(String parameterName, Reader reader) throws SQLException
```

- 동작: NClob은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setNClob(String parameterName, Reader reader, long length) throws SQLException
```

- 동작: NClob은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="c51066b2dacf05f8"></a>
#### setNString

```
void setNString(String parameterName, String value) throws SQLException
```

- 동작: NChar는 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="ea464b3dd01cf4dd"></a>
#### setNull

```
void setNull(String parameterName, int sqlType) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setNull(String parameterName, int sqlType, String typeName) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="cf0da60513373077"></a>
#### setObject

```
void setObject(String parameterName, Object x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setObject(String parameterName, Object x, int targetSqlType) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setObject(String parameterName, Object x, int targetSqlType, int scale) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="1e7231b76c234afc"></a>
#### setRowId

```
void setRowId(String parameterName, RowId x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="a77b42bb4d7001f7"></a>
#### setShort

```
void setShort(String parameterName, short x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="9301ffd5ed88542e"></a>
#### setSQLXML

```
void setSQLXML(String parameterName, SQLXML xmlObject) throws SQLException
```

- 동작: SQLXML 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="f4a128b7b03c1235"></a>
#### setString

```
void setString(String parameterName, String x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="5621dec9eb007878"></a>
#### setTime

```
void setTime(String parameterName, Time x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setTime(String parameterName, Time x, Calendar cal) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="9d617a825715d75e"></a>
#### setTimestamp

```
void setTimestamp(String parameterName, Timestamp x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setTimestamp(String parameterName, Timestamp x, Calendar cal) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="7a8365c356b650c1"></a>
#### setURL

```
void setURL(String parameterName, URL val) throws SQLException
```

- 동작: URL 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="d23c9b1f5450a9b4"></a>
#### wasNull

```
boolean wasNull()
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="4df7e91ee3b49f1d"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface)
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="dd87dceeb5735afd"></a>
#### unwrap

```
boolean isWrapperFor(Class<?> iface)
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="3f5b01bf9c0fccba"></a>
### Clob

클래스가 구현되지 않았다.

<a id="850a7f6ab01bc2aa"></a>
#### free

```
void free() throws SQLException
```

<a id="760f6ec91133ca8e"></a>
#### getAsciiStream

```
InputStream getAsciiStream() throws SQLException
```

<a id="d7fe1a8574afa637"></a>
#### getCharacterStream

```
Reader getCharacterStream() throws SQLException
```

```
Reader getCharacterStream(long pos, long length) throws SQLException
```

<a id="6db578da416c8db4"></a>
#### getSubString

```
String getSubString(long pos, int length) throws SQLException
```

<a id="28f32bb7830a7505"></a>
#### length

```
long length() throws SQLException
```

<a id="06a46eda2e58fd70"></a>
#### position

```
long position(Clob searchstr, long start) throws SQLException
```

```
long position(String searchstr, long start) throws SQLException
```

<a id="d8ab49932a480d08"></a>
#### setAsciiStream

```
OutputStream setAsciiStream(long pos) throws SQLException
```

<a id="ba6080b8bd9504f0"></a>
#### setCharacterStream

```
Writer setCharacterStream(long pos) throws SQLException
```

<a id="4e5a293b687dc039"></a>
#### setString

```
int setString(long pos, String str) throws SQLException
```

```
int setString(long pos, String str, int offset, int len) throws SQLException
```

<a id="5f661f03a562d1a0"></a>
#### truncate

```
void truncate(long len) throws SQLException
```

<a id="a6a83d6cefcc1cec"></a>
### CommonDataSource

<a id="887c572a8ad087b5"></a>
#### getLoginTimeout

```
int getLoginTimeout() throws SQLException
```

- 동작: 설정된 login timeout 값을 반환한다. Login timeout은 서버와 소켓을 연결할 때 timeout 값으로 사용된다. 설정되지 않은 경우, 0을 반환한다. 0은 무한 대기를 의미한다.
- 예외: 발생하지 않는다.

<a id="e52115cdf9b9567f"></a>
#### getLogWriter

```
PrintWriter getLogWriter() throws SQLException
```

- 동작: 이 DataSource에 설정된 log writer를 반환한다. 설정되지 않은 경우 null을 반환한다. Log writer는 각종 trace log를 기록할 PrintWriter를 의미한다. 자세한 내용은 [로깅](#d8e7c4d84358a1fe)을 참조한다.
- 예외: 발생하지 않는다.

<a id="596422b090cb94fa"></a>
#### setLoginTimeout

```
void setLoginTimeout(int seconds) throws SQLException
```

- 동작: Login timeout 값을 설정한다. Login timeout은 서버와 소켓을 연결할 때 timeout 값으로 사용된다. 0은 무한 대기를 의미한다.
- 예외: 발생하지 않는다.

<a id="34e8497519469e61"></a>
#### setLogWriter

```
void setLogWriter(PrintWriter out) throws SQLException
```

- 동작: 이 DataSource에 log writer를 설정한다. 설정하지 않으면 기본적으로 null이다. Log writer는 각종 trace log를 기록할 PrintWriter를 의미한다. 이 값을 설정하면 옵션에 따라 trace log, query log, protocol log를 기록하는데, 이 DataSource로부터 생성된 connection 객체와 그로부터 생성되는 모든 statement, ResultSet 등의 객체들이 로깅을 수행한다. Trace log, query log, protocol log 옵션은 connection URL이나 property에 명시할 수 있다. 자세한 내용은 [로깅](#d8e7c4d84358a1fe)을 참조한다.
- 예외: 발생하지 않는다.

<a id="5a0a30e5d5f381f2"></a>
#### setDataSourceName

```
void setDataSourceName(String aDataSourceName)
```

- 동작: Data source 이름을 설정한다. 연결에 필요한 정보는 아니다. 단지 객체를 구별하기 위해 별도로 부여할 수 있는 정보이다.
- 예외: 발생하지 않는다.

<a id="518c6e03068ce5d9"></a>
#### setServerName

```
void setServerName(String aServerName)
```

- 동작: 서버 이름, 즉 연결 URL을 설정한다. 연결에 필요한 필수 정보이다.
- 예외: 발생하지 않는다.

<a id="79c656175a6de8a9"></a>
#### setDatabaseName

```
void setDatabaseName(String aDBName)
```

- 동작: 데이터베이스 이름을 설정한다. 연결에 필요한 필수 정보이다.
- 예외: 발생하지 않는다.

<a id="0134cb867e51ceb9"></a>
#### setNetworkProtocol

```
void setNetworkProtocol(String aProtocol)
```

- 동작: 네트워크 프로토콜 정보이다. 연결에 필요한 정보는 아니다.
- 예외: 발생하지 않는다.

<a id="355c6bfe066ed851"></a>
#### setUser

```
void setUser(String aUser)
```

- 동작: 연결 계정 이름을 설정한다. 연결에 필요한 필수 정보이다.
- 예외: 발생하지 않는다.

<a id="d8952505d6e4a623"></a>
#### setPassword

```
void setPassword(String aPassword)
```

- 동작: 연결 계정 password를 설정한다. 연결에 필요한 필수 정보이다.
- 예외: 발생하지 않는다.

<a id="b7c9d51d06327b31"></a>
#### setPortNumber

```
void setPortNumber(int aPort)
```

- 동작: 서버에 접속할 때 사용할 포트 번호를 설정한다. 연결에 필요한 필수 정보이다.
- 예외: 발생하지 않는다.

```
void setPortNumber(String aPort)
```

- 동작: 서버에 접속할 때 사용할 포트 번호를 설정한다. 연결에 필요한 필수 정보이다.
- 예외: 발생하지 않는다.

<a id="7eab1a292da674c0"></a>
#### setRoleName

```
void setRoleName(String aRoleName)
```

- 동작: 서버에 접속할 때의 role을 명시한다. 연결에 필요한 필수 정보는 아니지만 연결 관련 정보이다. ""나 "ADMIN", "SYSDBA" 중의 하나를 명시한다
- 예외: 발생하지 않는다.

<a id="79654f34140df75a"></a>
#### setDescription

```
void setDescription(String aDescription)
```

- 동작: 이 data source에 대한 설명을 설정한다. 연결에 사용되지 않는다.
- 예외: 발생하지 않는다.

<a id="6da7bfeb5c0e3cd6"></a>
#### setConnectionProperties

```
void setConnectionProperties(Properties aProps)
```

- 동작: 각종 연결에 사용될 수 있는 속성을 정의한다.
- 예외: 발생하지 않는다.

<a id="918b16e1fe1a0c4d"></a>
#### setURL

```
void setURL(String aURL) throws SQLException
```

- 동작: URL 형태로 serverName, portNumber, databaseName을 지정해준다. DriverManager를 통해서 연결할 때와 똑같은 URL을 취한다.
- 예외: 잘못된 형식이면 SQLException이 발생한다.

```
void setUrl(String aUrl) throws SQLException
```

setURL (String aURL)과 동일하다.

<a id="ccb90af6c61c6584"></a>
#### setLogTarget

```
void setLogTarget(String aTarget)
```

- 동작: setLogWriter를 호출할 수 없을 경우 이 method를 통해 log writer를 설정할 수 있다. 현재는 aTarget이 "console"인 경우에만 지원된다. 다른 값은 무시된다. "console"로 설정하면 이 DataSource로부터 생성되는 모든 connection 객체 이하의 로깅들이 콘솔로 출력된다.
- 예외: 발생하지 않는다.

<a id="3cb49603512cae9f"></a>
#### setTraceLog

```
void setTraceLog(String aMode)
```

- 동작: Trace log를 설정한다. aMode가 on 이면 trace logging이 켜진다.
- 예외: 발생하지 않는다.

<a id="c5d8d0c013854a1a"></a>
#### setQueryLog

```
void setQueryLog(String aMode)
```

- 동작: Query log를 설정한다. aMode가 on 이면 query logging이 켜진다.
- 예외: 발생하지 않는다.

<a id="f587117aebd8dfbf"></a>
#### setProtocolLog

```
void setProtocolLog(String aMode)
```

- 동작: Protocol log를 설정한다. aMode가 on 이면 protocol logging이 켜진다.
- 예외: 발생하지 않는다.

<a id="cd757c6d19388fb7"></a>
### Connection

<a id="75348a8eeb7ec4a4"></a>
#### clearWarnings

```
void clearWarnings() throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- 동작: 현재 connection 객체가 가지고 있는 warning 객체(들)을 제거한다.
- 예외: 발생하지 않는다.

<a id="df5a6fdac48d3f32"></a>
#### close

```
void close() throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- 동작: 현재 connection을 더 이상 사용하지 않기 위해 GOLDILOCKS와의 연결을 끊고 이 객체로부터 만든 모든 statement 객체를 close한다. 이미 close되어 있으면 아무런 동작도 하지 않는다.
- 예외: 서버에서 에러가 발생하거나 응답이 없는 경우, 예외가 발생할 수 있다.

<a id="81017ff83c8b25d3"></a>
#### commit

```
void commit() throws SQLException
```

- 동작: Non-auto commit 모드일 경우 현재 connection에 대해 commit을 수행한다.
- 예외: 이미 close되어 있거나 auto commit 모드일 경우 SQLException이 발생한다.

<a id="827b9a2b52013fca"></a>
#### createArrayOf

```
Array createArrayOf(String typeName, Object[] elements) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="193ce511d00a3ed7"></a>
#### createBlob

```
Blob createBlob() throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="d70bb5a56596b8de"></a>
#### createClob

```
Clob createClob() throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="be9cf4f17c8286b7"></a>
#### createNClob

```
NClob createNClob() throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="9bec1ce63699564d"></a>
#### createSQLXML

```
SQLXML createSQLXML() throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="da8aa656c7ad0742"></a>
#### createStatement

```
Statement createStatement() throws SQLException
```

- 동작: Statement 객체를 생성한다. 이 statement로부터 생성되는 ResultSet의 타입은 ResultSet.TYPE_FORWARD_ONLY이며, concurrency는 ResultSet.CONCUR_READ_ONLY, holdability는 ResultSet.HOLD_CURSORS_OVER_COMMIT이다.
- 예외: 이미 close된 경우에는 SQLException이 발생한다.

```
Statement createStatement(int resultSetType, int resultSetConcurrency) throws SQLException
```

- 동작: 사용자가 지정한 resultset type과 resultset concurrency를 가지는 ResultSet을 생성하는 statement 객체를 생성한다. 이 statement 객체로부터 생성되는 ResultSet의 holdability는 connection의 holdability 타입과 동일하다. Connection의 기본 holdability 값은 ResultSet.HOLD_CURSORS_OVER_COMMIT이다.
- 예외: 이미 close된 경우에는 SQLException이 발생한다.

```
Statement createStatement(int resultSetType, int resultSetConcurrency, int resultSetHoldability) throws SQLException
```

- 동작: 사용자가 지정한 resultset type, resultset concurrency, holdability를 가지는 ResultSet을 생성하는 statement 객체를 생성한다.
- 예외: 이미 close된 경우에는 SQLException이 발생한다.

<a id="67319a16e5879e23"></a>
#### createStruct

```
Struct createStruct(String typeName, Object[] attributes) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="7a756c73ee65b9a6"></a>
#### getAutoCommit

```
boolean getAutoCommit() throws SQLException
```

- 동작: 현재 auto commit 모드를 반환한다. setAutoCommit()을 호출한 적이 없다면 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="ca9777a2181c2f88"></a>
#### getCatalog

```
String getCatalog() throws SQLException
```

- 동작: 데이터베이스의 현재 카탈로그 이름을 얻어온다.
- 예외: 서버로부터 에러가 발생하거나 응답이 없는 경우 SQLException이 발생한다.

<a id="dcc75627b3fe6e2b"></a>
#### getClientInfo

```
Properties getClientInfo() throws SQLException
```

- 동작: 사용자가 설정한 client 정보를 반환한다. 설정한 정보가 없으면 null을 반환한다.
- 예외: 발생하지 않는다.

```
String getClientInfo(String name) throws SQLException
```

- 동작: 사용자가 설정한 특정 client 정보를 반환한다. 설정한 정보가 없으면 null을 반환한다.
- 예외: 발생하지 않는다.

<a id="197e112c94599373"></a>
#### getHoldability

```
int getHoldability() throws SQLException
```

- 동작: 이 객체로부터 만들어지는 statement들의 기본 holdability 값을 반환한다. 기본값은 ResultSet.HOLD_CURSORS_OVER_COMMIT이다.
- 예외: 발생하지 않는다.

<a id="da4e598bd05e5dd3"></a>
#### getMetaData

```
DatabaseMetaData getMetaData() throws SQLException
```

- 동작: 이 객체로부터 메타 정보를 조회할 수 있는 DatabaseMetaData 객체를 얻는다. 항상 동일한 객체가 반환된다.
- 예외: 이미 close되어 있을 경우 SQLException이 발생한다.

<a id="46ec1c931afe2760"></a>
#### getTransactionIsolation

```
int getTransactionIsolation() throws SQLException
```

- 동작: 현재 세션 (connection)에 설정되어 있는 transaction isolation level을 얻는다. 서버에 설정된 기본값은 Connection.TRANSACTION_READ_COMMITTED이다.
- 예외: 서버로부터 에러를 응답받는 경우 SQLException이 발생한다.

<a id="6d9362a2856219b8"></a>
#### getTypeMap

```
Map<String,Class<?>> getTypeMap() throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="d73ae264b2c88677"></a>
#### getWarnings

```
SQLWarning getWarnings() throws SQLException
```

- 동작: 현재까지 connection 객체가 서버로부터 응답받은 warning을 반환한다. 존재하지 않거나 clearWarnings()를 한 후라면 null을 반환한다.
- 예외: 발생하지 않는다.

<a id="42cc19355818fb97"></a>
#### isClosed

```
boolean isClosed() throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- 동작: close()를 성공적으로 호출한 적이 있는지 여부를 묻는다. close()를 성공적으로 수행했을 경우 true를 반환하고 그렇지 않다면 false를 반환한다.
- 예외: 발생하지 않는다.

> 이 method는 실제 서버와의 연결이 끊겼는지 여부는 알려주지 않는다. 실제로 연결이 끊겼더라도 사용자가 close()를 호출한 적이 없다면 false를 반환한다.

<a id="4f8788db9c2f5a67"></a>
#### isReadOnly

```
boolean isReadOnly() throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- 동작: 이 세션 (connection)이 read-only 모드일 경우 true를, 그렇지 않을 경우 false를 반환한다. 기본값은 false이다. 서버와의 통신이 발생한다.
- 예외: 서버로부터 에러를 응답받거나 응답이 없는 경우 SQLException이 발생한다.

<a id="a6e236e0165b4124"></a>
#### isValid

```
boolean isValid(int timeout) throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- 동작: isClosed()가 true를 반환할 상태이거나 heart beat query를 서버로 보내 성공적으로 수행에 대한 응답을 받지 못할 경우 false를, 아닌 경우엔 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="3b55ad649bf6f05c"></a>
#### nativeSQL

```
String nativeSQL(String sql) throws <a class="link" href="http://docs.oracle.com/javase/6/docs/api/java/sql/SQLException.html">SQLException</a>
```

- 동작: 주어진 사용자 SQL 문에 대해 서버에서 인식하는 native SQL을 반환한다. GOLDILOCKS에서는 사용자의 SQL 문을 서버가 있는 그대로 인식하기 때문에 항상 사용자가 부여한 값 그대로를 반환한다.
- 예외: 발생하지 않는다.

<a id="1f13bfd5de17b22d"></a>
#### prepareCall

```
CallableStatement prepareCall(String sql) throws SQLException
```

- 동작: Stored procedures 호출을 위한 CallableStatement 객체를 사용자에게 반환한다. 이 CallableStatement로부터 생성되는 ResultSet의 type은 ResultSet.TYPE_FORWARD_ONLY이고 concurrency는 ResultSet.CONCUR_READ_ONLY, holdability는 ResultSet.HOLD_CURSORS_OVER_COMMIT이다.
- 예외: 이미 close 되었거나 SQL 문이 잘못된 경우, SQLException이 발생한다.

```
CallableStatement prepareCall(String sql, int resultSetType, int resultSetConcurrency) throws SQLException
```

- 동작: 사용자가 지정한 resultset type과 resultset concurrency를 가지는 ResultSet을 생성하는 CallableStatement 객체를 생성한다. 이 CallableStatement 로부터 생성되는 ResultSet의 holdability는 connection의 holdability 타입과 동일하다. Connection의 기본 holdability 값은 ResultSet.HOLD_CURSORS_OVER_COMMIT이다.
- 예외: 이미 close되었거나 SQL 문이 잘못된 경우, SQLException이 발생한다.

```
CallableStatement prepareCall(String sql, int resultSetType, int resultSetConcurrency, int resultSetHoldability) throws SQLException
```

- 동작: 사용자가 지정한 resultset type과 resultset concurrency, holdability를 가지는 ResultSet을 생성하는 CallableStatement 객체를 생성한다.
- 예외: 이미 close되었거나 SQL 문이 잘못된 경우, SQLException이 발생한다.

<a id="ad6afcd82012affb"></a>
#### prepareStatement

```
PreparedStatement prepareStatement(String sql) throws SQLException
```

- 동작: 서버에 SQL 문을 보내어 prepare (parsing, validation, optimization)하고, 그 prepared statement를 제어할 수 있는 PreparedStatement 객체를 사용자에게 반환한다. 이 PreparedStatement로부터 생성되는 ResultSet의 type은 ResultSet.TYPE_FORWARD_ONLY이며, concurrency는 ResultSet.CONCUR_READ_ONLY, holdability는 ResultSet.HOLD_CURSORS_OVER_COMMIT이다.
- 예외: 이미 close되었거나 SQL 문이 잘못되었을 경우, SQLException이 발생한다.

```
PreparedStatement prepareStatement(String sql, int autoGeneratedKeys) throws SQLException
```

- 동작: autoGeneratedKeys가 Statement.NO_GENERATED_KEYS일 경우 prepareStatement(String sql) method와 동일하게 동작한다. 그 외의 값에 대해서는 예외가 발생한다.
- 예외: 이미 close되었거나 SQL 문이 잘못되었을 경우, 그리고 autoGeneratedKeys 값이 Statement.NO_GENERATED_KEYS도 아니고 Statement.RETURN_GENERATED_KEYS도 아닌 경우에는 SQLException이 발생한다. autoGeneratedKeys가 Statement.RETURN_GENERATED_KEYS인 경우에는 SQLFeatureNotSupportedException이 발생한다.

```
PreparedStatement prepareStatement(String sql, int[] columnIndexes) throws SQLException
```

- 동작: columnIndexes가 null일 경우 prepareStatement(String sql) method와 동일하게 동작한다. 그 외의 값에 대해서는 예외가 발생한다.
- 예외: 이미 close되었거나 SQL 문이 잘못되었을 경우, SQLException이 발생한다. columnIndexes가 null이 아닐 경우, SQLFeatureNotSupportedException이 발생한다.

```
PreparedStatement prepareStatement(String sql, int resultSetType, int resultSetConcurrency) throws SQLException
```

- 동작: 서버에 SQL 문을 보내어 prepare (parsing, validation, optimization)하고, 그 prepared statement를 제어할 수 있는 PreparedStatement 객체를 사용자에게 반환한다. 사용자가 지정한 resultset type과 resultset concurrency를 가지는 ResultSet을 생성하는 PreparedStatement 객체를 생성한다. 이 PreparedStatement로부터 생성되는 ResultSet의 holdability는 connection의 holdability 타입과 동일하다. Connection의 기본 holdability 값은 ResultSet.HOLD_CURSORS_OVER_COMMIT이다.
- 예외: 이미 close되었거나 SQL 문이 잘못되었을 경우, SQLException이 발생한다.

```
PreparedStatement prepareStatement(String sql, int resultSetType, int resultSetConcurrency, int resultSetHoldability) throws SQLException
```

- 동작: 서버에 SQL 문을 보내어 prepare (parsing, validation, optimization)하고, 그 prepared statement를 제어할 수 있는 PreparedStatement 객체를 사용자에게 반환한다. 사용자가 지정한 resultset type과 resultset concurrency, holdability를 가지는 ResultSet을 생성하는 PreparedStatement 객체를 생성한다.
- 예외: 이미 close되었거나 SQL 문이 잘못되었을 경우, SQLException이 발생한다.

```
PreparedStatement prepareStatement(String sql, String[] columnNames) throws SQLException
```

- 동작: columnNames가 null일 경우 prepareStatement(String sql) method와 동일하게 동작한다. 그 외의 값에 대해서는 예외가 발생한다.
- 예외: 이미 close되었거나 SQL 문이 잘못되었을 경우에는 SQLException이 발생한다. columnNames가 null이 아닐 경우, SQLFeatureNotSupportedException이 발생한다.

<a id="9285e1daf489087c"></a>
#### releaseSavepoint

```
void releaseSavepoint(Savepoint savepoint) throws SQLException
```

- 동작: 해당 savepoint를 서버에서 제거한다. 이 savepoint 이후의 savepoint들도 모두 제거된다.
- 예외: 이미 close되었거나 해당 savepoint 객체가 이미 해제되었거나 GOLDILOCKS savepoint 객체가 아닌 경우 SQLException이 발생한다.

<a id="7012041dc7a3320f"></a>
#### rollback

```
void rollback() throws SQLException
```

- 동작: Non auto commit 모드일 경우 현재 트랜잭션을 rollback 한다.
- 예외: 이미 close되었거나 auto commit 모드일 경우, 또는 서버로부터 에러를 응답받은 경우 SQLException이 발생한다.

```
void rollback(Savepoint savepoint) throws SQLException
```

- 동작: Non auto commit 모드일 경우 현재 트랜잭션에 대해 해당 savepoint까지 partial rollback 한다.
- 예외: 이미 close되었거나 auto commit mode일 경우, 또는 서버로부터 에러를 응답받은 경우, 그리고 해당 savepoint가 유효하지 않을 경우 SQLException이 발생한다.

<a id="b87642615ac24e4d"></a>
#### setAutoCommit

```
void setAutoCommit(boolean autoCommit) throws SQLException
```

- 동작: 현재 connection에 대한 auto commit 모드를 변경한다. 수행된 트랜잭션이 있고 non auto commit 모드에서 auto commit 모드로 변경될 경우 commit이 수행된다.
- 예외: Commit 과정에서 발생할 수 있는 예외와 동일하다.

<a id="d90a178b6e1b8b0d"></a>
#### setCatalog

```
void setCatalog(String catalog) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="4a362ab943425d2e"></a>
#### setClientInfo

```
void setClientInfo(Properties properties) throws SQLException
```

- 동작: 사용자가 지정한 client 정보를 설정한다. 기존에 있던 client 정보는 없어진다. 서버에 아무런 영향을 주지 않는다.
- 예외: 발생하지 않는다.

```
void setClientInfo(String name, String value) throws SQLException
```

- 동작: 사용자가 지정한 client 정보를 추가한다. 기존에 있던 client 정보는 그대로 유지된다.
- 예외: 발생하지 않는다.

<a id="e672341246043f5b"></a>
#### setHoldability

```
void setHoldability(int holdability) throws SQLException
```

- 동작: 이 객체로부터 생성되는 statement들이 생성하는 ResultSet의 holdability를 설정한다. 이 method를 호출하지 않았을 때의 기본값은 ResultSet.HOLD_CURSORS_OVER_COMMIT이다.
- 예외: 발생하지 않는다.

<a id="1bd332950e50a344"></a>
#### setReadOnly

```
void setReadOnly(boolean readOnly) throws SQLException
```

- 동작: 현재 세션 (connection)의 read-only 속성을 설정한다. 기본값은 false이다.
- 예외: 이미 close되었거나 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="e2ce5034db216b24"></a>
#### setSavepoint

```
Savepoint setSavepoint() throws SQLException
```

- 동작: non auto commit 모드일 경우 현재 트랜잭션에 대해 savepoint를 설정한다. savepoint 이름은 내부적으로 결정된다.
- 예외: 이미 close되었거나 auto commit 모드일 경우, 또는 서버로부터 에러를 응답받은 경우에는 SQLException이 발생한다.

```
Savepoint setSavepoint(String name) throws SQLException
```

- 동작: Non auto commit 모드일 경우 현재 트랜잭션에 대해 사용자가 지정한 이름의 savepoint를 설정한다.
- 예외: 이미 close되었거나 auto commit 모드일 경우, 또는 서버로부터 에러를 응답받은 경우 SQLException이 발생한다.

<a id="86efb6d89885c71b"></a>
#### setTransactionIsolation

```
void setTransactionIsolation(int level) throws SQLException
```

- 동작: 현재 세션 (connection)에 대해 트랜잭션 isolation level을 변경한다. 지원되는 값은 Connection.TRANSACTION_READ_COMMITED, Connection.TRANSACTION_SERIALIZABLE이다. Connection.READ_UNCOMMITTED는 Connection.TRANSACTION_READ_COMMITED으로, Connection.TRANSACTION_REPEATABLE_READ는 Connection.TRANSACTION_SERIALIZABLE으로 변경되어 설정된다.
- 예외: 이미 close되었거나 level이 올바르지 않을 경우, SQLException이 발생한다.

<a id="f1d54ef5b0d647a0"></a>
#### setTypeMap

```
void setTypeMap(Map<String,Class<?>> map) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="f4c1ef38527bff43"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- 동작: 이 객체가 iface 인터페이스를 구현한 클래스인지 묻는다. 맞으면 true를, 아니면 false를 반환한다. GOLDILOCKS connection 객체는 다른 클래스의 wrapper가 아니므로 wrapper 유무는 판단하지 않고 오직 주어진 인자 클래스 타입을 구현했는지 여부만 묻는다.
- 예외: 발생하지 않는다.

<a id="8dd9ab3dcc3527fd"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- 동작: GOLDILOCKS connection은 다른 클래스의 wrapper가 아니므로 unwrap하더라도 결국 자기 자신을 반환한다. 해당 타입으로 캐스팅한 후 반환한다. iface가 isWrapperFor() method의 인자로 주었을 때 false를 반환하는 값일 경우, 이 method는 예외를 발생시킨다.
- 예외: iface가 이 객체 타입이 아닌 경우 (이 객체가 implement 하지 않은 타입을 부여한 경우) SQLException이 발생한다.

<a id="e7231c145b26141e"></a>
### ConnectionPoolDataSource

<a id="a3911b6c63d4a69b"></a>
#### getPooledConnection

```
PooledConnection getPooledConnection() throws SQLException
```

- 동작: PooledConnection 객체를 생성한다. User name, password, connection URL 등 각종 connection 정보는 사전에 setter method로 설정되어 있어야 한다.
- 예외: 연결에 실패하면 SQLException이 발생한다.

```
PooledConnection getPooledConnection(String user, String password) throws SQLException
```

- 동작: PooledConnection 객체를 생성한다. User name과 password는 argument를 따른다. 그 외 connection 정보들은 사전에 setter method로 설정되어 있어야 한다.
- 예외: 연결에 실패하면 SQLException이 발생한다.

<a id="3868e71e96201e4e"></a>
### DatabaseMetaData

<a id="ce4ceb8ef5d86240"></a>
#### allProceduresAreCallable

```
boolean allProceduresAreCallable() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="a463bf3e7cb1087c"></a>
#### allTablesAreSelectable

```
boolean allTablesAreSelectable() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="6092fa10150aa85d"></a>
#### autoCommitFailureClosesAllResultSets

```
boolean autoCommitFailureClosesAllResultSets() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="0e2ed10b1af7b3b4"></a>
#### dataDefinitionCausesTransactionCommit

```
boolean dataDefinitionCausesTransactionCommit() throws SQLException
```

- 동작: DDL 구문을 수행할 때 자동으로 commit되지 않기 때문에 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="6fba67fc0ff31be0"></a>
#### dataDefinitionIgnoredInTransactions

```
boolean dataDefinitionIgnoredInTransactions() throws SQLException
```

- 동작: DDL 구문도 트랜잭션에 포함되기 때문에 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="9b8e1978826d18db"></a>
#### deletesAreDetected

```
boolean deletesAreDetected(int type) throws SQLException
```

- 동작: type이 ResultSet.TYPE_SCROLL_SENSITIVE이면 true를, 그렇지 않으면 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="57c8f18a0f176bb2"></a>
#### doesMaxRowSizeIncludeBlobs

```
boolean doesMaxRowSizeIncludeBlobs() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="f0620b899ce63151"></a>
#### getAttributes

```
ResultSet getAttributes(String catalog, String schemaPattern, String typeNamePattern, String attributeNamePattern) throws SQLException
```

- 동작: Empty ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="2c4d0258e3839dd2"></a>
#### getBestRowIdentifier

```
ResultSet getBestRowIdentifier(String catalog, String schema, String table, int scope, boolean nullable) throws SQLException
```

- 동작: 모든 테이블에 대해서 rowid 타입을 지원하기 때문에 rowid에 대한 정보로 구성된 row 한 개를 가진 ResultSet을 반환한다. 해당 테이블이 없을 경우, empty ResultSet을 반환한다.
- 예외: 테이블이 null이거나 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="020971570d54f203"></a>
#### getCatalogs

```
ResultSet getCatalogs() throws SQLException
```

- 동작: 카탈로그 이름을 하나의 column으로 가지는 ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="c27989b7a9fc8a84"></a>
#### getCatalogSeparator

```
String getCatalogSeparator() throws SQLException
```

- 동작: Catalog separator 문자를 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="256dc97aed1c0189"></a>
#### getCatalogTerm

```
String getCatalogTerm() throws SQLException
```

- 동작: Catalog term 문자를 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="c7663126e35f477e"></a>
#### getClientInfoProperties

```
ResultSet getClientInfoProperties() throws SQLException
```

- 동작: Client 정보를 가지는 ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="e9db3c2c503a82e7"></a>
#### getColumnPrivileges

```
ResultSet getColumnPrivileges(String catalog, String schema, String table, String columnNamePattern) throws SQLException
```

- 동작: 해당 테이블 column의 column privilege 정보를 가지는 ResultSet을 반환한다. 해당 테이블이 없거나 column 이름 패턴에 해당하는 column이 없으면 empty ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="91c0a3be9ecd65cc"></a>
#### getColumns

```
ResultSet getColumns(String catalog, String schemaPattern, String tableNamePattern, String columnNamePattern) throws SQLException
```

- 동작: 해당 테이블의 모든 column 정보를 가지는 ResultSet을 반환한다. 해당 테이블이 없거나 column 이름 패턴에 해당하는 column이 없으면 empty ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="d1f74c8a34a0982a"></a>
#### getConnection

```
Connection getConnection() throws SQLException
```

- 동작: 이 DatabaseMetaData 객체를 생성한 연결 객체를 반환한다.
- 예외: 발생하지 않는다.

<a id="9700bb8fbeb85545"></a>
#### getCrossReference

```
ResultSet getCrossReference(String parentCatalog, String parentSchema, String parentTable, String foreignCatalog, String foreignSchema, String foreignTable) throws SQLException
```

- 동작: 주어진 foreign key 테이블에서 주어진 parent table을 참조하는 foreign key들의 정보를 가지는 ResultSet을 반환한다. 참조 관계가 없을 경우, empty ResultSet을 반환한다.
- 예외: Foreign table이나 parent table이 null이거나 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="058a1f68611bce88"></a>
#### getDatabaseMajorVersion

```
int getDatabaseMajorVersion() throws SQLException
```

- 동작: 제품의 major 버전을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="9ce27298306b261b"></a>
#### getDatabaseMinorVersion

```
int getDatabaseMinorVersion() throws SQLException
```

- 동작: 제품의 minor 버전을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="4d1c6f90971150c2"></a>
#### getDatabaseProductName

```
String getDatabaseProductName() throws SQLException
```

- 동작: 제품의 이름을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="5dd61be243465415"></a>
#### getDatabaseProductVersion

```
String getDatabaseProductVersion() throws SQLException
```

- 동작: 제품의 프로덕트 버전을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="6a40db26f9ee1a77"></a>
#### getDefaultTransactionIsolation

```
int getDefaultTransactionIsolation() throws SQLException
```

- 동작: Default transaction isolation을 반환한다. 서버에 설정된 기본값은 Connection.TRANSACTION_READ_COMMITTED이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="7ef8b5503e1ed230"></a>
#### getDriverMajorVersion

```
int getDriverMajorVersion() throws SQLException
```

- 동작: GOLDILOCKS JDBC driver의 major 버전을 반환한다.
- 예외: 발생하지 않는다.

<a id="bf5cdf346b811809"></a>
#### getDriverMinorVersion

```
int getDriverMinorVersion() throws SQLException
```

- 동작: GOLDILOCKS JDBC driver의 minor 버전을 반환한다.
- 예외: 발생하지 않는다.

<a id="bba7064003bf717b"></a>
#### getDriverName

```
String getDriverName() throws SQLException
```

- 동작: "GOLDILOCKS JDBC Driver"를 반환한다.
- 예외: 발생하지 않는다.

<a id="58056f8238b068e0"></a>
#### getDriverVersion

```
String getDriverVersion() throws SQLException
```

- 동작: GOLDILOCKS JDBC driver 버전 문자열을 반환한다. 프로토콜 버전도 포함한다.
- 예외: 발생하지 않는다.

<a id="7909f08e1c8beb03"></a>
#### getExportedKeys

```
ResultSet getExportedKeys(String catalog, String schema, String table) throws SQLException
```

- 동작: 주어진 테이블의 column을 참조하는 foreign key들을 정보로 가지는 ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="ea47551c5bacd1cc"></a>
#### getExtraNameCharacters

```
String getExtraNameCharacters() throws SQLException
```

- 동작: "-$"를 반환한다.
- 예외: 발생하지 않는다.

<a id="604deac16c3274fd"></a>
#### getFunctionColumns

```
ResultSet getFunctionColumns(String catalog, String schemaPattern, String functionNamePattern, String columnNamePattern) throws SQLException
```

- 동작: Empty ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="5b709978603566ca"></a>
#### getFunctions

```
ResultSet getFunctions(String catalog, String schemaPattern, String functionNamePattern) throws SQLException
```

- 동작: Empty ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="8ed6e61fcb357dca"></a>
#### getIdentifierQuoteString

```
String getIdentifierQuoteString() throws SQLException
```

- 동작: Identifier quote 문자를 반환한다. 서버에 설정된 값은 " 이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="40aee412362cda1b"></a>
#### getImportedKeys

```
ResultSet getImportedKeys(String catalog, String schema, String table) throws SQLException
```

- 동작: 주어진 테이블의 foreign key column이 참조하는 parent key 정보를 가지는 ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="990cf86502fc3a98"></a>
#### getIndexInfo

```
ResultSet getIndexInfo(String catalog, String schema, String table, boolean unique, boolean approximate) throws SQLException
```

- 동작: 주어진 테이블에 존재하는 인덱스 정보를 가지는 ResultSet을 반환한다. Unique가 true면 unique index 정보만 보여준다. Approximate 인자는 무시된다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="972de6a4ef477417"></a>
#### getJDBCMajorVersion

```
int getJDBCMajorVersion() throws SQLException
```

- 동작: GOLDILOCKS JDBC driver의 JDBC major 버전을 반환한다. 사용하는 jar 파일에 따라 다를 수 있다.
- 예외: 발생하지 않는다.

<a id="4e01b45d63883c01"></a>
#### getJDBCMinorVersion

```
int getJDBCMinorVersion() throws SQLException
```

- 동작: GOLDILOCKS JDBC driver의 JDBC minor 버전을 반환한다. 사용하는 jar 파일에 따라 다를 수 있다.
- 예외: 발생하지 않는다.

<a id="f9fd838f38b4b3c7"></a>
#### getMaxBinaryLiteralLength

```
int getMaxBinaryLiteralLength() throws SQLException
```

- 동작: 바이너리의 최대 길이를 서버로부터 얻어온다. 0은 최대 길이가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="044a4dfd6d62db45"></a>
#### getMaxCatalogNameLength

```
int getMaxCatalogNameLength() throws SQLException
```

- 동작: 카탈로그 이름의 최대 길이를 서버로부터 얻어온다. 0은 최대 길이가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="a570401c35dc3867"></a>
#### getMaxCharLiteralLength

```
int getMaxCharLiteralLength() throws SQLException
```

- 동작: 최대 literal 길이를 서버로부터 얻어온다. 0은 최대 길이가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="5422936d7812e03b"></a>
#### getMaxColumnNameLength

```
int getMaxColumnNameLength() throws SQLException
```

- 동작: Column 이름의 최대 길이를 서버로부터 얻어온다. 0은 최대 길이가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="e0e5aed729aa1760"></a>
#### getMaxColumnsInGroupBy

```
int getMaxColumnsInGroupBy() throws SQLException
```

- 동작: Group by 절에 사용할 수 있는 column의 최대 개수를 서버로부터 얻어온다. 0은 최대 개수가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="d1cb65205fbe4026"></a>
#### getMaxColumnsInIndex

```
int getMaxColumnsInIndex() throws SQLException
```

- 동작: 인덱스에 사용할 수 있는 column의 최대 개수를 서버로부터 얻어온다. 0은 최대 개수가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="be8d59852d830c2c"></a>
#### getMaxColumnsInOrderBy

```
int getMaxColumnsInOrderBy() throws SQLException
```

- 동작: Order by 절에 사용할 수 있는 column의 최대 개수를 서버로부터 얻어온다. 0은 최대 개수가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="a61d1dff427d1a81"></a>
#### getMaxColumnsInSelect

```
int getMaxColumnsInSelect() throws SQLException
```

- 동작: Select target 절에 올 수 있는 column의 최대 개수를 서버로부터 얻어온다. 0은 최대 개수가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="5dc7acfcccfb96d4"></a>
#### getMaxColumnsInTable

```
int getMaxColumnsInTable() throws SQLException
```

- 동작: 테이블에 올 수 있는 column의 최대 개수를 서버로부터 얻어온다. 0은 최대 개수가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="eeddfac1c04af9e0"></a>
#### getMaxConnections

```
int getMaxConnections() throws SQLException
```

- 동작: 서버와의 최대 connection 개수를 서버로부터 얻어온다. 0은 최대 개수가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="9c2e95274a80fe75"></a>
#### getMaxCursorNameLength

```
int getMaxCursorNameLength() throws SQLException
```

- 동작: 커서 이름의 최대 길이를 서버로부터 얻어온다. 0은 최대 길이가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="f9e7ac80dc777944"></a>
#### getMaxIndexLength

```
int getMaxIndexLength() throws SQLException
```

- 동작: 인덱스 키 한 개가 가질 수 있는 최대 크기를 서버로부터 얻어온다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

> JDBC 스펙에는 하나의 인덱스 전체가 가질 수 있는 최대 크기를 바이트로 반환한다고 정의하고 있지만 인덱스 크기에는 제한이 없으므로 그 값은 의미가 없고 ODBC와 동일한 의미가 되도록 하기 위해 이와 같이 작동한다.

<a id="7950e16d2ed180f5"></a>
#### getMaxProcedureNameLength

```
int getMaxProcedureNameLength() throws SQLException
```

- 동작: Procedure 이름의 최대 길이를 서버로부터 얻어온다. 0은 최대 길이가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="d7f670fa9e4421e1"></a>
#### getMaxRowSize

```
int getMaxRowSize() throws SQLException
```

- 동작: 한 테이블이 가질 수 있는 최대 row 개수를 서버로부터 얻어온다. 0은 최대 개수가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="c07e77814822d97c"></a>
#### getMaxSchemaNameLength

```
int getMaxSchemaNameLength() throws SQLException
```

- 동작: 스키마 이름의 최대 길이를 서버로부터 얻어온다. 0은 최대 길이가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="9f84b3ff2b4b196a"></a>
#### getMaxStatementLength

```
int getMaxStatementLength() throws SQLException
```

- 동작: 하나의 SQL 문이 가질 수 있는 최대 문자열 길이를 서버로부터 얻어온다. 0은 최대 길이가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="0e00368c492db57f"></a>
#### getMaxStatements

```
int getMaxStatements() throws SQLException
```

- 동작: 한 번에 open할 수 있는 최대 statement 개수를 서버로부터 얻어온다. 0은 최대 개수가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="16f1e23c44c96a84"></a>
#### getMaxTableNameLength

```
int getMaxTableNameLength() throws SQLException
```

- 동작: 테이블 이름이 가질 수 있는 최대 문자열의 길이를 서버로부터 얻어온다. 0은 최대 길이가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="e1656b14a4eec79c"></a>
#### getMaxTablesInSelect

```
int getMaxTablesInSelect() throws SQLException
```

- 동작: Select 구문에 사용할 수 있는 테이블의 최대 개수를 서버로부터 얻어온다. 0은 최대 개수가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="da830253cca74adc"></a>
#### getMaxUserNameLength

```
int getMaxUserNameLength() throws SQLException
```

- 동작: User name의 최대 문자열 길이를 서버로부터 얻어온다. 0은 최대 길이가 무한대라는 의미이다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="9b84a70697d5b4f3"></a>
#### getNumericFunctions

```
String getNumericFunctions() throws SQLException
```

- 동작: SQL 표준에 해당하는 숫자 관련 함수들의 목록을 불러온다. 각 함수 이름은 콤마 (,)로 구분된다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="f01f79ceb6af7183"></a>
#### getPrimaryKeys

```
ResultSet getPrimaryKeys(String catalog, String schema, String table) throws SQLException
```

- 동작: 주어진 테이블의 모든 primary key를 포함하는 ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="628b6212fdbc2453"></a>
#### getProcedureColumns

```
ResultSet getProcedureColumns(String catalog, String schemaPattern, String procedureNamePattern, String columnNamePattern) throws SQLException
```

- 동작: 주어진 procedure들에 대해 주어진 이름 패턴을 가진 column들의 정보를 가지는 ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="4b46fcc86ed320ac"></a>
#### getProcedures

```
ResultSet getProcedures(String catalog, String schemaPattern, String procedureNamePattern) throws SQLException
```

- 동작: 주어진 이름 패턴을 가지는 procedure들을 정보로 가지는 ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="db1ed1add0f8ac49"></a>
#### getProcedureTerm

```
String getProcedureTerm() throws SQLException
```

- 동작: Procedure를 지칭하는 키워드를 서버로부터 얻어온다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="ff56f2efac4b1594"></a>
#### getResultSetHoldability

```
int getResultSetHoldability() throws SQLException
```

- 동작: ResultSet의 기본 holdability 속성을 반환한다. ResultSet.HOLD_CURSORS_OVER_COMMIT이다.
- 예외: 발생하지 않는다.

<a id="b99ff5ce2ccb7dfc"></a>
#### getRowIdLifetime

```
RowIdLifetime getRowIdLifetime() throws SQLException
```

- 동작: 항상 RowIdLifetime.ROWID_VALID_FOREVER를 반환한다.
- 예외: 발생하지 않는다.

<a id="95a1c886ad5e6da1"></a>
#### getSchemas

```
ResultSet getSchemas() throws SQLException
```

- 동작: 서버에 있는 모든 스키마에 대한 정보를 가지는 ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

```
ResultSet getSchemas(String catalog, String schemaPattern) throws SQLException
```

- 동작: 주어진 스키마 이름의 패턴을 만족하는 모든 스키마에 대한 정보를 가지는 ResultSet을 반환한다. Catalog는 무시한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="d0b3696199040c38"></a>
#### getSchemaTerm

```
String getSchemaTerm() throws SQLException
```

- 동작: 스키마를 지칭하는 키워드를 서버로부터 얻어온다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="3325353c6900bc0d"></a>
#### getSearchStringEscape

```
String getSearchStringEscape() throws SQLException
```

- 동작: Like 구문에 사용되는 escape 문자들을 문자열로 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="289aefa29ecfe57b"></a>
#### getSQLKeywords

```
String getSQLKeywords() throws SQLException
```

- 동작: SQL 문에 사용할 수 없는 키워드들을 콤마 (,)로 구분하여 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="9b21cb2c1f2c548d"></a>
#### getSQLStateType

```
int getSQLStateType() throws SQLException
```

- 동작: 항상 DatabaseMetaData.sqlStateSQL99를 반환한다.
- 예외: 발생하지 않는다.

<a id="84727c7dd84210c4"></a>
#### getStringFunctions

```
String getStringFunctions() throws SQLException
```

- 동작: SQL 표준에 해당하는 문자열을 다루는 함수들의 목록을 불러온다. 각 함수 이름들은 콤마 (,)로 구분된다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="ea950d19ac4c7394"></a>
#### getSuperTables

```
ResultSet getSuperTables(String catalog, String schemaPattern, String tableNamePattern) throws SQLException
```

- 동작: Empty ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="c5ca5ccbe187c338"></a>
#### getSuperTypes

```
ResultSet getSuperTypes(String catalog, String schemaPattern, String typeNamePattern) throws SQLException
```

- 동작: Empty ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="15d9620f014c4555"></a>
#### getSystemFunctions

```
String getSystemFunctions() throws SQLException
```

- 동작: SQL 표준에 해당하는 시스템 함수들의 목록을 불러온다. 각 함수 이름들은 콤마 (,)로 구분된다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="5dade31e27daa202"></a>
#### getTablePrivileges

```
ResultSet getTablePrivileges(String catalog, String schemaPattern, String tableNamePattern) throws SQLException
```

- 동작: 해당 조건을 만족하는 모든 테이블의 privilege 정보를 가지는 ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="6f7e4391c2bec122"></a>
#### getTables

```
ResultSet getTables(String catalog, String schemaPattern, String tableNamePattern, String[] types) throws SQLException
```

- 동작: 해당 조건을 만족하는 모든 테이블들의 정보를 가지는 ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="7d7bd6755308ee40"></a>
#### getTableTypes

```
ResultSet getTableTypes() throws SQLException
```

- 동작: 모든 테이블 타입을 정보로 가지는 ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="47c1625b27c46272"></a>
#### getTimeDateFunctions

```
String getTimeDateFunctions() throws SQLException
```

- 동작: SQL 표준에 해당하는 time, date 관련 함수들의 목록을 불러온다. 각 함수 이름들은 콤마 (,)로 구분된다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="56f73542fed7db19"></a>
#### getTypeInfo

```
ResultSet getTypeInfo() throws SQLException
```

- 동작: 데이터 타입 정보를 가지는 ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="93d74d420a55c931"></a>
#### getUDTs

```
ResultSet getUDTs(String catalog, String schemaPattern, String typeNamePattern, int[] types) throws SQLException
```

- 동작: Empty ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="a5925f5cc3346059"></a>
#### getURL

```
String getURL() throws SQLException
```

- 동작: 서버에 접속할 때 사용한 URL을 반환한다.
- 예외: 발생하지 않는다.

<a id="afa63e90bce25eb6"></a>
#### getUserName

```
String getUserName() throws SQLException
```

- 동작: 세션을 유지하고 있는 현재 user name을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

> 세션 중에 user를 변경할 수 있기 때문에 처음 접속했을 때의 user name과 다를 수도 있다.

<a id="ccc0d987b75d0151"></a>
#### getVersionColumns

```
ResultSet getVersionColumns(String catalog, String schema, String table) throws SQLException
```

- 동작: Empty ResultSet을 반환한다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="282f88b2ba775b13"></a>
#### insertsAreDetected

```
boolean insertsAreDetected(int type) throws SQLException
```

- 동작: Type과 상관없이 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="bf410c515acffc3b"></a>
#### isCatalogAtStart

```
boolean isCatalogAtStart() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="0a6857a01268ae14"></a>
#### isReadOnly

```
boolean isReadOnly() throws SQLException
```

- 동작: 현재 연결이 read-only 모드인지 여부에 대한 정보를 서버로부터 얻어온다.
- 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="4bb0d040bfc855e2"></a>
#### locatorsUpdateCopy

```
boolean locatorsUpdateCopy() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="c49e1516fd2d22ce"></a>
#### nullPlusNonNullIsNull

```
boolean nullPlusNonNullIsNull() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="e9cda86dcc7f6502"></a>
#### nullsAreSortedAtEnd

```
boolean nullsAreSortedAtEnd() throws SQLException
```

- 동작: 항상 false를 반환한다. null만 따로 정렬하지 않는다.
- 예외: 발생하지 않는다.

<a id="21b5df1ade5dc357"></a>
#### nullsAreSortedAtStart

```
boolean nullsAreSortedAtStart() throws SQLException
```

- 동작: 항상 false를 반환한다. null만 따로 정렬하지 않는다.
- 예외: 발생하지 않는다.

<a id="6296bc0896c947ae"></a>
#### nullsAreSortedHigh

```
boolean nullsAreSortedHigh() throws SQLException
```

- 동작: 항상 true를 반환한다. Null은 default로 last에 위치한다.
- 예외: 발생하지 않는다.

<a id="a72aca33b33deff8"></a>
#### nullsAreSortedLow

```
boolean nullsAreSortedLow() throws SQLException
```

- 동작: 항상 false를 반환한다. Null은 default로 last에 위치한다.
- 예외: 발생하지 않는다.

<a id="a4e025d3e6a43cde"></a>
#### othersDeletesAreVisible

```
boolean othersDeletesAreVisible(int type) throws SQLException
```

- 동작: Type이 ResultSet.TYPE_SCROLL_SENSITIVE일 경우 true를, 그렇지 않은 경우에는 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="0fb72097fadcd0be"></a>
#### othersInsertsAreVisible

```
boolean othersInsertsAreVisible(int type) throws SQLException
```

- 동작: Type과 상관없이 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="2ea407b715f7957b"></a>
#### othersUpdatesAreVisible

```
boolean othersUpdatesAreVisible(int type) throws SQLException
```

- 동작: Type이 ResultSet.TYPE_SCROLL_SENSITIVE일 경우 true를, 그렇지 않은 경우에는 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="fab45f8f0f13dbdc"></a>
#### ownDeletesAreVisible

```
boolean ownDeletesAreVisible(int type) throws SQLException
```

- 동작: Type이 ResultSet.TYPE_SCROLL_SENSITIVE일 경우 true를, 그렇지 않은 경우에는 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="b8e14ba6c22f4d81"></a>
#### ownInsertsAreVisible

```
boolean ownInsertsAreVisible(int type) throws SQLException
```

- 동작: Type과 상관없이 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="f380d91ecd66acba"></a>
#### ownUpdatesAreVisible

```
boolean ownUpdatesAreVisible(int type) throws SQLException
```

- 동작: Type이 ResultSet.TYPE_SCROLL_SENSITIVE일 경우 true를, 그렇지 않은 경우에는 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="78dd6a24baa55673"></a>
#### storesLowerCaseIdentifiers

```
boolean storesLowerCaseIdentifiers() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="fe7d0fadb8f9d4e9"></a>
#### storesLowerCaseQuotedIdentifiers

```
boolean storesLowerCaseQuotedIdentifiers() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="f84d45d9a2318963"></a>
#### storesMixedCaseIdentifiers

```
boolean storesMixedCaseIdentifiers() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="5b4f387900fcadf5"></a>
#### storesMixedCaseQuotedIdentifiers

```
boolean storesMixedCaseQuotedIdentifiers() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="f92d645211cc163d"></a>
#### storesUpperCaseIdentifiers

```
boolean storesUpperCaseIdentifiers() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="30155589841816c3"></a>
#### storesUpperCaseQuotedIdentifiers

```
boolean storesUpperCaseQuotedIdentifiers() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="1d4868416665c615"></a>
#### supportsAlterTableWithAddColumn

```
boolean supportsAlterTableWithAddColumn() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="3b01a675426022d5"></a>
#### supportsAlterTableWithDropColumn

```
boolean supportsAlterTableWithDropColumn() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="574bfe8da737d438"></a>
#### supportsANSI92EntryLevelSQL

```
boolean supportsANSI92EntryLevelSQL() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="2b2005f9c113bd66"></a>
#### supportsANSI92FullSQL

```
boolean supportsANSI92FullSQL() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="f32057b444646e8a"></a>
#### supportsANSI92IntermediateSQL

```
boolean supportsANSI92IntermediateSQL() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="8b2f236c8ead14b8"></a>
#### supportsBatchUpdates

```
boolean supportsBatchUpdates() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="edceaf28e688f9a0"></a>
#### supportsCatalogsInDataManipulation

```
boolean supportsCatalogsInDataManipulation() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="320e0a22621b8d35"></a>
#### supportsCatalogsInIndexDefinitions

```
boolean supportsCatalogsInIndexDefinitions() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="a47fc38c0eb201be"></a>
#### supportsCatalogsInPrivilegeDefinitions

```
boolean supportsCatalogsInPrivilegeDefinitions() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="ce0930ce3569650f"></a>
#### supportsCatalogsInProcedureCalls

```
boolean supportsCatalogsInProcedureCalls() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="204b7f9f4ac9f82e"></a>
#### supportsCatalogsInTableDefinitions

```
boolean supportsCatalogsInTableDefinitions() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="58bafe21c30cef69"></a>
#### supportsColumnAliasing

```
boolean supportsColumnAliasing() throws SQLException
```

- 동작: Column aliasing 지원 여부를 서버로부터 얻어온다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="8a0db4abf36c0e34"></a>
#### supportsConvert

```
boolean supportsConvert() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="f7d3be8ece67f4bb"></a>
#### supportsConvert

```
boolean supportsConvert(int fromType, int toType) throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="e4bba48a334d9fc8"></a>
#### supportsCoreSQLGrammar

```
boolean supportsCoreSQLGrammar() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="ea4f328845767e79"></a>
#### supportsCorrelatedSubqueries

```
boolean supportsCorrelatedSubqueries() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="415c6fe75473d16c"></a>
#### supportsDataDefinitionAndDataManipulationTransactions

```
boolean supportsDataDefinitionAndDataManipulationTransactions() throws SQLException
```

- 동작: 항상 true를 반환한다. 한 트랜잭션으로 DML과 DDL을 수행할 수 있다.
- 예외: 발생하지 않는다.

<a id="2ddd80ced71abc69"></a>
#### supportsDataManipulationTransactionsOnly

```
boolean supportsDataManipulationTransactionsOnly() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="11d9c37508d61650"></a>
#### supportsDifferentTableCorrelationNames

```
boolean supportsDifferentTableCorrelationNames() throws SQLException
```

- 동작: Table correlation 이름이 테이블 이름과 달라야 하는지 여부를 서버로부터 얻어온다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="80a8f057848fda35"></a>
#### supportsExpressionsInOrderBy

```
boolean supportsExpressionsInOrderBy() throws SQLException
```

- 동작: Order by 절에 수식이 사용될 수 있는지의 여부를 서버로부터 얻어온다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="a100846b231d9a9d"></a>
#### supportsExtendedSQLGrammar

```
boolean supportsExtendedSQLGrammar() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="dc8eae48a6207bf4"></a>
#### supportsFullOuterJoins

```
boolean supportsFullOuterJoins() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="42a63694aee1959d"></a>
#### supportsGetGeneratedKeys

```
boolean supportsGetGeneratedKeys() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="772ad04b610e9fc0"></a>
#### supportsGroupBy

```
boolean supportsGroupBy() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="a083816ce330d11f"></a>
#### supportsGroupByBeyondSelect

```
boolean supportsGroupByBeyondSelect() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="dd56538d45daf940"></a>
#### supportsGroupByUnrelated

```
boolean supportsGroupByUnrelated() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="2191f087044cf7fe"></a>
#### supportsIntegrityEnhancementFacility

```
boolean supportsIntegrityEnhancementFacility() throws SQLException
```

- 동작: SQL 무결성 보강 기능을 지원하는지 여부를 서버로부터 얻어온다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="da83db1be5b0ce64"></a>
#### supportsLikeEscapeClause

```
boolean supportsLikeEscapeClause() throws SQLException
```

- 동작: Like 구문에 escape 절을 지원하는지 여부를 서버로부터 얻어온다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="ac07bc38a4fafea7"></a>
#### supportsLimitedOuterJoins

```
boolean supportsLimitedOuterJoins() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="fe3d28a84666bd39"></a>
#### supportsMinimumSQLGrammar

```
boolean supportsMinimumSQLGrammar() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="d59d0b7aa8060508"></a>
#### supportsMixedCaseIdentifiers

```
boolean supportsMixedCaseIdentifiers() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="9b61d948993d497b"></a>
#### supportsMixedCaseQuotedIdentifiers

```
boolean supportsMixedCaseQuotedIdentifiers() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="cb48598d56103463"></a>
#### supportsMultipleOpenResults

```
boolean supportsMultipleOpenResults() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="65d4ebe6aa99d800"></a>
#### supportsMultipleResultSets

```
boolean supportsMultipleResultSets() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="60ac9d74fb7a1a5f"></a>
#### supportsMultipleTransactions

```
boolean supportsMultipleTransactions() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="2fe11205058aaa21"></a>
#### supportsNamedParameters

```
boolean supportsNamedParameters() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="2443a26d63c4e1ae"></a>
#### supportsNonNullableColumns

```
boolean supportsNonNullableColumns() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="9d9f421ad445eae6"></a>
#### supportsOpenCursorsAcrossCommit

```
boolean supportsOpenCursorsAcrossCommit() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="96e7ab942cef2eea"></a>
#### supportsOpenCursorsAcrossRollback

```
boolean supportsOpenCursorsAcrossRollback() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="347fa6dde6f810eb"></a>
#### supportsOpenStatementsAcrossCommit

```
boolean supportsOpenStatementsAcrossCommit() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="d7c394877c1a5a2a"></a>
#### supportsOpenStatementsAcrossRollback

```
boolean supportsOpenStatementsAcrossRollback() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="c6d6dca1d45d9ec4"></a>
#### supportsOrderByUnrelated

```
boolean supportsOrderByUnrelated() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="7309230621f61b27"></a>
#### supportsOuterJoins

```
boolean supportsOuterJoins() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="52fcc59fd6e8668c"></a>
#### supportsPositionedDelete

```
boolean supportsPositionedDelete() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="849304c2818e9eae"></a>
#### supportsPositionedUpdate

```
boolean supportsPositionedUpdate() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="78a54c3bda195e89"></a>
#### supportsResultSetConcurrency

```
boolean supportsResultSetConcurrency(int type, int concurrency) throws SQLException
```

- 동작: 모든 ResultSet 타입과 모든 concurrency에 대해 true를, 잘못된 인자에 대해서는 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="c9b6fe7972291e43"></a>
#### supportsResultSetHoldability

```
boolean supportsResultSetHoldability(int holdability) throws SQLException
```

- 동작: Holdability가 ResultSet.CLOSE_CURSORS_AT_COMMIT이거나 ResultSet.HOLD_CURSORS_OVER_COMMIT이면 true를, 그렇지 않으면 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="2acb0149648c23d8"></a>
#### supportsResultSetType

```
boolean supportsResultSetType(int type) throws SQLException
```

- 동작: Type이 ResultSet.TYPE_FORWARD_ONLY이거나 ResultSet.TYPE_SCROLL_INSENSITIVE 또는ResultSet.TYPE_SCROLL_SENSITIVE이면 true를, 그렇지 않으면 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="82e4d7b3fac2604d"></a>
#### supportsSavepoints

```
boolean supportsSavepoints() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="1133514ddd8f73cc"></a>
#### supportsSchemasInDataManipulation

```
boolean supportsSchemasInDataManipulation() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="e384e21bfdc9d46a"></a>
#### supportsSchemasInIndexDefinitions

```
boolean supportsSchemasInIndexDefinitions() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="a44101448ee4e0fe"></a>
#### supportsSchemasInPrivilegeDefinitions

```
boolean supportsSchemasInPrivilegeDefinitions() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="0fa78a666ecf6b43"></a>
#### supportsSchemasInProcedureCalls

```
boolean supportsSchemasInProcedureCalls() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="ce8be0ec1c05fca8"></a>
#### supportsSchemasInTableDefinitions

```
boolean supportsSchemasInTableDefinitions() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="bf162b142c646a43"></a>
#### supportsSelectForUpdate

```
boolean supportsSelectForUpdate() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="05b25fff1e2242e0"></a>
#### supportsStatementPooling

```
boolean supportsStatementPooling() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="7b363f21d41adb08"></a>
#### supportsStoredFunctionsUsingCallSyntax

```
boolean supportsStoredFunctionsUsingCallSyntax() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="f8e6dedbad5ab2ac"></a>
#### supportsStoredProcedures

```
boolean supportsStoredProcedures() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="645222b5883fc1d3"></a>
#### supportsSubqueriesInComparisons

```
boolean supportsSubqueriesInComparisons() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="26105b25d27ddb52"></a>
#### supportsSubqueriesInExists

```
boolean supportsSubqueriesInExists() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="9569dc5371325c14"></a>
#### supportsSubqueriesInIns

```
boolean supportsSubqueriesInIns() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="3530e0a490615cbc"></a>
#### supportsSubqueriesInQuantifieds

```
boolean supportsSubqueriesInQuantifieds() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="f36d2f70d55f2401"></a>
#### supportsTableCorrelationNames

```
boolean supportsTableCorrelationNames() throws SQLException
```

- 동작: Table correlation 이름을 지원하는지 여부를 서버로부터 얻어온다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="ab9e6c62f39e55f4"></a>
#### supportsTransactionIsolationLevel

```
boolean supportsTransactionIsolationLevel(int level) throws SQLException
```

- 동작: 해당 트랜잭션의 isolation 레벨을 지원하는지 여부를 서버로부터 알아온다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="8f7e21726b08ac88"></a>
#### supportsTransactions

```
boolean supportsTransactions() throws SQLException
```

- 동작: 항상 true를 반환한다.
- 예외: 발생하지 않는다.

<a id="7972064b5c3dde64"></a>
#### supportsUnion

```
boolean supportsUnion() throws SQLException
```

- 동작: Union 연산을 지원하는지 여부를 서버로부터 얻어온다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="88ba91ed02e8a861"></a>
#### supportsUnionAll

```
boolean supportsUnionAll() throws SQLException
```

- 동작: Union all 연산을 지원하는지 여부를 서버로부터 얻어온다.
- 예외: 서버로부터 에러를 응답받으면 SQLException이 발생한다.

<a id="7e06b564a8b5c443"></a>
#### updatesAreDetected

```
boolean updatesAreDetected(int type) throws SQLException
```

- 동작: Type이 ResultSet.TYPE_SCROLL_SENSITIVE이면 true를, 그렇지 않으면 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="9ccbb1734a20d975"></a>
#### usesLocalFilePerTable

```
boolean usesLocalFilePerTable() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="21c322f6e0c0c2e8"></a>
#### usesLocalFiles

```
boolean usesLocalFiles() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="c0867ea7d7189a10"></a>
### DataSource

<a id="7301ee90539d7485"></a>
#### getConnection

```
Connection getConnection() throws SQLException
```

- 동작: 새로운 연결 객체를 열어 반환한다. 연결에 필요한 정보들은 별도의 비표준 method들로 사전에 설정되어 있어야 한다.
- 예외: 서버와의 연결에 실패하면 SQLException이 발생한다.

```
Connection getConnection(String username, String password) throws SQLException
```

- 동작: Username과 password로 새로운 연결 객체를 열어 반환한다. 연결에 필요한 그 외의 정보들은 별도의 비표준 method들로 사전에 설정되어 있어야 한다.
- 예외: 서버와의 연결에 실패하면 SQLException이 발생한다.

<a id="314389ccf6f5df56"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- 동작: 이 클래스는 다른 클래스의 wrapper로 구현하지 않았다. 이 객체가 iface의 instance이면 true를, 그렇지 않으면 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="bf14cedffa2f8a0b"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- 동작: 이 클래스는 다른 클래스의 wrapper로 구현되지 않았기 때문에 this를 반환한다.
- 예외: 이 객체가 iface의 instance가 아니면 SQLException이 발생한다.

<a id="23fded3145d174f9"></a>
### Driver

<a id="a571970b8fb145e9"></a>
#### acceptsURL

```
boolean acceptsURL(String url) throws SQLException
```

- 동작: url이 null이 아니고 "jdbc:goldilocks:"로 시작하면 true를, 그런지 않으면 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="7a7dea98194637f7"></a>
#### connect

```
Connection connect(String url, Properties info) throws SQLException
```

- 동작: 새로운 연결 객체를 생성하고 반환한다. url은 서버 주소, DB 이름, 포트를 포함하고 있어야 한다.
- 예외: 잘못된 url이거나 서버로부터의 연결에 성공하지 못하면 SQLException이 발생한다.

<a id="fcddc4c7981d4154"></a>
#### getMajorVersion

```
int getMajorVersion() throws SQLException
```

- 동작: GOLDILOCKS JDBC driver의 major 버전을 반환한다.
- 예외: 발생하지 않는다.

<a id="e75d66b5f4317339"></a>
#### getMinorVersion

```
int getMinorVersion() throws SQLException
```

- 동작: GOLDILOCKS JDBC driver의 minor 버전을 반환한다.
- 예외: 발생하지 않는다.

<a id="389c38086ef9dfad"></a>
#### getPropertyInfo

```
DriverPropertyInfo[] getPropertyInfo(String url, Properties info) throws SQLException
```

- 동작: GOLDILOCKS JDBC의 driver가 연결될 때 사용할 수 있는 속성의 목록을 얻어온다.
- 예외: 발생하지 않는다.

<a id="21edd553266227d2"></a>
#### jdbcCompliant

```
boolean jdbcCompliant() throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="0f1b53a59f7a14bd"></a>
### NClob

클래스가 구현되지 않았다.

<a id="0252eb5649a94ac7"></a>
#### free

```
void free() throws SQLException
```

<a id="d2d4ed1d765f8289"></a>
#### getAsciiStream

```
InputStream getAsciiStream() throws SQLException
```

<a id="99d8f0d536f46c51"></a>
#### getCharacterStream

```
Reader getCharacterStream() throws SQLException
```

```
Reader getCharacterStream(long pos, long length) throws SQLException
```

<a id="599231064c37cb45"></a>
#### getSubString

```
String getSubString(long pos, int length) throws SQLException
```

<a id="bb0dc37bef874a5c"></a>
#### length

```
long length() throws SQLException
```

<a id="95b066f25762e609"></a>
#### position

```
long position(Clob searchstr, long start) throws SQLException
```

```
long position(String searchstr, long start) throws SQLException
```

<a id="4e3237a1cfedb379"></a>
#### setAsciiStream

```
OutputStream setAsciiStream(long pos) throws SQLException
```

<a id="1a542927462429d5"></a>
#### setCharacterStream

```
Writer setCharacterStream(long pos) throws SQLException
```

<a id="582beada32096fa6"></a>
#### setString

```
int setString(long pos, String str) throws SQLException
```

```
int setString(long pos, String str, int offset, int len) throws SQLException
```

<a id="fd62a5d4acdfe8c2"></a>
#### truncate

```
void truncate(long len) throws SQLException
```

<a id="b58868b60471e2e9"></a>
### ParameterMetaData

ParameterMetaData 객체는 PreparedStatement.getParameterMetaData()를 통해서 얻을 수 있는데, GOLDILOCKS JDBC의 ParameterMetaData는 in/ out 여부에 대한 정보 외에 타입 등에 관한 정보는 실제 데이터베이스의 정보를 이용하지 않고 기본 타입인 varchar를 기준으로 한다. Prepare된 후에 parameter에 대해 서버로부터 얻을 수 있는 정보는 in/ out 뿐이기 때문이다. 예를 들어, "select * from t1 where a=?"라는 질의문으로 prepare를 할 경우, 조건절에 사용된 parameter의 타입은 정해지지 않은 상태이다. 서버는 기본적으로 varchar 타입이라고 가정할 뿐이다.

<a id="c00b5585bd542425"></a>
#### getParameterClassName

```
String getParameterClassName(int param) throws SQLException
```

- 동작: java.lang.String을 반환한다. 해당 parameter 타입은 varchar로 간주한다.
- 예외: param 값이 parameter 개수 범위를 벗어나면 SQLException이 발생한다.

<a id="00ff599ea09a1024"></a>
#### getParameterCount

```
int getParameterCount() throws SQLException
```

- 동작: Parameter 개수를 반환한다. 질의문에 사용된 ?의 개수이기도 하다.
- 예외: 발생하지 않는다.

<a id="7eef6d876b38dce6"></a>
#### getParameterMode

```
int getParameterMode(int param) throws SQLException
```

- 동작: 해당 param 번째 parameter의 in/ out 모드를 반환한다. ParameterMetaData.parameterModeIn, ParameterMetaData.parameterModeInOut, ParameterMetaData.parameterModeOut, ParameterMetaData.parameterModeUnknown 중의 하나를 반환한다. 아직까지는 실제로 parameterModeUnknown 값이 반환되는 경우는 없다.
- 예외: param 값이 parameter 개수 범위를 벗어나면 SQLException이 발생한다.

<a id="d940ff85a0c0c7b1"></a>
#### getParameterType

```
int getParameterType(int param) throws SQLException
```

- 동작: 모든 parameter에 대해 Types.VARCHAR를 반환한다.
- 예외: param 값이 parameter 개수 범위를 벗어나면 SQLException이 발생한다.

<a id="c37ee32c3fc82741"></a>
#### getParameterTypeName

```
String getParameterTypeName(int param) throws SQLException
```

- 동작: 모든 parameter에 대해 "VARCHAR"를 반환한다.
- 예외: param 값이 parameter 개수 범위를 벗어나면 SQLException이 발생한다.

<a id="2a72b87d79cb629f"></a>
#### getPrecision

```
int getPrecision(int param) throws SQLException
```

- 동작: 모든 parameter에 대해 4000을 반환한다. 기본적으로 parameter는 varchar(4000)으로 간주된다.
- 예외: param 값이 parameter 개수 범위를 벗어나면 SQLException이 발생한다.

<a id="0b2bc453d5303fa9"></a>
#### getScale

```
int getScale(int param) throws SQLException
```

- 동작: 모든 parameter에 대해 0을 반환한다. 기본적으로 parameter는 varchar(4000)으로 간주된다.
- 예외: param 값이 parameter 개수 범위를 벗어나면 SQLException이 발생한다.

<a id="4ba2fd0508daf963"></a>
#### isNullable

```
int isNullable(int param) throws SQLException
```

- 동작: 항상 ParameterMetaData.parameterNullableUnknown을 반환한다.
- 예외: param 값이 parameter 개수 범위를 벗어나면 SQLException이 발생한다.

<a id="46d5a394cc26718d"></a>
#### isSigned

```
boolean isSigned(int param) throws SQLException
```

- 동작: 항상 false를 반환한다.
- 예외: param 값이 parameter 개수 범위를 벗어나면 SQLException이 발생한다.

<a id="28be7898d792afcc"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- 동작: 이 객체가 iface의 인스턴스인지 묻고 인스턴스일 경우 true를, 그렇지 않으면 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="44c626a2854dbf06"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- 동작: 이 객체가 iface의 인스턴스일 경우, 이 객체를 iface 타입으로 캐스팅해 반환한다.
- 예외: 이 객체가 iface의 인스턴스가 아닐 경우, SQLException이 발생한다.

<a id="9e318a438bfb5013"></a>
### PooledConnection

<a id="54631653280f0a22"></a>
#### addConnectionEventListener

```
void addConnectionEventListener(ConnectionEventListener listener) throws SQLException
```

- 동작: ConnectionEventListener 객체를 등록한다. 이후 이 PooledConnection으로부터 얻은 connection 객체 (logical connection)의 close()가 호출되거나 실제 connection이 끊기면 등록된 listener들에게로 ConnectionEvent를 발생시킨다.
- 예외: 발생하지 않는다.

<a id="0af9f617ac505902"></a>
#### addStatementEventListener

```
void addStatementEventListener(StatementEventListener listener) throws SQLException
```

- 동작: 아무런 동작을 하지 않는다. GOLDILOCKS JDBC driver는 이 method를 구현하지 않았다. Statement pooling 기능은 외부 미들웨어에 맡겨둔다.
- 예외: 발생하지 않는다.

<a id="f7c2a9751eecd5ad"></a>
#### close

```
void close() throws SQLException
```

- 동작: 이 객체가 가지고 있는 physical connection의 close를 호출한다.
- 예외: Physical connection의 close에서 발생할 수 있다.

<a id="6752f6ed39d68087"></a>
#### getConnection

```
Connection getConnection() throws SQLException
```

- 동작: 이 객체가 가지고 있는 logical connection을 반환한다.
- 예외: 발생하지 않는다.

<a id="354cbf421c7749a1"></a>
#### removeConnectionEventListener

```
void removeConnectionEventListener(ConnectionEventListener listener) throws SQLException
```

- 동작: 등록된 ConnectionEventListener를 제거한다. 이후 이 listener에게는 ConnectionEvent가 전달되지 않는다.
- 예외: 발생하지 않는다.

<a id="5a3a60b1c7630bfd"></a>
#### removeStatementEventListener

```
void removeStatementEventListener(StatementEventListener listener) throws SQLException
```

- 동작: 아무런 동작을 하지 않는다.
- 예외: 발생하지 않는다.

<a id="7bbc3faf505d0c2b"></a>
### PreparedStatement

<a id="0b130854d5d6c277"></a>
#### addBatch

```
void addBatch() throws SQLException
```

- 동작: 현재 바인딩한 데이터들을 batch job으로 등록한다. Batch job이 하나라도 등록되어 있으면 execute(), executeUpdate(), executeQuery()를 실행할 때 에러가 발생한다. Parameter가 하나라도 바인딩되어 있지 않으면 에러가 발생한다. addBatch한 후 setXXX() 계열의 method로 바인딩하지 않은 상태에서 다시 addBatch하면 이전에 바인딩한 값으로 batch job을 등록한다.
- 예외: 한 번도 바인딩되지 않은 parameter가 있으면 예외가 발생한다.

<a id="103124681d259c82"></a>
#### clearParameters

```
void clearParameters() throws SQLException
```

- 동작: 현재 바인딩한 데이터와 정보를 모두 제거한다. 단 batch job이 하나라도 등록되어 있으면 아무런 작업도 하지 않는다.
- 예외: 발생하지 않는다.

<a id="2fa1e238e48cbe63"></a>
#### execute

```
boolean execute() throws SQLException
```

- 동작: 현재 parameter에 바인딩 된 데이터를 기반으로 prepare된 statement를 실행한다. 실행한 statement가 select 구문이면 true를, 그렇지 않으면 false를 반환한다. 즉 true가 반환되면 이 객체로부터 ResultSet을 얻을 수 있다.
- 예외: Batch job이 등록되었거나 바인딩 된 parameter가 부족하거나 execution 할 때 서버에서 에러가 발생하면 예외가 발생할 수 있다.

<a id="19021916df17907b"></a>
#### executeQuery

```
ResultSet executeQuery() throws SQLException
```

- 동작: 현재 parameter에 바인딩 된 데이터를 기반으로 prepare된 statement를 실행하고 fetch를 수행하여 ResultSet 객체를 생성하고 반환한다.
- 예외: Batch job이 등록되었거나, 바인딩 된 parameter가 부족하거나 execution 할 때 서버에서 에러가 발생하면 예외가 발생할 수 있다.

<a id="4cf07f3b5ae28403"></a>
#### executeUpdate

```
int executeUpdate() throws SQLException
```

- 동작: 현재 parameter에 바인딩 된 데이터를 기반으로 prepare된 statement를 실행한다. 갱신된 레코드 수를 반환하는데, DDL 구문 등으로 갱신된 레코드가 없을 경우 0을 반환한다.
- 예외: Batch job이 등록되었거나, statement가 select 구문이거나, 바인딩 된 parameter가 부족하거나 서버에서 에러가 발생하면 예외가 발생할 수 있다.

<a id="426a48a8e235665b"></a>
#### getMetaData

```
ResultSetMetaData getMetaData() throws SQLException
```

- 동작: ResultSetMetaData 객체를 얻는다. Prepare된 구문이 select가 아닌 경우, 즉 ResultSet을 반환하는 구문이 아닌 경우 빈 ResultSetMetaData를 반환한다. 이 method는 execute 되기 전에 호출될 수 있다.
- 예외: 서버에서 에러가 발생하면 예외가 발생할 수 있다.

<a id="de02bec7bf743a46"></a>
#### getParameterMetaData

```
ParameterMetaData getParameterMetaData() throws SQLException
```

- 동작: ParameterMetaData 객체를 얻는다. Execute 하기 전에 호출될 수 있다. 하지만 parameter들의 정확한 타입 관련 정보는 서버에서 알 수 없기 때문에 모든 parameter는 varchar(4000)으로 가정한다.
- 예외: 서버에서 에러가 발생하면 예외가 발생할 수 있다.

<a id="893d52f950cb1899"></a>
#### setArray

```
void setArray(int parameterIndex, Array x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="6954472ec3ae60f3"></a>
#### setAsciiStream

```
void setAsciiStream(int parameterIndex, InputStream x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 InputStream 객체를 LONG VARCHAR 타입으로 바인딩한다. 바이너리 형태로 데이터를 입력하기 때문에 encoding 작업을 하지 않는다. 따라서 character set을 고려하지 않고 ascii 데이터라고 가정한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

> LONG VARCHAR로 바인딩되기 때문에 서버에서 VARCHAR로 변환 비용이 발생한다. 길이를 알 수 있으면 void setAsciiStream(int parameterIndex, InputStream x, int length)를 사용하는게 좋다.

```
void setAsciiStream(int parameterIndex, InputStream x, int length) throws SQLException
```

- 동작: 해당 parameter 인덱스에 InputStream 객체를 LONG VARCHAR 타입으로 바인딩한다. 바이너리 형태로 데이터를 입력하기 때문에 encoding 작업을 하지 않는다. 따라서 character set을 고려하지 않고 ascii 데이터라고 가정한다. 영문 데이터를 입력하거나 서버, client character set 환경이 동일할 경우 varchar에 문자열을 입력하기 위해 이 method를 사용하는 것이 setCharacterStream이나 setString보다 빠르다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

```
void setAsciiStream(int parameterIndex, InputStream x, long length) throws SQLException
```

- 동작: 해당 parameter 인덱스에 InputStream 객체를 LONG VARCHAR 타입으로 바인딩한다. 바이너리 형태로 데이터를 입력하기 때문에 encoding 작업을 하지 않는다. 따라서 character set을 고려하지 않고 ascii 데이터라고 가정한다. 영문 데이터를 입력하거나 서버, client character set 환경이 동일할 경우 varchar에 문자열을 입력하기 위해 이 method를 사용하는 것이 setCharacterStream이나 setString보다 빠르다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="b3f86b179411a88b"></a>
#### setBigDecimal

```
void setBigDecimal(int parameterIndex, BigDecimal x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 BigDecimal 객체를 NUMBER 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="f4f1c74be09b7230"></a>
#### setBinaryStream

```
void setBinaryStream(int parameterIndex, InputStream x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 InputStream 객체를 LONG VARBINARY 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

```
void setBinaryStream(int parameterIndex, InputStream x, int length) throws SQLException
```

- 동작: 해당 parameter 인덱스에 InputStream 객체를 LONG VARBINARY 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

```
void setBinaryStream(int parameterIndex, InputStream x, long length) throws SQLException
```

- 동작: 해당 parameter 인덱스에 InputStream 객체를 LONG VARBINARY 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="248b9cfd03cfc794"></a>
#### setBlob

```
void setBlob(int parameterIndex, Blob x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setBlob(int parameterIndex, InputStream inputStream) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setBlob(int parameterIndex, InputStream inputStream, long length) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="f827682d38817e52"></a>
#### setBoolean

```
void setBoolean(int parameterIndex, boolean x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 BOOLEAN 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="38310182eac78721"></a>
#### setByte

```
void setByte(int parameterIndex, byte x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 NATIVE_SMALLINT 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="c4071eb1b9035242"></a>
#### setBytes

```
void setBytes(int parameterIndex, byte[] x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 VARBINARY 또는 LONG VARBINARY 타입으로 바인딩한다. x의 길이가 4000 이하이면 VARBINARY로, 4000보다 크면 LONG VARBINARY로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="8601b14e1764bcc6"></a>
#### setCharacterStream

```
void setCharacterStream(int parameterIndex, Reader reader) throws SQLException
```

- 동작: 해당 parameter 인덱스에 reader 객체를 LONG VARCHAR 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

```
void setCharacterStream(int parameterIndex, Reader reader, int length) throws SQLException
```

- 동작: 해당 parameter 인덱스에 reader 객체를 LONG VARCHAR 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

```
void setCharacterStream(int parameterIndex, Reader reader, long length) throws SQLException
```

- 동작: 해당 parameter 인덱스에 reader 객체를 LONG VARCHAR 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="2d048b8a8cbf0b2b"></a>
#### setClob

```
void setClob(int parameterIndex, Clob x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setClob(int parameterIndex, Reader reader) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setClob(int parameterIndex, Reader reader, long length) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="45f5dcb904efc035"></a>
#### setDate

```
void setDate(int parameterIndex, Date x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 DATE 타입으로 바인딩한다. setDate(parameterIndex, x, Calendar.getInstance())로 호출하는 것과 동일하다. 즉, local timezone을 적용한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

```
void setDate(int parameterIndex, Date x, Calendar cal) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 DATE 타입으로 바인딩한다. Date x는 cal의 timezone의 시간대로 간주한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="8311ec497cdb3e80"></a>
#### setDouble

```
void setDouble(int parameterIndex, double x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 NATIVE_DOUBLE 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="395c20d31f48eaed"></a>
#### setFloat

```
void setFloat(int parameterIndex, float x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 NATIVE_REAL 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="99f1fb53fc0f0c96"></a>
#### setInt

```
void setInt(int parameterIndex, int x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 NATIVE_INTEGER 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="a3c6c3aee89f55ca"></a>
#### setLong

```
void setLong(int parameterIndex, long x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 NATIVE_BIGINT 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="c6b49e998a4d6e71"></a>
#### setNCharacterStream

```
void setNCharacterStream(int parameterIndex, Reader value) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setNCharacterStream(int parameterIndex, Reader value, long length) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="64f901d31003afcb"></a>
#### setNClob

```
void setNClob(int parameterIndex, NClob value) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setNClob(int parameterIndex, Reader reader) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
void setNClob(int parameterIndex, Reader reader, long length) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="6c80c43cf9339d2a"></a>
#### setNString

```
void setNString(int parameterIndex, String value) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="dbaabfba920b6813"></a>
#### setNull

```
void setNull(int parameterIndex, int sqlType) throws SQLException
```

- 동작: 해당 parameter 인덱스에 null을 sqlType에 해당하는 GOLDILOCKS 타입으로 바인딩한다. sqlType에 매핑되는 GOLDILOCKS 타입은 [SQL 타입 → GOLDILOCKS 타입](#e234a5c29f761940)을 참조한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

```
void setNull(int parameterIndex, int sqlType, String typeName) throws SQLException
```

- 동작: 해당 parameter 인덱스에 null을 sqlType에 해당하는 GOLDILOCKS 타입으로 바인딩한다. sqlType에 매핑되는 GOLDILOCKS 타입은 [SQL 타입 → GOLDILOCKS 타입](#e234a5c29f761940)을 참조한다. REF나 사용자 타입은 지원하지 않기 때문에 세 번째 인자인 typeName은 무시된다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="072973daca96ef5c"></a>
#### setObject

```
void setObject(int parameterIndex, Object x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 매핑되는 해당 GOLDILOCKS 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

**Java 객체 → GOLDILOCKS 타입**

<a id="ccfa76b095a87789"></a>
| Java 클래스 | GOLDILOCKS 타입 |
| --- | --- |
| null | VARCHAR |
| Boolean | BOOLEAN |
| Byte | NATIVE_SMALLINT |
| Short | NATIVE_SMALLINT |
| Integer | NATIVE_INTEGER |
| Long | NATIVE_BIGINT |
| Float | NATIVE_REAL |
| Double | NATIVE_DOUBLE |
| BigInteger | NATIVE_BIGINT |
| BigDecimal | NUMBER |
| String | VARCHAR or LONG VARCHAR |
| byte[] | VARBINARY or LONG VARBINARY |
| Date | DATE |
| Time | TIME |
| Timestamp | TIMESTAMP |
| Blob | N/A |
| Clob | N/A |
| InputStream | LONG VARBINARY |
| Reader | LONG VARCHAR |
| GoldilocksInterval | 해당 INTERVAL 타입 |
| RowId | ROWID |
| 그 외 | N/A |

```
void setObject(int parameterIndex, Object x, int targetSqlType) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 targetSqlType에 해당하는 GOLDILOCKS 타입으로 바인딩한다. targetSqlType에 매핑되는 GOLDILOCKS 타입은 [SQL 타입 → GOLDILOCKS 타입](#e234a5c29f761940)을 참조한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

```
void setObject(int parameterIndex, Object x, int targetSqlType, int scaleOrLength) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 targetSqlType에 해당하는 GOLDILOCKS 타입으로 바인딩한다. targetSqlType에 매핑되는 GOLDILOCKS 타입은 [SQL 타입 → GOLDILOCKS 타입](#e234a5c29f761940)을 참조한다. x가 InputStream이나 reader인 경우 scaleOrLength는 데이터 길이를 나타낸다. 다른 타입에 대해서는 이 값이 무시된다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="d64fa8be253fadfd"></a>
#### setRef

```
void setRef(int parameterIndex, Ref x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="cf30f42fb794f243"></a>
#### setRowId

```
void setRowId(int parameterIndex, RowId x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 ROWID 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="a061c93fc9765e5d"></a>
#### setShort

```
void setShort(int parameterIndex, short x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 NATIVE_SMALLINT 타입으로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="923542d7f1b66b69"></a>
#### setSQLXML

```
void setSQLXML(int parameterIndex, SQLXML xmlObject) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="229bdcd45f09de2c"></a>
#### setString

```
void setString(int parameterIndex, String x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 VARCHAR 또는 LONG VARCHAR 타입으로 바인딩한다. x의 길이가 4000 이하이면 VARCHAR로, 그보다 크면 LONG VARCHAR로 바인딩한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="b3b6ce842a660b98"></a>
#### setTime

```
void setTime(int parameterIndex, Time x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 TIME 타입으로 바인딩한다. setTime(parameterIndex, x, Calendar.getInstance())로 호출하는 것과 동일하다. 즉, local timezone을 적용한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

```
void setTime(int parameterIndex, Time x, Calendar cal) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 TIME 타입으로 바인딩한다. Time x는 cal의 timezone의 시간대로 간주한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="7224eb1c17e5ff18"></a>
#### setTimestamp

```
void setTimestamp(int parameterIndex, Timestamp x) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 TIME 타입으로 바인딩한다. setTimestamp(parameterIndex, x, Calendar.getInstance())로 호출하는 것과 동일하다. 즉, local timezone을 적용한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

```
void setTimestamp(int parameterIndex, Timestamp x, Calendar cal) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 TIMESTAMP 타입으로 바인딩한다. Timestamp x는 cal의 timezone의 시간대로 간주한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

<a id="b4c2342408df1e38"></a>
#### setUnicodeStream

```
void setUnicodeStream(int parameterIndex, InputStream x, int length) throws SQLException
```

- 동작: 구현되어 있지 않다. (Deprecated된 method이다)
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="5b17dc99c7e8d87c"></a>
#### setURL

```
void setURL(int parameterIndex, URL x) throws SQLException
```

- 동작: 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="f08c6fcc9695b3d8"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- 동작: 이 객체가 iface 인터페이스를 구현한 클래스인지 여부를 묻는다. 맞으면 true를, 그렇지 않으면 false를 반환한다. GOLDILOCKS PreparedStatement 객체는 다른 클래스의 wrapper가 아니므로 wrapper의 유무는 판단하지 않고 오직 주어진 인자 클래스 타입을 구현했는지 여부만 묻는다.
- 예외: 발생하지 않는다.

<a id="b9bcb7e4f993ab98"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- 동작: GOLDILOCKS PreparedStatement는 다른 클래스의 wrapper가 아니므로 unwrap 하더라도 결국 자기 자신을 반환한다. 해당 타입으로 캐스팅한 후에 반환한다. iface가 isWrapperFor() method의 인자로 주어졌을 때 false를 반환하는 값이라면 이 method는 예외를 발생시킨다.
- 예외: iface가 이 객체의 타입이 아닌 경우 (이 객체가 implements 하지 않은 타입을 준 경우) SQLException이 발생한다.

<a id="4c90b1b3ecff776c"></a>
#### executeBatchAtomic

```
boolean executeBatchAtomic() throws SQLException
```

- 동작: executeBatch()와 같지만 atomic하게 수행된다. 즉 batch job이 모두 성공하거나 모두 실패하거나 둘 중 하나이다. executeBatch()보다 빠르게 수행된다. 수행한 구문이 select 구문이면 true를, 그렇지 않으면 false를 반환한다.
- 예외: Batch job이 등록되지 않았거나 서버에서 에러가 발생하면 SQLException이 발생한다.

> GOLDILOCKS JDBC의 고유한 기능으로써 PreparedStatement 객체를 GoldilocksPreparedStatement로 캐스팅 한 후에 사용할 수 있다.  
> 예: ((GoldilocksPreparedStatement)pstmt).executeBatchAtomic();

<a id="3f3067d1b8c5bd6c"></a>
#### setTimeTimeZone

```
void setTimeTimeZone(int parameterIndex, Time x, Calendar cal) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 TIME WITH TIME ZONE 타입으로 바인딩한다. Time x는 cal의 timezone의 시간대로 간주한다. 데이터베이스 column의 timezone 정보는 cal의 timezone을 참조한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

> GOLDILOCKS JDBC의 고유한 기능으로써 PreparedStatement 객체를 GoldilocksPreparedStatement로 캐스팅한 후에 사용할 수 있다.  
> 예: ((GoldilocksPreparedStatement)pstmt).setTimeTimeZone(1, aTime, aCalendar);

<a id="fedba2580ddc3692"></a>
#### setTimestampTimeZone

```
void setTimestampTimeZone(int parameterIndex, Timestamp x, Calendar cal) throws SQLException
```

- 동작: 해당 parameter 인덱스에 데이터 x를 TIMESTAMP WITH TIME ZONE 타입으로 바인딩한다. Timestamp x는 cal의 timezone의 시간대로 간주한다. 데이터베이스 column의 timezone 정보는 cal의 timezone을 참조한다.
- 예외: parameterIndex가 0보다 작거나 parameter 개수보다 클 경우에 예외가 발생한다.

> GOLDILOCKS JDBC의 고유한 기능으로써 PreparedStatement 객체를 GoldilocksPreparedStatement로 캐스팅 한 후에 사용할 수 있다.  
> 예: ((GoldilocksPreparedStatement)pstmt).setTimestampTimeZone(1, aTimestamp, aCalendar);

<a id="5eac45c6ae725c38"></a>
### Ref

클래스가 구현되지 않았다.

<a id="1bf04890815ceb2e"></a>
#### getBaseTypeName

```
String getBaseTypeName() throws SQLException
```

<a id="a1a274a96c0adaf2"></a>
#### getObject

```
Object getObject() throws SQLException
```

```
Object getObject(Map<String,Class<?>> map) throws SQLException
```

<a id="fcfa9ba7c905daa2"></a>
#### setObject

```
void setObject(Object value) throws SQLException
```

<a id="a7780716ff8d3822"></a>
### ResultSet

<a id="8a8bd0f5afc07fe7"></a>
#### absolute

```
boolean absolute(int row) throws SQLException
```

- 동작: Fetch한 row 커서 위치를 row 번째에 둔다. 첫 번째 row는 1이다. 0은 before first를 가리킨다. 음수이면 마지막 row부터 가리킨다. 즉 -1은 마지막 row, -2는 마지막에서 두 번째 row를 가리킨다. Fetch한 row 캐시 내에 커서를 위치시킬 수 있으면 캐시 내의 위치 정보만 바꾸고, 캐시 내에 위치시킬 수 없으면 서버로부터 다시 fetch 해온다. Row가 범위를 벗어나면 before first 또는 after last에 커서를 위치시키고 false를 반환한다. 그 외의 경우에는 해당 row에 위치시키고 true를 반환한다.
- 예외: ResultSet이 close되었거나 ResultSet 타입이 ResultSet.TYPE_FORWARD_ONLY이거나 fetch 할 때 서버로부터 에러가 발생하면 예외가 발생한다.

> 캐시 내에 없어서 다시 fetch 해와야 할 때, row가 현재 위치보다 뒤쪽이면, next()에 유리하도록 row 위치부터 n (fetch 할 때 서버로부터 가져오는 row 개수)개를 서버로부터 fetch해오고, row가 현재 위치보다 앞쪽이면, previous()에 유리하도록 (row-n+1) 위치부터 n개를 fetch해온다.

<a id="74be73692c113c26"></a>
#### afterLast

```
void afterLast() throws SQLException
```

- 동작: Row 커서를 after last에 위치시킨다. Row 캐시가 마지막 row set (전체 result set의 부분을 가리키는 용어)이면 커서 위치만 변경하고 그렇지 않으면 마지막 row set (전체 row 개수-n+1 부터 n개의 row, n은 fetch 할 때 서버로부터 가져오는 row 개수)을 fetch해 온 후에 커서를 after last에 위치시킨다.
- 예외: ResultSet이 close되었거나 ResultSet 타입이 ResultSet.TYPE_FORWARD_ONLY이거나 fetch 할 때 서버로부터 에러가 발생하면 예외가 발생한다.

<a id="446ba58b04d0e87d"></a>
#### beforeFirst

```
void beforeFirst() throws SQLException
```

- 동작: Row 커서를 before first에 위치시킨다. Row 캐시가 첫 번째 row set (전체 result set의 부분을 가리키는 용어)이면 커서 위치만 변경하고 그렇지 않으면 첫 번째 row set (1부터 n개의 row, n은 fetch 할 때 서버로부터 가져오는 row 개수)을 fetch해 온 후에 커서를 before first에 위치시킨다.
- 예외: ResultSet이 close되었거나 ResultSet 타입이 ResultSet.TYPE_FORWARD_ONLY이거나 fetch 할 때 서버로부터 에러가 발생하면 예외가 발생한다.

<a id="03c1d692f78c1a1e"></a>
#### cancelRowUpdates

```
void cancelRowUpdates() throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우에는 동작을 참조한다.

<a id="315ebf3a258ebc55"></a>
#### clearWarnings

```
void clearWarnings() throws SQLException
```

- 동작: ResultSet 객체가 가지고 있는 SQLWarning 객체들을 모두 제거한다.
- 예외: 발생하지 않는다.

<a id="7b5a651f95945cae"></a>
#### close

```
void close() throws SQLException
```

- 동작: 서버에 해당 커서가 열려 있으면 이를 닫게 하고 (이미 서버에 커서가 닫혀 있으면 이 작업을 수행하지 않는다. 즉, 프로토콜 전송이 일어나지 않는다.), 현재 ResultSet 객체의 상태를 closed로 변경한다. 이미 닫혀 있는 상태일 경우, 아무런 동작을 하지 않는다.
- 예외: 서버에서 에러가 발생하면 SQLException이 발생한다.

<a id="14d843daf47757c7"></a>
#### deleteRow

```
void deleteRow() throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있을 경우, SQLException이 발생한다. 그 외의 경우에는 동작을 참조한다.

<a id="5d70520306f51e63"></a>
#### findColumn

```
int findColumn(String columnLabel) throws SQLException
```

- 동작: 해당 column 이름의 인덱스를 반환한다. 첫 번째 column의 인덱스는 1이다.
- 예외: 이미 close되었거나 해당 이름의 column을 찾지 못하면 SQLException이 발생한다.

<a id="49228da437a05cac"></a>
#### first

```
boolean first() throws SQLException
```

- 동작: Row 커서를 first (첫 번째 row)에 위치시킨다. Row 캐시가 첫 번째 row set (전체 result set의 부분을 가리키는 용어)이면 커서 위치만 변경하고 그렇지 않으면 첫 번째 row set (1부터 n개의 row, n은 fetch 할 때 서버로부터 가져오는 row 개수)을 fetch해 온 후 커서를 first에 위치시킨다. 해당 row가 있으면 true를, 없으면 false를 반환한다.
- 예외: ResultSet이 close되었거나 ResultSet 타입이 ResultSet.TYPE_FORWARD_ONLY이거나 fetch 할 때 서버로부터 에러가 발생하면 예외가 발생한다.

<a id="384600ec18d433be"></a>
#### getArray

```
Array getArray(int columnIndex) throws SQLException
```

- 동작: Array 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
Array getArray(String columnLabel) throws SQLException
```

- 동작: Array 타입은 지원하지 않는다. GOLDILOCKS 타입 별 지원 여부 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="035a0f7cd471cda8"></a>
#### getAsciiStream

```
InputStream getAsciiStream(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 InputStream 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 InputStream으로 변환할 수 없을 경우, SQLException이 발생한다.

```
InputStream getAsciiStream(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 InputStream 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 InputStream으로 변환할 수 없을 경우, SQLException이 발생한다.

<a id="c2a5ea81d235f57f"></a>
#### getBigDecimal

```
BigDecimal getBigDecimal(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 BigDecimal 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 BigDecimal로 변환할 수 없을 경우, SQLException이 발생한다.

```
BigDecimal getBigDecimal(int columnIndex, int scale) throws SQLException
```

- 동작: Deprecated된 method이다. getBigDecimal(int columnIndex)과 동일하게 동작한다. Scale은 무시된다.
- 예외: [getBigDecimal](#ede23d0cd0691de4)(int columnIndex)을 참조한다.

```
BigDecimal getBigDecimal(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 BigDecimal 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 BigDecimal로 변환할 수 없을 경우, SQLException이 발생한다.

```
BigDecimal getBigDecimal(String columnLabel, int scale) throws SQLException
```

- 동작: Deprecated된 method이다. getBigDecimal(String columnLabel)과 동일하게 동작한다. Scale은 무시된다.
- 예외: [getBigDecimal](#ede23d0cd0691de4)(String columnLabel)을 참조한다.

<a id="d91c114ee38a5215"></a>
#### getBinaryStream

```
InputStream getBinaryStream(int columnIndex) throws SQLException
```

- 동작: getAsciiStream(int columnIndex)과 같다.
- 예외: [getAsciiStream](#760f6ec91133ca8e)(int columnIndex)을 참조한다.

```
InputStream getBinaryStream(String columnLabel) throws SQLException
```

- 동작: getAsciiStream(String columnLabel)과 같다.
- 예외 [getAsciiStream](#760f6ec91133ca8e)(String columnLabel)을 참조한다.

<a id="7e4bc72a8526772a"></a>
#### getBlob

```
Blob getBlob(int columnIndex) throws SQLException
```

- 동작: Blob 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
Blob getBlob(String columnLabel) throws SQLException
```

- 동작: Blob 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="81314c64d10b5745"></a>
#### getBoolean

```
boolean getBoolean(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 boolean 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 boolean으로 변환할 수 없을 경우, SQLException이 발생한다.

```
boolean getBoolean(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 boolean 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 boolean으로 변환할 수 없을 경우, SQLException이 발생한다.

<a id="e77c819153a1dbeb"></a>
#### getByte

```
byte getByte(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 byte 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548) 를 참조한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 byte로 변환할 수 없을 경우, SQLException이 발생한다.

```
byte getByte(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 byte 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 byte로 변환할 수 없을 경우, SQLException이 발생한다.

<a id="8c7bc0eec2e3c133"></a>
#### getBytes

```
byte[] getBytes(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 byte[] 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났을 경우 SQLException이 발생한다.

> 모든 GOLDILOCKS 데이터 타입에 대해 getBytes를 하면 데이터베이스에 저장된 바이너리 형태를 얻는다.

```
byte[] getBytes(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 byte[] 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없을 경우 SQLException이 발생한다.

> 모든 GOLDILOCKS 데이터 타입에 대해 getBytes를 하면 데이터베이스에 저장된 바이너리 형태를 얻는다.

<a id="da672c7b1fdf39ff"></a>
#### getCharacterStream

```
Reader getCharacterStream(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 reader 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 reader로 변환할 수 없을 경우, SQLException이 발생한다.

```
Reader getCharacterStream(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 reader 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 reader로 변환할 수 없을 경우, SQLException이 발생한다.

<a id="7b6fae63ec8aae02"></a>
#### getClob

```
Clob getClob(int columnIndex) throws SQLException
```

- 동작: Clob 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
Clob getClob(String columnLabel) throws SQLException
```

- 동작: Clob 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="6b6cb7f18c2b1d2b"></a>
#### getConcurrency

```
int getConcurrency() throws SQLException
```

- 동작: 현재 ResultSet 객체의 concurrency를 반환한다. 현재 ResultSet.CONCUR_READ_ONLY만 지원한다.
- 예외: 발생하지 않는다.

<a id="eca20ff1fd7dd13c"></a>
#### getCursorName

```
String getCursorName() throws SQLException
```

- 동작: 이 ResultSet이 가리키는 서버의 커서 이름을 얻어온다. 서버와 통신이 발생한다.
- 예외: ResultSet이 이미 close되었거나 서버에서 에러가 발생할 경우, SQLException이 발생한다.

<a id="d8cceb86805112da"></a>
#### getDate

```
Date getDate(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 date 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Date 객체를 만들 때 local timezone을 사용한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 date로 변환할 수 없을 경우, SQLException이 발생한다.

```
Date getDate(int columnIndex, Calendar cal) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 date 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Date 객체를 만들 때 cal의 timezone을 사용한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 date로 변환할 수 없을 경우, SQLException이 발생한다.

```
Date getDate(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 date 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Date 객체를 만들 때 local timezone을 사용한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 date로 변환할 수 없을 경우, SQLException이 발생한다.

```
Date getDate(String columnLabel, Calendar cal) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 date 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Date 객체를 만들 때 cal의 timezone을 사용한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 date로 변환할 수 없을 경우, SQLException이 발생한다.

<a id="ca339c9a02a0848a"></a>
#### getDouble

```
double getDouble(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 double 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 double로 변환할 수 없을 경우, SQLException이 발생한다.

```
double getDouble(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 double 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 double로 변환할 수 없을 경우, SQLException이 발생한다.

<a id="6bf56a70d0dda1c8"></a>
#### getFetchDirection

```
int getFetchDirection() throws SQLException
```

- 동작: 항상 ResultSet.FETCH_FORWARD만 반환한다. Backward fetch는 지원하지 않는다.
- 예외: ResultSet이 이미 close되었으면 SQLException이 발생한다.

<a id="94ede4ff4828fc6c"></a>
#### getFetchSize

```
int getFetchSize() throws SQLException
```

- 동작: 한 번 fetch 할 때 서버로부터 가져오는 row 개수를 얻어온다. 0일 경우 한 번 전송할 때 통신 패킷에 담을 수 있는 최대 row 개수를 자동으로 계산한다. 기본값은 0이다.
- 예외: ResultSet이 이미 close되었으면 SQLException이 발생한다.

<a id="f35852adc6f0ef7a"></a>
#### getFloat

```
float getFloat(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 float 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 float으로 변환할 수 없을 경우 SQLException이 발생한다.

```
float getFloat(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 float 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 float으로 변환할 수 없을 경우 SQLException이 발생한다.

<a id="53427f2d29bc7848"></a>
#### getHoldability

```
int getHoldability() throws SQLException
```

- 동작: 현재 ResultSet의 holdability를 반환한다. 이 값은 ResultSet 객체가 생성될 때 정해지며 도중에 변경할 수는 없다. 기본값은 ResultSet.HOLD_CURSOR_OVER_COMMIT이다.
- 예외: ResultSet이 이미 close되었으면 SQLException이 발생한다.

<a id="f756fadca24749fe"></a>
#### getInt

```
int getInt(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 int 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 int로 변환할 수 없을 경우 SQLException이 발생한다.

```
int getInt(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 int 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 int로 변환할 수 없을 경우 SQLException이 발생한다.

<a id="ab31684dfe6b28d5"></a>
#### getLong

```
long getLong(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 long 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close 되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 long으로 변환할 수 없을 경우 SQLException이 발생한다.

```
long getLong(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 long 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 long으로 변환할 수 없을 경우 SQLException이 발생한다.

<a id="c1ef955210b68139"></a>
#### getMetaData

```
ResultSetMetaData getMetaData() throws SQLException
```

- 동작: Column의 상세 정보를 얻을 수 있는 ResultSetMetaData 객체를 생성하고 반환한다.
- 예외: ResultSet이 이미 close되었거나 서버로부터 column 상세 정보를 가져오는 동안 에러가 발생하면 SQLException이 발생한다.

<a id="b648b954a38b2a3b"></a>
#### getNCharacterStream

```
Reader getNCharacterStream(int columnIndex) throws SQLException
```

- 동작: NCHAR 계열 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
Reader getNCharacterStream(String columnLabel) throws SQLException
```

- 동작: NCHAR 계열 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="b750b0dcbdd1ecfa"></a>
#### getNClob

```
NClob getNClob(int columnIndex) throws SQLException
```

- 동작: NCHAR 계열 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
NClob getNClob(String columnLabel) throws SQLException
```

- 동작: NCHAR 계열 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="26477a2cac362fe7"></a>
#### getNString

```
String getNString(int columnIndex) throws SQLException
```

- 동작: NCHAR 계열 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
String getNString(String columnLabel) throws SQLException
```

- 동작: NCHAR 계열 타입은 현재 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="4a6741b5078570c5"></a>
#### getObject

```
Object getObject(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 가장 적합한 Java 객체 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났을 경우, SQLException이 발생한다.

```
Object getObject(int columnIndex, Map<String,Class<?>> map) throws SQLException
```

- 동작: 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
Object getObject(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 가장 적합한 Java 객체 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없을 경우, SQLException이 발생한다.

```
Object getObject(String columnLabel, Map<String,Class<?>> map) throws SQLException
```

- 동작: 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="ffc9410a41eb92d2"></a>
#### getRef

```
Ref getRef(int columnIndex) throws SQLException
```

- 동작: REF 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
Ref getRef(String columnLabel) throws SQLException
```

- 동작: REF 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="037f9abbe9b9f7d4"></a>
#### getRow

```
int getRow() throws SQLException
```

- 동작: 현재 ResultSet 객체의 커서 위치를 반환한다. 첫 번째 row는 1이다. Before first인 경우 0을 반환한다.
- 예외: ResultSet이 이미 close되었으면 SQLException이 발생한다.

<a id="60bb41cda019fd7a"></a>
#### getRowId

```
RowId getRowId(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 RowId 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 RowId로 변환할 수 없을 경우, SQLException이 발생한다.

```
RowId getRowId(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 RowId 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 RowId로 변환할 수 없을 경우, SQLException이 발생한다.

<a id="ce40e59bf0d8cfda"></a>
#### getShort

```
short getShort(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 short 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 short로 변환할 수 없을 경우, SQLException이 발생한다.

```
short getShort(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 short 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 short로 변환할 수 없을 경우, SQLException이 발생한다.

<a id="0d1d0ae50417bca6"></a>
#### getSQLXML

```
SQLXML getSQLXML(int columnIndex) throws SQLException
```

- 동작: SQLXML 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
SQLXML getSQLXML(String columnLabel) throws SQLException
```

- 동작: SQLXML 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="e660eb90ec95970b"></a>
#### getStatement

```
Statement getStatement() throws SQLException
```

- 동작: 이 ResultSet 객체를 생성한 statement 객체를 반환한다.
- 예외: ResultSet이 이미 close되었으면 SQLException이 발생한다.

<a id="1835cb103e596794"></a>
#### getString

```
String getString(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 string 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. BINARY, VARBINARY, LONG VARBINARY에 대해 getString()을 하면 hex code의 문자열을 반환받는다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났을 경우, SQLException이 발생한다.

```
String getString(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 string 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. BINARY, VARBINARY, LONG VARBINARY에 대해 getString()을 하면 hex code의 문자열을 반환받는다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없을 경우, SQLException이 발생한다.

<a id="a315d626a17e1818"></a>
#### getTime

```
Time getTime(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 time 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Time 객체를 만들 때는 local timezone을 사용한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 time으로 변환할 수 없을 경우, SQLException이 발생한다.

```
Time getTime(int columnIndex, Calendar cal) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 time 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Time 객체를 만들 때 cal의 timezone을 사용한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 time으로 변환할 수 없을 경우, SQLException이 발생한다.

```
Time getTime(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 time 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Time 객체를 만들 때 local timezone을 사용한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 time으로 변환할 수 없을 경우 SQLException이 발생한다.

```
Time getTime(String columnLabel, Calendar cal) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 time 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Time 객체를 만들 때 local timezone을 사용한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 time으로 변환할 수 없을 경우 SQLException이 발생한다.

<a id="8a0dcd62e2ac8e01"></a>
#### getTimestamp

```
Timestamp getTimestamp(int columnIndex) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 timestamp 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Timestamp 객체를 만들 때 local timezone을 사용한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 timestamp로 변환할 수 없을 경우, SQLException이 발생한다.

```
Timestamp getTimestamp(int columnIndex, Calendar cal) throws SQLException
```

- 동작: columnIndex 번째 column의 데이터를 timestamp 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Timestamp 객체를 만들 때, cal의 timezone을 사용한다.
- 예외: ResultSet이 이미 close되었거나 columnIndex가 범위를 벗어났거나 해당 타입을 timestamp로 변환할 수 없을 경우, SQLException이 발생한다.

```
Timestamp getTimestamp(String columnLabel) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 timestamp 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Timestamp 객체를 만들 때 local timezone을 사용한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 timestamp로 변환할 수 없을 경우, SQLException이 발생한다.

```
Timestamp getTimestamp(String columnLabel, Calendar cal) throws SQLException
```

- 동작: 이름이 columnLabel인 column의 데이터를 timestamp 타입으로 얻는다. GOLDILOCKS 타입 별 지원 여부는 [GOLDILOCKS 타입에 대한 getter method 지원 여부-1](#26907a2b935b9548)를 참조한다. Timestamp 객체를 만들 때, cal의 timezone을 사용한다.
- 예외: ResultSet이 이미 close되었거나 해당 columnLabel을 찾을 수 없거나 해당 타입을 timestamp로 변환할 수 없을 경우, SQLException이 발생한다.

<a id="9633099203f9d053"></a>
#### getType

```
int getType() throws SQLException
```

- 동작: 현재 ResultSet 타입을 반환한다. ResultSet.TYPE_FORWARD_ONLY, ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.TYPE_SCROLL_SENSITIVE 중의 하나를 반환한다.
- 예외: ResultSet이 이미 close되어 있으면 SQLException이 발생한다.

<a id="28587e0735dcad08"></a>
#### getUnicodeStream

```
InputStream getUnicodeStream(int columnIndex) throws SQLException
```

- 동작: Deprecated 된 method이다. 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

```
InputStream getUnicodeStream(String columnLabel) throws SQLException
```

- 동작: Deprecated 된 method이다. 구현되어 있지 않다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="e356cbdb894878ff"></a>
#### getURL

```
URL getURL(int columnIndex) throws SQLException
```

- 동작: URL 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

```
URL getURL(String columnLabel) throws SQLException
```

- 동작: URL 타입은 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="ba69ca5f60c49520"></a>
#### getWarnings

```
SQLWarning getWarnings() throws SQLException
```

- 동작: 현재까지 이 객체에 축적된 SQLWarning 목록을 반환한다. 서버로부터 경고를 전달받으면 SQLWarning을 생성하는데 clearWarning하지 않을 경우 계속 누적된다. 없을 경우, null이 반환된다.
- 예외: 발생하지 않는다.

<a id="d97bda2b264d2779"></a>
#### insertRow

```
void insertRow() throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우에는 동작을 참조한다.

<a id="843c9c34b0a93e21"></a>
#### isAfterLast

```
boolean isAfterLast() throws SQLException
```

- 동작: 현재 커서 위치가 after last인지 묻는다. 맞으면 true를, 그렇지 않으면 false를 반환한다.
- 예외: ResultSet이 이미 close되어 있으면 SQLException이 발생한다.

<a id="9b3511f533f9d61a"></a>
#### isBeforeFirst

```
boolean isBeforeFirst() throws SQLException
```

- 동작: 현재 커서 위치가 before first인지 묻는다. 맞으면 true를, 그렇지 않으면 false를 반환한다.
- 예외: ResultSet이 이미 close되어 있으면 SQLException이 발생한다.

<a id="31fee6a30d67a08c"></a>
#### isClosed

```
boolean isClosed() throws SQLException
```

- 동작: 현재 ResultSet이 close되었는지 묻는다. Close되었으면 true를, 그렇지 않으면 false를 반환한다. 사용자가 close를 호출하지 않았더라도 서버의 커서가 close되어 ResultSet이 close될 수 있다. 예를 들어 ResultSet을 생성한 statement가 close 되거나 holdability가 ResultSet.CLOSE_CURSOR_AT_COMMIT 모드일 때 트랜잭션이 commit 되거나, fetch 도중에 서버로부터 에러를 반환받을 때 등이다.
- 예외: 발생하지 않는다.

<a id="fd454b6df56835cf"></a>
#### isFirst

```
boolean isFirst() throws SQLException
```

- 동작: 현재 커서 위치가 first (첫 번째 row)인지 여부를 묻는다. 맞으면 true를, 그렇지 않으면 false를 반환한다.
- 예외: ResultSet이 이미 close되어 있으면 SQLException이 발생한다.

<a id="35bf4e3274b737c3"></a>
#### isLast

```
boolean isLast() throws SQLException
```

- 동작: 현재 커서 위치가 last (마지막 row)인지 여부를 묻는다. 맞으면 true를, 그렇지 않으면 false를 반환한다.
- 예외: ResultSet이 이미 close되어 있으면 SQLException이 발생한다.

<a id="16a60c8ea2339da1"></a>
#### last

```
boolean last() throws SQLException
```

- 동작: Row 커서를 last (마지막 row)에 위치시킨다. Row 캐시가 마지막 row set (전체 result set의 일부)이면 커서 위치만 변경하고 그렇지 않으면 마지막 row set (last-n+1부터 last의 row, n은 fetch 할 때 서버로부터 가져오는 row 개수)을 fetch해 온 후 커서를 last에 위치시킨다. 해당 row가 있으면 true를, 없으면 false를 반환한다.
- 예외: ResultSet이 close되었거나 ResultSet 타입이 ResultSet.TYPE_FORWARD_ONLY이거나 fetch 할 때 서버로부터 에러가 발생하면 예외가 발생한다.

<a id="388039aecb059b1a"></a>
#### moveToCurrentRow

```
void moveToCurrentRow() throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="74fab57cec5f4940"></a>
#### moveToInsertRow

```
void moveToInsertRow() throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="33058126b086e1bc"></a>
#### next

```
boolean next() throws SQLException
```

- 동작: Row 커서를 현재 row 다음에 위치시킨다. 현재 row가 row 캐시의 마지막 row이면 서버로부터 다음 row 캐시를 가져온다. 해당 row가 있으면 true를, 없으면 false를 반환한다.
- 예외: ResultSet이 close되었거나 fetch 할 때 서버로부터 에러가 발생하면 예외가 발생한다.

<a id="663c58e6556d8eda"></a>
#### previous

```
boolean previous() throws SQLException
```

- 동작: Row 커서를 현재 위치 이전 row에 위치시킨다. 현재 row가 row 캐시의 첫 번째 row이면 서버로부터 이전 row 캐시 (x-n부터 x-1까지 n개의 row, x는 현재 row 인덱스)를 가져온다. 해당 row가 있으면 true를, 없으면 false를 반환한다.
- 예외: ResultSet이 close되었거나 ResultSet 타입이 ResultSet.TYPE_FORWARD_ONLY이거나 fetch 할 때 서버로부터 에러가 발생하면 예외가 발생한다.

<a id="140d93edccc09f93"></a>
#### refreshRow

```
void refreshRow() throws SQLException
```

- 동작: ResultSet 타입이 ResultSet.SCROLL_SENSITIVE일 경우, 서버로부터 현재 row 캐시를 다시 가져온다. 그동안 (동일 트랜잭션에 의해서든, 타 트랜잭션에 의해서든) row에 갱신된 것이 있으면 반영된다. ResultSet 타입이 ResultSet.Scroll_INSENSITIVE일 경우 아무런 작업을 하지 않는다.
- 예외: ResultSet이 close되었거나 ResultSet 타입이 ResultSet.TYPE_FORWARD_ONLY이거나 fetch 할 때 서버로부터 에러가 발생하면 예외가 발생한다.

<a id="9998556abc5fb71c"></a>
#### relative

```
boolean relative(int rows) throws SQLException
```

- 동작: Row 커서를 현재 위치로부터 rows 만큼 떨어진 곳으로 이동시킨다. 현재 row 캐시 내에서 이동할 수 있으면 커서 위치만 변경시키고, 그렇지 않으면 서버로부터 해당 row 캐시를 fetch해온 후 커서를 위치시킨다. 이 때 이동할 위치가 현재 위치보다 뒤쪽이면 (next 방향이면) (next에 유리하도록) row 캐시를 rows부터 rows+n-1까지 fetch하고, 현재 위치보다 앞쪽이면 (previous 방향이면) (previous에 유리하도록) row 캐시를 rows-n+1부터 rows까지 fetch한다.
- 예외: ResultSet이 close되었거나 ResultSet 타입이 ResultSet.TYPE_FORWARD_ONLY이거나 fetch 할 때 서버로부터 에러가 발생하면 예외가 발생한다.

<a id="92a17504049af1fe"></a>
#### rowDeleted

```
boolean rowDeleted() throws SQLException
```

- 동작: 현재 커서 위치의 row가 (동일 트랜잭션에 의해서든, 타 트랜잭션에 의해서든) delete 되었는지 여부를 묻는다. Delete 되었으면 true를, 그렇지 않으면 false를 반환한다.
- 예외: ResultSet이 close되었거나 ResultSet 타입이 ResultSet.TYPE_FORWARD_ONLY이면 예외가 발생한다.

<a id="7ec474e53fc3973f"></a>
#### rowInserted

```
boolean rowInserted() throws SQLException
```

- 동작: 현재 커서 위치의 row가 (동일 트랜잭션에 의해서든, 타 트랜잭션에 의해서든) insert 되었는지 여부를 묻는다. Insert되었으면 true를, 그렇지 않으면 false를 반환한다.
- 예외: ResultSet이 close되었거나 ResultSet 타입이 ResultSet.TYPE_FORWARD_ONLY이면 예외가 발생한다.

<a id="f8a55debe92df40f"></a>
#### rowUpdated

```
boolean rowUpdated() throws SQLException
```

- 동작: 현재 커서 위치의 row가 (동일 트랜잭션에 의해서든, 타 트랜잭션에 의해서든) update 되었는지 여부를 묻는다. Update되었으면 true를, 그렇지 않으면 false를 반환한다.
- 예외: ResultSet이 close되었거나 ResultSet 타입이 ResultSet.TYPE_FORWARD_ONLY이면 예외가 발생한다.

<a id="4e917dd81effe818"></a>
#### setFetchDirection

```
void setFetchDirection(int direction) throws SQLException
```

- 동작: 서버가 backward fetch를 지원하지 않는다. 따라서 ResultSet.FETCH_FORWARD만 가능하다. 다른 값이 입력되면 SQLWarning을 생성한다.
- 예외: ResultSet이 이미 close되었거나 정의된 값이 아닌 다른 값이 인자로 입력되었을 경우 예외가 발생한다.

<a id="c718213f779b973f"></a>
#### setFetchSize

```
void setFetchSize(int rows) throws SQLException
```

- 동작: 서버로부터 한 번에 fetch 할 row 개수를 지정한다. 0이면 서버가 자동으로 결정한다. 0일 경우 forward only 커서에 대해서는 한 번의 통신 패킷에 담을 수 있는 row 개수로 정하고, scrollable 커서일 경우 100개로 정한다.
- 예외: ResultSet이 이미 close되었으면 예외가 발생한다.

<a id="b6ad1b11e36d7aa1"></a>
#### updateArray

```
void updateArray(int columnIndex, Array x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateArray(String columnLabel, Array x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="01d2a62e2b7b4ffc"></a>
#### updateAsciiStream

```
void updateAsciiStream(int columnIndex, InputStream x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우엔 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateAsciiStream(int columnIndex, InputStream x, int length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateAsciiStream(int columnIndex, InputStream x, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateAsciiStream(String columnLabel, InputStream x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateAsciiStream(String columnLabel, InputStream x, int length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateAsciiStream(String columnLabel, InputStream x, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="51452f2354372f18"></a>
#### updateBigDecimal

```
void updateBigDecimal(int columnIndex, BigDecimal x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBigDecimal(String columnLabel, BigDecimal x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="022119c831fbeb7a"></a>
#### updateBinaryStream

```
void updateBinaryStream(int columnIndex, InputStream x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBinaryStream(int columnIndex, InputStream x, int length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBinaryStream(int columnIndex, InputStream x, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBinaryStream(String columnLabel, InputStream x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBinaryStream(String columnLabel, InputStream x, int length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBinaryStream(String columnLabel, InputStream x, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="67971702ae426501"></a>
#### updateBlob

```
void updateBlob(int columnIndex, Blob x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBlob(int columnIndex, InputStream inputStream) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBlob(int columnIndex, InputStream inputStream, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBlob(String columnLabel, Blob x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBlob(String columnLabel, InputStream inputStream) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBlob(String columnLabel, InputStream inputStream, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="4271b84fb7621391"></a>
#### updateBoolean

```
void updateBoolean(int columnIndex, boolean x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBoolean(String columnLabel, boolean x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="d7098dce9fdce76f"></a>
#### updateByte

```
void updateByte(int columnIndex, byte x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateByte(String columnLabel, byte x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="84f40a37a8debcbb"></a>
#### updateBytes

```
void updateBytes(int columnIndex, byte[] x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateBytes(String columnLabel, byte[] x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="4b5ccc5d28f2e3e6"></a>
#### updateCharacterStream

```
void updateCharacterStream(int columnIndex, Reader x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateCharacterStream(int columnIndex, Reader x, int length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateCharacterStream(int columnIndex, Reader x, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateCharacterStream(String columnLabel, Reader reader) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateCharacterStream(String columnLabel, Reader reader, int length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateCharacterStream(String columnLabel, Reader reader, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="1845adf381e9ab5c"></a>
#### updateClob

```
void updateClob(int columnIndex, Clob x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateClob(int columnIndex, Reader reader) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateClob(int columnIndex, Reader reader, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateClob(String columnLabel, Clob x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateClob(String columnLabel, Reader reader) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateClob(String columnLabel, Reader reader, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="704a984f1b6ae51a"></a>
#### updateDate

```
void updateDate(int columnIndex, Date x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateDate(String columnLabel, Date x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="700c7ca8712dd0e2"></a>
#### updateDouble

```
void updateDouble(int columnIndex, double x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateDouble(String columnLabel, double x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="4a46edc847834458"></a>
#### updateFloat

```
void updateFloat(int columnIndex, float x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateFloat(String columnLabel, float x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="362de27466d82b92"></a>
#### updateInt

```
void updateInt(int columnIndex, int x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateInt(String columnLabel, int x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="4cfdaa6c31d98a0a"></a>
#### updateLong

```
void updateLong(int columnIndex, long x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateLong(String columnLabel, long x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="92644ba70d93282d"></a>
#### updateNCharacterStream

```
void updateNCharacterStream(int columnIndex, Reader x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateNCharacterStream(int columnIndex, Reader x, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateNCharacterStream(String columnLabel, Reader reader) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateNCharacterStream(String columnLabel, Reader reader, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="6b856792634ecb26"></a>
#### updateNClob

```
void updateNClob(int columnIndex, NClob nClob) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateNClob(int columnIndex, Reader reader) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateNClob(int columnIndex, Reader reader, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateNClob(String columnLabel, NClob nClob) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateNClob(String columnLabel, Reader reader) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateNClob(String columnLabel, Reader reader, long length) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="3fc6ff9f79521f48"></a>
#### updateNString

```
void updateNString(int columnIndex, String nString) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateNString(String columnLabel, String nString) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="d12b6dd351e813d4"></a>
#### updateNull

```
void updateNull(int columnIndex) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateNull(String columnLabel) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="4c66af4206622e1d"></a>
#### updateObject

```
void updateObject(int columnIndex, Object x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateObject(int columnIndex, Object x, int scaleOrLength) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateObject(String columnLabel, Object x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateObject(String columnLabel, Object x, int scaleOrLength) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="926d8580a974f9df"></a>
#### updateRef

```
void updateRef(int columnIndex, Ref x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateRef(String columnLabel, Ref x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="d38ee5c9926df72b"></a>
#### updateRow

```
void updateRow() throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="2fed18f77460eb56"></a>
#### updateRowId

```
void updateRowId(int columnIndex, RowId x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateRowId(String columnLabel, RowId x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="cd809b60910ae108"></a>
#### updateShort

```
void updateShort(int columnIndex, short x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateShort(String columnLabel, short x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="48239859749abb3b"></a>
#### updateSQLXML

```
void updateSQLXML(int columnIndex, SQLXML xmlObject) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateSQLXML(String columnLabel, SQLXML xmlObject) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="9daea620567f04a7"></a>
#### updateString

```
void updateString(int columnIndex, String x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateString(String columnLabel, String x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="ed85234cdfed5d5c"></a>
#### updateTime

```
void updateTime(int columnIndex, Time x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateTime(String columnLabel, Time x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="4a321f1106a119b1"></a>
#### updateTimestamp

```
void updateTimestamp(int columnIndex, Timestamp x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

```
void updateTimestamp(String columnLabel, Timestamp x) throws SQLException
```

- 동작: Cursor update 기능은 아직 구현되어 있지 않다. ResultSet concurrency가 ResultSet.CONCUR_READ_ONLY일 경우에는 SQLException이 발생하고 ResultSet.CONCUR_UPDATABLE일 경우에는 SQLFeatureNotSupportedException이 발생한다.
- 예외: 이미 close되어 있으면 SQLException이 발생한다. 그 외의 경우는 동작을 참조한다.

<a id="95aafad807786162"></a>
#### wasNull

```
boolean wasNull() throws SQLException
```

- 동작: 마지막으로 읽은 column의 값이 NULL인지 여부를 묻는다. NULL이면 true를, 그렇지 않으면 false를 반환한다.
- 예외: ResultSet이 이미 close되었거나 column 값을 읽은 적이 없으면 SQLException이 발생한다.

<a id="1164913bb93bd40f"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface)
```

- 동작: 이 객체가 iface 인터페이스를 구현한 클래스인지 여부를 묻는다. 맞으면 true를, 그렇지 않으면 false를 반환한다. GOLDILOCKS ResultSet 객체는 다른 클래스의 wrapper가 아니므로 wrapper의 유무는 판단하지 않고 오직 주어진 인자 클래스 타입을 구현했는지 여부만 묻는다.
- 예외: 발생하지 않는다.

<a id="ad3f31e11b28770d"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface)
```

- 동작: GOLDILOCKS ResultSet은 다른 클래스의 wrapper가 아니므로 unwrap 하더라도 결국 자기 자신을 반환한다. 해당 타입으로 캐스팅한 후에 반환한다. iface가 isWrapperFor() method의 인자로 주어졌을 때 false를 반환하는 값일 경우, 이 method는 예외를 발생시킨다.
- 예외: iface가 이 객체의 타입이 아닌 경우 (이 객체가 implement 하지 않은 타입인 경우) SQLException이 발생한다.

<a id="386263471e61bbdb"></a>
### ResultSetMetaData

<a id="cb91951d6e805caa"></a>
#### getCatalogName

```
String getCatalogName(int column) throws SQLException
```

- 동작: 해당 column의 카탈로그 이름을 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="2c6feb51654fb59c"></a>
#### getColumnClassName

```
String getColumnClassName(int column) throws SQLException
```

- 동작: 해당 column의 타입에 가장 적합한 Java 클래스의 이름을 반환한다. java.math.BigDecimal 등으로 명시되며, Java 내부의 getName()method를 참조한다. Binary 타입의 경우에는 byte[].class.getName()을 참조하기 때문에 '[B'등으로 표시될 수 있다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="c2cc4d96d2f57c49"></a>
#### getColumnCount

```
int getColumnCount() throws SQLException
```

- 동작: ResultSet이 가지는 column 개수를 반환한다.
- 예외: 발생하지 않는다.

<a id="d3debfd5795c1bac"></a>
#### getColumnDisplaySize

```
int getColumnDisplaySize(int column) throws SQLException
```

- 동작: 해당 column의 값을 출력할 때 최대 폭을 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="7691a4952d0e9a26"></a>
#### getColumnLabel

```
String getColumnLabel(int column) throws SQLException
```

- 동작: 해당 column의 label을 얻어온다. 예를 들어 "select C1 + 1 from t1"과 같은 질의문의 경우 label은 "C1 + 1"이고 name은 ""이다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="24b967f4b154b585"></a>
#### getColumnName

```
String getColumnName(int column) throws SQLException
```

- 동작: 해당 column의 alias name을 반환한다. JDBC 스펙에는 alias name이 아니라 column의 원래 이름을 얻어오도록 명시했지만, 각종 view의 경우 원래 이름들이 의미없거나 복잡하므로 alias name을 사용하는게 더 좋다. 예를 들어 "select C1 as C2 from t1"과 같은 질의문의 경우 name과 label 모두 "C2"가 된다. name과 label이 다른 경우는 [getColumnLabel](#7691a4952d0e9a26)을 참조한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="2c9c8f041d85a392"></a>
#### getColumnType

```
int getColumnType(int column) throws SQLException
```

- 동작: 해당 column의 타입을 반환한다. 반환값은 types에 정의된 값이다. GOLDILOCKS interval 계열 타입에 대해서는 Types.OTHERS가 반환된다. 그 외 다른 타입들에 대해서는 해당 types의 상수값이 반환된다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="e6e487d7caf115de"></a>
#### getColumnTypeName

```
String getColumnTypeName(int column) throws SQLException
```

- 동작: 해당 column의 GOLDILOCKS column 타입 이름이 반환된다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="9d27c0b376b5d557"></a>
#### getPrecision

```
int getPrecision(int column) throws SQLException
```

- 동작: 해당 column의 precision을 반환한다. Precision이 없는 타입에 대해서는 0을 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="8f3baf918d6e77e4"></a>
#### getScale

```
int getScale(int column) throws SQLException
```

- 동작: 해당 column의 scale을 반환한다. Scale이 없는 타입에 대해서는 0을 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="03690ae0d3786487"></a>
#### getSchemaName

```
String getSchemaName(int column) throws SQLException
```

- 동작: 해당 column의 스키마 이름을 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="579539cba0817a0f"></a>
#### getTableName

```
String getTableName(int column) throws SQLException
```

- 동작: 해당 column의 테이블 이름을 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="d6d9042e2c5ade4b"></a>
#### isAutoIncrement

```
boolean isAutoIncrement(int column) throws SQLException
```

- 동작: 해당 column이 자동으로 고유값을 부여받는 column인지 여부를 반환한다. 맞으면 true를 그렇지 않으면 false를 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="add68118cfac264f"></a>
#### isCaseSensitive

```
boolean isCaseSensitive(int column) throws SQLException
```

- 동작: 해당 column이 대소문자를 구별하는지 여부를 반환한다. 구별하면 true를, 구별하지 않으면 false를 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="421ec746248f3061"></a>
#### isCurrency

```
boolean isCurrency(int column) throws SQLException
```

- 동작: 서버에서 column의 currency 판단을 할 수 없으므로 항상 false를 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="15f0fd44628d73e9"></a>
#### isDefinitelyWritable

```
boolean isDefinitelyWritable(int column) throws SQLException
```

- 동작: 해당 column의 updatable 여부를 반환한다. GOLDILOCKS에서 definitely writable은 지원하지 않는다. 항상 isUpdatable()과 같은 값을 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="33525845b3d546f7"></a>
#### isNullable

```
int isNullable(int column) throws SQLException
```

- 동작: 해당 column이 NULL을 가질 수 있는지 여부를 반환한다. columnNullable이나 columnNoNulls 중 하나를 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="ccff4e191d27f27c"></a>
#### isReadOnly

```
boolean isReadOnly(int column) throws SQLException
```

- 동작: 해당 column의 read-only 여부를 반환한다. 항상 isUpdatable()의 반대값을 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="1a89db1d80c97789"></a>
#### isSearchable

```
boolean isSearchable(int column) throws SQLException
```

- 동작: 해당 column이 조건절에 사용될 수 있는지 여부를 반환한다. GOLDILOCKS의 모든 target column이 조건절에 사용될 수 있으므로 항상 true를 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="5f521e02b812bb56"></a>
#### isSigned

```
boolean isSigned(int column) throws SQLException
```

- 동작: 해당 column이 부호를 가지는지 여부를 반환한다. 부호를 가지면 true를, 그렇지 않으면 false를 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="3b1543c28386960d"></a>
#### isWritable

```
boolean isWritable(int column) throws SQLException
```

- 동작: 해당 column이 updatable인지 여부를 반환한다.
- 예외: Column이 잘못된 값이면 SQLException이 발생한다.

<a id="e3cd1631408036f0"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface)
```

- 동작: 이 객체가 iface 인터페이스를 구현한 클래스인지 여부를 묻는다. 맞으면 true를, 그렇지 않으면 false를 반환한다. GOLDILOCKS ResultSetMetaData 객체는 다른 클래스의 wrapper가 아니므로 wrapper의 유무는 판단하지 않고 오직 주어진 인자 클래스 타입을 구현했는지 여부만 묻는다.
- 예외: 발생하지 않는다.

<a id="3ca06eca4302f0f3"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface)
```

- 동작: GOLDILOCKS ResultSetMetaData는 다른 클래스의 wrapper가 아니므로 unwrap 하더라도 결국 자기 자신을 반환한다. 해당 타입으로 캐스팅한 후에 반환한다. iface가 isWrapperFor() method의 인자로 주어졌을 때 false를 반환하는 값이라면 이 method는 예외를 발생시킨다.
- 예외: iface가 이 객체의 타입이 아닌 경우 (이 객체가 implement 하지 않은 타입을 부여한 경우) SQLException이 발생한다.

<a id="8fb5124addb7c93c"></a>
### RowId

<a id="6b046fda6ba3f35e"></a>
#### equals

```
boolean equals(Object obj) throws SQLException
```

- 동작: 이 객체가 obj와 같은 RowId를 나타내면 true를, 그렇지 않으면 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="0333b9962b8eea5f"></a>
#### getBytes

```
byte[] getBytes() throws SQLException
```

- 동작: RowId의 바이트 배열 값을 반환한다.
- 예외: 발생하지 않는다.

<a id="ae47b112e4113b13"></a>
#### hashCode

```
int hashCode() throws SQLException
```

- 동작: 해시 코드 값을 반환한다.
- 예외: 발생하지 않는다.

<a id="131047ca0e792b20"></a>
#### toString

```
String toString() throws SQLException
```

- 동작: RowId 값의 base-64 문자열을 반환한다.
- 예외: 발생하지 않는다.

<a id="eb30cfe40842342b"></a>
### RowSet

클래스가 구현되지 않았다.

<a id="835bead721b2f93c"></a>
#### addRowSetListener

```
void addRowSetListener(RowSetListener listener) throws SQLException
```

<a id="ab17b1e870899b9e"></a>
#### clearParameters

```
void clearParameters() throws SQLException
```

<a id="133222419812bc42"></a>
#### execute

```
void execute() throws SQLException
```

<a id="7780460f461a2c53"></a>
#### getCommand

```
String getCommand() throws SQLException
```

<a id="a3bfe46bf59e7b49"></a>
#### getDataSourceName

```
String getDataSourceName() throws SQLException
```

<a id="4134d7b643e61213"></a>
#### getEscapeProcessing

```
boolean getEscapeProcessing() throws SQLException
```

<a id="6b1acf36f1ad67be"></a>
#### getMaxFieldSize

```
int getMaxFieldSize() throws SQLException
```

<a id="3c8ea6f4e50b992e"></a>
#### getMaxRows

```
int getMaxRows() throws SQLException
```

<a id="a123e3778f589756"></a>
#### getPassword

```
String getPassword() throws SQLException
```

<a id="a7ff4ac9dd31eb6c"></a>
#### getQueryTimeout

```
int getQueryTimeout() throws SQLException
```

<a id="59c370a8e7defd32"></a>
#### getTransactionIsolation

```
int getTransactionIsolation() throws SQLException
```

<a id="174af01aba38688a"></a>
#### getTypeMap

```
Map<String,Class<?>> getTypeMap() throws SQLException
```

<a id="c9324716d5db96f6"></a>
#### getUrl

```
String getUrl() throws SQLException
```

<a id="f799c53e63e5847a"></a>
#### getUsername

```
String getUsername() throws SQLException
```

<a id="a11139013758b4ba"></a>
#### isReadOnly

```
boolean isReadOnly() throws SQLException
```

<a id="f4ee2c1c367d420c"></a>
#### removeRowSetListener

```
void removeRowSetListener(RowSetListener listener) throws SQLException
```

<a id="40bffc1ece8f33d8"></a>
#### setArray

```
void setArray(int i, Array x) throws SQLException
```

<a id="04641e6b5749c7f6"></a>
#### setAsciiStream

```
void setAsciiStream(int parameterIndex, InputStream x) throws SQLException
```

```
void setAsciiStream(int parameterIndex, InputStream x, int length) throws SQLException
```

```
void setAsciiStream(String parameterName, InputStream x) throws SQLException
```

```
void setAsciiStream(String parameterName, InputStream x, int length) throws SQLException
```

<a id="33a7fb787076fb2a"></a>
#### setBigDecimal

```
void setBigDecimal(int parameterIndex, BigDecimal x) throws SQLException
```

```
void setBigDecimal(String parameterName, BigDecimal x) throws SQLException
```

<a id="7d21bf8f40a822e0"></a>
#### setBinaryStream

```
void setBinaryStream(int parameterIndex, InputStream x) throws SQLException
```

```
void setBinaryStream(int parameterIndex, InputStream x, int length) throws SQLException
```

```
void setBinaryStream(String parameterName, InputStream x) throws SQLException
```

```
void setBinaryStream(String parameterName, InputStream x, int length) throws SQLException
```

<a id="a3ee27b76bce8080"></a>
#### setBlob

```
void setBlob(int i, Blob x) throws SQLException
```

```
void setBlob(int parameterIndex, InputStream inputStream) throws SQLException
```

```
void setBlob(int parameterIndex, InputStream inputStream, long length) throws SQLException
```

```
void setBlob(String parameterName, Blob x) throws SQLException
```

```
void setBlob(String parameterName, InputStream inputStream) throws SQLException
```

```
void setBlob(String parameterName, InputStream inputStream, long length) throws SQLException
```

<a id="72e1c64dde8f16de"></a>
#### setBoolean

```
void setBoolean(int parameterIndex, boolean x) throws SQLException
```

```
void setBoolean(String parameterName, boolean x) throws SQLException
```

<a id="0bd0d579713e3075"></a>
#### setByte

```
void setByte(int parameterIndex, byte x) throws SQLException
```

```
void setByte(String parameterName, byte x) throws SQLException
```

<a id="2d102e9fa0f48320"></a>
#### setBytes

```
void setBytes(int parameterIndex, byte[] x) throws SQLException
```

```
void setBytes(String parameterName, byte[] x) throws SQLException
```

<a id="14c9d6571b5452fd"></a>
#### setCharacterStream

```
void setCharacterStream(int parameterIndex, Reader reader) throws SQLException
```

```
void setCharacterStream(int parameterIndex, Reader reader, int length) throws SQLException
```

```
void setCharacterStream(String parameterName, Reader reader) throws SQLException
```

```
void setCharacterStream(String parameterName, Reader reader, int length) throws SQLException
```

<a id="f0bc91f222bd8c2d"></a>
#### setClob

```
void setClob(int i, Clob x) throws SQLException
```

```
void setClob(int parameterIndex, Reader reader) throws SQLException
```

```
void setClob(int parameterIndex, Reader reader, long length) throws SQLException
```

```
void setClob(String parameterName, Clob x) throws SQLException
```

```
void setClob(String parameterName, Reader reader) throws SQLException
```

```
void setClob(String parameterName, Reader reader, long length) throws SQLException
```

<a id="58104cffacd750c7"></a>
#### setCommand

```
void setCommand(String cmd) throws SQLException
```

<a id="17e37af5e8c9c3a7"></a>
#### setConcurrency

```
void setConcurrency(int concurrency) throws SQLException
```

<a id="b2b1bb60f4739c5d"></a>
#### setDataSourceName

```
void setDataSourceName(String name) throws SQLException
```

<a id="3a1f6932f19b2058"></a>
#### setDate

```
void setDate(int parameterIndex, Date x) throws SQLException
```

```
void setDate(int parameterIndex, Date x, Calendar cal) throws SQLException
```

```
void setDate(String parameterName, Date x) throws SQLException
```

```
void setDate(String parameterName, Date x, Calendar cal) throws SQLException
```

<a id="b8f8f0745567d860"></a>
#### setDouble

```
void setDouble(int parameterIndex, double x) throws SQLException
```

```
void setDouble(String parameterName, double x) throws SQLException
```

<a id="f21caa3e29ccdd05"></a>
#### setEscapeProcessing

```
void setEscapeProcessing(boolean enable) throws SQLException
```

<a id="7d902fd32d4c0a88"></a>
#### setFloat

```
void setFloat(int parameterIndex, float x) throws SQLException
```

```
void setFloat(String parameterName, float x) throws SQLException
```

<a id="7108158de2b80b28"></a>
#### setInt

```
void setInt(int parameterIndex, int x) throws SQLException
```

```
void setInt(String parameterName, int x) throws SQLException
```

<a id="39f52038dc5c9a12"></a>
#### setLong

```
void setLong(int parameterIndex, long x) throws SQLException
```

```
void setLong(String parameterName, long x) throws SQLException
```

<a id="a2b3c93e6098d20c"></a>
#### setMaxFieldSize

```
void setMaxFieldSize(int max) throws SQLException
```

<a id="fe0278615ea08f25"></a>
#### setMaxRows

```
void setMaxRows(int max) throws SQLException
```

<a id="97a067ae8cc25ec1"></a>
#### setNCharacterStream

```
void setNCharacterStream(int parameterIndex, Reader value) throws SQLException
```

```
void setNCharacterStream(int parameterIndex, Reader value, long length) throws SQLException
```

```
void setNCharacterStream(String parameterName, Reader value) throws SQLException
```

```
void setNCharacterStream(String parameterName, Reader value, long length) throws SQLException
```

<a id="384cef516c814599"></a>
#### setNClob

```
void setNClob(int parameterIndex, NClob value) throws SQLException
```

```
void setNClob(int parameterIndex, Reader reader) throws SQLException
```

```
void setNClob(int parameterIndex, Reader reader, long length) throws SQLException
```

```
void setNClob(String parameterName, NClob value) throws SQLException
```

```
void setNClob(String parameterName, Reader reader) throws SQLException
```

```
void setNClob(String parameterName, Reader reader, long length) throws SQLException
```

<a id="f7abbf755dc1f0cf"></a>
#### setNString

```
void setNString(int parameterIndex, String value) throws SQLException
```

```
void setNString(String parameterName, String value) throws SQLException
```

<a id="4363ff47863cc265"></a>
#### setNull

```
void setNull(int parameterIndex, int sqlType) throws SQLException
```

```
void setNull(int paramIndex, int sqlType, String typeName) throws SQLException
```

```
void setNull(String parameterName, int sqlType) throws SQLException
```

```
void setNull(String parameterName, int sqlType, String typeName) throws SQLException
```

<a id="847673d117684aee"></a>
#### setObject

```
void setObject(int parameterIndex, Object x) throws SQLException
```

```
void setObject(int parameterIndex, Object x, int targetSqlType) throws SQLException
```

```
void setObject(int parameterIndex, Object x, int targetSqlType, int scaleOrLength) throws SQLException
```

```
void setObject(String parameterName, Object x) throws SQLException
```

```
void setObject(String parameterName, Object x, int targetSqlType) throws SQLException
```

```
void setObject(String parameterName, Object x, int targetSqlType, int scale) throws SQLException
```

<a id="6e90431fcff342d6"></a>
#### setPassword

```
void setPassword(String password) throws SQLException
```

<a id="e6a047b698107b55"></a>
#### setQueryTimeout

```
void setQueryTimeout(int seconds) throws SQLException
```

<a id="84a1a667abfa4a18"></a>
#### setReadOnly

```
void setReadOnly(boolean value) throws SQLException
```

<a id="c182fa065bf68ea3"></a>
#### setRef

```
void setRef(int i, Ref x) throws SQLException
```

<a id="bab59471304f0eed"></a>
#### setRowId

```
void setRowId(int parameterIndex, RowId x) throws SQLException
```

```
void setRowId(String parameterName, RowId x) throws SQLException
```

<a id="27ee931b4e8b866f"></a>
#### setShort

```
void setShort(int parameterIndex, short x) throws SQLException
```

```
void setShort(String parameterName, short x) throws SQLException
```

<a id="dcc73ae4b6f46601"></a>
#### setSQLXML

```
void setSQLXML(int parameterIndex, SQLXML xmlObject) throws SQLException
```

```
void setSQLXML(String parameterName, SQLXML xmlObject) throws SQLException
```

<a id="3ca84c321f914745"></a>
#### setString

```
void setString(int parameterIndex, String x) throws SQLException
```

```
void setString(String parameterName, String x) throws SQLException
```

<a id="e25a152f98a28da8"></a>
#### setTime

```
void setTime(int parameterIndex, Time x) throws SQLException
```

```
void setTime(int parameterIndex, Time x, Calendar cal) throws SQLException
```

```
void setTime(String parameterName, Time x) throws SQLException
```

```
void setTime(String parameterName, Time x, Calendar cal) throws SQLException
```

<a id="ec144062d1e24409"></a>
#### setTimestamp

```
void setTimestamp(int parameterIndex, Timestamp x) throws SQLException
```

```
void setTimestamp(int parameterIndex, Timestamp x, Calendar cal) throws SQLException
```

```
void setTimestamp(String parameterName, Timestamp x) throws SQLException
```

```
void setTimestamp(String parameterName, Timestamp x, Calendar cal) throws SQLException
```

<a id="61ae9e53ac406e1e"></a>
#### setTransactionIsolation

```
void setTransactionIsolation(int level) throws SQLException
```

<a id="db4736ef7bca787b"></a>
#### setType

```
void setType(int type) throws SQLException
```

<a id="2e9e0d0402fbacf0"></a>
#### setTypeMap

```
void setTypeMap(Map<String,Class<?>> map) throws SQLException
```

<a id="08367067ff0854e6"></a>
#### setURL

```
void setURL(int parameterIndex, URL x) throws SQLException
```

<a id="de86d64c5f843abd"></a>
#### setUrl

```
void setUrl(String url) throws SQLException
```

<a id="8be11c6be9a91886"></a>
#### setUsername

```
void setUsername(String name) throws SQLException
```

<a id="02ae86bcf545c0f3"></a>
### RowSetMetaData

클래스가 구현되지 않았다.

<a id="40303ecb83606fe6"></a>
#### setAutoIncrement

```
void setAutoIncrement(int columnIndex, boolean property) throws SQLException
```

<a id="53eacbfd6c610ce2"></a>
#### setCaseSensitive

```
void setCaseSensitive(int columnIndex, boolean property) throws SQLException
```

<a id="07360f2287a2364a"></a>
#### setCatalogName

```
void setCatalogName(int columnIndex, String catalogName) throws SQLException
```

<a id="4abbcbe0492ec07a"></a>
#### setColumnCount

```
void setColumnCount(int columnCount) throws SQLException
```

<a id="7e91b24d2df5c448"></a>
#### setColumnDisplaySize

```
void setColumnDisplaySize(int columnIndex, int size) throws SQLException
```

<a id="c0fae431064e8409"></a>
#### setColumnLabel

```
void setColumnLabel(int columnIndex, String label) throws SQLException
```

<a id="cffb7a980e19a1ea"></a>
#### setColumnName

```
void setColumnName(int columnIndex, String columnName) throws SQLException
```

<a id="e32f5050d72b4a38"></a>
#### setColumnType

```
void setColumnType(int columnIndex, int SQLType) throws SQLException
```

<a id="d8d7616b3b7af55c"></a>
#### setColumnTypeName

```
void setColumnTypeName(int columnIndex, String typeName) throws SQLException
```

<a id="ce2f5b263651a2f4"></a>
#### setCurrency

```
void setCurrency(int columnIndex, boolean property) throws SQLException
```

<a id="5be824dac1eed959"></a>
#### setNullable

```
void setNullable(int columnIndex, int property) throws SQLException
```

<a id="054496dc14682163"></a>
#### setPrecision

```
void setPrecision(int columnIndex, int precision) throws SQLException
```

<a id="d5cd2ca6a6431d0e"></a>
#### setScale

```
void setScale(int columnIndex, int scale) throws SQLException
```

<a id="8b75840728ad65f7"></a>
#### setSchemaName

```
void setSchemaName(int columnIndex, String schemaName) throws SQLException
```

<a id="bde9e328daded700"></a>
#### setSearchable

```
void setSearchable(int columnIndex, boolean property) throws SQLException
```

<a id="00260573c714d873"></a>
#### setSigned

```
void setSigned(int columnIndex, boolean property) throws SQLException
```

<a id="e639e2b45a9d7b06"></a>
#### setTableName

```
void setTableName(int columnIndex, String tableName) throws SQLException
```

<a id="00e0400d2b00940d"></a>
### Savepoint

<a id="b698e2a294ea15c9"></a>
#### getSavepointId

```
int getSavepointId() throws SQLException
```

- 동작: 자동으로 부여된 ID 값을 반환한다.
- 예외: Savepoint 객체에 이름을 주어 생성한 경우 ID를 가지지 않으므로 SQLException이 발생한다.

<a id="93270aab32664a11"></a>
#### getSavepointName

```
String getSavepointName() throws SQLException
```

- 동작: Savepoint 객체를 생성할 때 지정한 이름을 반환한다.
- 예외: 자동 ID 값으로 savepoint 객체를 생성한 경우, SQLException이 발생한다.

<a id="15910a518407c9b4"></a>
### SQLData

클래스가 구현되지 않았다.

<a id="70dbe48dc3c98b61"></a>
#### getSQLTypeName

```
String getSQLTypeName() throws SQLException
```

<a id="ba885b203f906f34"></a>
#### readSQL

```
void readSQL(SQLInput stream, String typeName) throws SQLException
```

<a id="79870f82024f8a81"></a>
#### writeSQL

```
void writeSQL(SQLOutput stream) throws SQLException
```

<a id="04f2713731871fc1"></a>
### SQLXML

클래스가 구현되지 않았다.

<a id="d331b4e0fe22e359"></a>
#### free

```
void free() throws SQLException
```

<a id="3b56c12e7c22a34b"></a>
#### getBinaryStream

```
InputStream getBinaryStream() throws SQLException
```

<a id="fffe87f96b8f08bc"></a>
#### getCharacterStream

```
Reader getCharacterStream() throws SQLException
```

<a id="df0a15d85f0ad6df"></a>
#### getSource

```
<T extends Source> T getSource(Class<T> sourceClass) throws SQLException
```

<a id="263cf33cb008789a"></a>
#### getString

```
String getString() throws SQLException
```

<a id="8bfefcb78194cd90"></a>
#### setBinaryStream

```
OutputStream setBinaryStream() throws SQLException
```

<a id="48bad084e70724f3"></a>
#### setCharacterStream

```
Writer setCharacterStream() throws SQLException
```

<a id="eaf94b1fe860012b"></a>
#### setResult

```
<T extends Result> T setResult(Class<T> resultClass) throws SQLException
```

<a id="cd57acfcc78ffa63"></a>
#### setString

```
void setString(String value) throws SQLException
```

<a id="70e762462728e85d"></a>
### Statement

<a id="62e2fd4abb38b617"></a>
#### addBatch

```
void addBatch(String sql) throws SQLException
```

- 동작: SQL 문을 batch job에 추가한다.
- 예외: 발생하지 않는다.

<a id="850c0ec9e1a561ff"></a>
#### cancel

```
void cancel() throws SQLException
```

- 동작: 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException을 반환한다.

<a id="cc53d77ad8a4f365"></a>
#### clearBatch

```
void clearBatch() throws SQLException
```

- 동작: 등록된 batch job들을 모두 제거한다. 등록된 batch job이 없을 경우, 아무런 작업도 하지 않는다.
- 예외: 발생하지 않는다.

<a id="192059906554ce2c"></a>
#### clearWarnings

```
void clearWarnings() throws SQLException
```

- 동작: Statement 객체가 가지고 있는 SQLWarning 객체들을 모두 제거한다.
- 예외: 발생하지 않는다.

<a id="f8648a150085c6e7"></a>
#### close

```
void close() throws SQLException
```

- 동작: 현재 statement 객체를 close하고 서버에 할당된 statement 관련 정보가 있을 경우, 이를 해제한다. 이 객체에서 생성한 ResultSet이 있으면 이를 모두 close한다. 이 statement 객체를 생성한 connection 객체로부터 이 객체를 제거한다.
- 예외: 서버로부터 statement 정보를 해제할 때 에러가 발생하면 예외가 발생한다.

<a id="6c05a6599abb6e25"></a>
#### execute

```
boolean execute(String sql) throws SQLException
```

- 동작: SQL 문을 실행한다. 실행한 SQL 문이 ResultSet을 가지면 true를, 그렇지 않으면 false를 반환한다.
- 예외: Statement가 이미 close되었거나 batch job이 등록되어 있거나 실행할 때 서버로부터 에러가 발생하면 예외가 발생한다.

```
boolean execute(String sql, int autoGeneratedKeys) throws SQLException
```

- 동작: SQL 문을 실행한다. 실행한 SQL 문이 ResultSet을 가지면 true를, 그렇지 않으면 false를 반환한다. Auto key generation은 지원하지 않는다.
- 예외: Statement가 이미 close되었거나 batch job이 등록되어 있거나 실행할 때 서버로부터 에러가 발생하면 예외가 발생한다. autoGeneratedKeys가 Statement.NO_GENERATED_KEYS가 아닐 경우, SQLFeatureNotSupportedException이 발생한다.

```
boolean execute(String sql, int[] columnIndexes) throws SQLException
```

- 동작: SQL 문을 실행한다. 실행한 SQL 문이 ResultSet을 가지면 true를, 그렇지 않으면 false를 반환한다. Auto key generation은 지원하지 않는다.
- 예외: Statement가 이미 close되었거나 batch job이 등록되어 있거나 실행할 때 서버로부터 에러가 발생하면 예외가 발생한다. acolumnIndexes가 null이 아닐 경우, SQLFeatureNotSupportedException이 발생한다.

```
boolean execute(String sql, String[] columnNames) throws SQLException
```

- 동작: SQL 문을 실행한다. 실행한 SQL 문이 ResultSet을 가지면 true를, 그렇지 않으면 false를 반환한다. Auto key generation은 지원하지 않는다.
- 예외: Statement가 이미 close되었거나 batch job이 등록되어 있거나 실행할 때 서버로부터 에러가 발생하면 예외가 발생한다. columnNames가 null이 아닐 경우, SQLFeatureNotSupportedException이 발생한다.

<a id="8362379b371a2732"></a>
#### executeBatch

```
int[] executeBatch() throws SQLException
```

- 동작: 등록된 batch job을 차례대로 execute한다. 각 batch job마다 서버와 통신이 발생한다. 각 batch job이 실행된 후 갱신된 row 개수들의 배열이 반환된다.
- 예외: Statement가 이미 close되었거나 등록된 batch job이 없거나 실행할 때 서버로부터 에러가 발생하면 예외가 발생한다.

> Batch job들이 한 번에 서버로 전송되어 실행되는 구조가 아니기 때문에 일반 execute()에 비해 성능상 큰 이점은 없다. 빠른 처리를 위해서는 PreparedStatement의 batch execution을 사용하는 것이 좋다.

<a id="11d36a0d830fa862"></a>
#### executeQuery

```
ResultSet executeQuery(String sql) throws SQLException
```

- 동작: 주어진 SQL 문을 실행하고 결과의 일부를 받아서 ResultSet을 생성한다.
- 예외: Statement가 이미 close되었거나 batch job이 등록되어 있거나 실행할 때 서버로부터 에러가 발생하였거나 SQL 문이 select 구문이 아닐 경우 예외가 발생한다.

> execute()와 동작이 조금 다르다. 동일한 SQL 문에 대해 execute() 후 getResultSet()을 하면 서버와 두 번 통신하게 되는데, execute() 할 때는 실행 명령이, getResultSet() 할 때는 fetch 관련 명령이 수행된다. 이에 반해 executeQuery()는 SQL 문이 select 문이라고 가정하고 fetch 할 때까지 한 번의 통신으로 모두 수행한다.

<a id="733def78c05a18ed"></a>
#### executeUpdate

```
int executeUpdate(String sql) throws SQLException
```

- 동작: SQL 문을 실행한다. 실행에 의해 갱신된 row의 개수를 반환한다.
- 예외: Statement가 이미 close되었거나 batch job이 등록되어 있거나 실행할 때 서버로부터 에러가 발생하였거나 SQL 문이 select 문일 경우, 예외가 발생한다.

```
int executeUpdate(String sql, int autoGeneratedKeys) throws SQLException
```

- 동작: SQL 문을 실행한다. 실행에 의해 갱신된 row의 개수를 반환한다. Auto key generation 기능은 지원하지 않는다.
- 예외: Statement가 이미 close되었거나 batch job이 등록되어 있거나 실행할 때 서버로부터 에러가 발생하였거나 SQL 문이 select 문일 경우 예외가 발생한다. autoGeneratedKeys가 Statement.NO_GENERATED_KEYS가 아닐 경우, SQLFeatureNotSupportedException이 발생한다.

```
int executeUpdate(String sql, int[] columnIndexes) throws SQLException
```

- 동작: SQL 문을 실행한다. 실행에 의해 갱신된 row의 개수를 반환한다. Auto key generation 기능은 지원하지 않는다.
- 예외: Statement가 이미 close되었거나 batch job이 등록되어 있거나 실행할 때 서버로부터 에러가 발생하였거나 SQL 문이 select 문일 경우 예외가 발생한다. columnIndexes가 null이 아닐 경우, SQLFeatureNotSupportedException이 발생한다.

```
int executeUpdate(String sql, String[] columnNames) throws SQLException
```

- 동작: SQL 문을 실행한다. 실행에 의해 갱신된 row의 개수를 반환한다. Auto key generation 기능은 지원하지 않는다.
- 예외: Statement가 이미 close되었거나 batch job이 등록되어 있거나 실행할 때 서버로부터 에러가 발생하였거나 SQL 문이 select 문일 경우 예외가 발생한다. columnNames가 null이 아닐 경우, SQLFeatureNotSupportedException이 발생한다.

<a id="e16ae5cf125d99da"></a>
#### getConnection

```
Connection getConnection() throws SQLException
```

- 동작: 이 객체를 생성한 connection 객체를 반환한다. PooledConnection을 통해 얻은 logical connection으로 statement 객체를 생성하였을 경우, 사용자는 이 method를 통해 physical connection이 아닌 logical connection을 얻는다.
- 예외: Statement가 이미 close 된 경우에는 예외가 발생한다.

<a id="fde20cb973ab7860"></a>
#### getExplainPlan

```
String getExplainPlan() throws SQLException
```

- 동작: 비표준 method로써 GoldilocksStatement의 고유한 method이다. 생성된 plan text를 얻어온다. 이 method를 사용하려면 setExplainPlanOption() method를 통해 plan text를 생성하도록 설정해야 한다. 자세한 사용법은 [Plan Text 조회](#373c97263781c47e)를 참조한다.
- 예외: Statement가 이미 close되었거나 서버에서 에러가 발생할 경우 예외가 발생한다.

<a id="32fb83911bb27143"></a>
#### getExplainPlanOption

```
int getExplainPlanOption() throws SQLException
```

- 동작: 비표준 method로써 GoldilocksStatement의 고유한 method이다. 현재 설정된 plan text 생성에 대한 옵션을 얻어온다. 반환되는 값은 다음 값 중의 하나이고, 기본값은 GoldilocksStatement.EXPLAIN_PLAN_OPTION_OFF이다.
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_OFF
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_ON
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_ON_VERBOSE
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_ONLY
- 예외: 발생하지 않는다.

<a id="8d9add4294aebdcb"></a>
#### getFetchDirection

```
int getFetchDirection() throws SQLException
```

- 동작: 항상 ResultSet.FETCH_FORWARD를 반환한다.
- 예외: Statement가 이미 close되었을 경우, 예외가 발생한다.

<a id="ca8647862e1f0220"></a>
#### getFetchSize

```
int getFetchSize() throws SQLException
```

- 동작: 이 statement 객체로부터 얻는 ResultSet의 기본 fetch size를 반환한다. 기본값은 0이고, 0일 경우 fetch 할 row 개수를 서버가 자동으로 결정한다. 자세한 내용 ResultSet의 [getFetchSize](#94ede4ff4828fc6c)를 참조한다.
- 예외: Statement가 이미 close 되었을 경우, 예외가 발생한다.

<a id="77f64ced8f84aa6d"></a>
#### getGeneratedKeys

```
ResultSet getGeneratedKeys() throws SQLException
```

- 동작: 지원하지 않는다.
- 예외: 항상 SQLFeatureNotSupportedException이 발생한다.

<a id="0a9ffe63f3eb2f69"></a>
#### getMaxFieldSize

```
int getMaxFieldSize() throws SQLException
```

- 동작: Max field size를 반환한다. 이 값은 column의 최대 길이를 제한한다. Fetch 할 때 column 값이 이 길이보다 길면 나머지 데이터는 잘린다. 기본값은 0이고, 0일 경우 최대 길이는 무한대이다.
- 예외: Statement가 이미 close 되었을 경우, 예외가 발생한다.

<a id="1d5d47497c057585"></a>
#### getMaxRows

```
int getMaxRows() throws SQLException
```

- 동작: Max rows를 반환한다. Max rows는 이 statement로부터 얻은 ResultSet이 가질 수 있는 최대 row 개수를 의미한다. 최대 row 개수 이상의 row들은 무시된다. 기본값은 0이고, 0은 무제한을 의미한다.
- 예외: Statement가 이미 close되었을 경우, 예외가 발생한다.

<a id="0054251cc1343dd5"></a>
#### getMoreResults

```
boolean getMoreResults() throws SQLException
```

- 동작: 현재는 한 번의 execution당 하나의 ResultSet만 가질 수 있기 때문에 항상 false를 반환한다. 현재의 ResultSet은 close된다.
- 예외: Statement가 이미 close되었을 경우, 예외가 발생한다.

```
boolean getMoreResults(int current) throws SQLException
```

<a id="a8aa539e16b337e5"></a>
#### getQueryTimeout

```
int getQueryTimeout() throws SQLException
```

- 동작: Query timeout 값을 얻는다. 이 값은 서버가 execution 할 때 적용하는 timeout 값으로써 실행 시간이 이 시간을 넘기면 execution이 취소되고 사용자는 timeout 관련 에러를 반환받는다. 단위는 초이며 사용자가 특별히 설정하지 않을 경우, 세션의 기본값을 가져온다. 세션의 기본값은 프로퍼티로 지정하지 않을 경우 0이며 0은 무한 대기를 의미한다.
- 예외: Statement가 이미 close되었을 경우, 예외가 발생한다.

<a id="e95c644e407cd105"></a>
#### getResultSet

```
ResultSet getResultSet() throws SQLException
```

- 동작: 현재 수행된 execution에 대해 fetch를 수행하고 fetch 결과의 일부를 받아 ResultSet을 생성한 후 반환한다. JDBC 스펙에 명시된 것처럼 execution 한 번당 이 method를 한 번만 호출하도록 구현하지 않고 이 method를 여러 번 부르더라도 같은 객체를 반환하도록 했다.
- 예외: Statement가 이미 close되었을 경우, 예외가 발생한다. Fetch 할 때 서버로부터 에러가 발생하면 예외가 발생한다.

<a id="c38a60547f0c8934"></a>
#### getResultSetConcurrency

```
int getResultSetConcurrency() throws SQLException
```

- 동작: ResultSet concurrency를 반환한다. 이 값은 이 객체로부터 생성되는 ResultSet의 concurrency를 결정한다. 기본값은 ResultSet.CONCUR_READ_ONLY이다. Updatable cursor는 아직 지원하지 않는다.
- 예외: Statement가 이미 close되었을 경우, 예외가 발생한다.

<a id="2eeb357cc00674db"></a>
#### getResultSetHoldability

```
int getResultSetHoldability() throws SQLException
```

- 동작: ResultSet holdability를 반환한다. 이 값은 이 객체로부터 생성되는 ResultSet의 holdability를 결정한다. 기본값은 ResultSet.HOLD_CURSORS_OVER_COMMIT이다.
- 예외: Statement가 이미 close되었을 경우, 예외가 발생한다.

<a id="889cb6a1aca3c3a6"></a>
#### getResultSetType

```
int getResultSetType() throws SQLException
```

- 동작: ResultSet type을 반환한다. 이 값은 이 객체로부터 생성되는 ResultSet의 type을 결정한다. 기본값은 ResultSet.TYPE_FORWARD_ONLY이다.
- 예외: Statement가 이미 close되었을 경우, 예외가 발생한다.

<a id="21f8659957a7a702"></a>
#### getUpdateCount

```
int getUpdateCount() throws SQLException
```

- 동작: 마지막으로 수행한 execution에 대한 갱신이 반영된 row 개수를 반환한다. 마지막으로 수행한 SQL 문이 UPDATE, INSERT 문이 아닐 경우에는 -1을 반환한다.
- 예외: Statement가 이미 close되었을 경우, 예외가 발생한다.

<a id="a80504fce774cda7"></a>
#### getUpdateRowCount

```
long getUpdateRowCount() throws SQLException
```

- 동작: getUpdateCount와 같지만 반환되는 타입이 long이다. 비표준 method로써 GoldilocksStatement 타입으로 캐스팅해야 사용할 수 있다.
- 예외: 발생하지 않는다.

<a id="58fa27afce9a7bda"></a>
#### getWarnings

```
SQLWarning getWarnings() throws SQLException
```

- 동작: 이 객체에 축적된 SQLWarning을 반환한다. 없으면 null을 반환한다.
- 예외: 발생하지 않는다.

<a id="47432fe242912145"></a>
#### isClosed

```
boolean isClosed() throws SQLException
```

- 동작: 이 statement가 close 되었는지 여부를 반환한다. Close되었으면 true를, 그렇지 않으면 false를 반환한다. 사용자가 명시적으로 close()를 호출했을 때 뿐만 아니라 서버에 의해서나 connection 객체에 의해서도 close 될 수 있다.
- 예외: 발생하지 않는다.

<a id="44833374bd5e29b8"></a>
#### isPoolable

```
boolean isPoolable() throws SQLException
```

- 동작: Statement pooling은 지원하지 않는다. 항상 false를 반환한다.
- 예외: 발생하지 않는다.

<a id="9cf17fa6cc7bce26"></a>
#### setCursorName

```
void setCursorName(String name) throws SQLException
```

- 동작: 현재 수행된 statement에 의해 생성된 커서의 이름을 설정한다.
- 예외: 커서 이름을 설정할 때 서버로부터 에러가 발생하면 예외가 발생한다.

<a id="3d345635c3236d16"></a>
#### setEscapeProcessing

```
void setEscapeProcessing(boolean enable) throws SQLException
```

- 동작: SQL 문의 escape는 서버의 parser에서 처리되기 때문에 JDBC에서 그 기능을 막을 수는 없다. 아무런 동작도 하지 않는다.
- 예외: Statement가 이미 close되었을 경우, 예외가 발생한다.

<a id="0fe1f16bcc1073c7"></a>
#### setExplainPlanOption

```
void setExplainPlanOption(int option) throws SQLException
```

- 동작: 비표준 method로써 GoldilocksStatement의 고유 method이다. Plan text 생성 옵션을 지정한다. Option은 다음 값 중의 하나로 설정되어야 하며 그 의미는 다음과 같다.
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_OFF: Plan text를 생성하지 않는다.
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_ON: 실행할 때 plan text를 생성한다.
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_ON_VERBOSE: 실행할 때 더 자세한 plan text를 생성한다.
    - GoldilocksStatement.EXPLAIN_PLAN_OPTION_ONLY: 실행할 때 plan text를 생성하지만 실제 실행은 수행하지 않는다.
- 예외: 위의 네 가지 이외의 다른 값을 설정할 경우 예외가 발생한다.

<a id="9e83e72a1827c871"></a>
#### setFetchDirection

```
void setFetchDirection(int direction) throws SQLException
```

- 동작: Fetch 방향을 설정한다. GOLDILOCKS는 forward fetch만 지원하기 때문에 direction이 ResultSet.FETCH_FORWARD가 아닐 경우, 예외가 발생한다.
- 예외: Statement가 이미 close되었거나 direction이 FETCH_FORWARD가 아닌 경우 예외가 발생한다.

<a id="7e9c3b109baafe2c"></a>
#### setFetchSize

```
void setFetchSize(int rows) throws SQLException
```

- 동작: 이 statement 객체로부터 얻는 ResultSet의 기본 fetch size를 설정한다. 기본값은 0이고, 0일 경우 fetch 할 때 row 개수를 서버가 자동으로 결정한다. 자세한 내용은 ResultSet의 [setFetchSize](#c718213f779b973f)를 참조한다.
- 예외: Statement가 이미 close 되었을 경우, 예외가 발생한다.

<a id="d4d52178a3c729ad"></a>
#### setMaxFieldSize

```
void setMaxFieldSize(int max) throws SQLException
```

- 동작: Max field size를 설정한다. 이 값은 column의 최대 길이를 제한한다. Fetch 할 때 column 값이 이 길이보다 길면 나머지 데이터는 잘린다. 기본값은 0이고, 0은 최대 길이가 무한대라는 의미이다. CHAR, VARCHAR, LONG VARCHAR, BINARY, VARBINARY, LONG VARBINARY 타입에 대해서만 유효하다.
- 예외: Statement가 이미 close되었을 경우, 예외가 발생한다.

<a id="eaf452ddf0a985b7"></a>
#### setMaxRows

```
void setMaxRows(int max) throws SQLException
```

- 동작: Max rows를 설정한다. Max rows는 이 statement로부터 얻은 ResultSet이 가질 수 있는 최대 row 개수를 의미한다. 최대 row 개수 이상의 row들은 무시된다. 기본값은 0이고, 0은 무제한을 의미한다.
- 예외: Statement가 이미 close 되었을 경우, 예외가 발생한다.

<a id="61c886670315807b"></a>
#### setPoolable

```
void setPoolable(boolean poolable) throws SQLException
```

- 동작: Statement pooling은 지원하지 않는다. 아무런 동작을 하지 않는다.
- 예외: 발생하지 않는다.

<a id="664b74f88c578aec"></a>
#### setQueryTimeout

```
void setQueryTimeout(int seconds) throws SQLException
```

- 동작: Query timeout 값을 설정한다. 이 값은 서버가 execution 할 때 적용하는 timeout 값으로써 실행 시간이 이 시간을 넘기면 execution이 취소되고 사용자는 timeout 관련 에러를 반환받는다. 단위는 초이다. 사용자가 특별히 설정하지 않으면 세션의 기본값이 적용된다. 세션의 기본값은 프로퍼티로 지정하지 않을 경우, 0이며 이는 무한 대기를 의미한다.
- 예외: Statement가 이미 close되었을 경우, 예외가 발생한다.

<a id="e5d2cd0649c95d76"></a>
#### isWrapperFor

```
boolean isWrapperFor(Class<?> iface) throws SQLException
```

- 동작: 이 객체가 iface 인터페이스를 구현한 클래스인지 여부를 묻는다. 맞으면 true를, 그렇지 않으면 false를 반환한다. GOLDILOCKS statement 객체는 다른 클래스의 wrapper가 아니므로 wrapper의 유무는 판단하지 않고 오직 주어진 인자 클래스 타입을 구현했는지 여부만 묻는다.
- 예외: 발생하지 않는다.

<a id="6e313a22261e94cb"></a>
#### unwrap

```
<T> T unwrap(Class<T> iface) throws SQLException
```

- 동작: GOLDILOCKS statement는 다른 클래스의 wrapper가 아니므로 unwrap 하더라도 결국 자기 자신을 반환한다. 해당 타입으로 캐스팅한 후에 반환한다. iface가 isWrapperFor() method의 인자로 주어졌을 때 false를 반환하는 값이라면 이 method가 예외를 발생시킨다.
- 예외: iface가 이 객체의 타입이 아닌 경우 (이 객체가 implement 하지 않은 타입을 준 경우) SQLException이 발생한다.

<a id="c509311505517e81"></a>
### Struct

클래스가 구현되지 않았다.

<a id="66e1d44db9ede13a"></a>
#### getAttributes

```
Object[] getAttributes() throws SQLException
```

<a id="69225c0d0eca0639"></a>
#### getAttributes

```
Object[] getAttributes(Map<String,Class<?>> map) throws SQLException
```

<a id="c0c711a9fe4f7b01"></a>
#### getSQLTypeName

```
String getSQLTypeName() throws SQLException
```

<a id="8e6a0318c60c861a"></a>
### XAConnection

<a id="2ad35ff1e64b78c8"></a>
#### getXAResource

```
XAResource getXAResource() throws SQLException
```

- 동작: XA 명령을 수행할 수 있는 XAResource 객체를 반환한다. Method를 여러 번 호출하면 계속 같은 결과를 반환받는다.
- 예외: 발생하지 않는다.

<a id="238bd4cb214d7cb2"></a>
### XADataSource

<a id="c00a929d3a667a72"></a>
#### getXAConnection

```
XAConnection getXAConnection() throws SQLException
```

- 동작: XAConnection 객체를 생성하고 반환한다. 연결에 필요한 정보들은 별도의 비표준 method들로 사전에 설정되어 있어야 한다.
- 예외: 서버와의 연결에 실패하면 SQLException이 발생한다.

```
XAConnection getXAConnection(String user, String password) throws SQLException
```

- 동작: Username과 password로 새로운 XAConnection 객체를 열어서 반환한다. 그 외에 연결에 필요한 정보들은 별도의 비표준 method들로 사전에 설정되어 있어야 한다.
- 예외: 서버와의 연결에 실패하면 SQLException이 발생한다.

<a id="fb50b4320a6d8355"></a>
### XAResource

<a id="e68a512576f68c7c"></a>
#### commit

```
void commit(Xid xid, boolean onePhase) throws XAException
```

- 동작: 글로벌 트랜잭션 xid에 대해 XA commit 명령을 수행한다. onePhase를 true로 설정하면 one phase commit이 수행된다.
- 예외: 수행 결과 에러가 발생하면 XAException이 발생한다.

<a id="cf47a12005f7510a"></a>
#### end

```
void end(Xid xid, int flags) throws XAException
```

- 동작: 글로벌 트랜잭션 xid에 대해 XA end 명령을 수행한다. flags는 TMSUCCESS, TMFAIL 또는 TMSUSPEND 중의 하나를 가진다.
- 예외: 수행 결과 에러가 발생하면 XAException이 발생한다.

<a id="1ff54e63ed07c93a"></a>
#### forget

```
void forget(Xid xid) throws XAException
```

- 동작: 글로벌 트랜잭션 xid에 대해 XA forget 명령을 수행한다.
- 예외: 수행 결과 에러가 발생하면 XAException이 발생한다.

<a id="755407fa0e0b3f7f"></a>
#### getTransactionTimeout

```
int getTransactionTimeout() throws XAException
```

- 동작: GOLDILOCKS는 트랜잭션 타임아웃을 지원하지 않는다. 항상 0을 반환한다.
- 예외: 발생하지 않는다.

<a id="9aadf799da2ac7fd"></a>
#### isSameRM

```
boolean isSameRM(XAResource xares) throws XAException
```

- 동작: XAResource 객체가 생성될 때 고유의 rmid를 가지는데 이 rmid로 동일한 XAResource 객체인지 여부를 판단한다.
- 예외: 발생하지 않는다.

<a id="a78034235e402e54"></a>
#### prepare

```
int prepare(Xid xid) throws XAException
```

- 동작: 글로벌 트랜잭션 xid에 대해 XA prepare 명령을 수행한다.
- 예외: 수행 결과 에러가 발생하면 XAException이 발생한다.

<a id="d970a1cdf656b4f6"></a>
#### recover

```
Xid[] recover(int flag) throws XAException
```

- 동작: 주어진 flag로 XA recover 명령을 수행하고 prepare된 트랜잭션 브랜치들의 배열을 반환받는다. flag는 TMSTARTRSCAN, TMENDRSCAN, TMNOFLAGS 중 하나의 값을 가질 수 있다.
- 예외: 수행 결과 에러가 발생하면 XAException이 발생한다.

<a id="97d64fe4b50ead76"></a>
#### rollback

```
void rollback(Xid xid) throws XAException
```

- 동작: 글로벌 트랜잭션 xid에 대해 XA rollback 명령을 수행한다.
- 예외: 수행 결과 에러가 발생하면 XAException이 발생한다.

<a id="e90261c99181fbe6"></a>
#### setTransactionTimeout

```
boolean setTransactionTimeout(int seconds) throws XAException
```

- 동작: GOLDILOCKS는 트랜잭션 타임아웃을 지원하지 않는다. 아무런 작업을 하지 않는다.
- 예외: 발생하지 않는다.

<a id="2d34268101b6d5a1"></a>
#### start

```
void start(Xid xid, int flags) throws XAException
```

- 동작: 주어진 flag로 글로벌 트랜잭션을 시작한다. flag는 TMNOFLAGS, TMJOIN, TMRESUME 중 하나의 값을 가질 수 있다.
- 예외: 수행 결과 에러가 발생하면 XAException이 발생한다.

<a id="8db3c186cf434146"></a>
### GoldilocksInterval

GoldilocksInterval 객체를 사용하여 GOLDILOCKS의 column에 값을 부여하려면 [추가 타입 사용하기](#94b4ca2893aa3371)를 참조한다.

<a id="7465ff409c851081"></a>
#### createIntervalYear

```
public static GoldilocksInterval createIntervalYear(int yearPrecision, boolean sign, int year) throws SQLException
```

- 동작: 주어진 year 값을 가지고 GoldilocksInterval 객체를 생성한다. yearPrecision은 year가 가질 수 있는 자릿수를 의미한다. Year는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: 주어진 year 값이 yearPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalYear(int yearPrecision, String year) throws SQLException
```

- 동작: 주어진 year 값을 가지고 GoldilocksInterval 객체를 생성한다. yearPrecision은 year가 가질 수 있는 자릿수를 의미한다. Year는 0 이상의 정수 값이어야 한다.
- 예외: 주어진 year 값이 yearPrecision을 초과하면 에러가 발생한다.

<a id="73a41991fc5afc34"></a>
#### createIntervalMonth

```
public static GoldilocksInterval createIntervalMonth(int monthPrecision, boolean sign, int month) throws SQLException
```

- 동작: 주어진 month 값을 가지고 GoldilocksInterval 객체를 생성한다. monthPrecision은 month가 가질 수 있는 자릿수를 의미한다. Month는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: 주어진 month 값이 monthPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalMonth(int monthPrecision, String month) throws SQLException
```

- 동작: 주어진 month 값을 가지고 GoldilocksInterval 객체를 생성한다. monthPrecision은 month가 가질 수 있는 자릿수를 의미한다. Month는 0 이상의 정수 값이어야 한다.
- 예외: 주어진 month 값이 monthPrecision을 초과하면 에러가 발생한다.

<a id="b739b92917443a76"></a>
#### createIntervalYearToMonth

```
public static GoldilocksInterval createIntervalYearToMonth(int yearPrecision, boolean sign, int year, int month) throws SQLException
```

- 동작: 주어진 year, month 값을 가지고 GoldilocksInterval 객체를 생성한다. yearPrecision은 year가 가질 수 있는 자릿수를 의미한다. Year, month는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: 주어진 year 값이 yearPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalYearToMonth(int yearPrecision, String yearToMonth) throws SQLException
```

- 동작: 주어진 yearToMonth 값을 가지고 GoldilocksInterval 객체를 생성한다. yearPrecision은 year가 가질 수 있는 자릿수를 의미한다. yearToMonth는 "yy-mm" 패턴을 만족해야 한다.
- 예외: 주어진 year 값이 yearPrecision을 초과하면 에러가 발생한다.

<a id="a651d3bb29725e83"></a>
#### createIntervalDay

```
public static GoldilocksInterval createIntervalDay(int dayPrecision, boolean sign, int day) throws SQLException
```

- 동작: 주어진 day 값을 가지고 GoldilocksInterval 객체를 생성한다. dayPrecision은 day가 가질 수 있는 자릿수를 의미한다. Day는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: 주어진 day 값이 dayPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalDay(int dayPrecision, String day) throws SQLException
```

- 동작: 주어진 day 값을 가지고 GoldilocksInterval 객체를 생성한다. dayPrecision은 day가 가질 수 있는 자릿수를 의미한다. Day는 0 이상의 정수 값이어야 한다.
- 예외: 주어진 day 값이 dayPrecision을 초과하면 에러가 발생한다.

<a id="271d264c6f1856f2"></a>
#### createIntervalHour

```
public static GoldilocksInterval createIntervalHour(int hourPrecision, boolean sign, int hour) throws SQLException
```

- 동작: 주어진 hour 값을 가지고 GoldilocksInterval 객체를 생성한다. hourPrecision은 hour가 가질 수 있는 자릿수를 의미한다. Hour는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고, 음수이면 false이다.
- 예외: 주어진 hour 값이 hourPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalHour(int hourPrecision, String hour) throws SQLException
```

- 동작: 주어진 hour 값을 가지고 GoldilocksInterval 객체를 생성한다. hourPrecision은 hour가 가질 수 있는 자릿수를 의미한다. Hour는 0 이상의 정수 값이어야 한다.
- 예외: 주어진 hour 값이 hourPrecision을 초과하면 에러가 발생한다.

<a id="d5a0223f7b94a1de"></a>
#### createIntervalMinute

```
public static GoldilocksInterval createIntervalMinute(int minutePrecision, boolean sign, int minute) throws SQLException
```

- 동작: 주어진 minute 값을 가지고 GoldilocksInterval 객체를 생성한다. minutePrecision은 minute가 가질 수 있는 자릿수를 의미한다. Minute는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: 주어진 minute 값이 minutePrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalMinute(int minutePrecision, String minute) throws SQLException
```

- 동작: 주어진 minute 값을 가지고 GoldilocksInterval 객체를 생성한다. minutePrecision은 minute가 가질 수 있는 자릿수를 의미한다. Minute는 0 이상의 정수 값이어야 한다.
- 예외: 주어진 minute 값이 minutePrecision을 초과하면 에러가 발생한다.

<a id="a5239065d70a95e9"></a>
#### createIntervalSecond

```
public static GoldilocksInterval createIntervalSecond(int secondPrecision, int fractionalPrecision, boolean sign, int second, int microsecond) throws SQLException
```

- 동작: 주어진 second 값을 가지고 GoldilocksInterval 객체를 생성한다. secondPrecision은 second가 가질 수 있는 자릿수를 의미한다. fractionalPrecision은 microsecond가 가질 수 있는 자릿수를 의미한다. Second와 microsecond는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: 주어진 second 값이 secondPrecision을 초과하거나 microSecond 값이 fractionalPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalSecond(int secondPrecision, int fractionalPrecision, boolean sign, int day, int hour, int minute, int second, int microsecond) throws SQLException
```

- 동작: 주어진 day, hour, minute, second, microsecond 값을 가지고 GoldilocksInterval 객체를 생성한다. secondPrecision은 day, hour, minute, second를 second로 환산했을 때 second가 가질 수 있는 자릿수를 의미한다. fractionalPrecision은 microsecond가 가질 수 있는 자릿수를 의미한다. Day, hour, minute, second, microsecond는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: 환산된 second 값이 secondPrecision을 초과하거나 microSecond 값이 fractionalPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalSecond(int secondPrecision, int fractionalPrecision, String second) throws SQLException
```

- 동작: 주어진 second 문자열을 가지고 GoldilocksInterval 객체를 생성한다. secondPrecision은 second가 가질 수 있는 자릿수를 의미한다. fractionalPrecision은 microsecond가 가질 수 있는 자릿수를 의미한다. Second 문자열은 "dd hh:mm:ss.ffffff"나 "dd hh:mm:ss", "dd hh:mm", "dd hh", "hh:mm", "ss.ffffff", "ss" 패턴 중 하나여야 한다.
- 예외: 환산된 second 값이 secondPrecision을 초과하거나 microSecond 값이 fractionalPrecision을 초과하면 에러가 발생한다. 문자열이 정해진 포맷에 적합하지 않을 경우에도 에러가 발생한다.

<a id="2d89dc80bee215fa"></a>
#### createIntervalDayToHour

```
public static GoldilocksInterval createIntervalDayToHour(int dayPrecision, boolean sign, int day, int hour) throws SQLException
```

- 동작: 주어진 day, hour 값을 가지고 GoldilocksInterval 객체를 생성한다. dayPrecision은 day가 가질 수 있는 자릿수를 의미한다. Day, hour는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: Day 값이 dayPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalDayToHour(int dayPrecision, String dayToHour) throws SQLException
```

- 동작: 주어진 dayToHour 문자열을 가지고 GoldilocksInterval 객체를 생성한다. dayPrecision은 day가 가질 수 있는 자릿수를 의미한다. dayToHour는 "dd hh" 포맷을 만족해야 한다. 혹은 "dd hh:mm:ss"와 같은 포맷일 경우, dd, hh 외에는 모두 0이어야 한다.
- 예외: Day 값이 dayPrecision을 초과하거나 주어진 문자열이 포맷을 만족하지 않으면 에러가 발생한다.

<a id="4223ea66cd2e0692"></a>
#### createIntervalDayToMinute

```
public static GoldilocksInterval createIntervalDayToMinute(int dayPrecision, boolean sign, int day, int hour, int minute) throws SQLException
```

- 동작: 주어진 day, hour, minute 값을 가지고 GoldilocksInterval 객체를 생성한다. dayPrecision은 day가 가질 수 있는 자릿수를 의미한다. Day, hour, minute는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: Day 값이 dayPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalDayToMinute(int dayPrecision, String dayToMinute) throws SQLException
```

- 동작: 주어진 dayToMinute 문자열을 가지고 GoldilocksInterval 객체를 생성한다. dayPrecision은 day가 가질 수 있는 자릿수를 의미한다. dayToMinute는 "dd hh:mm" 포맷을 만족해야 한다. 혹은 "dd hh:mm:ss"와 같은 포맷일 경우, dd, hh, mm 외에는 모두 0이어야 한다.
- 예외: Day 값이 dayPrecision을 초과하거나 주어진 문자열이 포맷을 만족하지 않으면 에러가 발생한다.

<a id="233fc20c521930a1"></a>
#### createIntervalDayToSecond

```
public static GoldilocksInterval createIntervalDayToSecond(int dayPrecision, int fractionalPrecision, boolean sign, int day, int hour, int minute, int second, int microsecond) throws SQLException
```

- 동작: 주어진 day, hour, minute, second, microsecond 값을 가지고 GoldilocksInterval 객체를 생성한다. dayPrecision은 day가 가질 수 있는 자릿수를 의미한다. fractionalPrecision은 microsecond가 가질 수 있는 자릿수를 의미한다. Day, hour, minute, second, microsecond는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: Day 값이 dayPrecision을 초과하거나 microsecond 값이 fractionalPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalDayToSecond(int dayPrecision, String dayToSecond) throws SQLException
```

- 동작: 주어진 dayToSecond 문자열을 가지고 GoldilocksInterval 객체를 생성한다. dayPrecision은 day가 가질 수 있는 자릿수를 의미한다. fractionalPrecision은 microsecond가 가질 수 있는 자릿수를 의미한다. dayToSecond는 "dd hh:mm:ss.ffffff", "dd hh:mm:ss", "hh:mm:ss" 또는 "hh:mm" 포맷을 만족해야 한다.
- 예외: Day 값 또는 환산된 day 값이 dayPrecision을 초과하거나 microsecond 값이 fractionalPrecision을 초과하거나 주어진 문자열이 포맷을 만족하지 않을 경우, 에러가 발생한다.

<a id="4bbfa72e4c6281b7"></a>
#### createIntervalHourToMinute

```
public static GoldilocksInterval createIntervalHourToMinute(int hourPrecision, boolean sign, int hour, int minute) throws SQLException
```

- 동작: 주어진 hour, minute 값을 가지고 GoldilocksInterval 객체를 생성한다. hourPrecision은 hour가 가질 수 있는 자릿수를 의미한다. Hour, minute는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: Hour 값이 hourPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalHourToMinute(int hourPrecision, boolean sign, int day, int hour, int minute) throws SQLException
```

- 동작: 주어진 day, hour, minute 값을 가지고 GoldilocksInterval 객체를 생성한다. hourPrecision은 hour가 가질 수 있는 자릿수를 의미한다. Day, hour, minute는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: Hour 값 또는 환산된 hour 값이 이 hourPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalHourToMinute(int hourPrecision, String hourToMinute) throws SQLException
```

- 동작: 주어진 hourToMinute 문자열을 가지고 GoldilocksInterval 객체를 생성한다. hourPrecision은 hour가 가질 수 있는 자릿수를 의미한다. hourToMinute는 "hh:mm"를 만족해야 한다. 다른 포맷일 경우 ss나 ffffff 값은 모두 0이어야 한다.
- 예외: Hour 값 또는 환산된 hour 값이 hourPrecision을 초과하면 에러가 발생한다. 주어진 문자열이 포맷을 만족하지 않아도 에러가 발생한다.

<a id="f5a87157e38c3a5d"></a>
#### createIntervalHourToSecond

```
public static GoldilocksInterval createIntervalHourToSecond(int hourPrecision, int fractionalPrecision, boolean sign, int hour, int minute, int second, int microsecond) throws SQLException
```

- 동작: 주어진 hour, minute, second, microsecond 값을 가지고 GoldilocksInterval 객체를 생성한다. hourPrecision은 hour가 가질 수 있는 자릿수를 의미한다. fractionalPrecision은 microsecond가 가질 수 있는 자릿수를 의미한다. Hour, minute, second, microsecond는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: Hour 값이 hourPrecision을 초과하거나 microsecond 값이 fractionalPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalHourToSecond(int hourPrecision, int fractionalPrecision, boolean sign, int day, int hour, int minute, int second, int microsecond) throws SQLException
```

- 동작: 주어진 day, hour, minute, second, microsecond 값을 가지고 GoldilocksInterval 객체를 생성한다. hourPrecision은 hour가 가질 수 있는 자릿수를 의미한다. fractionalPrecision은 microsecond가 가질 수 있는 자릿수를 의미한다. Day, hour, minute, second, microsecond는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: Hour 값 또는 환산된 hour 값이 hourPrecision을 초과하거나 microsecond 값이 fractionalPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalHourToSecond(int hourPrecision, int fractionalPrecision, String hourToSecond) throws SQLException
```

- 동작: 주어진 hourToSecond 문자열을 가지고 GoldilocksInterval 객체를 생성한다. hourPrecision은 hour가 가질 수 있는 자릿수를 의미한다. fractionalPrecision은 microsecond가 가질 수 있는 자릿수를 의미한다. hourToSecond는 "hh:mm:ss.ffffff", "hh:mm:ss" 또는 "hh:mm" 포맷을 만족해야 한다. dd를 포함할 경우, 환산된 hour 값이 hourPrecision을 초과하면 안된다.
- 예외: Hour 값 또는 환산된 hour 값이 hourPrecision을 초과하거나 microsecond 값이 fractionalPrecision을 초과하거나 주어진 문자열이 포맷을 만족하지 않으면 에러가 발생한다.

<a id="4add99934926ab25"></a>
#### createIntervalMinuteToSecond

```
public static GoldilocksInterval createIntervalMinuteToSecond(int minutePrecision, int fractionalPrecision, boolean sign, int minute, int second, int microsecond) throws SQLException
```

- 동작: 주어진 minute, second, microsecond 값을 가지고 GoldilocksInterval 객체를 생성한다. minutePrecision은 minute가 가질 수 있는 자릿수를 의미한다. fractionalPrecision은 microsecond가 가질 수 있는 자릿수를 의미한다. Minute, second, microsecond는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: Minute 값이 minutePrecision을 초과하거나 microsecond 값이 fractionalPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalMinuteToSecond(int minutePrecision, int fractionalPrecision, boolean sign, int day, int hour, int minute, int second, int microsecond) throws SQLException
```

- 동작: 주어진 day, hour, minute, second, microsecond 값을 가지고 GoldilocksInterval 객체를 생성한다. minutePrecision은 minute가 가질 수 있는 자릿수를 의미한다. fractionalPrecision은 microsecond가 가질 수 있는 자릿수를 의미한다. Day, hour, minute, second, microsecond는 0 이상의 값이어야 한다. Sign은 시간이 양수이면 true이고 음수이면 false이다.
- 예외: Minute 값 또는 환산된 minute 값이 minutePrecision을 초과하거나 microsecond 값이 fractionalPrecision을 초과하면 에러가 발생한다.

```
public static GoldilocksInterval createIntervalMinuteToSecond(int minutePrecision, int fractionalPrecision, String minuteToSecond) throws SQLException
```

- 동작: 주어진 minuteToSecond 문자열을 가지고 GoldilocksInterval 객체를 생성한다. minutePrecision은 minute가 가질 수 있는 자릿수를 의미한다. fractionalPrecision은 microsecond가 가질 수 있는 자릿수를 의미한다. minuteToSecond는 "mm:ss.ffffff"나 "mm:ss" 포맷을 만족해야 한다. dd나 hh를 포함할 경우, 환산된 minute 값이 minutePrecision을 넘으면 안된다.
- 예외: Minute 값 또는 환산된 minute 값이 minutePrecision을 초과하거나 microsecond 값이 fractionalPrecision을 초과하거나 주어진 문자열이 포맷을 만족하지 않을 경우, 에러가 발생한다.

<a id="c6911bfbd6e1d7cc"></a>
#### getSign

```
public int getSign()
```

- 동작: 시간이 양수이면 1을, 음수이면 -1을 반환한다.
- 예외: 발생하지 않는다.

<a id="b20529cce532ce9b"></a>
#### getYear

```
public int getYear()
```

- 동작: Year 값을 반환한다. Interval 객체가 음수인지 여부는 getYear()를 통해 반환되지 않는다.
- 예외: 발생하지 않는다.

<a id="52bc9ac4eac16e33"></a>
#### getMonth

```
public int getMonth()
```

- 동작: Month 값을 반환한다. Interval 객체가 음수인지 여부는 getMonth()를 통해 반환되지 않는다.
- 예외: 발생하지 않는다.

<a id="06859c18a65fe012"></a>
#### getAccumulatedMonth

```
public int getAccumulatedMonth()
```

- 동작: Year와 month를 month로 환산한 값을 반환한다.
- 예외: 발생하지 않는다.

<a id="963eb7c3aaf4b9ee"></a>
#### getDay

```
public int getDay()
```

- 동작: Day 값을 반환한다. Interval 객체가 음수인지 여부는 getDay()를 통해 반환되지 않는다.
- 예외: 발생하지 않는다.

<a id="8d723366bbde42b6"></a>
#### getHour

```
public int getHour()
```

- 동작: Hour 값을 반환한다. Interval 객체가 음수인지 여부는 getHour()를 통해 반환되지 않는다.
- 예외: 발생하지 않는다.

<a id="aa2f5b69cab175e2"></a>
#### getAccumulatedHour

```
public int getAccumulatedHour()
```

- 동작: Day와 hour를 hour로 환산한 값을 반환한다.
- 예외: 발생하지 않는다.

<a id="8991bbe25f345e00"></a>
#### getMinute

```
public int getMinute()
```

- 동작: Minute 값을 반환한다. Interval 객체가 음수인지 여부는 getMinute()를 통해 반환되지 않는다.
- 예외: 발생하지 않는다.

<a id="aa37a11c2b9a0754"></a>
#### getAccumulatedMinute

```
public int getAccumulatedMinute()
```

- 동작: Day, hour, minute를 minute로 환산한 값을 반환한다.
- 예외: 발생하지 않는다.

<a id="215cbfb350b3dfb1"></a>
#### getSecond

```
public int getSecond()
```

- 동작: Second 값을 반환한다. Interval 객체가 음수인지 여부는 getSecond()를 통해 반환되지 않는다.
- 예외: 발생하지 않는다.

<a id="379886b2e6225193"></a>
#### getAccumulatedSecond

```
public int getAccumulatedSecond()
```

- 동작: Day, hour, minute, second를 second로 환산한 값을 반환한다.
- 예외: 발생하지 않는다.

<a id="f8f94a486be275f2"></a>
#### getMicroSecond

```
public int getMicroSecond()
```

- 동작: Microsecond 값을 반환한다. Interval 객체의 음수 여부는 getMicroSecond()를 통해 반환되지 않는다.
- 예외: 발생하지 않는다.

<a id="e040927895f0cac5"></a>
#### getAccumulatedMicroSecond

```
public long getAccumulatedMicroSecond()
```

- 동작: Day, hour, minute, second, microsecond를 microsecond로 환산한 값을 반환한다.
- 예외: 발생하지 않는다.

<a id="b5cc6714a739ec52"></a>
#### getTypeName

```
public String getTypeName()
```

- 동작: 타입 이름을 반환한다.
- 예외: 발생하지 않는다.

<a id="ca61f5bf3185fe96"></a>
#### getSqlType

```
public int getSqlType()
```

- 동작: 이 객체에 해당되는 타입을 GoldilocksTypes에 정의된 타입 상수로 반환한다.
- 예외: 발생하지 않는다.

<a id="af953b53603a2cb4"></a>
#### toString

```
public String toString()
```

- 동작: 이 객체가 나타내는 interval 값을 문자열로 반환한다.
- 예외: 발생하지 않는다.

<a id="8de46581f9864c53"></a>
### GOLDILOCKS Type

<a id="ab66adc722fc61e0"></a>
#### 상수 정의

```
public static final int INTERVAL_YEAR;
public static final int INTERVAL_MONTH;
public static final int INTERVAL_DAY;
public static final int INTERVAL_HOUR;
public static final int INTERVAL_MINUTE;
public static final int INTERVAL_SECOND;
public static final int INTERVAL_YEAR_TO_MONTH;
public static final int INTERVAL_DAY_TO_HOUR;
public static final int INTERVAL_DAY_TO_MINUTE;
public static final int INTERVAL_DAY_TO_SECOND;
public static final int INTERVAL_HOUR_TO_MINUTE;
public static final int INTERVAL_HOUR_TO_SECOND;
public static final int INTERVAL_MINUTE_TO_SECOND;
public static final int TIME_WITH_TIME_ZONE;
public static final int TIMESTAMP_WITH_TIME_ZONE;
```

이 상수들은 java.sql.Types의 상수처럼 사용된다. 즉, PreparedStatement의 setObject나 ResultSet의 getObject에 타입을 명시할 때 사용된다. 이 타입들은 JDBC 표준에는 정의되어 있지 않으므로 GoldilocksTypes를 통해 별도로 제공된다.

<a id="c96e8c51732ba82e"></a>
### 타입 변환

다음 표는 타입 변환 방법을 설명한다.

**SQL 타입 → GOLDILOCKS 타입**

<a id="e234a5c29f761940"></a>
| SQL 타입 | GOLDILOCKS 타입 |
| --- | --- |
| Types.BIGINT | NATIVE_BIGINT |
| Types.BINARY | BINARY(2000) |
| Types.BIT | BOOLEAN |
| Types.BOOLEAN | BOOLEAN |
| Types.BLOB | N/A |
| Types.CHAR | CHAR(2000) |
| Types.CLOB | N/A |
| Types.DATE | DATE |
| Types.DECIMAL | DECIMAL |
| Types.DOUBLE | NATIVE_DOUBLE |
| Types.FLOAT | FLOAT |
| Types.NUMERIC | NUMBER |
| Types.INTEGER | NATIVE_INTEGER |
| Types.LONGVARBINARY | LONG VARBINARY |
| Types.LONGVARCHAR | LONG VARCHAR |
| Types.REAL | NATIVE_REAL |
| Types.ROWID | ROWID |
| Types.SMALLINT | NATIVE_SMALLINT |
| Types.TIME | TIME |
| Types.TIMESTAMP | TIMESTAMP |
| Types.VARBINARY | VARBINARY(4000) |
| Types.VARCHAR | VARCHAR(4000) |
| GoldilocksTypes.INTERVAL_YEAR | INTERVAL YEAR |
| GoldilocksTypes.INTERVAL_MONTH | INTERVAL MONTH |
| GoldilocksTypes.INTERVAL_YEAR_TO_MONTH | INTERVAL YEAR TO MONTH |
| GoldilocksTypes.INTERVAL_DAY | INTERVAL DAY |
| GoldilocksTypes.INTERVAL_HOUR | INTERVAL HOUR |
| GoldilocksTypes.INTERVAL_MINUTE | INTERVAL MINUTE |
| GoldilocksTypes.INTERVAL_SECOND | INTERVAL SECOND |
| GoldilocksTypes.INTERVAL_DAY_TO_HOUR | INTERVAL DAY TO HOUR |
| GoldilocksTypes.INTERVAL_DAY_TO_MINUTE | INTERVAL DAY TO MINUTE |
| GoldilocksTypes.INTERVAL_DAY_TO_SECOND | INTERVAL DAY TO SECOND |
| GoldilocksTypes.INTERVAL_HOUR_TO_MINUTE | INTERVAL HOUR TO MINUTE |
| GoldilocksTypes.INTERVAL_HOUR_TO_SECOND | INTERVAL HOUR TO SECOND |
| GoldilocksTypes.INTERVAL_MINUTE_TO_SECOND | INTERVAL MINUTE TO SECOND |
| Types.OTHER | N/A |
| Types.ARRAY | N/A |
| Types.DATALINK | N/A |
| Types.DISTINCT | N/A |
| Types.NCHAR | N/A |
| Types.NCLOB | N/A |
| Types.NVARCHAR | N/A |
| Types.JAVA_OBJECT | N/A |
| Types.REF | N/A |
| Types.SQLXML | N/A |
| Types.STRUCT | N/A |

**GOLDILOCKS 타입에 대한 getter method 지원 여부-1**

<a id="26907a2b935b9548"></a>
|  | NATIVE_SMALLINT | NATIVE_INTEGER | NATIVE_BIGINT | NATIVE_REAL | NATIVE_DOUBLE |
| --- | --- | --- | --- | --- | --- |
| getByte | O | O | O | O | O |
| getShort | O | O | O | O | O |
| getInt | O | O | O | O | O |
| getLong | O | O | O | O | O |
| getFloat | O | O | O | O | O |
| getDouble | O | O | O | O | O |
| getBigDecimal | O | O | O | O | O |
| getBoolean | 0,1일 경우만 가능 | 0,1일 경우만 가능 | 0,1일 경우만  가능 | 0,1일 경우만 가능 | 0,1일 경우만 가능 |
| getString | O | O | O | O | O |
| getBytes | raw 데이터 | raw 데이터 | raw 데이터 | raw 데이터 | raw 데이터 |
| getDate | X | X | X | X | X |
| getTime | X | X | X | X | X |
| getTimestamp | X | X | X | X | X |
| getAsciiStream | raw 데이터 | raw 데이터 | raw 데이터 | raw 데이터 | raw 데이터 |
| getBinaryStream | raw 데이터 | raw 데이터 | raw 데이터 | raw 데이터 | raw 데이터 |
| getCharacterStream | X | X | X | X | X |
| getClob | X | X | X | X | X |
| getBlob | X | X | X | X | X |
| getArray | X | X | X | X | X |
| getRef | X | X | X | X | X |
| getURL | X | X | X | X | X |
| getObject | Short | Integer | Long | Float | Double |
| getRowId | X | X | X | X | X |

**GOLDILOCKS 타입에 대한 getter method 지원 여부-2**

<a id="a8636064ea2285ea"></a>
|  | BOOLEAN | FLOAT/ NUMBER | CHAR/ VARCHAR/ LONG VARCHAR | BINARY/ VARBINARY/LONG VARBINARY | ROWID |
| --- | --- | --- | --- | --- | --- |
| getByte | 0 or 1 | O | 숫자일 경우만  가능 | X | X |
| getShort | 0 or 1 | O | 숫자일 경우만  가능 | X | X |
| getInt | 0 or 1 | O | 숫자일 경우만  가능 | X | X |
| getLong | 0 or 1 | O | 숫자일 경우만 가능 | X | X |
| getFloat | 0 or 1 | O | 숫자일 경우만  가능 | X | X |
| getDouble | 0 or 1 | O | 숫자일 경우만  가능 | X | X |
| getBigDecimal | 0 or 1 | O | 숫자일 경우만  가능 | X | X |
| getBoolean | O | 0,1일 경우만 가능 | "t", "f", "true", "false", "y", "n", "yes", "no", "on", "off", "1", "0" 일 경우만 가능(대소문자구별안함) | X | X |
| getString | "TRUE" or "FALSE" | O | O | O | O |
| getBytes | raw 데이터 | raw 데이터 | raw 데이터 | O | raw 데이터 |
| getDate | X | X | Date format일 경우만 가능 | X | X |
| getTime | X | X | Time format일 경우만 가능 | X | X |
| getTimestamp | X | X | Timestamp format일 경우만 가능 | X | X |
| getAsciiStream | raw 데이터 | raw 데이터 | raw 데이터 | O | raw 데이터 |
| getBinaryStream | raw 데이터 | raw 데이터 | raw 데이터 | O | raw 데이터 |
| getCharacterStream | X | X | O | X | X |
| getClob | X | X | X | X | X |
| getBlob | X | X | X | X | X |
| getArray | X | X | X | X | X |
| getRef | X | X | X | X | X |
| getURL | X | X | X | X | X |
| getObject | Boolean | BigDecimal | String | byte[] | RowId |
| getRowId | X | X | X | X | O |

**GOLDILOCKS 타입에 대한 getter method 지원 여부-3**

<a id="d45c04eff6cb5ebb"></a>
|  | DATE | TIME/ TIME WITH TIME ZONE | TIMESTAMP/ TIMESTAMP WITH TIME ZONE | INTERVAL |
| --- | --- | --- | --- | --- |
| getByte | X | X | X | 단일 항목 타입만 가능 |
| getShort | X | X | X | 단일 항목 타입만 가능 |
| getInt | X | X | X | 단일 항목 타입만 가능 |
| getLong | X | X | X | 단일 항목 타입만 가능 |
| getFloat | X | X | X | 단일 항목 타입만 가능 |
| getDouble | X | X | X | 단일 항목 타입만 가능 |
| getBigDecimal | X | X | X | 단일 항목 타입만 가능 |
| getBoolean | X | X | X | X |
| getString | O | O | O | O |
| getBytes | raw 데이터 | raw 데이터 | raw 데이터 | raw 데이터 |
| getDate | O | O | O | X |
| getTime | O | O | O | X |
| getTimestamp | O | O | O | X |
| getAsciiStream | raw 데이터 | raw 데이터 | raw 데이터 | raw 데이터 |
| getBinaryStream | raw 데이터 | raw 데이터 | raw 데이터 | raw 데이터 |
| getCharacterStream | X | X | X | X |
| getClob | X | X | X | X |
| getBlob | X | X | X | X |
| getArray | X | X | X | X |
| getRef | X | X | X | X |
| getURL | X | X | X | X |
| getObject | Date | Time | Timestamp | GoldilocksInterval |
| getRowId | X | X | X | X |

---

[← 25. ODBC](25-odbc.md) · [전체 목차](../README.md) · [27. Embedded SQL →](27-embedded-sql.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
