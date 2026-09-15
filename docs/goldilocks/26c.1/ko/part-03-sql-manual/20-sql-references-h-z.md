<a id="6e846b2106373ae4"></a>

# 20. SQL References (H~Z)

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/6e846b2106373ae4)  
> 태그: `26c.1_0_tag`

[← 19. SQL References (C~G)](19-sql-references-c-g.md) · [전체 목차](../README.md) · [21. Overview of PSM →](../part-04-sql-psm-manual/21-overview-of-psm.md)

<a id="4b00ba4f4c0eed30"></a>
## INSERT INTO

<a id="0cee2f512080e0ee"></a>
### 기능

테이블에 새로운 row들을 생성한다.

<a id="fc99743a3c8bacfa"></a>
### 구문

```
<insert statement> ::=
    INSERT [ /*+ <append insert hint clause> */ ]
        INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
    ;

<append insert hint clause> ::=
    APPEND [ ( append insert option element [, ...] ) ]

<append insert option element> ::=
      PARALLEL [NOLOGGING]
    | STATEMENT_NOFORCE
    | <index maintenance options>

<insert maintenance options> ::=
      IMMEDIATE_INDEX_MAINTENANCE
    | DEFERRED_INDEX_MAINTENANCE
    | SKIP_INDEX_MAINTENANCE

<insert source> ::=
      <values clause>
    | <from subquery>
    | <from default>

<values clause> ::=
    VALUES { ( { <value expression> | DEFAULT } [, ...] ) } [, ...]

<from subquery> ::=
    <query expression>

<from default> ::=
    DEFAULT VALUES
```

<a id="23a5e5a14963bb48"></a>
### 사용 범위 및 접근 권한

&lt;insert statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- INSERT 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Insert 대상이 되는 모든 column에 대해 INSERT(columns) ON TABLE 
    - 테이블에 대해 (INSERT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (INSERT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - INSERT ANY TABLE ON DATABASE

- &lt;from subquery&gt;를 사용할 경우, 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="b577448375082241"></a>
### 구문 규칙 및 파라미터

<a id="a8ff253928fe36fe"></a>
#### &lt;append insert hint clause&gt;

APPEND INSERT 방식으로 데이터를 추가하도록 지정하는 힌트이다.

- APPEND
    - APPEND INSERT를 사용하기 위한 힌트이다.

<a id="074b8737bea45d9d"></a>
#### &lt;append insert option element&gt;

APPEND INSERT 방식으로 데이터를 추가할 때 사용할 수 있는 옵션이다. 만약 사용자가 기술한 옵션을 사용할 수 없는 경우 insert statement는 실패한다.

- PARALLEL
    - 여러 세션에서 동시에 APPEND INSERT를 수행하기 위한 옵션이다.
    - PARALLEL 옵션을 지정하지 않으면 APPEND INSERT는 serial 방식으로 수행된다.
- NOLOGGING
    - PARALLEL 옵션과 함께 사용되며, 데이터 추가 과정에서 생성되는 로그 기록을 최소화 한다.
- STATEMENT_NOFORCE
    - Statement가 완료될 때 사용한 페이지를 디스크에 반영하는 작업을 동기화하지 않는다.
    - STATEMENT_NOFORCE 옵션을 지정하지 않으면 사용한 페이지를 디스크에 반영한 후 statement가 완료된다.

<a id="1d7f9413dcb680b5"></a>
#### &lt;index maintenance options&gt;

APPEND INSERT 방식으로 데이터를 추가할 때 사용할 수 있는 인덱스 관리 옵션이다.

- IMMEDIATE_INDEX_MAINTENANCE
    - 테이블에 레코드가 입력되는 즉시 인덱스에 반영한다.
    - 인덱스의 무결성 제약을 만족하지 못하면 statement는 실패한다.
    - PARALLEL 옵션과 함께 사용할 수 없다.
- DEFERRED_INDEX_MAINTENANCE
    - APPEND INSERT를 수행한 트랜잭션이 완료될 때 인덱스에 일괄적으로 반영한다.
    - 인덱스 반영 과정에서 저장 공간이 부족하거나 인덱스 무결성이 손상될 경우 해당 인덱스를 unusable 세그먼트로 설정한다.
- SKIP_INDEX_MAINTENANCE
    - APPEND INSERT를 수행한 트랜잭션이 완료될 때 테이블에 생성된 모든 인덱스를 unusable 세그먼트로 설정한다.

<a id="6aa9fb52b17803c9"></a>
#### table_name

Row를 생성할 대상 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="0baa7f6b0f6d0b71"></a>
#### [ ( column_name [, ...] ) ]

테이블의 column 이름이다.   
Column 리스트는 생략할 수 있다.   
Column의 개수와 &lt;insert source&gt; 값의 개수는 동일해야 하며, 생략된 column에는 DEFAULT 값을 할당한다.

<a id="8f02f842a9de9138"></a>
#### &lt;values clause&gt;

대응하는 column에 할당할 값의 리스트이다.

- &lt;value expression&gt; 
    - 대응하는 column에 할당할 값이나 연산식이다. 
- DEFAULT 
    - 대응하는 column의 값은 [CREATE TABLE](19-sql-references-c-g.md#ce6ecbcf1ea593ea) 구문을 통해 정의한 기본값을 사용한다. 
    - 정의하지 않았을 경우 NULL 값이 할당된다.

다음과 같이 다수의 row를 생성할 수 있다.

```
INSERT INTO table_name VALUES ( 1, 'A' ), ( 2, 'B' ), ( 3, 'C' )
```

<a id="d868e696e9cf8138"></a>
#### &lt;from subquery&gt;

Row들을 생성할 질의이다.  
자세한 내용은 [SELECT](#2070458035e417b9) 구문의 [query expression](#f971bccfc0bcab55) 절을 참조한다.

<a id="161e12e5dc743cce"></a>
#### DEFAULT VALUES

모든 column들을 기본값으로 채운다.

DEFAULT VALUES 절은 다음과 같은 의미이다.

```
VALUES ( DEFAULT, DEFAULT, ..., DEFAULT )
```

<a id="29f774699d5debe6"></a>
### 설명

<a id="dbb1379de8f145b6"></a>
#### INSERT 관련 구문들의 차이점

- [INSERT INTO](#4b00ba4f4c0eed30)
    - 테이블에 하나 또는 다수의 row를 생성한다. 
    - 예: INSERT INTO t1 SELECT * FROM t1; 
- [INSERT INTO name RETURNING](#c73c45a86ae5a183)
    - 테이블에 하나 또는 다수의 row를 생성하고, 생성한 row들을 SELECT 구문과 동일한 방식 (SQLFetch() 등의 API)으로 검색할 수 있다. 
    - 예: INSERT INTO t1 SELECT * FROM t1 RETURNING c1; 
- [INSERT INTO name RETURNING .. INTO](#995e5aa709d17272)
    - 한 건 이하의 row를 생성할 수 있으며, 생성한 row가 한 건일 경우 RETURNING INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: INSERT INTO t1 DEFAULT VALUES RETURNING c1 INTO :v1;

<a id="fd0a3b11264b0239"></a>
### 사용 예

다음은 INSERT 구문을 이용해 row 하나를 생성하는 예이다.

```
gSQL> INSERT INTO region VALUES ( 0, 'AFRICA' );

1 row created.
```

다음은 INSERT 구문에서 column의 DEFAULT 값 또는 identity 값을 사용하는 예이다.

```
gSQL> CREATE TABLE region
(
    r_regionkey   BIGINT    GENERATED BY DEFAULT AS IDENTITY
  , r_name        CHAR(25)  DEFAULT 'N/A'
);

Table created.

gSQL> COMMIT;

Commit complete.
```

- 모든 column을 DEFAULT로 입력한다.

```
gSQL> INSERT INTO region DEFAULT VALUES;

1 row created.
```

- 모든 column을 DEFAULT로 입력한다.

```
gSQL> INSERT INTO region VALUES (DEFAULT, DEFAULT);

1 row created.
```

- Column이 생략된 경우 r_name column의 DEFAULT 값을 사용한다.

```
gSQL> INSERT INTO region(r_regionkey) VALUES (-100);

1 row created.
```

- Column이 생략된 경우 r_regionkey column의 identity 값을 사용한다.

```
gSQL> INSERT INTO region(r_name) VALUES ('ASIA');

1 row created.


gSQL> SELECT * FROM region;

R_REGIONKEY R_NAME                   
----------- -------------------------
          1 N/A                      
          2 N/A                      
       -100 N/A                      
          3 ASIA                     

4 rows selected.
```

다음은 VALUES 구문에 다수의 row를 기술하여 생성하는 예이다.

```
gSQL> INSERT INTO region
       VALUES ( 1, 'AFRICA' ),
              ( 2, 'ASIA'   ),
              ( 3, 'EUROPE' );

3 rows created.
```

다음은 subquery를 사용하여 다수의 row를 생성하는 예이다.

```
gSQL> INSERT INTO region SELECT r_regionkey, r_name FROM tmp_region WHERE r_regionkey < 3;

3 rows created.
```

<a id="e72eb9479595ffab"></a>
### 호환성

**SQL 표준 호환성**

<a id="766a43dd88fd0575"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| F222 | INSERT statement: DEFAULT VALUES clause | O |
| S204 | Enhanced structured types | X |
| S043 | Enhanced reference types | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="7b53ec1f21a8658e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [SELECT](#2070458035e417b9)
- [INSERT INTO name RETURNING](#c73c45a86ae5a183)
- [INSERT INTO name RETURNING .. INTO](#995e5aa709d17272)

<a id="c73c45a86ae5a183"></a>
## INSERT INTO name RETURNING

<a id="d56715b44d77205d"></a>
### 기능

테이블에 새로운 row를 생성하고, 생성한 row들을 검색한다.

<a id="1689295a43c8db1a"></a>
### 구문

```
<insert statement> ::=
    INSERT [ /*+ <append insert hint clause> */ ]
        INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
        <returning clause>
    ;

<append insert hint clause> ::=
    APPEND [ ( append insert option element [, ...] ) ]

<append insert option element> ::=
      PARALLEL [NOLOGGING]
    | STATEMENT_NOFORCE
    | <index maintenance options>

<insert maintenance options> ::=
      IMMEDIATE_INDEX_MAINTENANCE
    | DEFERRED_INDEX_MAINTENANCE
    | SKIP_INDEX_MAINTENANCE

<insert source> ::=
      <values clause>
    | <from subquery>
    | <from default>

<values clause> ::=
    VALUES { ( { <value expression> | DEFAULT } [, ...] ) } [, ...]

<from subquery> ::=
    <query expression>

<from default> ::=
    DEFAULT VALUES

<returning clause> ::=
      [ RETURN | RETURNING ] { * | { <value expression> [ [AS] alias_name ] } [, ...]
```

<a id="0814991eaf920fa2"></a>
### 사용 범위 및 접근 권한

&lt;insert returning query statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- INSERT 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Insert 대상이 되는 모든 column에 대해 INSERT(columns) ON TABLE 
    - 테이블에 대해 (INSERT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (INSERT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - INSERT ANY TABLE ON DATABASE

- &lt;from subquery&gt;를 사용할 경우, 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="06e82bcbb2bc7dc8"></a>
### 구문 규칙 및 파라미터

<a id="f6007bdb0b4453ad"></a>
#### &lt;append insert hint clause&gt;

APPEND INSERT 방식으로 데이터를 추가하도록 지정하는 힌트이다.

- APPEND
    - APPEND INSERT를 사용하기 위한 힌트이다.

<a id="ebe3260e459d41f1"></a>
#### &lt;append insert option element&gt;

APPEND INSERT 방식으로 데이터를 추가할 때 사용할 수 있는 옵션이다. 만약 사용자가 기술한 옵션을 사용할 수 없는 경우 insert statement는 실패한다.

- PARALLEL
    - 여러 세션에서 동시에 APPEND INSERT를 수행하기 위한 옵션이다.
    - PARALLEL 옵션을 지정하지 않으면 APPEND INSERT는 serial 방식으로 수행된다.
- NOLOGGING
    - PARALLEL 옵션과 함께 사용되며, 데이터 추가 과정에서 생성되는 로그 기록을 최소화 한다.
- STATEMENT_NOFORCE
    - Statement가 완료될 때 사용한 페이지를 디스크에 반영하는 작업을 동기화하지 않는다.
    - STATEMENT_NOFORCE 옵션을 지정하지 않으면 사용한 페이지를 디스크에 반영한 후 statement가 완료된다.

<a id="d9a9db16673498a7"></a>
#### &lt;index maintenance options&gt;

APPEND INSERT 방식으로 데이터를 추가할 때 사용할 수 있는 인덱스 관리 옵션이다.

- IMMEDIATE_INDEX_MAINTENANCE
    - 테이블에 레코드가 입력되는 즉시 인덱스에 반영한다.
    - 인덱스의 무결성 제약을 만족하지 못하면 statement는 실패한다.
    - PARALLEL 옵션과 함께 사용할 수 없다.
- DEFERRED_INDEX_MAINTENANCE
    - APPEND INSERT를 수행한 트랜잭션이 완료될 때 인덱스에 일괄적으로 반영한다.
    - 인덱스 반영 과정에서 저장 공간이 부족하거나 인덱스 무결성이 손상될 경우 해당 인덱스를 unusable 세그먼트로 설정한다.
- SKIP_INDEX_MAINTENANCE
    - APPEND INSERT를 수행한 트랜잭션이 완료될 때 테이블에 생성된 모든 인덱스를 unusable 세그먼트로 설정한다.

<a id="ad71b511a9796968"></a>
#### table_name

Row를 생성할 대상 테이블의 이름이다.

<a id="681a9102b0d9e4d6"></a>
#### [ ( column_name [, ...] ) ]

테이블의 column 이름이다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문을 참조한다.

<a id="d993f7705a6d7b0c"></a>
#### &lt;values clause&gt;

대응하는 column에 할당할 값의 리스트이다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문을 참조한다.

<a id="74982ecfbca82676"></a>
#### &lt;from subquery&gt;

Row들을 생성할 질의이다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문을 참조한다.

<a id="4383030bbc5c5ae4"></a>
#### DEFAULT VALUES

모든 column들을 기본값으로 채운다.   
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문을 참조한다.

<a id="fdd001ca80a447d1"></a>
#### &lt;returning clause&gt;

INSERT 된 row들을 반환한다.

- 생성된 row들을 결과 집합으로 하고, 이들 중 검색할 column을 기술한다. 
    - RETURNING 절은 INSERT 구문으로 삽입된 row들을 결과 집합으로 하는 결과를 반환한다. 
    - &lt;value expression&gt; 
        - SELECT 구문의 &lt;select list&gt;와 동일하지만 aggregation 등을 사용할 수 없다. 
    - [[AS] alias_name] 
        - AS 절을 사용하여 value expression의 이름을 지정할 수 있다.

RETURN과 RETURNING은 동일한 의미의 키워드이다.

<a id="b4a9c515080ef37f"></a>
### 설명

자세한 내용은 [INSERT 관련 구문들의 차이점](#dbb1379de8f145b6)을 참조한다.

<a id="3c2cab7ae1e555f2"></a>
### 사용 예

다음은 INSERT 구문으로 생성된 column 값을 검색하는 예이다.

```
gSQL> CREATE TABLE region
(
    r_regionkey   BIGINT    GENERATED BY DEFAULT AS IDENTITY
  , r_name        CHAR(25)  DEFAULT 'N/A'
);

Table created.

gSQL> COMMIT;

Commit complete.
```

- 생성된 DEFAULT 값을 RETURNING 하는 경우

```
gSQL> INSERT INTO region VALUES ( DEFAULT, DEFAULT ) RETURNING r_regionkey, r_name;

R_REGIONKEY R_NAME                   
----------- -------------------------
          1 N/A                      

1 row created.
```

- 생략된 column의 값을 RETURNING 하는 경우

```
gSQL> INSERT INTO region(r_name) VALUES ('ASIA') RETURNING r_regionkey;

R_REGIONKEY
-----------
          2

1 row created.
```

다음은 subquery로부터 생성된 row들을 검색하는 예이다.

```
gSQL> INSERT INTO region 
      SELECT r_regionkey, r_name FROM tmp_region WHERE r_regionkey < 3 
      RETURNING r_regionkey, r_name;

R_REGIONKEY R_NAME                   
----------- -------------------------
          0 AFRICA                   
          1 AMERICA                  
          2 ASIA                     

3 rows created.
```

<a id="00cbc8d05e970b15"></a>
### 호환성

SQL 표준에서는 &lt;insert returning query statement&gt; 구문을 정의하지 않고 있다.

<a id="5f8549a6e68b0bab"></a>
### 참조

관련 내용은 다음을 참조한다.

- [INSERT INTO](#4b00ba4f4c0eed30)
- [INSERT INTO name RETURNING .. INTO](#995e5aa709d17272)

<a id="995e5aa709d17272"></a>
## INSERT INTO name RETURNING .. INTO

<a id="887097ca88d24f3e"></a>
### 기능

테이블에 row 하나를 생성하고, 생성한 row의 값을 호스트 변수로 얻어온다.

<a id="e2c3f7e736cd983b"></a>
### 구문

```
<insert statement> ::=
    INSERT [ /*+ <append insert hint clause> */ ]
        INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
        <returning into clause>
    ;

<append insert hint clause> ::=
    APPEND [ ( append insert option element [, ...] ) ]

<append insert option element> ::=
      PARALLEL [NOLOGGING]
    | STATEMENT_NOFORCE
    | <index maintenance options>

<insert maintenance options> ::=
      IMMEDIATE_INDEX_MAINTENANCE
    | DEFERRED_INDEX_MAINTENANCE
    | SKIP_INDEX_MAINTENANCE

<insert source> ::=
      <values clause>
    | <from subquery>
    | <from default>

<values clause> ::=
    VALUES { ( { <value expression> | DEFAULT } [, ...] ) } [, ...]

<from subquery> ::=
    <query expression>

<from default> ::=
    DEFAULT VALUES

<returning into clause> ::=
      [ RETURN | RETURNING ] { * | { <value expression> [ [AS] alias_name ] } [, ...] INTO variable_name [, ...]
```

<a id="fd8a1701fba47ac5"></a>
### 사용 범위 및 접근 권한

&lt;insert returning into statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- INSERT 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Insert 대상이 되는 모든 column에 대해 INSERT(columns) ON TABLE 
    - 테이블에 대해 (INSERT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (INSERT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - INSERT ANY TABLE ON DATABASE

- &lt;from subquery&gt;를 사용할 경우, 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="58e1e6ae295afb4a"></a>
### 구문 규칙 및 파라미터

<a id="b6d3853ed6cf30a4"></a>
#### &lt;append insert hint clause&gt;

APPEND INSERT 방식으로 데이터를 추가하도록 지정하는 힌트이다.

- APPEND
    - APPEND INSERT를 사용하기 위한 힌트이다.

<a id="fb6f8aa2fc630d29"></a>
#### &lt;append insert option element&gt;

APPEND INSERT 방식으로 데이터를 추가할 때 사용할 수 있는 옵션이다. 만약 사용자가 기술한 옵션을 사용할 수 없는 경우 insert statement는 실패한다.

- PARALLEL
    - 여러 세션에서 동시에 APPEND INSERT를 수행하기 위한 옵션이다.
    - PARALLEL 옵션을 지정하지 않으면 APPEND INSERT는 serial 방식으로 수행된다.
- NOLOGGING
    - PARALLEL 옵션과 함께 사용되며, 데이터 추가 과정에서 생성되는 로그 기록을 최소화 한다.
- STATEMENT_NOFORCE
    - Statement가 완료될 때 사용한 페이지를 디스크에 반영하는 작업을 동기화하지 않는다.
    - STATEMENT_NOFORCE 옵션을 사용하지 않은 경우 사용한 페이지에 대한 디스크 반영이 완료되어야 statement 완료된다.

<a id="58c9286c34900487"></a>
#### &lt;index maintenance options&gt;

APPEND INSERT 방식으로 데이터를 추가할 때 사용할 수 있는 인덱스 관리 옵션이다.

- IMMEDIATE_INDEX_MAINTENANCE
    - 테이블에 레코드가 입력되는 즉시 인덱스에 반영한다.
    - 인덱스의 무결성 제약을 만족하지 못하면 statement는 실패한다.
    - PARALLEL 옵션과 함께 사용할 수 없다.
- DEFERRED_INDEX_MAINTENANCE
    - APPEND INSERT를 수행한 트랜잭션이 완료될 때 인덱스에 일괄적으로 반영한다.
    - 인덱스 반영 과정에서 저장 공간이 부족하거나 인덱스 무결성이 손상될 경우 해당 인덱스를 unusable 세그먼트로 설정한다.
- SKIP_INDEX_MAINTENANCE
    - APPEND INSERT를 수행한 트랜잭션이 완료될 때 테이블에 생성된 모든 인덱스를 unusable 세그먼트로 설정한다.

<a id="2e56b53322b609ee"></a>
#### table_name

Row를 생성할 대상 테이블의 이름이다.

<a id="118abdc34e4773db"></a>
#### [ ( column_name [, ...] ) ]

테이블의 column 이름이다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문을 참조한다.

<a id="11fbba19e04c0fc8"></a>
#### &lt;values clause&gt;

대응하는 column에 할당할 값의 리스트이다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문을 참조한다.

<a id="ce62910a4024b66b"></a>
#### &lt;from subquery&gt;

Row들을 생성할 질의이다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문을 참조한다.

<a id="40409cae796f954c"></a>
#### DEFAULT VALUES

모든 column들을 기본값으로 채운다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문을 참조한다.

<a id="c94dd0758d08dd88"></a>
#### &lt;returning clause&gt;

INSERT 된 row를 반환한다.  
자세한 내용은 [INSERT INTO name RETURNING](#c73c45a86ae5a183) 구문의 &lt;[returning clause&gt;](#fdd001ca80a447d1) 절을 참조한다.

<a id="3c5ed0e1478b7481"></a>
##### INTO variable_name [, ...]

INTO 절에 기술된 변수의 개수는 RETURNING 절에 기술된 expression의 개수와 동일해야 한다.   
생성할 row가 한 건 이하여야 한다. Row가 두 건 이상 생성될 경우, 에러가 발생한다.

<a id="7c2d6352b2871587"></a>
### 설명

자세한 내용은 [INSERT 관련 구문들의 차이점](#dbb1379de8f145b6)을 참조한다.

<a id="c3a277d5824edf3b"></a>
### 사용 예

다음은 생성된 row의 값을 호스트 변수에 얻어오는 예이다.

```
gSQL> CREATE TABLE region
(
    r_regionkey   BIGINT    GENERATED BY DEFAULT AS IDENTITY
  , r_name        CHAR(25)  DEFAULT 'N/A'
);

Table created.

gSQL> COMMIT;

Commit complete.
```

- 호스트 변수들을 선언한다.

```
\VAR v_key  BIGINT
\VAR v_name VARCHAR(128)
```

- 생성된 DEFAULT 값을 호스트 변수로 얻어오는 경우

```
gSQL> INSERT INTO region 
      VALUES ( DEFAULT, DEFAULT ) 
      RETURNING r_regionkey, r_name 
      INTO :v_key, :v_name;

V_KEY V_NAME                   
----- -------------------------
    1 N/A                      

1 row created.
```

- 생략된 column의 값을 호스트 변수에 얻어오는 경우

```
gSQL> INSERT INTO region(r_name) 
      VALUES ('ASIA') 
      RETURNING r_regionkey 
      INTO :v_key;

V_KEY
-----
    2

1 row created.
```

<a id="69ca1e8c21279d03"></a>
### 호환성

SQL 표준에서는 &lt;insert returning into statement&gt; 구문을 정의하지 않고 있다.

<a id="3158b2349f4dec35"></a>
### 참조

관련 내용은 다음을 참조한다.

- [INSERT INTO](#4b00ba4f4c0eed30)
- [INSERT INTO name RETURNING](#c73c45a86ae5a183)

<a id="b41e8eea9acdd98a"></a>
## INSERT INTO name ... UPDATE

<a id="32062506f9cdeeec"></a>
### 기능

테이블에 새로운 row들을 생성한다. 만약 unique 제약 조건에 위배될 경우에는 기존 row들을 갱신한다.

<a id="6a881459abcc1fd6"></a>
### 구문

```
<upsert statement> ::=
    INSERT INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
        <duplicate key clause>
    ;

<insert source> ::=
      <values clause>
    | <from subquery>
    | DEFAULT VALUES

<values clause> ::=
    VALUES { ( { <value expression> | DEFAULT } [, ...] ) } [, ...]

<from subquery> ::=
    <query expression>

<duplicate key clause>
    ON DUPLICATE KEY { DO NOTHING | <do update clause> }

<do update clause> ::=
    [DO] UPDATE [SET] <set clause>  [, ...]

<set value clause> ::= 
      <value expression>
    | DEFAULT
    | VALUES( column_name )

<set clause> ::=
      column_name = <set value clause>
    | ( column_name [, ...] ) = ( <set value clause> [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )
```

<a id="ba2e40c305a6176a"></a>
### 사용 범위 및 접근 권한

&lt;upsert statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 해당 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Insert 대상이 되는 모든 column에 대해 INSERT(columns) ON TABLE
    - 테이블에 대해 (INSERT 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (INSERT TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - INSERT ANY TABLE ON DATABASE
    - Update 대상이 되는 모든 column에 대해 UPDATE(columns) ON TABLE
    - 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - UPDATE ANY TABLE ON DATABASE

- &lt;from subquery&gt;를 사용할 경우, 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="a1895f6201c8a8b2"></a>
### 구문 규칙 및 파라미터

<a id="c099696353be6b4f"></a>
#### table_name

Row를 생성할 대상 테이블의 이름이다.   
만약 unique 제약 조건에 위배되어 update가 수행될 경우에는 변경될 대상 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우에는 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="e94e7836917c454e"></a>
#### [ ( column_name [, ...] ) ]

테이블의 column 이름이다.   
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문의 [[ ( column_name [, ...] ) ]](#0baa7f6b0f6d0b71) 절을 참조한다.

<a id="602a10a56fa2dccc"></a>
#### &lt;values clause&gt;

대응하는 column에 할당할 값의 리스트이다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문의 [&lt;values clause&gt;](#8f02f842a9de9138)를 참조한다.

<a id="a245e053fdf613de"></a>
#### &lt;from subquery&gt;

Row들을 생성할 질의이다.  
자세한 내용은 [SELECT](#2070458035e417b9) 구문의 [query expression](#f971bccfc0bcab55) 절을 참조한다.

<a id="0c74ba14e1f5e386"></a>
#### DEFAULT VALUES

모든 column들을 기본값으로 채운다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문의 [DEFAULT VALUES](#161e12e5dc743cce) 절을 참조한다.

<a id="dd51ae22549a1538"></a>
#### &lt;duplicate key clause&gt;

Unique 제약 조건에 위배되었을 경우에 수행할 action을 정의한다.

<a id="fa5d974a5a471cd9"></a>
#### DO NOTHING

Unique 제약 조건에 위배되는 경우에는 아무것도 하지 않는다.

<a id="b9c8de940fbad23c"></a>
#### &lt;do update clause&gt;

Unique 제약 조건에 위배되는 경우에는 &lt;set clause&gt;에 따라 column들의 값을 갱신한다.

<a id="99522b30a8e6fe1a"></a>
#### &lt;set value clause&gt;

갱신할 column에 할당할 값을 정의한다.

다음과 같은 방법으로 정의할 수 있다.

- column_name = &lt;value expression&gt;

```
DO UPDATE SET column1 = value1, column2 = value2, column3 = value3
```

- column_name = DEFAULT

```
DO UPDATE SET column1 = DEFAULT, column2 = DEFAULT, column3 = DEFAULT
```

- column_name = VALUES( column_name )

&lt;insert source&gt;의 값을 갱신할 값으로 사용한다.

```
DO UPDATE SET column1 = VALUES(column1), column2 = VALUES(column2), column3 = VALUES(column2)
```

<a id="5306ea5dd8d8c480"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.

다음과 같은 방법으로 정의할 수 있다.

- column_name = { &lt;set value clause&gt; }

```
ON DUPLICATE KEY
   DO UPDATE SET column1 = value1, column2 = value2, column3 = value3
```

- ( column_name [, ...] ) = ( &lt;set value clause&gt; } [, ...] )

```
ON DUPLICATE KEY
   DO UPDATE SET ( column1, column2, column3 ) = ( value1, value2, value3 )
```

- ( column_name [, ...] ) = ( &lt;query expression&gt; )

```
ON DUPLICATE KEY
   DO UPDATE SET column1 = ( SELECT max(value1) FROM other_table_name )
```

&lt;query expression&gt;은 row 하나를 생성하는 질의여야 한다.

Column 값으로 DEFAULT를 사용할 경우, [CREATE TABLE](19-sql-references-c-g.md#ce6ecbcf1ea593ea)을 수행할 때 정의한 기본값 ([&lt;default clause&gt;](19-sql-references-c-g.md#092150e3dd719845) 참조)을 사용하며, 정의되지 않은 경우에는 NULL 값이 할당된다.

<a id="21041e6376f6a111"></a>
### 설명

<a id="222fb432e3ab50bc"></a>
#### INSERT INTO name ... UPDATE 관련 구문들의 차이점

- [INSERT INTO name ... UPDATE](#b41e8eea9acdd98a)
    - 테이블에 row를 생성한다. 만약 unique 제약 조건에 위배되는 경우에는 기존 row를 갱신한다. 
    - 예: INSERT INTO t1 VALUES ( 1, 1 ) ON DUPLICATE KEY UPDATE c2 = c2 + 1; 
- [INSERT INTO name ... UPDATE RETURNING](#578ff997d251b193)
    - 테이블에 row를 생성하거나 기존 row를 갱신한다. 삽입하거나 갱신된 row들을 SELECT 구문과 동일한 방식 (SQLFetch() 등의 API)으로 검색할 수 있다. 
    - 예: INSERT INTO t1 VALUES ( 1, 1 ) ON DUPLICATE KEY UPDATE c2 = c2 + 1 RETURNING c2; 
- [INSERT INTO name ... UPDATE RETURNING ... INTO](#4a39c3ddcaf6dd8a)
    - 한 건 이하의 row를 생성하거나 갱신할 수 있으며, 생성하거나 갱신한 row가 한 건일 경우 RETURNING INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: INSERT INTO t1 VALUES ( 1, 1 ) ON DUPLICATE KEY UPDATE c2 = c2 + 1 RETURNING c2 INTO :v1;

<a id="e9830d2b531c5694"></a>
#### &lt;upsert statement&gt;는 deterministic statement 이다.

다음과 같이 동치인 서로 다른 두 개의 UPSERT 구문은 동일한 결과를 만들어야 한다.

- INSERT INTO t1 VALUES( 1 ),( 2 ),( 3 ) ON DUPLICATE KEY UPDATE c1 = c1 + 1;
- INSERT INTO t1 VALUES( 3 ),( 2 ),( 1 ) ON DUPLICATE KEY UPDATE c1 = c1 + 1;

```
gSQL> CREATE TABLE t1 ( c1 INTEGER UNIQUE );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 ),( 2 ),( 3 );

3 rows created.

gSQL> INSERT INTO t1 VALUES( 1 ),( 2 ),( 3 ) ON DUPLICATE KEY UPDATE c1 = c1 + 1;

3 rows created.

gSQL> SELECT * FROM t1;

C1
--
 2
 3
 4

3 rows selected.
```

```
gSQL> CREATE TABLE t1 ( c1 INTEGER UNIQUE );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 ),( 2 ),( 3 );

3 rows created.

gSQL> INSERT INTO t1 VALUES( 3 ),( 2 ),( 1 ) ON DUPLICATE KEY UPDATE c1 = c1 + 1;

3 rows created.

gSQL> SELECT * FROM t1;

C1
--
 2
 3
 4

3 rows selected.
```

<a id="8f767dc9a673b62d"></a>
### 사용 예

다음은 unique 제약 조건에 위배되어 row 한 개가 갱신되는 예이다.

```
gSQL> CREATE TABLE t1 ( c1 INTEGER UNIQUE );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 );

1 row created.

gSQL> INSERT INTO t1 VALUES( 1 ) ON DUPLICATE KEY UPDATE c1 = c1 + 1;

1 row created.

gSQL> SELECT * FROM t1;

C1
--
 2

1 row selected.
```

다음은 unique 제약 조건에 위배되었을 때 row를 갱신하지 않는 예이다.

```
gSQL> CREATE TABLE t1 ( c1 INTEGER UNIQUE );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 );

1 row created.

gSQL> INSERT INTO t1 VALUES( 1 ) ON DUPLICATE KEY DO NOTHING;

no rows created.

gSQL> SELECT * FROM t1;

C1
--
 1

1 row selected.
```

다음은 subquery를 사용하여 다수의 row를 삽입하거나 갱신하는 예이다.

```
gSQL> CREATE TABLE t1 ( c1 INTEGER UNIQUE );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 ),( 2 ),( 3 ),( 4 );

4 rows created.

gSQL> INSERT INTO t1 ( SELECT c1 FROM t1 ) ON DUPLICATE KEY UPDATE c1 = c1 + 1;

4 rows created.

gSQL> SELECT * FROM t1;

C1
--
 2
 3
 4
 5

4 rows selected.
```

<a id="f0194f789c05526d"></a>
### 호환성

SQL 표준은 &lt;upsert statement&gt; 구문을 정의하지 않고 있다.

<a id="7121ed413af0ffdc"></a>
### 참조

관련 내용은 다음을 참조한다.

- [INSERT INTO](#4b00ba4f4c0eed30)
- [INSERT INTO name ... UPDATE RETURNING](#578ff997d251b193)
- [INSERT INTO name ... UPDATE RETURNING ... INTO](#4a39c3ddcaf6dd8a)
- [UPDATE](#d07bac444b3a8009)

<a id="578ff997d251b193"></a>
## INSERT INTO name ... UPDATE RETURNING

<a id="c437fd4255ba20b2"></a>
### 기능

테이블에 새로운 row들을 생성한다. 만약 unique 제약 조건에 위배되는 경우에는 기존 row들을 갱신한다. 이후 생성 또는 변경된 row들을 검색한다.

<a id="4266b626c00bb864"></a>
### 구문

```
<upsert returning statement> ::=
    INSERT INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
        <duplicate key clause>
        <returning clause>    
    ;
<insert source> ::=
      <values clause>
    | <from subquery>
    | DEFAULT VALUES

<values clause> ::=
    VALUES { ( { <value expression> | DEFAULT } [, ...] ) } [, ...]

<from subquery> ::=
    <query expression>

<duplicate key clause>
    ON DUPLICATE KEY { DO NOTHING | <do update clause> }

<do update clause> ::=
    [DO] UPDATE [SET] <set clause>  [, ...]

<set value clause> ::= 
      <value expression>
    | DEFAULT
    | VALUES( column_name )

<set clause> ::=
      column_name = <set value clause>
    | ( column_name [, ...] ) = ( <set value clause> [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )

<returning clause> ::=
    [ RETURN | RETURNING ] { * | { <value expression> [ [AS] alias_name ] } [, ...]
```

<a id="819581ae06a34097"></a>
### 사용 범위 및 접근 권한

&lt;upsert returning statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 해당 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Insert 대상이 되는 모든 column에 대해 INSERT(columns) ON TABLE
    - 테이블에 대해 (INSERT 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (INSERT TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - INSERT ANY TABLE ON DATABASE
    - Update 대상이 되는 모든 column에 대해 UPDATE(columns) ON TABLE
    - 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - UPDATE ANY TABLE ON DATABASE

- &lt;from subquery&gt;를 사용할 경우, 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="27c019ebc6a40431"></a>
### 구문 규칙 및 파라미터

<a id="fedbd2787584dbf9"></a>
#### table_name

Row를 생성할 대상 테이블의 이름이다.   
만약 unique 제약 조건에 위배되어 update가 수행될 경우에는 변경될 대상 테이블의 이름이다.  
자세한 내용은 [INSERT INTO name ... UPDATE](#b41e8eea9acdd98a) 구문의 [table_name](#c099696353be6b4f) 절을 참조한다.

<a id="49d0fd420d9e1606"></a>
#### [ ( column_name [, ...] ) ]

테이블의 column 이름이다.   
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문의 [[ ( column_name [, ...] ) ]](#0baa7f6b0f6d0b71) 절을 참조한다.

<a id="c271a9855c0bf31e"></a>
#### &lt;values clause&gt;

대응하는 column에 할당할 값의 리스트이다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문의 [&lt;values clause&gt;](#8f02f842a9de9138)를 참조한다.

<a id="f3380a62f47bb7b4"></a>
#### &lt;from subquery&gt;

Row들을 생성할 질의이다.  
자세한 내용은 [SELECT](#2070458035e417b9) 구문의 [query expression](#f971bccfc0bcab55) 절을 참조한다.

<a id="95d38f84c6fa54d6"></a>
#### DEFAULT VALUES

모든 column들을 기본값으로 채운다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문의 [DEFAULT VALUES](#161e12e5dc743cce) 절을 참조한다.

<a id="ee05318de285153f"></a>
#### &lt;duplicate key clause&gt;

Unique 제약 조건에 위배되었을 경우에 수행할 action을 정의한다.

<a id="ef2db29d7766f5b8"></a>
#### DO NOTHING

Unique 제약 조건에 위배되는 경우에는 아무것도 하지 않는다.

<a id="37ec78358bb70b3f"></a>
#### &lt;do update clause&gt;

Unique 제약 조건에 위배되는 경우에는 &lt;set clause&gt;에 따라 column들의 값을 갱신한다.

<a id="d8d68e2c1d121768"></a>
#### &lt;set value clause&gt;

갱신할 column에 할당할 값을 정의한다.  
자세한 내용은 [INSERT INTO name ... UPDATE](#b41e8eea9acdd98a) 구문의 [&lt;set value clause&gt;](#99522b30a8e6fe1a)를 참조한다.

<a id="861374b4ad2350db"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.  
자세한 내용은 [INSERT INTO name ... UPDATE](#b41e8eea9acdd98a) 구문의 [&lt;set clause&gt;](#5306ea5dd8d8c480)를 참조한다.

<a id="1a32f74a7821f635"></a>
#### &lt;returning clause&gt;

삽입 또는 변경된 row들을 반환한다.

- 생성된 row들을 결과 집합으로 하고, 이들 중에서 검색할 column을 기술한다. 
    - RETURNING 절은 삽입되었거나 변경된 row들을 결과 집합으로 하는 결과를 반환한다. 
    - &lt;value expression&gt; 
        - SELECT 구문의 &lt;select list&gt;와 동일하지만 aggregation 등을 사용할 수 없다. 
    - [[AS] alias_name] 
        - AS 절을 사용하여 value expression의 이름을 지정할 수 있다.

<a id="d82cec3b4800e5e5"></a>
### 설명

자세한 내용은 [INSERT INTO name ... UPDATE 관련 구문들의 차이점](#222fb432e3ab50bc)을 참조한다.

다음은 네 개의 row들을 삽입한 후에 삽입된 결과를 반환하는 예이다.

```
gSQL> CREATE TABLE t1 ( c1 INTEGER UNIQUE );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 ), ( 2 ), ( 3 ), ( 4 ) ON DUPLICATE KEY UPDATE c1 = c1 + 1 RETURNING c1;

C1
--
 1
 2
 3
 4

4 rows created.
```

다음은 unique 제약 조건에 위배되어 row들을 갱신한 이후에 갱신된 결과를 반환하는 예이다.

```
gSQL> CREATE TABLE t1 ( c1 INTEGER UNIQUE );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 ),( 2 ),( 3 ),( 4 );

4 rows created.

gSQL> INSERT INTO t1 ( SELECT c1 FROM t1 ) ON DUPLICATE KEY UPDATE c1 = c1 + 1 RETURNING c1;

C1
--
 2
 3
 4
 5

4 rows created.
```

<a id="d3b10d4864ec5125"></a>
### 호환성

SQL 표준에서는 &lt;upsert returning statement&gt; 구문을 정의하고 있지 않다.

<a id="965509eadd9a059a"></a>
### 참조

관련 내용은 다음을 참조한다.

- [INSERT INTO name ... UPDATE](#b41e8eea9acdd98a)
- [INSERT INTO name ... UPDATE RETURNING ... INTO](#4a39c3ddcaf6dd8a)

<a id="4a39c3ddcaf6dd8a"></a>
## INSERT INTO name ... UPDATE RETURNING ... INTO

<a id="18f2e8725a041857"></a>
### 기능

테이블에 row 하나를 생성한다. 만약 unique 제약 조건에 위배되는 경우에는 기존 row들을 갱신한다. 이후 생성 또는 변경된 row의 값을 호스트 변수로 얻어온다.

<a id="9ebe26c70c4f7af9"></a>
### 구문

```
<upsert returning into statement> ::=
    INSERT INTO table_name [ ( column_name [, ...] ) ]
        <insert source>
        <duplicate key clause>
        <returning clause>    
        <into clause>    
    ;
<insert source> ::=
      <values clause>
    | <from subquery>
    | DEFAULT VALUES

<values clause> ::=
    VALUES { ( { <value expression> | DEFAULT } [, ...] ) } [, ...]

<from subquery> ::=
    <query expression>

<duplicate key clause>
    ON DUPLICATE KEY { DO NOTHING | <do update clause> }

<do update clause> ::=
    [DO] UPDATE [SET] <set clause>  [, ...]

<set value clause> ::= 
      <value expression>
    | DEFAULT
    | VALUES( column_name )

<set clause> ::=
      column_name = <set value clause>
    | ( column_name [, ...] ) = ( <set value clause> [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )

<returning clause> ::=
    [ RETURN | RETURNING ] { * | { <value expression> [ [AS] alias_name ] } [, ...] 

<into clause> ::= INTO variable_name [, ...]
```

<a id="4a12f28ed660e383"></a>
### 사용 범위 및 접근 권한

&lt;upsert returning into statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- 해당 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Insert 대상이 되는 모든 column에 대해 INSERT(columns) ON TABLE
    - 테이블에 대해 (INSERT 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (INSERT TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - INSERT ANY TABLE ON DATABASE
    - Update 대상이 되는 모든 column에 대해 UPDATE(columns) ON TABLE
    - 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE
    - 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA
    - UPDATE ANY TABLE ON DATABASE

- &lt;from subquery&gt;를 사용할 경우, 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나가 있어야 한다.
    - 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="f1c753d078a8074c"></a>
### 구문 규칙 및 파라미터

<a id="6bfe0eccc7d26163"></a>
#### table_name

Row를 생성할 대상 테이블의 이름이다.   
만약 unique 제약 조건에 위배되어 update가 수행될 경우에는 변경될 대상 테이블의 이름이다.  
자세한 내용은 [INSERT INTO name ... UPDATE](#b41e8eea9acdd98a) 구문의 [table_name](#c099696353be6b4f) 절을 참조한다.

<a id="a4cdf30e8d82b04f"></a>
#### [ ( column_name [, ...] ) ]

테이블의 column 이름이다.   
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문의 [[ ( column_name [, ...] ) ]](#0baa7f6b0f6d0b71) 절을 참조한다.

<a id="a80de6e1130fe972"></a>
#### &lt;values clause&gt;

대응하는 column에 할당할 값의 리스트이다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문의 [&lt;values clause&gt;](#8f02f842a9de9138) 절을 참조한다.

<a id="9c53b23a484ced7f"></a>
#### &lt;from subquery&gt;

Row들을 생성할 질의이다.  
자세한 내용은 [SELECT](#2070458035e417b9) 구문의 [query expression](#f971bccfc0bcab55) 절을 참조한다.

<a id="96b5e91205873a98"></a>
#### DEFAULT VALUES

모든 column들을 기본값으로 채운다.  
자세한 내용은 [INSERT INTO](#4b00ba4f4c0eed30) 구문의 [DEFAULT VALUES](#161e12e5dc743cce) 절을 참조한다.

<a id="484e50725b106ddf"></a>
#### &lt;duplicate key clause&gt;

Unique 제약 조건에 위배되었을 경우에 수행할 action을 정의한다.

<a id="903791ea4c733f4b"></a>
#### DO NOTHING

Unique 제약 조건에 위배되는 경우에는 아무것도 하지 않는다.

<a id="863eb86b51cd113e"></a>
#### &lt;do update clause&gt;

Unique 제약 조건에 위배되는 경우에는 &lt;set clause&gt;에 따라 column들의 값을 갱신한다.

<a id="3b3b3cd305ebc040"></a>
#### &lt;set value clause&gt;

갱신할 column에 할당할 값을 정의한다.  
자세한 내용은 [INSERT INTO name ... UPDATE](#b41e8eea9acdd98a) 구문의 [&lt;set value clause&gt;](#99522b30a8e6fe1a) 절을 참조한다.

<a id="f7b432e434731a21"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.  
자세한 내용은 [INSERT INTO name ... UPDATE](#b41e8eea9acdd98a) 구문의 [&lt;set clause&gt;](#5306ea5dd8d8c480) 절을 참조한다.

<a id="a9de80aed672e7a8"></a>
#### &lt;returning clause&gt;

삽입 또는 변경된 row를 반환한다.  
자세한 내용은 [INSERT INTO name ... UPDATE RETURNING](#578ff997d251b193) 구문의 [&lt;returning clause&gt;](#1a32f74a7821f635) 절을 참조한다.

<a id="80ba2003b69106ba"></a>
#### &lt;into clause&gt;

INTO 절에 기술된 변수의 개수는 RETURNING 절에 기술된 expression의 개수와 동일해야 한다.   
생성할 row가 한 건 이하여야 한다. Row가 두 건 이상 생성되면 에러가 발생한다.

<a id="36adbe7cb2bb1563"></a>
### 설명

자세한 내용은 [INSERT INTO name ... UPDATE 관련 구문들의 차이점](#222fb432e3ab50bc)을 참조한다.

다음은 row 하나를 삽입한 이후에 삽입된 결과를 호스트 변수로 얻어오는 예이다.

```
gSQL> \VAR v_c1 INTEGER;

gSQL> CREATE TABLE t1 ( c1 INTEGER UNIQUE );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 ) ON DUPLICATE KEY UPDATE c1 = c1 + 1 RETURNING c1 INTO :v_c1;

V_C1
----
   1

1 row created.
```

다음은 unique 제약 조건에 위배되어 row 하나를 갱신한 이후에 갱신된 결과를 호스트 변수로 얻어오는 예이다.

```
gSQL> \VAR v_c1 INTEGER;

gSQL> CREATE TABLE t1 ( c1 INTEGER UNIQUE );

Table created.

gSQL> INSERT INTO t1 VALUES( 1 );

1 row created.

gSQL> INSERT INTO t1 VALUES( 1 ) ON DUPLICATE KEY UPDATE c1 = c1 + 1 RETURNING c1 INTO :v_c1;

V_C1
----
   2

1 row created.
```

<a id="9c37c69e3e638968"></a>
### 호환성

SQL 표준에서는 &lt;upsert returning into statement&gt; 구문을 정의하고 있지 않다.

<a id="94b7fa7ca5cd0779"></a>
### 참조

관련 내용은 다음을 참조한다.

- [INSERT INTO name ... UPDATE](#b41e8eea9acdd98a)
- [INSERT INTO name ... UPDATE RETURNING](#578ff997d251b193)

<a id="aa7af8e829d2f1c4"></a>
## LOCK TABLE

<a id="87566987b54e849c"></a>
### 기능

하나 이상의 테이블에 lock을 설정한다.

<a id="23f4b9fc995b81f6"></a>
### 구문

```
<lock table statement> ::=
    LOCK TABLE lock target [, ...] 
    IN <lock mode> MODE [<wait clause>]
    ;

<lock mode> ::=
    SHARE
    | EXCLUSIVE
    | ROW SHARE
    | ROW EXCLUSIVE
    | SHARE ROW EXCLUSIVE


<wait clause> ::=
    NOWAIT
    | WAIT time
```

<a id="70b3fe3c4572f86b"></a>
### 사용 범위 및 접근 권한

&lt;lock table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블에 대해 (LOCK 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (LOCK TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- LOCK ANY TABLE ON DATABASE

<a id="38e94fc4a0ee47e6"></a>
### 구문 규칙 및 파라미터

<a id="297b311a14d16d72"></a>
#### &lt;lock target&gt;

LOCK 대상 테이블을 명시한다.

<a id="686354c4ec79162d"></a>
#### &lt;lock mode&gt;

LOCK mode를 명시한다.

- SHARE 
    - Locked table에 대한 동시성 질의를 허용하지만 테이블 update는 금지한다. 
- EXCLUSIVE 
    - Locked table에 대한 배타적인 질의 처리를 허용한다. 
- ROW SHARE 
    - Locked table에 동시성 접근을 허용하지만 exclusive access를 위한 전체 table locking은 금지한다. 
- ROW EXCLUSIVE 
    - Locked table에 동시성 접근을 허용하지만 exclusive access를 위한 전체 table locking은 금지한다. 
    - ROW EXCLUSIVE mode가 설정되어 있는 경우, SHARE mode의 locking은 거부한다. 
    - ROW EXCLUSIVE mode는 update, insert, delete 할 때 자동으로 부여된다. 
- SHARE ROW EXCLUSIVE 
    - Table 전체를 탐색하거나 다른 사용자에게 table의 row들을 탐색하게 할 때 사용한다. 
    - SHARE mode의 lock이 부여된 table이나 update되고 있는 row들에 다른 사용자가 접근하지 못하도록 한다.

<a id="369b3f9d14cbd55e"></a>
#### &lt;wait clause&gt;

Lock을 획득하기 위한 대기 시간을 명시한다.

- NOWAIT 
    - 대상에 대한 lock 제어를 즉시 획득한다. 
    - 다른 사용자에 의해 이미 lock이 설정된 경우 즉시 제어권을 넘겨받는다. 
        - 이 경우 database가 message를 발생시킨다. 
- WAIT time 
    - Lock을 획득하기 위한 대기 시간을 설정한다.
    - 초 단위이며 0 ~ 1000000000 의 값을 사용할 수 있다.
- 명시하지 않을 경우 lock을 획득할 때까지 무기한 WAIT 하도록 한다.

<a id="bd4a9e9275bb8b9f"></a>
### 설명

Transaction을 COMMIT 하거나 ROLLBACK 할 경우 획득한 모든 lock은 자동으로 해제된다. ROLLBACK TO SAVEPOINT 구문을 사용할 경우 해당 savepoint 이후에 획득한 모든 lock이 해제된다.

<a id="ed969f1adac8ab72"></a>
### 사용 예

다음은 다른 transaction이 TABLE t1에 대해 어떠한 변경 연산도 수행할 수 없도록 하는 예이다.

```
gSQL> LOCK TABLE t1 IN EXCLUSIVE MODE;

Table locked.
```

다음은 다수의 table에 LOCK 구문을 수행하는 예이다.

```
gSQL> LOCK TABLE t1, t2 IN EXCLUSIVE MODE;

Table locked.
```

다음은 TABLE t1에 SHARE ROW EXCLUSIVE lock을 획득하는 예이다.

```
gSQL> LOCK TABLE t1 IN SHARE ROW EXCLUSIVE MODE;

Table locked.
```

다음은 해당 TABLE에 즉시 lock을 획득할 수 있을 경우에만 수행할 수 있는 구문이다. Lock을 획득할 수 없을 경우에는 에러가 발생한다.

```
gSQL> LOCK TABLE t1 IN EXCLUSIVE MODE NOWAIT;

Table locked.
```

다음은 lock을 획득하기 위해 10 초 동안 대기하도록 하는 예이다.

```
gSQL> LOCK TABLE t1 IN EXCLUSIVE MODE WAIT 10;

Table locked.
```

<a id="fb8c3dcb685e6d7f"></a>
### 호환성

SQL 표준은 lock table에 대한 개념을 다루지 않고 있다.

<a id="53155cb624ae4ce0"></a>
### 참조

관련 내용은 다음을 참조한다.

- [COMMIT](19-sql-references-c-g.md#9d9942a1324d8ced)
- [ROLLBACK](#1ba3b433854d9411)

<a id="bc136bf193bf403b"></a>
## MERGE

<a id="17c4ce098b17fc3a"></a>
### 기능

변경 대상 테이블에 조건에 맞는 레코드를 insert 또는 update 또는 delete 한다.

<a id="2859c29487418b52"></a>
### 구문

```
<merge statement> ::=
    MERGE [ <hint clause> ] INTO <target table> [ [ AS ] <target alias> ]
    USING <source relation>
    ON <merge join condition>
    <merge operation specification>
    ;

<target table> ::=
    <table name>

<target alias> ::=
    <correlation name>
    
<source relation> ::=
    {
        <table name> [ [ AS ] <source alias> ]
      | <table subquery> [ [ AS ] <source alias> ]    
    }

<source alias> ::=
    <correlation name>

<merge join condition> ::=
    <search condition>
    
<merge operation specification> ::=
    <merge when clause> [...]

<merge when clause> ::=
      <merge when matched clause>
    | <merge when not matched clause>

<merge when matched clause> ::=
    WHEN MATCHED [ AND <search condition> ] 
        THEN { <merge update> | <merge delete> | <merge do nothing> }

<merge when not matched clause> ::=
    WHEN NOT MATCHED [ AND <search condition> ] 
        THEN { <merge insert> | <merge do nothing> }

<merge update> ::=
    UPDATE SET
    {
        <column name> = { <value expression> | DEFAULT }
      | <left paren> <column name> [, ...] <right paren>
        = <left paren> { <value expression> | DEFAULT } [, ...] <right paren>
    } [, ...]

<merge delete> ::=
    DELETE

<merge insert> ::=
    INSERT
    [ <left paren> <column name> [, ...] <right paren> ]
    {
        VALUES <left paren> <merge insert value element> [, ...] <right paren>
      | DEFAULT VALUES
    }

<merge do nothing> ::=
    DO NOTHING

<merge insert value element> ::=
      <value expression>
    | DEFAULT
```

<a id="6c9dc724b3d874e3"></a>
### 사용 범위 및 접근 권한

MERGE 를 위한 별도의 권한은 없다.

&lt;merge statement&gt; 구문을 수행하기 위해 사용자는 다음과 같은 권한이 필요하다.

- &lt;merge update&gt; 가 명시된 경우 update 대상이 되는 모든 컬럼에 대해 UPDATE 권한
    - UPDATE를 수행하기 위해서는 다음 권한 중 하나가 있어야 한다.
        - Update 대상이 되는 모든 컬럼에 대해 UPDATE(columns) ON TABLE
        - 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE
        - 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA
        - UPDATE ANY TABLE ON DATABASE

- &lt;merge delete&gt; 가 명시된 경우 테이블에 대한 DELETE 권한
    - DELETE를 수행하기 위해서는 다음 권한 중 하나가 있어야 한다.
        - 테이블에 대해 (DELETE 또는 CONTROL TABLE) ON TABLE
        - 테이블이 속한 스키마에 대해 (DELETE TABLE 또는 CONTROL SCHEMA) ON SCHEMA
        - DELETE ANY TABLE ON DATABASE

- &lt;merge insert&gt; 가 명시된 경우 테이블에 대한 INSERT 권한
    - INSERT를 수행하기 위해서는 다음 권한 중 하나가 있어야 한다.
        - Insert 대상이 되는 모든 컬럼에 대해 INSERT(columns) ON TABLE
        - 테이블에 대해 (INSERT 또는 CONTROL TABLE) ON TABLE
        - 테이블이 속한 스키마에 대해 (INSERT TABLE 또는 CONTROL SCHEMA) ON SCHEMA
        - INSERT ANY TABLE ON DATABASE

- &lt;target table&gt; 과 &lt;source relation&gt; 의 참조되는 모든 컬럼에 대한 SELECT 권한
    - &lt;target table&gt; 과 &lt;source relation&gt; 의 참조되는 모든 컬럼에 대해 다음 권한 중 하나가 있어야 한다.
        - &lt;target table&gt; 과 &lt;source relation&gt; 의 참조되는 모든 컬럼에 대해 SELECT(columns) ON TABLE
        - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE
        - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA
        - SELECT ANY TABLE ON DATABASE

<a id="91e89623dde6bab1"></a>
### 구문 규칙 및 파라미터

<a id="3c6acffa6ee7cf9e"></a>
#### &lt;hint clause&gt;

&lt;target table&gt; 과 &lt;source relation&gt; 의 조인 결과를 얻기 위한 질의 수행에 필요한 힌트를 기술한다.  
자세한 내용은  [SQL Hint](15-sql-tuning.md#54d9bce5449eb296) 를 참조한다.

<a id="d1dc12b195e7faa4"></a>
#### &lt;target table&gt;

변경 대상 테이블을 지정한다.  
테이블의 이름에는 schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
변경 대상 테이블에는 table 또는 temporary table 을 지정할 수 있다.

<a id="2e486244471d1c38"></a>
#### &lt;target alias&gt;

&lt;target table&gt; 의 대체 이름 (별칭)이다.

<a id="87feff2e25e0b5ae"></a>
#### &lt;source relation&gt;

변경 대상 테이블인 &lt;target table&gt; 로 병합할 행을 제공하는 source relation 이다.

- 기술 가능한 relation
    - Table
    - View 
    - Subquery

<a id="68996dbd54ec655f"></a>
#### &lt;source alias&gt;

&lt;source relation&gt; 의 대체 이름 (별칭)이다.

<a id="df74d15c931d5df7"></a>
#### &lt;merge join condition&gt;

&lt;target table&gt; 과 &lt;source relation&gt; 의 join 조건을 명시한다.  
&lt;search condition&gt; 에 &lt;target table&gt;의 컬럼과 &lt;source relation&gt; 의 컬럼을 기술할 수 있다.

<a id="582bb0638d1323b2"></a>
#### &lt;merge operation specification&gt;

하나 이상의 &lt;merge when clause&gt;를 기술한다.

<a id="a45955a54e3940c7"></a>
#### &lt;merge when clause&gt;

&lt;search condition&gt; 이 없는 &lt;merge when matched clause&gt; 는 하나만 기술할 수 있다.  
&lt;search condition&gt; 이 없는 &lt;merge when matched clause&gt; 가 기술된 경우, 더 이상의 &lt;merge when matched clause&gt; 를 기술할 수 없다.

```
gSQL> 
MERGE INTO t1
USING t2
ON t1.c1 = t2.c1
WHEN MATCHED THEN UPDATE SET ( c1, c2 ) = ( t2.c1, t2.c2 )
WHEN MATCHED AND t1.c1 = 100 THEN DO NOTHING;

ERR-42000(16614): unreachable WHEN clause specified after unconditional WHEN clause : 
WHEN MATCHED AND t1.c1 = 100 THEN DO NOTHING
*
ERROR at line 5:
```

&lt;search condition&gt; 이 없는 &lt;merge when not matched clause&gt; 는 하나만 기술할 수 있다.  
&lt;search condition&gt; 이 없는 &lt;merge when not matched clause&gt; 가 기술된 경우, 더 이상의 &lt;merge when not matched clause&gt; 를 기술할 수 없다.

```
gSQL> 
MERGE INTO t1
USING t2
ON t1.c1 = t2.c1
WHEN NOT MATCHED THEN INSERT VALUES ( c1, c2 )
WHEN NOT MATCHED AND c1 = 4 THEN INSERT DEFAULT VALUES;

ERR-42000(16614): unreachable WHEN clause specified after unconditional WHEN clause : 
WHEN NOT MATCHED AND c1 = 4 THEN INSERT DEFAULT VALUES
*
ERROR at line 5:
```

<a id="4fcb9a55147d650d"></a>
#### &lt;merge when matched clause&gt;

&lt;merge when matched clause&gt; 는 &lt;target table&gt; 과 &lt;source relation&gt; 의 join 결과 레코드들을 대상으로 평가한다.

&lt;target table&gt; 의 레코드들 중 다음을 만족하는 경우 &lt;merge when matched clause&gt; 가 수행된다.  
• &lt;merge when matched clause&gt; 의 &lt;search condition&gt; 이 true 로 평가   
• &lt;merge when matched clause&gt; 의 &lt;search condition&gt; 이 없는 경우

&lt;merge when matched clause&gt; 의 &lt;search condition&gt; 에는 &lt;target table&gt; 과 &lt;source relation&gt; 의 컬럼을 모두 참조할 수 있다.

&lt;merge when matched clause&gt; 는 다음 중 하나의 기능을 수행한다.  
• &lt;merge update&gt; : 대상 후보 레코드를 갱신한다.  
• &lt;merge delete&gt; : 대상 후보 레코드를 삭제한다.  
• &lt;merge do nothing&gt; : 대상 후보 레코드에 대한 아무런 일도 하지 않는다.

대상 후보로 결정된 레코드는 이후 기술된 &lt;merge when matched clause&gt; 들의 대상 후보 레코드에서 제외된다.

<a id="75f9ddf195f6f612"></a>
#### &lt;merge when not matched clause&gt;

&lt;merge when not matched clause&gt; 는 &lt;target table&gt; 과 &lt;source relation&gt; 의 join 조건을 만족하지 않는 &lt;source relation&gt; 의 레코드들을 대상으로 평가한다.

&lt;source relation&gt; 의 레코드들 중 다음을 만족하는 경우 &lt;merge when not matched clause&gt; 가 수행된다.   
• &lt;merge when not matched clause&gt; 의 &lt;search condition&gt; 이 true 로 평가   
• &lt;merge when not matched clause&gt; 의 &lt;search condition&gt; 이 없는 경우

&lt;merge when not matched clause&gt; 의 &lt;search condition&gt; 에는 &lt;source relation&gt; 의 컬럼만 참조할 수 있다.

&lt;merge when not matched clause&gt; 는 다음 중 하나의 기능을 수행한다.   
• &lt;merge insert&gt; : &lt;target table&gt; 에 새로운 레코드를 삽입한다.   
• &lt;merge do nothing&gt; : 대상 후보 레코드에 대한 아무런 일도 하지 않는다.

대상 후보로 결정된 레코드는 이후 기술된 &lt;merge when not matched clause&gt; 들의 대상 후보 레코드에서 제외된다.

<a id="286f60900cecce42"></a>
#### &lt;merge update&gt;

&lt;merge when matched clause&gt; 에서 선정된 대상 후보 레코드들에 대한 갱신을 수행한다.

UPDATE 구문의 &lt;set clause&gt; 만 기술 가능하다.

자세한 내용은 UPDATE 구문의 [&lt;set clause&gt;](#62d20dc31fe68cd2) 을 참조한다.

&lt;set clause&gt; 의 &lt;column name&gt; 에는 &lt;target table&gt; 의 컬럼만 기술하여야 하며, &lt;value expression&gt; 에는 &lt;target table&gt; 과 &lt;source relation&gt; 의 컬럼을 모두 참조할 수 있다.

<a id="76c84cda05c7a293"></a>
#### &lt;merge delete&gt;

&lt;merge when matched clause&gt; 에서 선정된 대상 후보 레코드들에 대한 삭제를 수행한다.

<a id="e4f6759ff8306fd7"></a>
#### &lt;merge do nothing&gt;

&lt;merge when matched clause&gt; 또는 &lt;merge when not matched clause&gt; 에서 선정된 대상 후보 레코드들에 대한 아무런 일도 하지 않는다.

<a id="73f0a90d5b9d6a00"></a>
#### &lt;merge insert&gt;

&lt;merge when not matched clause&gt; 에서 선정된 대상 후보 레코드들이 있을 경우, &lt;target table&gt; 에 삽입할 레코드를 지정한다.  
&lt;merge insert value element&gt; 의 &lt;value expression&gt; 으로 &lt;source relation&gt; 의 컬럼을 참조할 수 있다.

<a id="05d74ebb8379349b"></a>
### 설명

MERGE 구문은 조건부로 INSERT, UPDATE 또는 DELETE 를 수행하는 단일 SQL 문이다.  
MERGE 구문 수행 결과는 일반 INSERT, UPDATE, DELETE 구문을 수행한 결과와 동일하다.  
MERGE 구문의 INSERT, UPDATE, DELETE에는 대상 테이블을 지정하는 구문이 없고, WHERE 절과 OFFSET/LIMIT 절이 없다.

MERGE 구문은 &lt;target table&gt; 과 &lt;source relation&gt; 의 조인 결과를 이용해 조건에 맞게 레코드를 &lt;target table&gt; 에 INSERT 또는 UPDATE 또는 DELETE 하는 작업을 수행한다.

수행 절차는 다음과 같다.

1. &lt;target table&gt; 과 &lt;source relation&gt; 의 조인 결과로 대상 후보 레코드를 결정한다.
2. 각 대상 후보 레코드에 대해 MATCHED 또는 NOT MATCHED 상태가 결정된다.
    1. MATCHED
        1. &lt;target table&gt; 과 &lt;source relation&gt; 의 join 조건을 만족하는 join 결과 레코드
    2. NOT MATCHED
        1. &lt;target table&gt; 과 &lt;source relation&gt; 의 join 조건을 만족하지 않는 &lt;source relation&gt; 의 레코드
3. MATCHED 또는 NOT MATCHED 상태가 결정된 레코드는 WHEN 절이 기술된 순서대로 평가된다.
    1. 각 대상 후보 레코드에 대한 WHEN 절 평가시 TRUE 로 평가되는 첫번째 WHEN 절이 수행된다.
        1. &lt;search condition&gt; 이 TRUE 로 평가
        2. &lt;search condition&gt; 이 없는 경우
4. 대상 후보 레코드에 대해 하나 이상의 WHEN 절은 수행되지 않는다.
    1. 3 에서 수행된 대상 후보 레코드는 이후 기술된 WHEN 절 수행시 제외된다.

MERGE 수행 과정 예시

```
### table 정보

gSQL> 
SELECT * FROM t_target ORDER BY c1, c2;
C1 C2
-- --
 2  2
 4  4
 6  6
 8  8
4 rows selected.

gSQL>  
SELECT * FROM t_source ORDER BY c1, c2;
C1 C2
-- --
 2  1
 4  2
 6  3
 8  4
10  5
12  6
14  7
7 rows selected.
```

```
### MERGE 구문

MERGE INTO t_target
USING t_source
ON t_target.c1 = t_source.c1
WHEN MATCHED AND t_target.c1 = 4 THEN DELETE
WHEN MATCHED AND t_target.c1 = 2 THEN DO NOTHING
WHEN MATCHED THEN UPDATE SET c1 = t_target.c1 + 100
WHEN NOT MATCHED AND t_source.c1 = 14 THEN DO NOTHING
WHEN NOT MATCHED THEN INSERT VALUES ( t_source.c1, t_source.c1 );
```

```
### <target table> 과 <source relation> 의 조인 결과로 대상 후보 레코드를 결정

t_target.c1 t_target.c2 t_source.c1 t_source.c2
----------- ----------- ----------- -----------
          2           2           2           1  <-- MATCHED
          4           4           4           2  <-- MATCHED
          6           6           6           3  <-- MATCHED
          8           8           8           4  <-- MATCHED
       null        null          10           5  <-- NOT MATCHED
       null        null          12           6  <-- NOT MATCHED
       null        null          14           7  <-- NOT MATCHED
```

<pre><code>### MATCHED 또는 NOT MATCHED 상태가 결정된 레코드는 WHEN 절이 기술된 순서대로 평가

WHEN MATCHED AND t_target.c1 = 4 THEN DELETE                      ❶
WHEN MATCHED AND t_target.c1 = 2 THEN DO NOTHING                  ❷
WHEN MATCHED THEN UPDATE SET c1 = t_target.c1 + 100               ❸
WHEN NOT MATCHED AND t_source.c1 = 14 THEN DO NOTHING             ❹
WHEN NOT MATCHED THEN INSERT VALUES ( t_source.c1, t_source.c1 ); ❺

t_target.c1 t_target.c2 t_source.c1 t_source.c2
----------- ----------- ----------- -----------
          2           2           2           1  &lt;-- MATCHED     ❷ DO NOTHING
          <del>4           4 </del>          4           2  &lt;-- MATCHED     ❶ DELETE
          6 (106)     6           6           3  &lt;-- MATCHED     ❸ UPDATE
          8 (108)     8           8           4  &lt;-- MATCHED     ❸ UPDATE
       null (10)   null (10)     10           5  &lt;-- NOT MATCHED ❺ INSERT
       null (12)   null (12)     12           6  &lt;-- NOT MATCHED ❺ INSERT
       null        null          14           7  &lt;-- NOT MATCHED ❹ DO NOTHING</code></pre>

```
### MERGE 구문 수행 결과 

gSQL> 
MERGE INTO t_target
USING t_source
ON t_target.c1 = t_source.c1
WHEN MATCHED AND t_target.c1 = 4 THEN DELETE
WHEN MATCHED AND t_target.c1 = 2 THEN DO NOTHING
WHEN MATCHED THEN UPDATE SET c1 = t_target.c1 + 100
WHEN NOT MATCHED AND t_source.c1 = 14 THEN DO NOTHING
WHEN NOT MATCHED THEN INSERT VALUES ( t_source.c1, t_source.c1 );
5 rows merged.

gSQL> 
SELECT * FROM t_target ORDER BY c2, c1;
 C1 C2
--- --
  2  2
106  6
108  8
 10 10
 12 12
5 rows selected.
```

<a id="de6fc16dcec13b34"></a>
### 사용 예

다음은 직원들의 부서 이동 등의 변동 사항을 employee 테이블에 반영하는 질의 예이다.

```
DROP TABLE employee;
CREATE TABLE employee ( id              INTEGER,
                        department_id   INTEGER,
                        name            VARCHAR( 10 ) );

INSERT INTO employee VALUES ( 1, 10, 'KIM' );
INSERT INTO employee VALUES ( 2, 10, 'LEE' );
INSERT INTO employee VALUES ( 3, 20, 'PARK' );
INSERT INTO employee VALUES ( 4, 20, 'JUNG' );
INSERT INTO employee VALUES ( 5, 30, 'SONG' );
COMMIT;

DROP TABLE dep_transfer;
CREATE TABLE dep_transfer( emp_id              INTEGER,
                           curr_department_id  INTEGER,
                           new_department_id   INTEGER,
                           name                VARCHAR( 10 ),
                           is_retire           BOOLEAN );

INSERT INTO dep_transfer VALUES ( 1,   10,   30,   'KIM', FALSE );
INSERT INTO dep_transfer VALUES ( 3,   20,   30,  'PARK', FALSE );
INSERT INTO dep_transfer VALUES ( 4,   20, NULL,  'JUNG', TRUE );
INSERT INTO dep_transfer VALUES ( 5,   30,   10,  'SONG', FALSE );
INSERT INTO dep_transfer VALUES ( 6, NULL,   10, 'HWANG', FALSE );
COMMIT;

gSQL> 
MERGE INTO employee
USING dep_transfer
ON employee.id = dep_transfer.emp_id
WHEN MATCHED AND is_retire = TRUE THEN DELETE
WHEN MATCHED THEN UPDATE SET department_id = new_department_id
WHEN NOT MATCHED THEN INSERT VALUES ( emp_id, new_department_id, name );
5 rows merged.

gSQL> 
SELECT * FROM employee;      
ID DEPARTMENT_ID NAME 
-- ------------- -----
 1            30 KIM  
 2            10 LEE  
 3            30 PARK 
 5            10 SONG 
 6            10 HWANG
5 rows selected.
```

<a id="83acc7a8767fcdca"></a>
### 호환성

SQL 표준은 MERGE 구문에서 DO NOTHING 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="abf7abe292afd6bc"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| S024 | Enhanced structured types | X |
| F312 | MERGE statement | O |
| F313 | Enhanced MERGE statement | O |
| F314 | MERGE statement with DELETE branch | O |

<a id="3850093d0a8f1a7b"></a>
### 참조

관련 내용은 다음을 참조한다.

- [query expression](#f971bccfc0bcab55)
- [INSERT INTO name ... UPDATE](#b41e8eea9acdd98a)
- [INSERT INTO](#4b00ba4f4c0eed30)
- [UPDATE](#d07bac444b3a8009)
- [DELETE FROM](19-sql-references-c-g.md#ef8408aa8bc980db)

<a id="2a39421bd3a74134"></a>
## NOAUDIT POLICY

<a id="91624b8ed88478fe"></a>
### 기능

Audit policy를 비활성화한다.

<a id="e0c05b8d1cd8c81b"></a>
### 구문

```
<noaudit policy statement> ::= 
    NOAUDIT POLICY policy_name
    [ <specified_user_option> ]
    ;

<specified_user_option> ::=
      BY user_name [, ...]
```

<a id="dc5d9444b4ee10f2"></a>
### 사용 범위 및 접근 권한

&lt;noaudit policy statement&gt; 구문을 수행하려면 사용자에게 AUDIT SYSTEM ON DATABASE 권한이 있어야 한다.

<a id="8fe378cf57dca448"></a>
### 구문 규칙 및 파라미터

<a id="ce6b9822cb1f9024"></a>
#### policy_name

비활성화할 audit policy 객체의 이름이다.   
비활성화 된 audit policy는 기존 session에 영향을 미치지 않으며 새로 생성되는 session에만 영향을 준다.

<a id="696484db792d214a"></a>
#### &lt;specified_user_option&gt;

감사 대상에서 제외할 사용자를 명시한다.

AUDIT POLICY 구문과 달리 NOAUDIT POLICY 구문에는 EXCEPT 옵션이 없다.

AUDIT POLICY name BY 절을 사용한 경우 NOAUDIT POLICY name BY 구문으로 비활성화하며   
AUDIT POLICY name EXCEPT 절을 사용한 경우 BY 절 없이 NOAUDIT POLICY name 구문으로 비활성화해야 한다.

AUDIT POLICY 구문의 사용 방법에 따라 다음과 같이 NOAUDIT POLICY 구문을 사용하여 해당 옵션을 비활성화해야 한다.

**Audit policy 활성화/ 비활성화**

<a id="f55fd92d57ef4fbe"></a>
| 유형 | AUDIT POLICY 구문 | NOAUDIT POLICY 구문 |
| --- | --- | --- |
| 전체 사용자 | AUDIT POLICY p1 | NOAUDIT POLICY p1 |
| BY를 사용 | AUDIT POLICY p1 BY u1 | NOAUDIT POLICY p1 BY u1 |
| EXCEPT를 사용 | AUDIT POLICY p1 EXCEPT u1 | NOAUDIT POLICY p1 |

활성화된 모든 user들을 비활성화한 경우, audit policy 객체가 완전히 비활성화된다.

<a id="ab3bab8c5bb0721f"></a>
### 설명

Audit policy 객체의 활성화 정보는 다음과 같이 조회한다.

```
SELECT policy_name
     , enabled_opt
     , user_name
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';
```

NOAUDIT POLICY 구문은 AUDIT POLICY 지정 방식에 따라 생성된 개별 활성화 정보를 삭제한다.   
위의 질의를 통해 활성화한 정보가 없을 경우, audit policy는 완전히 비활성화된다.

다음과 같이 모든 user를 활성화한 경우, NOAUDIT POLICY BY 절은 영향을 미치지 않는다.

```
AUDIT POLICY p1;
```

- 어떠한 영향도 미치지 않는다.

```
NOAUDIT POLICY p1 BY u1;
```

- 다음과 같이 비활성화해야 한다.

```
NOAUDIT POLICY p1;
```

하나 이상의 user들을 개별적으로 활성화한 경우 AUDIT POLICY 설정 방법에 따라 NOAUDIT POLICY 구문을 사용해야 한다.

<a id="19e3d8736b4bff0b"></a>
#### BY를 이용해 활성화한 경우

다음과 같이 audit policy를 활성화한 경우,

```
AUDIT POLICY p1 WHENEVER NOT SUCCESSFUL;
AUDIT POLICY p1 BY u1;
AUDIT POLICY p1 BY u2;
```

활성화 정보를 조회하면 다음과 같다.

```
SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

POLICY_NAME  ENABLED_OPT  USER_NAME    WHEN_SUCCESS  WHEN_FAILURE
-----------  -----------  ---------    ------------  ------------
P1           BY           ALL USERS    NO            YES
P1           BY           U1           YES           YES
P1           BY           U2           YES           YES
```

다음은 NOAUDIT POLICY 구문을 수행하고 활성화 정보를 조회하는 예이다.

```
NOAUDIT POLICY p1;

SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

POLICY_NAME  ENABLED_OPT  USER_NAME    WHEN_SUCCESS    WHEN_FAILURE
-----------  -----------  ---------    ------------    ------------
P1           BY           U1           YES             YES
P1           BY           U2           YES             YES
```

ALL USERS의 failure에 대한 감사가 비활성화되었으며, u1, u2 사용자에 대한 감사는 여전히 활성화되어 있다.

다음과 같이 BY 옵션을 통해 NOAUDIT POLICY 구문을 추가적으로 사용하면 audit policy p1은 완전히 비활성화된다.

```
NOAUDIT POLICY p1 BY u1, u2;

SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

no rows selected.
```

<a id="c417ff5323421a42"></a>
#### EXCEPT를 이용해 활성화한 경우

다음과 같이 audit policy를 활성화한 경우,

```
AUDIT POLICY p1 EXCEPT u1, sys;
```

활성화 정보를 조회하면 다음과 같다.

```
SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

POLICY_NAME  ENABLED_OPT  USER_NAME    WHEN_SUCCESS    WHEN_FAILURE
-----------  -----------  ---------    ------------    ------------
P1           EXCEPT       U1           YES             YES
P1           EXCEPT       SYS          YES             YES
```

AUDIT POLICY 구문과 달리 NOAUDIT POLICY 구문에는 EXCEPT option이 없으므로 다음과 같이 옵션 없이 구문을 수행한다.

```
NOAUDIT POLICY p1;

SELECT policy_name
     , enabled_opt
     , user_name
     , when_success
     , when_failure
  FROM audit_policy_enabled
 WHERE policy_name = 'P1';

no rows selected.
```

즉, EXCEPT 옵션을 이용해 audit policy를 활성화한 경우, NOAUDIT POLICY 구문으로 개별 사용자를 다시 비활성화할 수 없다.

<a id="bb35e8d15ec87c45"></a>
### 사용 예

다음은 전체 사용자를 비활성화한 예이다.

```
NOAUDIT POLICY table_pol;
```

다음은 BY를 사용하여 활성화된 특정 사용자를 비활성화하는 예이다.

```
NOAUDIT POLICY table_pol BY u1;
```

<a id="7f11c27c048b6f34"></a>
### 호환성

SQL 표준에는 audit policy가 없다.

<a id="c7267cc81ee75c5d"></a>
### 참조

관련 내용은 다음을 참조한다.

- Audit policy 객체 관리
    - [CREATE AUDIT POLICY](19-sql-references-c-g.md#079c12405d0687f7)
    - [DROP AUDIT POLICY](19-sql-references-c-g.md#5665b185fc830eaa)
    - [ALTER AUDIT POLICY](18-sql-references-a-b.md#e6d664ed42cb125a)

- Audit policy 활성화/ 비활성화
    - [AUDIT POLICY](18-sql-references-a-b.md#c26186987b5864cf)
    - [NOAUDIT POLICY](#2a39421bd3a74134)

- Audit trail 조회: [AUDIT_TRAIL](../part-02-administration-manual/9-database-information.md#28a87ad95b910b03)

- Audit trail 제거: [ALTER DATABASE CLEAR AUDIT TRAIL](18-sql-references-a-b.md#f4b53fa2e7dce2b7)

<a id="674c9a50006ee689"></a>
## OPEN cursor_name

<a id="5c3a610d43d0d2a3"></a>
### 기능

커서를 연다.

<a id="e3e01506d44d8c08"></a>
### 구문

```
<open statement> ::=
    OPEN cursor_name [ <parameter using clause> ]
    ;

<parameter using clause> ::=
      <using parameter arguments>

<using parameter arguments> ::=
    USING variable_name [, ...]
```

<a id="d81a232ea9f54414"></a>
### 사용 범위 및 접근 권한

cursor_name이 [PREPARE statement_name](#d5d393507a5fefe6) 구문과 [DECLARE cursor_name](19-sql-references-c-g.md#d0200d8897a107da) 구문을 사용해 선언한 동적 커서인 경우 embedded SQL에서 사용 가능하다.

cursor_name을 선언한 [DECLARE cursor_name](19-sql-references-c-g.md#d0200d8897a107da) 구문에 포함된 [&lt;cursor query&gt;](19-sql-references-c-g.md#c3e59d4f58b86b2a)의 권한과 동일하다.

<a id="3fd957a6d49cd41f"></a>
### 구문 규칙 및 파라미터

<a id="fccfc24030fa7a78"></a>
#### cursor_name

세션 내에서 [DECLARE cursor_name](19-sql-references-c-g.md#d0200d8897a107da) 구문으로 선언된 커서이어야 한다.

<a id="1d9109bf379ff239"></a>
#### &lt;parameter using clause&gt;

Embedded SQL에서 사용할 수 있다.

&lt;parameter using clause&gt; 구문이 사용될 경우, cursor_name이 [PREPARE statement_name](#d5d393507a5fefe6) 구문과 [DECLARE cursor_name](19-sql-references-c-g.md#d0200d8897a107da) 구문을 이용해 선언한 동적 커서여야 한다.

<a id="de1b52262e7fba80"></a>
#### &lt;using parameter arguments&gt;

&lt;using parameter arguments&gt; 구문이 사용될 경우, variable_name의 개수는 [PREPARE statement_name](#d5d393507a5fefe6) 구문이 참조하는 query 문장에 포함된 parameter의 개수와 동일해야 한다.

variable_name은 나열된 순서에 따라 dynamic parameter에 순서대로 대응된다.

```
{
    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT c1, c2 FROM t1 WHERE c1 IN ( ?, ?, ? )';
    EXEC SQL DECLARE cur1 CURSOR FOR stmt1;
    EXEC SQL OPEN cur1 USING :sValue1, :sValue2, :sValue3;
    ...
    EXEC SQL WHENEVER NOT FOUND DO break;
    for(;;)
    {
        EXEC SQL FETCH cur1 INTO :sC1, :sC2;    
    }
    EXEC SQL WHENEVER NOT FOUND CONTINUE;
    ...
    EXEC SQL CLOSE cur1;    
    ... 
}
```

<a id="5f416ba88723f697"></a>
### 설명

Cursor는 session 내에서 구별되는 객체이며, 현재 session 내에서 사용되고 있는 cursor는 다른 session에서 사용되고 있는 cursor와 무관하다.

OPEN cursor_name 구문을 사용하려면 [DECLARE cursor_name](19-sql-references-c-g.md#d0200d8897a107da) 구문으로 선언된 커서여야 하며, 커서는 닫혀 있는 상태여야 한다.

<a id="e5fa15434b7c2546"></a>
### 사용 예

다음은 interactive SQL (gsql)에서 cursor를 선언하고 OPEN cursor 구문을 사용하는 예이다.

```
gSQL> DECLARE cur1 CURSOR FOR SELECT id, data FROM t1;

Cursor declared.

gSQL> OPEN cur1;

Cursor is open.

gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   1 data_1

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   2 data_2

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   3 data_3

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   4 data_4

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

V_ID V_DATA
---- ------
   5 data_5

1 row fetched.

gSQL> FETCH cur1 INTO :v_id, :v_data;

no rows fetched.

gSQL> CLOSE cur1;

Cursor closed.
```

<a id="c77433f722d88446"></a>
### 호환성

**SQL 표준 호환성**

<a id="df12c525b1aef389"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic dynamic SQL | O |

<a id="7a80bb51a567fd37"></a>
### 참조

관련 내용은 다음을 참조한다.

- [DECLARE cursor_name](19-sql-references-c-g.md#d0200d8897a107da)
- [FETCH cursor_name](19-sql-references-c-g.md#189c41bd169bad81)
- [CLOSE cursor_name](19-sql-references-c-g.md#98a34ae5c82860ff)
- [PREPARE statement_name](#d5d393507a5fefe6)

<a id="d5d393507a5fefe6"></a>
## PREPARE statement_name

<a id="836e1192706b13d0"></a>
### 기능

반복 수행을 위한 dynamic SQL 문장을 준비한다.

<a id="e95396fb727f61f0"></a>
### 구문

```
<prepare statement> ::=
    PREPARE statement_name FROM <SQL statement variable>
    ;

<SQL statement variable> ::=
      variable_name
    | 'sql statement'
    | "sql statement"
    | sql statement
```

<a id="23d49442bf1d618c"></a>
### 사용 범위 및 접근 권한

Embedded SQL에서 사용할 수 있다.  
Dynamic SQL 구문의 종류에 부합하는 수행 권한이 있어야 한다.

<a id="d6ab9bc23fc6fc6b"></a>
### 구문 규칙 및 파라미터

<a id="e282a0a7a02af6dd"></a>
#### statement_name

준비할 statement의 이름이다.  
statement 이름의 길이는 128 바이트보다 작아야 한다.  
이후에 수행될 [EXECUTE statement_name](19-sql-references-c-g.md#7dafd7d0e446b4b9) 구문 또는 [DECLARE cursor_name](19-sql-references-c-g.md#d0200d8897a107da) 구문은 statement_name을 참조한다.  
동일한 statement_name이 존재할 경우, 이전에 준비된 dynamic SQL은 삭제된다.

```
{
    ...

    EXEC SQL PREPARE stmt1 FROM 'DELETE FROM t1';
    ...
    EXEC SQL PREPARE stmt1 FROM 'UPDATE t1 SET c1 = c1 + 10';
    ...
}
```

<a id="c84a255b50d0765c"></a>
#### &lt;SQL statement variable&gt;

&lt;SQL statement variable&gt;은 다음과 같이 네 가지 유형으로 사용된다.

- variable_name: SQL이 저장된 변수 
- 'sql statement': Single quote (')로 묶인 SQL 문장 
- "sql statement": Double quote (")로 묶인 SQL 문장 
- sql statement: Quote 없는 SQL 문장

Single-quoted string 내에 문자열 data를 표현하려면 다음과 같이 single quote (')를 두 번 기술한다.

```
{
    ...
    PREPARE stmt_name FROM 'INSERT INTO t1 VALUES ( ''literal data'' )'; 
    ...
}
```

&lt;SQL statement variable&gt;이 참조하는 dynamic SQL 문장은 host 변수 (:var)나 parameter marker (?)를 사용할 수 있다.   
단, quote 없는 SQL 문장을 사용할 경우 parameter marker (?)를 사용할 수 없다.

참조되는 dynamic SQL 문장의 특성에 따라 변수는 input 또는 output dynamic parameter가 된다.  
Dynamic SQL 문장 내에 기술된 dynamic parameter는 변수의 이름이 아무 의미가 없으며 종류에 관계없이 구문에 기술된 순서에 따라 식별된다.

- 예제 1

```
{
    ...
    int sValue1;
    int sValue2;
    ...
    EXEC SQL PREPARE stmt1 FROM 'DELETE FROM t1 WHERE c1 BETWEEN ? AND ?';
    EXEC SQL EXECUTE stmt1 USING :sValue1, :sValue2;   
    ...
}
```

- 모든 parameter marker가 input dynamic parameter이다. 
- 식별 순서 
    - 1번 - BETWEEN ? 
        - input dynamic parameter 
        - :sValue1 값을 사용한다. 
    - 2번 - AND ? 
        - input dynamic parameter 
        - :sValue2 값을 사용한다.

- 예제 2

```
{
    ...
    int sValue1;
    int sValue2;
    ...
    EXEC SQL PREPARE stmt1 FROM 'SELECT SUM(c2) INTO :v1 FROM t1 WHERE c1 > :v2';
    EXEC SQL EXECUTE stmt1 USING :sValue1, :sValue2;
    ...
}
```

- input dynamic parameter와 output dynamic parameter가 존재한다. 
- 식별 순서 
    - 1번 - :v1 
        - output dynamic parameter 
        - :sValue1에 값이 저장된다. 
    - 2번 - :v2 
        - input dynamic parameter 
        - :sValue2 값을 사용한다.

<a id="c82b38eb27c0b62c"></a>
#### variable_name

variable_name에 대응하는 type은 character string이어야 한다.   
variable_name에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="9b682991fb930e2c"></a>
#### sql statement

sql statement에 정의된 dynamic SQL 문장은 유효한 문장이어야 한다.

<a id="458f0b874e3cf573"></a>
### 설명

PREPARE statement_name FROM sql_string 구문은 EXECUTE나 cursor를 사용하기 위해 SQL 문을 분석한다. statement_name은 embedded SQL 소스 코드에서 precompiler에게 statement를 알려주는 식별자로써 host variable이 아니기 때문에 별도의 type이나 선언이 필요하지 않다.

자세한 내용은 [Embedded Dynamic SQL](../part-05-developer-manual/36-embedded-sql.md#70d95d21f1b0a78f)을 참조한다.

<a id="b94bfef055c86646"></a>
### 사용 예

다음은 embedded SQL 소스 코드 내에서 PREPARE statement_name를 사용하는 예이다.

```
{
    ...
    sprintf( sUpdateSql, "UPDATE EMP SET sal = sal * :v1 WHERE JOB = 'SALES'");
    EXEC SQL PREPARE UPDATE_STMT FROM :sUpdateSql;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    sRatio = 1.1;
    EXEC SQL EXECUTE UPDATE_STMT USING :sRatio;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    ...
}
```

PREPARE statement_name이 사용된 전체 소스 코드는 [Dynamic Embedded SQL Example Program](../part-05-developer-manual/36-embedded-sql.md#96d2b117af21a815)에서 확인할 수 있다.

<a id="fcf3cef3b32d831e"></a>
### 호환성

**SQL 표준 호환성**

<a id="a93a07c9ba5f4662"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B031 | Basic Dynamic SQL | O |
| B034 | Dynamic specification of cursor attributes | X |

<a id="dac0884e78959fd5"></a>
### 참조

관련 내용은 다음을 참조한다.

- [EXECUTE statement_name](19-sql-references-c-g.md#7dafd7d0e446b4b9)
- [DECLARE cursor_name](19-sql-references-c-g.md#d0200d8897a107da)
- [EXECUTE IMMEDIATE 'sql_string'](19-sql-references-c-g.md#c36765396dd362e5)
- [Embedded Dynamic SQL](../part-05-developer-manual/36-embedded-sql.md#70d95d21f1b0a78f)

<a id="a7e56bce11b6b2cf"></a>
## PURGE

<a id="7cda0939d4daac8a"></a>
### 기능

휴지통에 저장되어 있는 객체들을 영구적으로 제거한다.

<a id="7017fd3504de5f18"></a>
### 구문

```
<purge statement> :==
    PURGE <purge action>
    ;

<purge action> :==
     TABLE table_name
   | INDEX index_name
   | CONSTRAINT constraint_name
   | TRIGGER trigger_name  
   | TABLESPACE tablespace_name [ USER user_name ]
   | RECYCLEBIN 
   | USER_RECYCLEBIN
   | DBA_RECYCLEBIN
```

<a id="be2575be69fb74fb"></a>
### 사용 범위 및 접근 권한

&lt;purge statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 해당 테이블의 소유자 
- 해당 테이블에 대해 CONTROL TABLE ON TABLE 
- 테이블이 속한 스키마에 대해 (DROP TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY TABLE ON DATABASE

<a id="73c54bed7fd8e2f9"></a>
### 구문 규칙 및 파라미터

<a id="06bc0e2772d11508"></a>
#### table_name

휴지통에 저장된 객체 이름 또는 제거된 테이블의 이름이다.  
제거된 테이블의 이름에는 schema_name.table_name과 같이 테이블이 소속한 스키마를 정의할 수 있으며, schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
테이블과 관련된 인덱스와 제약 조건들도 함께 제거된다.

<a id="8c8dfb87df293e76"></a>
#### index_name

휴지통에 저장된 객체 이름 또는 제거된 인덱스의 이름이다.  
schema_name.index_name과 같이 인덱스가 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우, 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.  
제약 조건으로 생성된 key 인덱스는 제약 조건으로 삭제해야 한다.

<a id="3ba093352e69f339"></a>
#### constraint_name

휴지통에 저장된 객체 이름 또는 삭제된 제약 조건의 이름이다.

<a id="c7982825edc03999"></a>
#### trigger_name

휴지통에 저장된 객체 이름 또는 삭제된 trigger의 이름이다.

<a id="d7dd2ce7b55adf0d"></a>
#### tablespace_name

테이블스페이스의 이름이다.  
USER를 지정할 때는 DROP ANY TABLE ON DATABASE 권한이 필요하다.

<a id="41ae82e8050799b3"></a>
#### user_name

사용자의 이름이다.

<a id="ef20d877aaee3f69"></a>
#### recyclebin

user_recyclebin의 alias 이다.

<a id="9089162091751c13"></a>
#### user_recyclebin

사용자가 소유한 휴지통을 모두 제거한다.

<a id="9909545f751f38f1"></a>
#### dba_recyclebin

데이터베이스의 모든 휴지통을 제거한다.  
PURGE DBA_RECYCLEBIN ON DATABASE 권한이 필요하다.

<a id="3470006034d011ec"></a>
### 설명

휴지통에 저장된 객체 이름이나 제거된 테이블의 이름을 사용하여 휴지통에 보관되어 있는 객체들을 영구적으로 제거한다. 만약 제거 대상 테이블과 동일한 이름의 테이블이 있는 경우, 가장 오래된 객체를 제거한다.

사용자가 소유한 휴지통 객체에서 테이블스페이스를 지정하여 테이블스페이스에 포함된 객체들을 제거할 수 있는데 이 때 사용자를 지정하면 해당 사용자의 명시된 테이블스페이스에 포함된 객체들만 제거할 수 있다.

PURGE TABLE, INDEX, CONSTRAINT 구문은 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다. 반면 PURGE TABLESPACE, RECYCLEBIN, DBA_RECYCLEBIN 구문은 ROLLBACK 할 수 없으며, 구문을 수행한 트랜잭션이 자동으로 COMMIT 된다.

<a id="fc07ef34f2107af2"></a>
### 사용 예

다음은 휴지통에 저장된 테이블을 제거하는 예이다.

```
gSQL> SELECT OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

OBJECT_NAME                          ORIGINAL_NAME        OBJECT_TYPE
------------------------------------ -------------------- -----------
BIN$135B9908166111EA9C5C835D3E4BBBF7 T1                   TABLE      
BIN$135B993A166111EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY       CONSTRAINT 
BIN$135B991C166111EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY_INDEX INDEX      
BIN$135B9926166111EA9C5C835D3E4BBBF7 T1_IDX1              INDEX      

4 rows selected.

gSQL> PURGE TABLE t1;

Table purged.
```

다음은 휴지통에 저장된 인덱스를 제거하는 예이다.

```
gSQL> SELECT OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

OBJECT_NAME                          ORIGINAL_NAME        OBJECT_TYPE
------------------------------------ -------------------- -----------
BIN$135B9908166111EA9C5C835D3E4BBBF7 T1                   TABLE      
BIN$135B993A166111EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY       CONSTRAINT 
BIN$135B991C166111EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY_INDEX INDEX      
BIN$135B9926166111EA9C5C835D3E4BBBF7 T1_IDX1              INDEX      

4 rows selected.

gSQL> PURGE INDEX t1_idx1;

Index purged.
```

다음은 휴지통에 저장된 제약 조건을 제거하는 예이다.

```
gSQL> SELECT OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

OBJECT_NAME                          ORIGINAL_NAME        OBJECT_TYPE
------------------------------------ -------------------- -----------
BIN$135B9908166111EA9C5C835D3E4BBBF7 T1                   TABLE      
BIN$135B993A166111EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY       CONSTRAINT 
BIN$135B991C166111EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY_INDEX INDEX      

3 rows selected.

gSQL> PURGE CONSTRAINT t1_primary_key;

Constraints purged.
```

다음은 휴지통에 저장된 테이블스페이스에 포함된 객체들을 제거하는 예이다.

```
gSQL> SELECT OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE, TABLESPACE_NAME FROM USER_RECYCLEBIN;

OBJECT_NAME                          ORIGINAL_NAME OBJECT_TYPE TABLESPACE_NAME
------------------------------------ ------------- ----------- ---------------
BIN$02C76B24166311EA9C5C835D3E4BBBF7 T1            TABLE       MEM_DATA_TBS   

1 row selected.

gSQL> PURGE TABLESPACE MEM_DATA_TBS;

Tablespace purged.
```

다음은 사용자가 소유한 휴지통을 모두 제거하는 예이다.

```
gSQL> SELECT OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

OBJECT_NAME                          ORIGINAL_NAME        OBJECT_TYPE
------------------------------------ -------------------- -----------
BIN$64F6BFFC166311EA9C5C835D3E4BBBF7 T1                   TABLE      
BIN$64F6C042166311EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY       CONSTRAINT 
BIN$64F6C010166311EA9C5C835D3E4BBBF7 T1_PRIMARY_KEY_INDEX INDEX      
BIN$64F6C024166311EA9C5C835D3E4BBBF7 T1_IDX1              INDEX      

4 rows selected.

gSQL> PURGE USER_RECYCLEBIN;

Recyclebin purged.
```

다음은 시스템의 모든 휴지통을 제거하는 예이다.

```
gSQL> SELECT OWNER, OBJECT_NAME, ORIGINAL_NAME, OBJECT_TYPE FROM USER_RECYCLEBIN;

OWNER OBJECT_NAME                          ORIGINAL_NAME        OBJECT_TYPE
----- ------------------------------------ -------------------- -----------
TEST  BIN$F0FB26F0166311EAA7C5D51B86D72AB6 T1                   TABLE      
TEST  BIN$F0FB272C166311EAA7C5D51B86D72AB6 T1_PRIMARY_KEY       CONSTRAINT 
TEST  BIN$F0FB2704166311EAA7C5D51B86D72AB6 T1_PRIMARY_KEY_INDEX INDEX      
TEST  BIN$F0FB2718166311EAA7C5D51B86D72AB6 T1_IDX1              INDEX      

4 rows selected.

gSQL> PURGE DBA_RECYCLEBIN;

DBA Recyclebin purged.
```

<a id="cfed67766f01c2c2"></a>
### 호환성

SQL 표준에서는 &lt;purge statement&gt;를 다루지 않고 있다.

<a id="3e010d86b04d2066"></a>
### 참조

관련 내용은 다음을 참조한다.

- [테이블 휴지통 관리](13-sql-objects.md#3292cebd4a0cc225)
- [FLASHBACK TABLE](19-sql-references-c-g.md#c55e929f3b9856f0)

<a id="820eff57a94d3af0"></a>
## RELEASE SAVEPOINT savepoint_specifier

<a id="cb57edd9f3912568"></a>
### 기능

저장점을 제거한다.

<a id="9c165abd1483cc19"></a>
### 구문

```
<release savepoint statement> ::=
    RELEASE SAVEPOINT savepoint_name 
    ;
```

<a id="70ee9f544a8c612e"></a>
### 구문 규칙 및 파라미터

<a id="8da48c85d9acd910"></a>
#### savepoint_name

저장점의 이름으로써 반드시 존재해야 한다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="67ceca81bc617941"></a>
### 설명

다수의 savepoint가 정의되어 있을 경우, RELEASE SAVEPOINT savepoint_name 구문을 수행할 때savepoint_name 이후에 정의된 savepoint도 함께 제거된다.

<a id="1c6a75e881dc2370"></a>
### 사용 예

다음은 savepoint를 제거하는 예이다.

```
gSQL> RELEASE SAVEPOINT sp2;

Savepoint dropped.
```

<a id="fbbab1dc37537576"></a>
### 호환성

**SQL 표준 호환성**

<a id="db510b7714a9e344"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T271 | Savepoints | O |

<a id="54af51cce0b5d258"></a>
### 참조

관련 내용은 다음을 참조한다.

- [COMMIT](19-sql-references-c-g.md#9d9942a1324d8ced)
- [ROLLBACK](#1ba3b433854d9411)
- [SAVEPOINT savepoint_specifier](#903816d217929cbc)

<a id="dd5b2688d6e617c1"></a>
## REVOKE privileges FROM

<a id="ce07abfbf50c7e54"></a>
### 기능

사용자 또는 role에게 부여된 권한을 취소한다.

<a id="429182bb22b5c3e1"></a>
### 구문

```
<revoke privilege statement> ::=
    REVOKE [ <revoke option extention> ] <privilege>
      FROM <grantee> [, ...]
      [ <revoke behavior> ]
    ;

<revoke option extention> ::=
      GRANT OPTION FOR

<grantee> ::=
      PUBLIC
    | <user_identifier>
    | <role_name>

<revoke behavior> ::=
      RESTRICT
    | CASCADE
    | CASCADE CONSTRAINTS
```

<a id="bed2df97790a5706"></a>
### 구문 규칙 및 파라미터

<a id="19f5dbad5fd58e9c"></a>
#### &lt;privilege&gt;

Revokee (권한을 취소당할 사용자 또는 role)로부터 취소할 권한이다.

Revoker (구문을 수행하는 사용자)는 다음 조건 중 하나를 만족해야 한다.

- Revoker가 revokee에게 부여한 &lt;privilege&gt;의 경우 
    - Revoker가 revokee에게 부여한 &lt;privilege&gt;만 취소한다. 
- Revoker가 ACCESS CONTROL ON DATABASE 권한을 소유한 경우
    - 다른 grantor들이 revokee에게 부여한 &lt;privilege&gt;들을 취소한다.

ALL [PRIVILEGES]를 사용하는 경우, 만족하는 &lt;privilege&gt;가 없더라도 성공한다.

&lt;privilege&gt; 종류에 대한 내용은 [GRANT privileges TO](19-sql-references-c-g.md#3283bbfc30fb00b0) 구문의 [&lt;privilege&gt;](19-sql-references-c-g.md#e4df850b21114c76) 절을 참조한다.

<a id="45bab7be55a009c5"></a>
#### &lt;grantee&gt;

권한을 취소당할 사용자 또는 role이다.

- &lt;user_identifier&gt;
    - 해당 사용자의 권한을 취소한다
- &lt;role_name&gt;
    - 해당 role의 권한을 취소한다.
- PUBLIC 
    - 모든 사용자와 role을 의미하는 authorization 객체이다.

<a id="98ef4e24fffdc8ae"></a>
#### GRANT OPTION FOR

권한에 포함된 WITH GRANT OPTION을 삭제한다.   
Dependent privilege의 WITH GRANT OPTION도 함께 삭제한다.

권한은 그대로 유지된다.

<a id="1caebe158c1a6af5"></a>
#### &lt;revoke behavior&gt;

- Dependent privilege: WITH GRANT OPTION으로 &lt;privilege&gt;를 부여받은 revokee가 다른 사용자에게 부여한 것과 동일한 &lt;privilege&gt;이다.
- RESTRICT 
    - Dependent privilege가 존재할 경우 revoke 할 수 없다. 
- CASCADE 
    - Dependent privilege도 함께 revoke 한다.
- CASCADE CONSTRAINTS 
    - Dependent privilege도 함께 revoke 한다.
- 생략할 경우, 기본값은 CASCADE 이다.

<a id="1ef5be432df7559f"></a>
### 설명

REVOKE privilege와 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

다음과 같은 DROP 구문을 수행할 경우, 별도로 REVOKE 구문을 수행하지 않더라도 해당 객체와 관련된 모든 권한 정보가 삭제된다.

- SQL schema object 관련 DROP 구문
    - [DROP TABLE](19-sql-references-c-g.md#cdb39a166c5e9daf)
    - [DROP VIEW](19-sql-references-c-g.md#cad962c71dd7d5e3)
    - [DROP SEQUENCE](19-sql-references-c-g.md#a567fca70147b0b5)
    - [ALTER TABLE name SET UNUSED COLUMN](18-sql-references-a-b.md#2389dc92f034f678)
    - [DROP FUNCTION](../part-04-sql-psm-manual/31-psm-sql-references.md#799b77ea31fecf81)
    - [DROP PROCEDURE](../part-04-sql-psm-manual/31-psm-sql-references.md#47bed13ab733e3a0)
    - [DROP PACKAGE](../part-04-sql-psm-manual/31-psm-sql-references.md#561079b3305fcaea)
    - [DROP LIBRARY](../part-04-sql-psm-manual/31-psm-sql-references.md#11be420b5d5517c9)
    - [DROP TRIGGER](../part-04-sql-psm-manual/31-psm-sql-references.md#405a8fa6b4a11ae3)

- Non-schema object 관련 DROP 구문
    - [DROP SCHEMA](19-sql-references-c-g.md#f7dd83119c08a573)
    - [DROP TABLESPACE](19-sql-references-c-g.md#6f8b24f831f2bd7f)
    - [DROP USER](19-sql-references-c-g.md#19e745a811890279)

<a id="f5a6b8d928a178d1"></a>
### 사용 예

다음은 table t1에 대한 다수의 권한을 REVOKE하는 예이다.

```
gSQL> REVOKE INSERT, UPDATE, DELETE, LOCK, ALTER, INDEX ON t1 FROM u1;

Revoke succeeded.
```

다음은 모든 authorization (사용자와 role)을 의미하는 PUBLIC 계정에 부여된 SELECT ON TABLE t1 권한을 REVOKE 하는 예이다. 단, PUBLIC 계정의 권한만 제거될 뿐, 특정 사용자 또는 role에게 명시적으로 부여된 SELECT ON TABLE t1 권한이 제거되는 것은 아니다.

```
gSQL> REVOKE SELECT ON t1 FROM PUBLIC;

Revoke succeeded.
```

다음은 user u1에게 부여된 SELECT ON TABLE t1 권한은 그대로 두고 다른 사용자에게 해당 권한을 부여할 수 있는 GRANT OPTION만 REVOKE하는 예이다.

```
gSQL> REVOKE GRANT OPTION FOR SELECT ON t1 FROM u1;

Revoke succeeded.
```

다음은 RESTRICT 옵션을 이용해 user u1에게 부여한 권한을 REVOKE 하면서 u1이 다른 사용자에게 해당 권한을 부여할 경우 에러가 발생하는 예이다. 이런 dependent privilege들도 함께 제거하려 할 경우 CASCADE 옵션을 사용한다.

```
gSQL> REVOKE SELECT ON t1 FROM u1 RESTRICT;

ERR-2B000(16235): dependent privilege descriptors still exist

gSQL> REVOKE SELECT ON t1 FROM u1 CASCADE;

Revoke succeeded.
```

다음은 role1에게서 table t1에 대한 다수의 권한을 REVOKE 하는 예이다.

```
gSQL> REVOKE INSERT, UPDATE, DELETE, LOCK, ALTER, INDEX ON t1 FROM role1;

Revoke succeeded.
```

<a id="9f8b88cdd78f6ef3"></a>
### 호환성

SQL 표준에서는 다음 privilege들을 정의하지 않고 있다.

- &lt;database privilege&gt; 
- &lt;tablespace privilege&gt; 
- &lt;schema privilege&gt;

SQL 표준의 &lt;revoke behavior&gt;와는 다음과 같은 차이가 있다.

- SQL 표준의 기본값은 RESTRICT 이다. 
- SQL 표준은 CASCADE CONSTRAINTS 가 없다.

**SQL 표준 호환성**

<a id="b45a0a7112b6b08e"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T331 | Basic roles | O |
| T332 | Extended roles | X |
| F034 | Extended REVOKE statement | O |
| S081 | Subtables | X |

<a id="f45ec4dd58362d82"></a>
### 참조

관련 내용은 다음을 참조한다.

- [GRANT privileges TO](19-sql-references-c-g.md#3283bbfc30fb00b0)
- [&lt;database privilege&gt;](19-sql-references-c-g.md#e6dbfe1d5eb190a0)
- [&lt;tablespace privilege&gt;](19-sql-references-c-g.md#5f934a4bfca2d678)
- [&lt;schema privilege&gt;](19-sql-references-c-g.md#9f087336634921ca)
- [&lt;table privilege&gt;](19-sql-references-c-g.md#ed9520102f5a17a2)
- [Column privilege ](19-sql-references-c-g.md#2736a7461ac07dc1)
- &lt;[sequence privilege&gt;](19-sql-references-c-g.md#ad1a917985398383)

<a id="25b534416caec4de"></a>
## REVOKE role FROM

<a id="976b465852de0866"></a>
### 기능

다른 사용자나 role에게 부여된 role을 취소한다.

<a id="9bc63f0810c5e6e0"></a>
### 구문

```
<revoke role statement> ::=
     REVOKE [ ADMIN OPTION FOR ] <role revoked> [ , ...... ] 
            FROM <grantee> [ , ...... ]
     ;

<grantee> ::=
      PUBLIC
    | <user_identifier>
    | <role_name>

<role revoked> ::=
     <role_name>
```

<a id="62454fcc72b27200"></a>
### 사용 범위 및 접근 권한

&lt;revoke role statement&gt; 구문을 수행하기 위해서는 다음 조건 중 하나를 만족해야 한다.

- 사용자에게 GRANT ROLE ON DATABASE 권한이 있어야 한다.
- &lt;role_name&gt;에 대한 WITH ADMIN OPTION이 부여되어야 한다.

<a id="572426e66ce7d79a"></a>
### 구문 규칙 및 파라미터

<a id="419901c0ee69c1a6"></a>
#### &lt;role revoked&gt;

Role을 취소하고자 하는 role 이름이다.

<a id="f1e7df920ce9e7ae"></a>
#### &lt;grantee&gt;

Role을 취소당할 사용자 또는 role이다.

- &lt;user_identifier&gt;
    - 해당 사용자의 role을 취소한다
- &lt;role_name&gt;
    - 해당 role의 role을 취소한다.
- PUBLIC 
    - 모든 사용자와 role을 의미하는 authorization 객체이다.

<a id="db655fcfe8b24324"></a>
#### ADMIN OPTION FOR

Role에 대한 WITH ADMIN OPTION을 삭제한다.  
부여된 role은 그대로 유지된다.

<a id="75be12a41fd8a016"></a>
### 설명

다른 사용자나 role에게서 role을 회수한다.  
REVOKE role과 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.  
[DROP ROLE](19-sql-references-c-g.md#84a501362442f591)을 수행할 경우, 별도로 REVOKE role 구문을 수행하지 않더라도 부여된 role 정보는 모두 삭제된다.

<a id="8df4eb50624fdc1d"></a>
### 사용 예

다음은 GRANT ROLE ON DATABASE 권한이 있는 사용자가 role을 취소하는 예이다.

```
gSQL> GRANT GRANT ROLE ON DATABASE TO u1;

Grant succeeded.

gSQL> SELECT grantee, privilege
        FROM dba_sys_privs
       WHERE grantee = 'U1';

GRANTEE PRIVILEGE                  
------- ---------------------------
U1      CREATE SESSION ON DATABASE 
U1      GRANT ROLE ON DATABASE     

2 rows selected.

gSQL> SELECT grantee, granted_role, admin_option 
        FROM dba_role_privs 
       WHERE granted_role = 'ROLE1';

GRANTEE GRANTED_ROLE ADMIN_OPTION
------- ------------ ------------
ROLE2   ROLE1        NO          

1 row selected.

gSQL> \connect u1 u1

gSQL> REVOKE role1 FROM role2;

Revoke succeeded.
```

다음은 role에 대한 WITH ADMIN OPTION이 있는 사용자가 role을 취소하는 예이다.

```
gSQL> GRANT role1 TO u1 WITH ADMIN OPTION;

Grant succeeded.

gSQL> SELECT grantee, privilege
        FROM dba_sys_privs
       WHERE grantee = 'U1';

GRANTEE PRIVILEGE                  
------- ---------------------------
U1      CREATE SESSION ON DATABASE 

1 row selected.

gSQL> SELECT grantee, granted_role, admin_option 
        FROM dba_role_privs 
       WHERE granted_role = 'ROLE1';

GRANTEE GRANTED_ROLE ADMIN_OPTION
------- ------------ ------------
ROLE2   ROLE1        NO          
U1      ROLE1        YES         

2 rows selected.


gSQL> \connect u1 u1

gSQL> REVOKE role1 FROM role2;

Revoke succeeded.
```

<a id="ae6eb7520f501837"></a>
### 호환성

**SQL 표준 호환성**

<a id="3f120aa1a1bbd095"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T331 | Basic roles | O |
| T332 | Extended roles | X |
| F034 | Extended REVOKE statement | O |
| S081 | Subtables | X |

<a id="10e23a5bbebb656e"></a>
### 참조

관련 내용은 다음을 참조한다.

- [GRANT role TO](19-sql-references-c-g.md#fd27b8c95b0f1bc2)
- [DROP ROLE](19-sql-references-c-g.md#84a501362442f591)

<a id="1ba3b433854d9411"></a>
## ROLLBACK

<a id="65d5c120b8d13bea"></a>
### 기능

트랜잭션을 취소하거나, 저장점 이후의 작업을 취소한다.

<a id="4310199658159f8d"></a>
### 구문

```
<rollback statement> ::=
    ROLLBACK [ WORK ] [ <rollback force clause> | <savepoint clause> ]
    ;

<rollback force clause> ::=
    FORCE 'xid_string' [ COMMENT 'comment_string' ]

<savepoint clause> ::=
    TO SAVEPOINT savepoint_name
```

<a id="9925d27882d7d077"></a>
### 구문 규칙 및 파라미터

<a id="63b5972e5b08136b"></a>
#### WORK

동작에 영향을 미치지 않는 예약어이다.

<a id="ca7bf93593ebc431"></a>
#### &lt;rollback force clause&gt;

분산 트랜잭션을 수동으로 rollback 할 때 사용한다.

- FORCE 'xid_string'
    - 'xid_string'에 해당하는 분산 트랜잭션을 rollback 한다.
    - 'xid_string'은 'format_id.transaction_id.branch_id'로 구성된다.
- COMMENT 'comment_string'
    - 분산 트랜잭션을 rollback 할 때 트랜잭션에 주석을 지정한다.

<a id="6fb076ee3d3cc611"></a>
#### &lt;savepoint clause&gt;

현재 트랜잭션의 ROLLBACK 범위를 명시한다.

- 명시하지 않은 경우 
    - 현재 트랜잭션의 모든 작업을 취소한다. 
    - 트랜잭션을 종료한다. 
    - 모든 savepoint 들을 제거한다. 
    - 모든 lock 들을 해제한다.

- TO SAVEPOINT savepoint_name 
    - 현재 트랜잭션에서 savepoint_name 이후의 작업을 취소한다. 
    - 트랜잭션을 종료하지는 않는다. 
    - savepoint_name 이후의 savepoint 들을 제거한다. 
    - savepoint_name 이후에 획득한 lock 들을 해제한다.

<a id="85d2346395376632"></a>
### 설명

ROLLBACK 구문은 트랜잭션 내에서 수행된 다음 구문들을 rollback 한다.

- Data Manipulation Language (DML) 구문
    - 데이터를 변경하는 INSERT, UPDATE, DELETE 등의 구문
- Data Definition Language (DDL) 구문 
    - 객체의 구조 및 정의를 변경하는 CREATE, DROP, ALTER, TRUNCATE, GRANT, REVOKE 등의 구문

예외적으로, DDL 중에 OS 자원을 다루거나 DATA TYPE을 변경하는 다음 구문들은 rollback 되지 않고 구문을 수행할 때 자동으로 COMMIT 된다.

- [CREATE TABLESPACE](19-sql-references-c-g.md#6b51bf8a71edc61b)
- [DROP TABLESPACE](19-sql-references-c-g.md#6f8b24f831f2bd7f)
- [ALTER TABLESPACE](18-sql-references-a-b.md#7d3341dc7c3f738f)
- ALTER TABLE .. ALTER COLUMN .. SET DATA TYPE: [&lt;alter column data type clause&gt;](18-sql-references-a-b.md#c3cbf4f521dbd868)

<a id="430380d069154080"></a>
### 사용 예

다음은 INSERT 구문을 ROLLBACK 하는 예이다.

```
gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous

1 row selected.

gSQL> ROLLBACK;

Rollback complete.

gSQL> SELECT * FROM t1;

no rows selected.
```

다음은 DROP TABLE 구문을 수행한 후에 이를 ROLLBACK 하는 예이다.

```
gSQL> DROP TABLE t1;

Table dropped.

gSQL> SELECT * FROM t1;

ERR-42000(16040): table or view does not exist : 
SELECT * FROM t1
              *
ERROR at line 1:

gSQL> ROLLBACK;

Rollback complete.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous

1 row selected.
```

<a id="46ca35933389dc37"></a>
### 호환성

**SQL 표준 호환성**

<a id="dad262222536224d"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T271 | Savepoints | O |
| T261 | Chained transactions | X |

<a id="d4f52243c878ac3c"></a>
### 참조

관련 내용은 다음을 참조한다.

- [COMMIT](19-sql-references-c-g.md#9d9942a1324d8ced)
- [SAVEPOINT savepoint_specifier](#903816d217929cbc)

<a id="903816d217929cbc"></a>
## SAVEPOINT savepoint_specifier

<a id="b21c6e3314573c4c"></a>
### 기능

저장점을 정의한다.

<a id="d5c95cb3456f4c74"></a>
### 구문

```
<savepoint statement> ::=
    SAVEPOINT savepoint_name 
    ;
```

<a id="63814c1c59d5d782"></a>
### 구문 규칙 및 파라미터

<a id="f8eb289ae7a71029"></a>
#### savepoint_name

저장점 이름이다.   
저장점 이름이 기존의 저장점 이름과 중복될 경우 기존의 저장점이 삭제된다.   
이름의 길이는 128 바이트보다 작아야 한다.

<a id="48b8741bf315a194"></a>
### 설명

정의한 savepoint는 ROLLBACK TO SAVEPOINT 구문 ([ROLLBACK](#1ba3b433854d9411) 구문 참조)에서 사용되며, 해당 savepoint까지 수행된 DML, DDL 구문이 철회되고 해당 구문이 획득한 lock도 해제된다.

정의한 savepoint는 transaction을 COMMIT 하거나 ROLLBACK 할 때 자동으로 제거되는데 [RELEASE SAVEPOINT savepoint_specifier](#820eff57a94d3af0) 구문을 사용하여 명시적으로 제거할 수도 있다.

<a id="fb7a09f283275307"></a>
### 사용 예

다음은 savepoint를 정의하고 ROLLBACK TO SAVEPOINT 구문을 사용하는 예이다.

```
gSQL> SAVEPOINT sp1;

Savepoint created.

gSQL> INSERT INTO t1 VALUES ( 1, 'anonymous' );

1 row created.

gSQL> SAVEPOINT sp2;

Savepoint created.

gSQL> INSERT INTO t1 VALUES ( 2, 'someone' );

1 row created.

gSQL> SAVEPOINT sp3;

Savepoint created.

gSQL> INSERT INTO t1 VALUES ( 3, 'anyone' );

1 row created.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous
 2 someone  
 3 anyone   

3 rows selected.

gSQL> ROLLBACK TO SAVEPOINT sp3;

Rollback complete.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous
 2 someone  

2 rows selected.

gSQL> ROLLBACK TO SAVEPOINT sp2;

Rollback complete.

gSQL> SELECT * FROM t1;

ID DATA     
-- ---------
 1 anonymous

1 row selected.

gSQL> ROLLBACK TO SAVEPOINT sp1;

Rollback complete.

gSQL> SELECT * FROM t1;

no rows selected.
```

<a id="f8bdb4eafc97b31d"></a>
### 호환성

**SQL 표준 호환성**

<a id="cbbf2451e9fefa5c"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T271 | Savepoints | O |

<a id="906d068dfb1facea"></a>
### 참조

관련 내용은 다음을 참조한다.

- [COMMIT](19-sql-references-c-g.md#9d9942a1324d8ced)
- [ROLLBACK](#1ba3b433854d9411)
- [RELEASE SAVEPOINT savepoint_specifier](#820eff57a94d3af0)

<a id="2070458035e417b9"></a>
## SELECT

<a id="f971bccfc0bcab55"></a>
### query expression

<a id="ba0057c317b31fad"></a>
#### 기능

하나 이상의 table 또는 view에서 원하는 row를 검색한다.

<a id="5ea57e17a7af8404"></a>
#### 구문

```
<query expression> ::=
    [ <with clause> ] <query expression body> [ <order by clause> ] [ <offset limit clause> ]

<query expression body> ::=
      <query term>
    | <set operator>

<query term> ::=
      <query specification>
    | <left paren> <query expression body> [ <order by clause> ] [ <offset limit clause> ] <right paren>
```

<a id="79022d069a7fe241"></a>
#### 사용 범위 및 접근 권한

&lt;query expression&gt; 구문을 수행하려면 구문에 사용된 모든 테이블에 대해 다음 권한 중 하나를 가져야 한다.

- 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
- 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- SELECT ANY TABLE ON DATABASE

<a id="b04401cf4166d41f"></a>
#### 구문 규칙 및 파라미터

<a id="fa0be9c3fb581576"></a>
##### &lt;with clause&gt;

&lt;with clause&gt;는 임시 결과 집합을 정의하고, 그 결과 집합을 참조할 수 있다.   
자세한 내용은 [with clause](#18f7553fc2f0e9d6)를 참조한다.

<a id="83c107c56cd1d31e"></a>
##### &lt;set operator&gt;

부질의 (subquery) 간의 집합 연산을 수행한다.  
자세한 내용은 [set operator](#8fd806f5930143e4) 절을 참조한다.

<a id="9e0ad59912fd49e5"></a>
##### &lt;query specification&gt;

하나의 부질의 (subquery)를 기술한다.  
자세한 내용은 [query specification](#7ad631319ea8ccd2) 절을 참조한다.

<a id="64a9ed1bbc0961a6"></a>
##### &lt;order by clause&gt;

검색 결과에 대한 정렬 정보를 기술한다.  
자세한 내용은 [order by clause](#14bc5c63df59d6ec)를 참조한다.

<a id="df47b9fa22b85f37"></a>
##### &lt;offset limit clause&gt;

검색 결과 집합에서 skip 할 row의 개수와 fetch 할 row의 개수를 기술한다.  
자세한 내용은 [offset limit clause](#4685bb3308f27adc)를 참조한다.

<a id="08980df2bafd6d8f"></a>
#### 설명

SELECT 구문으로 query를 기술한다.  
&lt;with clause&gt;, &lt;order by clause&gt;, &lt;offset limit clause&gt;는 생략할 수 있다.  
&lt;set operator&gt;를 사용하여 둘 이상의 부질의 (subquery)를 가질 수 있다.

<a id="b020c0e338b9b52b"></a>
#### 사용 예

다음은 SELECT 구문의 예이다.

```
gSQL> SELECT s_name, s_nation FROM supplier;

S_NAME                    S_NATION     
------------------------- -------------
Supplier#1                FRANCE       
Supplier#2                KOREA        
Supplier#3                GERMANY      
Supplier#4                UNITED STATES
Supplier#5                CANADA       

5 rows selected.
```

다음은 &lt;order by clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT s_name, s_nation FROM supplier ORDER BY s_name DESC;

S_NAME                    S_NATION
------------------------- -------------
Supplier#5                CANADA
Supplier#4                UNITED STATES
Supplier#3                GERMANY
Supplier#2                KOREA
Supplier#1                FRANCE

5 rows selected.
```

다음은 &lt;offset limit clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT s_name, s_nation FROM supplier OFFSET 1;

S_NAME                    S_NATION
------------------------- -------------
Supplier#2                KOREA
Supplier#3                GERMANY
Supplier#4                UNITED STATES
Supplier#5                CANADA

4 rows selected.

gSQL> SELECT s_name, s_nation FROM supplier LIMIT 1; 

S_NAME                    S_NATION
------------------------- --------
Supplier#1                FRANCE  

1 row selected.
```

다음은 &lt;order by clause&gt;와 &lt;offset limit clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT s_name, s_nation FROM supplier ORDER BY s_name DESC OFFSET 3 LIMIT 1; 

S_NAME                    S_NATION
------------------------- --------
Supplier#2                KOREA   

1 row selected.
```

다음은 &lt;with clause&gt;를 사용한 SELECT 구문의 예이다.

```
* Non Recursive CTE

gSQL>
WITH revenue ( supplier_no, total_revenue ) AS
      (
            SELECT
                   l_suppkey,
                   SUM(l_extendedprice * (1 - l_discount))
              FROM lineitem
             WHERE l_shipdate >= DATE '1996-01-01'
               AND l_shipdate < DATE '1996-01-01' + INTERVAL '3' MONTH
             GROUP BY
                   l_suppkey
      )
select
       s_suppkey,
       s_name,
       s_address,
       s_phone,
       ROUND( total_revenue, 2 ) as total_revenue
  from
       supplier,
       revenue
 where
       s_suppkey = supplier_no
   and total_revenue = (
                           select
                                  max(total_revenue)
                             from
                                  revenue
                       )
order by
      s_suppkey;

S_SUPPKEY S_NAME                    S_ADDRESS         S_PHONE         TOTAL_REVENUE
--------- ------------------------- ----------------- --------------- -------------
     8449 Supplier#000008449        Wp34zim9qYFbVctdW 20-469-856-8873    1772627.21

1 row selected.

* Recursive CTE

gSQL>
WITH GenerateRecord ( c1, c2 ) AS 
     (
          SELECT 1, 11
            FROM dual
          UNION ALL
          SELECT c1 + 1, c2 + 1
            FROM GenerateRecord
           WHERE c1 < 10
     )
SELECT c1, c2 FROM GenerateRecord;

C1 C2
-- --
 1 11
 2 12
 3 13
 4 14
 5 15
 6 16
 7 17
 8 18
 9 19
10 20

10 rows selected.
```

<a id="c4a0b51a8dc72ef0"></a>
#### 호환성

**SQL 표준 호환성**

<a id="7aa51e4715267dba"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T121 | WITH (excluding RECURSIVE ) in query expression | O |
| T122 | WITH (excluding RECURSIVE ) in subquery | O |
| T131 | Recursive query | O |
| T132 | Recursive query in subquery | O |
| F661 | Simple tables | O |
| F302 | INTERSECT table operator | O |
| F301 | CORRESPONDING in query expressions | X |
| T551 | Optional key words for default syntax | O |
| F304 | EXCEPT ALL table operator | O |
| F850 | Top-level &lt;order by clause&gt;in &lt;query expression&gt; | O |
| F851 | &lt;order by clause&gt;in subqueries | O |
| F855 | Nested &lt;order by clause&gt;in &lt;query expression&gt; | O |
| F856 | Nested &lt;fetch first clause&gt;in &lt;query expression&gt; | O |
| F857 | Top-level &lt;fetch first clause&gt;in &lt;query expression&gt; | O |
| F858 | &lt;fetch first clause&gt;in subqueries | O |
| F860 | dynamic &lt;fetch first row count&gt;in &lt;fetch first clause&gt; | X |
| F861 | Top-level &lt;result offset clause&gt;in &lt;query expression&gt; | O |
| F862 | &lt;result offset clause&gt;in subqueries | O |
| F863 | Nested &lt;result offset clause&gt;in &lt;query expression&gt; | O |
| F865 | dynamic &lt;offset row count&gt;in &lt;result offset clause&gt; | X |
| F866 | FETCH FIRST clause: PERCENT option | X |
| F867 | FETCH FIRST clause: WITH TIES option | X |

<a id="18f7553fc2f0e9d6"></a>
### with clause

<a id="e0a183fd080af024"></a>
#### 기능

&lt;with clause&gt;는 임시 결과 집합을 정의하고, 그 결과 집합을 참조할 수 있다.  
이는 SELECT 구문 내에서 정의되고 참조되며 이름이 부여된 임시 결과 집합으로서 Common Table Expression (CTE) 이라고 한다.

<a id="93835be63232ae37"></a>
#### 구문

```
<with clause> ::=
    WITH <with list>

<with list> ::=
    <with list element> [ { <comma> <with list element> }... ]

<with list element> ::=
    <query name> [ <left paren> <with column list> <right paren> ] 
        AS <table subquery> [ <search or cycle clause> ]

<with column list> ::=
    <column name list>   
 
<search or cycle clause> ::=
    <search clause>
  | <cycle clause>
  | <search clause> <cycle clause>

<search clause> ::=
    SEARCH <recursive search order> SET <sequence column>

<recursive search order> ::=
    DEPTH FIRST BY <ordering column list>
  | BREADTH FIRST BY <ordering column list>

<ordering column list> ::= 
    <ordering column> [ { <comma> <ordering column> }... ]

<ordering column> ::= 
    <column name> [ ASC | DESC ] [ NULLS FIRST | NULLS LAST ]

<sequence column> ::=
    <column name>

<cycle clause> ::=
    CYCLE <cycle column list> SET <cycle mark column> TO <cycle mark value>
        DEFAULT <non-cycle mark value>

<cycle column list> ::=
    <cycle column> [ { <comma> <cycle column> }... ]

<cycle column> ::=
    <column name>
    
<cycle mark column> ::=
    <column name>
 
<cycle mark value> ::=
    <value expression>

<non-cycle mark value> ::=
    <value expression>
```

<a id="851426e22076ad2c"></a>
#### 사용 범위 및 접근 권한

&lt;query expression&gt; 구문에서 지원되며 이를 수행하려면 사용자가 &lt;query expression&gt;의 접근 권한을 만족해야 한다.  
자세한 내용은 [query expression](#f971bccfc0bcab55) 을 참조한다.

<a id="4361e2489ecf51bb"></a>
#### 구문 규칙 및 파라미터

<a id="d9201901d4486089"></a>
##### &lt;with list&gt;

여러 개의 &lt;with list element&gt;를 정의할 수 있다.

<a id="172d023db84a08c7"></a>
##### &lt;with list element&gt;

기술한 &lt;query name&gt;의 임시 결과 집합을 정의한다.  
&lt;with list element&gt;를 Common Table Expression (CTE) 이라고 한다.  
CTE는 recursive CTE와 non-recursive CTE로 구분된다.  
자세한 내용은 [설명](#d810ea839b63d5a6) 부분을 참조한다.

- CTE 참조
    - 기술된 순서에 따라 CTE 참조를 제한한다.
    - 현재 CTE 이전에 기술된 CTE를 참조할 수 있다.
    - 현재 CTE 이후에 기술된 CTE는 참조할 수 없다.
- non-recursive CTE
    - &lt;with list element&gt;에서는 현재 CTE 이전에 기술된 CTE를 참조할 수 있다.
- recursive CTE
    - &lt;with list element&gt;에서는 현재 CTE 이전에 기술된 CTE 또는 self CTE를 참조할 수 있다.
    - Self-reference CTE는 CTE 내에서 한 번만 허용된다.

```
--# success : non recursive CTE
WITH CTE_1( c1 ) AS
    (
         SELECT i1
           FROM t1
    ),
    CTE_2( c2 ) AS
    (
         SELECT c1
           FROM CTE_1      ❶ 선행 CTE 참조
    )
SELECT c2 FROM CTE_2;

--# error : non recursive CTE
WITH CTE_1( c1 ) AS
    (  
         SELECT c2
           FROM CTE_2      ❷ 후행 CTE 참조
    ),
    CTE_2( c2 ) AS
    (  
         SELECT i1
           FROM t1
    )
SELECT c1 FROM CTE_1;
```

```
--# success : recursive CTE
WITH CTE_1( c1 ) AS
     (  
          SELECT i1
            FROM t1
     ),
     CTE_2( c2 ) AS
     (  
          SELECT c1
            FROM CTE_1         ❶ 선행 CTE 참조
     ),
     CTE_3( c3 ) AS
     (  
          SELECT 1
            FROM CTE_1
          UNION ALL
          SELECT 1
           FROM CTE_2, CTE_3    ❷ 선행 CTE 또는 self CTE 참조
     )
SELECT c3 FROM CTE_3;

--# error : recursive CTE
WITH CTE_RECURSIVE( c1 ) AS  
   (  
          SELECT i1
            FROM t1
          WHERE i1 IS NULL
          UNION ALL
          SELECT 1
            FROM CTE_RECURSIVE A, CTE_RECURSIVE B   ❸ self-reference CTE는 한 번만 허용
          WHERE 1 = 0
     )
SELECT c1 FROM CTE_RECURSIVE;
```

<a id="3b172b4632698b1f"></a>
##### &lt;query name&gt;

&lt;query name&gt;은 WITH clause 내에서 중복되지 않아야 한다.

<a id="788b0dde19f442fe"></a>
##### &lt;with column list&gt;

Recursive CTE는 &lt;with column list&gt;를 생략할 수 없다.

<a id="699a542b756b535d"></a>
##### &lt;search clause&gt;

- Non-recursive CTE
    - &lt;search clause&gt;를 기술할 수 없다.
- Recursive CTE 
    - CTE 결과 레코드의 정렬 순서를 기술한다.

- &lt;recursive search order&gt;
    - DEPTH FIRST BY
        - 형제행이 반환되기 전에 자식행들이 반환된다.
    - BREADTH FIRST BY
        - 자식행이 반환되기 전에 형제행들이 반환된다.

- &lt;ordering column list&gt;
    - column list의 정렬방식을 지정한다.
    - 정렬순서
        - ASC 
        - DESC
        - 명시하지 않은 경우, 기본값은 ASC 이다.
    - Null ordering
        - NULLS FIRST 
        - NULLS LAST
        - 명시하지 않은 경우, 기본값은 NULLS LAST 이다.
    - &lt;with list element&gt;에 선언된 &lt;with column list&gt;을 기술해야 한다.
    - LONG type (LONG VARCHAR, LONG VARBINARY)은 지원하지 않는다.

- &lt;sequence column&gt;
    - CTE 결과 레코드의 순서를 저장한다.
    - &lt;column name&gt;은 아래 항목과 중복되지 않아야 한다.
        - &lt;with list element&gt;의 &lt;with column list&gt;에 선언된 column name
        - &lt;cycle clause&gt;의 &lt;cycle column list&gt;에 선언된 column name

<a id="3781e408f5e8abd4"></a>
##### &lt;cycle clause&gt;

- Non-recursive CTE
    - &lt;cycle clause&gt;를 기술할 수 없다.
- Recursive CTE
    - &lt;cycle clause&gt;를 생략하면 cycle 발생시 error를 반환한다.

Cycle 발생 유무에 따라 &lt;cycle mark column&gt;에 &lt;cycle mark value&gt; 또는 &lt;non-cycle mark value&gt;를 저장한다.

- &lt;cycle column list&gt;
    - &lt;with list element&gt;에 선언된 &lt;with column list&gt;을 기술해야 한다.

- &lt;cycle mark column&gt; 
    - &lt;column name&gt;은 아래 항목과 중복되지 않아야 한다.
        - &lt;with list element&gt;의 &lt;with column list&gt;에 선언된 column name
        - &lt;search clause&gt;의 &lt;sequence column&gt;에 선언된 column name

- &lt;cycle mark value&gt; 또는 &lt;non-cycle mark value&gt;
    - 1 byte 문자만 기술할 수 있다.

<a id="d810ea839b63d5a6"></a>
#### 설명

&lt;with clause&gt;는 임시 결과 집합을 정의하고, 그 결과 집합을 참조할 수 있다.  
SELECT 구문 내에서 정의되고 참조되며 이름이 부여된 임시 결과 집합이다.  
이를 Common Table Expression (CTE)라고 한다.  
CTE는 recursive CTE와 non-recursive CTE로 구분된다.

- Recursive CTE: CTE 내에서 현재 정의하고 있는 CTE를 참조 (self-reference CTE)하는 경우

```
WITH RECURSIVE_CTE ( c1 ) AS
     (
          SELECT 1 
            FROM dual
          UNION ALL
          SELECT c1 + 1 
            FROM RECURSIVE_CTE
           WHERE c1 < 10
     )
SELECT c1 FROM RECURSIVE_CTE;
```

- Non-recursive CTE: Recursive CTE가 아닌 경우

```
WITH NON_RECURSIVE_CTE ( c1 ) AS 
     (
          SELECT i1
            FROM t1
          UNION ALL
          SELECT i1
            FROM t2 
     )
SELECT c1 FROM NON_RECURSIVE_CTE;
```

&lt;with clause&gt;는 SELECT, INSERT, UPDATE, DELETE, CREATE TABLE AS SELECT, CREATE VIEW 구문에 기술할 수 있다.

<a id="9b2fbeba0a434762"></a>
##### &lt;with list element&gt;

기술한 &lt;query name&gt;의 임시 결과 집합을 정의한다.  
&lt;with list element&gt;를 Common Table Expression (CTE)라고 한다.  
CTE는 recursive CTE와 non-recursive CTE로 구분된다.

- Recursive CTE
    - CTE 내에서 현재 정의하고 있는 CTE를 참조 (self-reference CTE)하는 경우
    - Self-reference CTE를 포함한 query block을 recursive member query라고 한다. 
    - Recursive member query가 아닌 나머지 query block을 anchor member query라 한다.
    - Recursive member query와 anchor member query는 UNION ALL로 구성되어야 한다.
    - Recursive member query는 하나만 기술할 수 있다.

- Non-recursive CTE: Recursive CTE가 아닌 경우

```
WITH CTE_RECURSIVE( c1, c2 ) AS
    (  
         SELECT i1, i2                          ❶ Anchor member query
           FROM t1
          WHERE i2 IS NULL
         UNION ALL
         SELECT i1, i2                          ❷ Recursive member query
           FROM CTE_RECURSIVE, t1      ❸ Self reference
          WHERE CTE_RECURSIVE.c1 = t1.i2
    )
SELECT c1, c2 FROM CTE_RECURSIVE;
```

- Recursive member query는 다음과 같은 항목들을 포함할 수 없다.
    - GROUP BY 또는 DISTINCT clause
        - (X) SELECT i1, i2 FROM CTE_RECURSIVE, t1 WHERE CTE_RECURSIVE.c1 = t1.i2 GROUP BY i1, i2
        - (X) SELECT DISTINCT i1, i2 FROM CTE_RECURSIVE, t1 WHERE CTE_RECURSIVE.c1 = t1.i2
    - LEFT, RIGHT, OUTER JOIN의 inner part에서의 CTE 참조
        - (X) SELECT i1, i2 FROM t1 LEFT OUTER JOIN CTE_RECURSIVE ON t1.i2 = CTE_RECURSIVE.c1
    - Aggregation function
        - (X) SELECT MAX(i1), MAX(i2) FROM CTE_RECURSIVE, t1 WHERE CTE_RECURSIVE.c1 = t1.i2
    - Self-reference CTE를 포함하는 subquery
        - (X) SELECT i1, i2 FROM ( SELECT * FROM CTE_RECURSIVE ) cte, t1 WHERE cte.c1 = t1.i2

<a id="66617d5445a6a2c3"></a>
##### &lt;search clause&gt;

CTE 결과 레코드의 정렬 순서를 기술한다.   
형제행들을 &lt;ordering column list&gt;로 정렬하고, 정렬된 레코드에 대해 형제행과 자식행의 반환 순서를 명시한다.   
&lt;sequence column&gt;에는 결과 레코드의 순서를 저장한다.

- DEPTH FIRST BY
    - 형제행이 반환되기 전에 자식행들이 반환되도록 한다. 
- BREADTH FIRST BY 
    - 자식행이 반환되기 전에 형제행들이 반환되도록 한다.

```
gSQL>
SELECT * FROM t1;

I1  I2 
--- ---
A   ---
AA  A  
AB  A  
AC  A  
AAX AA 
ABX AB 
ACX AC 

7 rows selected.

* SEARCH BREADTH FIRST BY

gSQL> 
WITH w1( w_i1, w_i2 ) AS
    ( 
         SELECT i1, i2
           FROM t1
          WHERE i1 = 'A'
         UNION ALL
         SELECT i1, i2
           FROM w1, t1
          WHERE w_i1 = i2
    ) SEARCH BREADTH FIRST BY w_i1, w_i2 SET w_seq
SELECT w_i1, w_i2, w_seq
 FROM w1;

W_I1 W_I2 W_SEQ
---- ---- -----
A    ---      1
AA   A        2
AB   A        3
AC   A        4
AAX  AA       5
ABX  AB       6
ACX  AC       7

7 rows selected.

* SEARCH DEPTH FIRST BY

gSQL> 
WITH w1( w_i1, w_i2 ) AS
    ( 
         SELECT i1, i2
           FROM t1
          WHERE i1 = 'A'
         UNION ALL
         SELECT i1, i2
           FROM w1, t1
          WHERE w_i1 = i2
    ) SEARCH DEPTH FIRST BY w_i1, w_i2 SET w_seq
SELECT w_i1, w_i2, w_seq
  FROM w1;

W_I1 W_I2 W_SEQ
---- ---- -----
A    ---      1
AA   A        2
AAX  AA       3
AB   A        4
ABX  AB       5
AC   A        6
ACX  AC       7

7 rows selected.
```

<a id="f56140132024420e"></a>
##### &lt;cycle clause&gt;

&lt;cycle clause&gt; 구문을 기술하지 않은 경우, cycle이 발생할 때 에러가 발생한다.

&lt;cycle column list&gt;는 cycle을 검사하는데 사용된다.   
Cycle 발생 유무에 따라 &lt;cycle mark column&gt;에 &lt;cycle mark value&gt; 또는 &lt;non-cycle mark value&gt;를 저장한다.   
&lt;cycle mark value&gt; 또는 &lt;non-cycle mark value&gt;에는 1 byte 문자만 기술할 수 있다.   
Cycle 발생 레코드의 &lt;cycle mark column&gt;에는 &lt;cycle mark value&gt;를 저장한다. 이 때, 더 이상의 recursion 없이 cycle이 발생한 레코드까지만 반환한다.   
Cycle이 발생하지 않은 형제행들에 대해서는 recursion이 계속 진행된다.

```
gSQL>
SELECT * FROM t1;

I1  I2 
--- ---
A   ---
AA  A  
AB  A  
AC  A  
AA  AA 
AAX AA 
ABX AB 
ACX AC 

8 rows selected.
```

- Cycle이 발생하고 cycle clause를 기술하지 않은 경우

```
gSQL> 
WITH w1( w_i1, w_i2 ) AS
     (     
          SELECT i1, i2
            FROM t1
           WHERE i1 = 'A'
          UNION ALL
          SELECT i1, i2
            FROM w1, t1
           WHERE w_i1 = i2
     )
SELECT w_i1, w_i2
  FROM w1;

ERR-42000(16511): cycle detected while executing recursive WITH query
```

- Cycle이 발생하고 cycle clause를 기술한 경우

```
gSQL> 
WITH w1( w_i1, w_i2 ) AS
     ( 
          SELECT i1, i2
            FROM t1
           WHERE i1 = 'A'
          UNION ALL
          SELECT i1, i2
            FROM w1, t1
           WHERE w_i1 = i2
     ) CYCLE w_i1, w_i2 SET c_cycle TO 'T' DEFAULT 'F'
SELECT w_i1, w_i2, c_cycle
  FROM w1;

W_I1 W_I2 C_CYCLE
---- ---- -------
A    ---  F      
AC   A    F      
AB   A    F      
AA   A    F      
ACX  AC   F      
ABX  AB   F      
AAX  AA   F      
AA   AA   F      
AAX  AA   F      
AA   AA   T      

10 rows selected.
```

<a id="8b71d46d90021334"></a>
#### 사용 예

다음은 WITH 절을 사용한 SELECT 구문의 예이다.

- Non-recursive CTE

```
gSQL>
WITH revenue ( supplier_no, total_revenue ) AS
      (
            SELECT
                   l_suppkey,
                   SUM(l_extendedprice * (1 - l_discount))
              FROM lineitem
             WHERE l_shipdate >= DATE '1996-01-01'
               AND l_shipdate < DATE '1996-01-01' + INTERVAL '3' MONTH
             GROUP BY
                   l_suppkey
      )
select
       s_suppkey,
       s_name,
       s_address,
       s_phone,
       ROUND( total_revenue, 2 ) as total_revenue
  from
       supplier,
       revenue
 where
       s_suppkey = supplier_no
   and total_revenue = (
                           select
                                  max(total_revenue)
                             from
                                  revenue
                       )
order by
      s_suppkey;

S_SUPPKEY S_NAME                    S_ADDRESS         S_PHONE         TOTAL_REVENUE
--------- ------------------------- ----------------- --------------- -------------
     8449 Supplier#000008449        Wp34zim9qYFbVctdW 20-469-856-8873    1772627.21

1 row selected.
```

- Recursive CTE

```
gSQL> 
WITH GenerateRecord ( c1, c2 ) AS 
     (
          SELECT 1, 11
            FROM dual
          UNION ALL
          SELECT c1 + 1, c2 + 1
            FROM GenerateRecord
           WHERE c1 < 10
     )
SELECT c1, c2 FROM GenerateRecord;

C1 C2
-- --
 1 11
 2 12
 3 13
 4 14
 5 15
 6 16
 7 17
 8 18
 9 19
10 20

10 rows selected.
```

다음은 WITH 절 예제에 사용될 emp 테이블의 레코드 검색 결과이다.

```
gSQL>
SELECT * FROM emp;

NAME    MGR    
------- -------
Kelly   null   
Bill    Kelly  
Jackson Kelly  
Joe     Kelly  
Scott   Bill   
Larry   Bill   
Paul    Jackson
Bill    Bill   

8 rows selected.
```

다음은 SEARCH BREADTH FIRST BY를 사용한 예이다.

- Cycle 발생

```
gSQL> 
WITH w_emp( w_name, w_mgr ) AS
     (
         SELECT name, mgr
           FROM emp
          WHERE mgr IS NULL
         UNION ALL
         SELECT name, mgr
           FROM emp, w_emp
          WHERE mgr = w_emp.w_name
     ) SEARCH BREADTH FIRST BY w_name SET w_seq
SELECT w_name, w_mgr, w_seq
  FROM w_emp;

ERR-42000(16511): cycle detected while executing recursive WITH query
```

- Cycle이 발생한 바로 위 구문에 cycle clause를 기술하여 검색

```
gSQL> 
WITH w_emp( w_name, w_mgr ) AS
     (
         SELECT name, mgr
           FROM emp
          WHERE mgr IS NULL
         UNION ALL
         SELECT name, mgr
           FROM emp, w_emp
          WHERE mgr = w_emp.w_name
     ) SEARCH BREADTH FIRST BY w_name SET w_seq
       CYCLE w_name SET w_cycle TO 'T' DEFAULT 'F'
SELECT w_name, w_mgr, w_seq, w_cycle
  FROM w_emp;

W_NAME  W_MGR   W_SEQ W_CYCLE
------- ------- ----- -------
Kelly   null        1 F      
Bill    Kelly       2 F      
Jackson Kelly       3 F      
Joe     Kelly       4 F      
Bill    Bill        5 T      
Larry   Bill        6 F      
Paul    Jackson     7 F      
Scott   Bill        8 F      

8 rows selected.
```

다음은 SEARCH DEPTH FIRST BY를 사용한 예이다.

```
gSQL>
WITH w_emp( w_name, w_mgr ) AS
     (
          SELECT name, mgr
            FROM emp
           WHERE mgr IS NULL
          UNION ALL
          SELECT name, mgr
            FROM emp, w_emp
           WHERE mgr = w_emp.w_name
     ) SEARCH DEPTH FIRST BY w_name SET w_seq
       CYCLE w_name SET w_cycle TO 'T' DEFAULT 'F'
SELECT w_name, w_mgr, w_seq, w_cycle
  FROM w_emp;

W_NAME  W_MGR   W_SEQ W_CYCLE
------- ------- ----- -------
Kelly   null        1 F      
Bill    Kelly       2 F      
Bill    Bill        3 T      
Larry   Bill        4 F      
Scott   Bill        5 F      
Jackson Kelly       6 F      
Paul    Jackson     7 F      
Joe     Kelly       8 F      

8 rows selected.
```

다음은 CREATE TABLE AS SELECT 구문에 with clause를 사용한 예이다.

```
gSQL> 
CREATE TABLE new_emp AS
WITH w_emp( w_name, w_mgr ) AS
     (
          SELECT name, mgr
            FROM emp
           WHERE mgr IS NULL
          UNION ALL
          SELECT name, mgr
            FROM emp, w_emp
           WHERE mgr = w_emp.w_name
     ) SEARCH BREADTH FIRST BY w_name SET w_seq
       CYCLE w_name SET w_cycle TO 'T' DEFAULT 'F'
SELECT w_name, w_mgr, w_seq, w_cycle
  FROM w_emp;

Table created.
```

다음은 INSERT 구문에 with clause를 사용한 예이다.

```
gSQL>
INSERT INTO new_emp
WITH w_emp( w_name, w_mgr ) AS
     (
          SELECT name, mgr
            FROM emp
           WHERE mgr = 'Bill'
          UNION ALL
          SELECT name, mgr
            FROM emp, w_emp
           WHERE mgr = w_emp.w_name
     ) SEARCH BREADTH FIRST BY w_name SET w_seq
       CYCLE w_name SET w_cycle TO 'T' DEFAULT 'F'
SELECT w_name, w_mgr, w_seq, w_cycle
  FROM w_emp;

6 rows created.
```

다음은 UPDATE 구문에 with clause를 사용한 예이다.

```
gSQL>
UPDATE new_emp SET w_name = NULL
 WHERE ( w_name, w_mgr ) 
       IN ( WITH w_emp( w_name, w_mgr ) AS
                (
                    SELECT name, mgr
                      FROM emp
                     WHERE mgr = 'Bill'
                    UNION ALL
                    SELECT name, mgr
                      FROM emp, w_emp
                     WHERE mgr = w_emp.w_name
                ) SEARCH BREADTH FIRST BY w_name SET w_seq
                  CYCLE w_name SET w_cycle TO 'T' DEFAULT 'F'
            SELECT w_name, w_mgr
              FROM w_emp );

9 rows updated.
```

다음은 DELETE 구문에 with clause를 사용한 예이다.

```
gSQL>
DELETE FROM new_emp
WHERE ( w_mgr ) 
      IN ( WITH w_emp( w_name, w_mgr ) AS
               (
                   SELECT name, mgr
                     FROM emp
                    WHERE mgr = 'Bill'
                   UNION ALL
                   SELECT name, mgr
                     FROM emp, w_emp
                    WHERE mgr = w_emp.w_name
               ) SEARCH BREADTH FIRST BY w_name SET w_seq
                 CYCLE w_name SET w_cycle TO 'T' DEFAULT 'F'
           SELECT w_mgr
             FROM w_emp );

9 rows deleted.
```

다음은 CREATE VIEW 구문에 with clause를 사용한 예이다.

```
gSQL>
CREATE VIEW v_emp AS
WITH w_emp( w_name, w_mgr ) AS
     (
          SELECT name, mgr
            FROM emp
           WHERE mgr IS NULL
          UNION ALL
          SELECT name, mgr
            FROM emp, w_emp
           WHERE mgr = w_emp.w_name
     ) SEARCH BREADTH FIRST BY w_name SET w_seq
       CYCLE w_name SET w_cycle TO 'T' DEFAULT 'F'
SELECT w_name, w_mgr, w_seq, w_cycle
  FROM w_emp;

View created.
```

<a id="7ad631319ea8ccd2"></a>
### query specification

<a id="061ff3f22ac8fb8d"></a>
#### 기능

&lt;table expression&gt; 결과로부터 파생된 table을 기술한다.

<a id="3fce45442f62fd46"></a>
#### 구문

```
<query specification> ::=
    SELECT [ <hint clause> ] [ <set quantifier> ] <select list> <table expression>

<set quantifier> ::=
      ALL
    | DISTINCT

<table expression> ::=
      <from clause> [ <where clause> ] [ <hierarchical query clause> ] [ <group by clause> ] [ <having clause> ] [ <window clause> ]
```

<a id="1efcc3eeeea022e5"></a>
#### 사용 범위 및 접근 권한

&lt;query specification&gt; 구문을 수행하려면 다음 조건 중 하나를 만족해야 한다.

- 테이블의 소유자 
- 테이블에 대한 SELECT 권한 
- 테이블이 속한 스키마에 대해 SELECT TABLE, CONTROL TABLE, CONTROL 권한 중 하나를 소유 
- Database에 대한 SELECT TABLE 권한을 소유

<a id="20bf9d024c994c97"></a>
#### 구문 규칙 및 파라미터

<a id="f3de568325fa47ec"></a>
##### &lt;hint clause&gt;

질의 수행에 필요한 힌트를 기술한다.  
자세한 내용은 [SQL Hint](15-sql-tuning.md#54d9bce5449eb296)를 참조한다.

<a id="29a007b8ca7fa79f"></a>
##### &lt;set quantifier&gt;

질의 결과의 중복 제거 여부를 기술한다.  
생략할 경우, ALL과 동일하게 동작한다.

<a id="64c7507f28d30ae7"></a>
##### &lt;select list&gt;

질의 결과로부터 검색할 column을 기술한다.  
자세한 내용은 [select list](#806e99db5dd57a0e)를 참조한다.

<a id="b54f73a0bbdec991"></a>
##### &lt;from clause&gt;

검색할 table들을 기술한다.  
자세한 내용은 [from clause](#d8f9755e05abe1cf)를 참조한다.

<a id="9dd9234d9b3d676f"></a>
##### &lt;where clause&gt;

검색 조건을 기술한다.  
자세한 내용은 [where clause](#74a33d522dd6bfcc)를 참조한다.

<a id="fc11e6788263ca92"></a>
##### &lt;hierarchical query clause&gt;

계층 모델 데이터를 계층 구조로 검색하도록 기술한다.   
자세한 내용은 [hierarchical query clause](#263f6cdbec620b99)를 참조한다.

<a id="d30dbb05d9f6a8f1"></a>
##### &lt;group by clause&gt;

검색 결과에 대한 grouping을 기술한다.  
자세한 내용은 [group by clause](#14659507262e5348)를 참조한다.

<a id="dbc75b4e84453361"></a>
##### &lt;having clause&gt;

Grouping 된 결과에 대한 조건을 기술한다.  
자세한 내용은 [having clause](#e8e681b7980f3e0f)를 참조한다.

<a id="db8b116211d3faa5"></a>
##### &lt;window clause&gt;

Window function의 수행 범위를 기술한다.  
자세한 내용은 [window clause](#f9eea6d4ba5feccc)를 참조한다.

<a id="8d8f3787280d031e"></a>
#### 설명

<a id="9b42782e80e83970"></a>
##### &lt;hint clause&gt;

&lt;hint clause&gt;는 사용자가 optimizer에게 SQL 구문 수행 방법을 직접 지시하기 위해 사용하는 comment이다.

GOLDILOCKS의 optimizer는 사용자가 기술한 &lt;hint clause&gt;를 우선 적용한다.  
만약 적용할 수 없을 경우에는 cost 계산을 통해 최적의 실행 계획을 선택한다.

GOLDILOCKS는 기본적으로 &lt;hint clause&gt;에 구문상 에러가 발생하더라도 이를 무시하도록 설정되어 있다. &lt;hint clause&gt;에 구문상 에러가 있는지 확인하려면 [HINT_ERROR](../part-02-administration-manual/10-server-property.md#c43339e41d788f8b) property를 on으로 설정하고 질의를 수행하도록 한다

<a id="20984694c0b5c7fd"></a>
##### &lt;set quantifier&gt;

&lt;set quantifier&gt;는 &lt;select list&gt; expression들로 구성된 결과 집합에서 중복을 제거할지 여부를 설정한다.

- ALL: 결과 집합에서 중복을 제거하지 않는다.
- DISTINCT: 결과 집합에서 중복을 제거한다.
- 생략할 경우, ALL을 기술한 것과 동일하게 동작한다.

<a id="8fa8a89a46908393"></a>
##### &lt;select list&gt;

질의 결과로부터 검색할 column을 기술한다.  
이 목록은 콤마 (,) 리스트로 구분하여 기술한다.  
&lt;from clause&gt;에 기술한 모든 column들을 기술하고 싶은 경우에는 별표 (*)를 사용한다.

<a id="69906f9d2e0967f6"></a>
##### &lt;from clause&gt;

&lt;from clause&gt;는 검색할 table 또는 view들을 기술한다.

<a id="a621a04d4f8db14f"></a>
##### &lt;where clause&gt;

&lt;where clause&gt;는 &lt;from clause&gt;로부터 얻은 결과 집합 중에 원하는 결과만 가져오도록 검색 조건을 기술한다.

<a id="d077b6fc31181121"></a>
##### &lt;hierarchical query clause&gt;

계층 모델 데이터를 계층 구조로 검색하도록 기술한다.   
시작 조건과 하위 연결 조건을 이용하여 테이블의 레코드들을 depth-first 순서의 계층 구조로 반환한다.

<a id="d96ae6289d527afd"></a>
##### &lt;group by clause&gt;

&lt;group by clause&gt;는 &lt;where clause&gt;를 적용한 결과 집합의 grouping 방법을 기술한다.

&lt;group by clause&gt;가 기술된 경우, &lt;select list&gt;에 올 수 있는 expression은 다음과 같다.

- 상수
- group by에 기술된 expression
- group by에 기술된 expression의 연산식
- group에 속하는 expression에 대한 집계 함수

<a id="cf3a8373515b38f2"></a>
##### &lt;having clause&gt;

&lt;having clause&gt;는 grouping된 결과 집합에 대한 검색 조건을 기술한다.  
일반적으로 &lt;group by clause&gt;와 함께 사용된다.

<a id="7329fbf770978db3"></a>
##### &lt;window clause&gt;

select list와 order by clause에 기술되는 window function의 수행 범위를 기술한다.

<a id="45e30cbb01e4396f"></a>
#### 사용 예

다음은 &lt;hint clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT /*+ INDEX_DESC(supplier, supplier_pk_index) */ s_name, s_nation FROM supplier;

S_NAME                    S_NATION
------------------------- -------------
Supplier#5                CANADA
Supplier#4                UNITED STATES
Supplier#3                GERMANY
Supplier#2                KOREA
Supplier#1                FRANCE

5 rows selected.
```

다음은 &lt;set quantifier&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT ALL p_type FROM part;

P_TYPE
------
COPPER
NICKEL
STEEL
NICKEL
STEEL

5 rows selected.

gSQL> SELECT DISTINCT p_type FROM part;

P_TYPE
------
COPPER
STEEL
NICKEL

3 rows selected.
```

다음은 &lt;where clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT p_name, p_brand, p_type, p_size FROM part where p_size < 10;

P_NAME P_BRAND    P_TYPE P_SIZE
------ ---------- ------ ------
Part#1 Brand#1    COPPER      7
Part#2 Brand#1    NICKEL      1

2 rows selected.
```

다음은 &lt;hierarchical query clause&gt;를 사용하여 SELECT 구문의 계층 구조 데이터를 조회하는 예이다.

```
gSQL>
SELECT *
  FROM emp
START WITH mgr IS NULL
CONNECT BY NOCYCLE mgr = PRIOR name
ORDER SIBLINGS BY name;

NAME    MGR    
------- -------
Kelly   null   
Bill    Kelly  
Larry   Bill   
Scott   Bill   
Jackson Kelly  
Paul    Jackson
Joe     Kelly  

7 rows selected.
```

다음은 &lt;group by clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT ps_partkey, SUM(ps_availqty) FROM partsupp GROUP BY ps_partkey;

PS_PARTKEY SUM(PS_AVAILQTY)
---------- ----------------
         1            11401
         2             8025
         3            13864
         4            11564
         5             8744

5 rows selected.
```

다음은 &lt;having clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT ps_partkey, SUM(ps_availqty) FROM partsupp GROUP BY ps_partkey having SUM(ps_availqty) > 10000;

PS_PARTKEY SUM(PS_AVAILQTY)
---------- ----------------
         1            11401
         3            13864
         4            11564

3 rows selected.
```

다음은 &lt;window clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> 
SELECT item_no,
       sales_date,
       sales,
       SUM( sales ) OVER W1 cumulative_sales, 
       AVG( sales ) OVER w1 avg_sales
  FROM store
WINDOW w1 AS ( PARTITION BY item_no
               ORDER BY sales_date
               ROWS BETWEEN UNBOUNDED PRECEDING
                        AND CURRENT ROW );

ITEM_NO SALES_DATE SALES CUMULATIVE_SALES AVG_SALES
------- ---------- ----- ---------------- ---------
    100 2001-01-01   150              150       150
    100 2001-01-02   100              250       125
    100 2001-01-03   170              420       140
    100 2001-01-04    90              510     127.5
    100 2001-01-05   200              710       142
    235 2001-01-01    70               70        70
    235 2001-01-02   130              200       100
    235 2001-01-03   190              390       130
    235 2001-01-04   150              540       135
    235 2001-01-05    50              590       118

10 rows selected.
```

<a id="fd4896d4b6358680"></a>
#### 호환성

**SQL 표준 호환성**

<a id="cce8fdb3f80d393c"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F801 | Full set function | X |
| T051 | Row types | X |
| T301 | Functional dependencies | X |
| T325 | Qualified SQL parameter references | X |
| T053 | Explicit aliases for all-fields reference | O |
| T285 | Enhanced derived column names | O |

<a id="2c591b6a69a416a1"></a>
#### 참조

관련 내용은 [query expression](#f971bccfc0bcab55)을 참조한다.

<a id="806e99db5dd57a0e"></a>
### select list

<a id="915ebdbd58652588"></a>
#### 기능

질의 결과로부터 검색할 column을 기술한다.

<a id="e9fe3aa9b3622901"></a>
#### 구문

```
<select list> ::=
      <asterisk>
    | <select sublist> [ { <comma> <select sublist> } ... ]

<select sublist> ::=
      <derived column>
    | <qualified asterisk>

<qualified asterisk> ::=
      <asterisked identifier chain> <period> <asterisk>

<asterisked identifier chain> ::=
    <asterisked identifier> [ { <period> <asterisked identifier> } ... ]

<derived column> ::=
    <value expression> [ <as clause> ]

<as clause> ::=
    [ AS ] <column name>
```

<a id="25e377350580115f"></a>
#### 사용 범위 및 접근 권한

&lt;select list&gt; 구문에 column이나 subquery가 존재할 때 다음을 만족해야 한다.

- column에 대한 접근 권한
- subquery에 존재하는 table 및 column에 대한 접근 권한

<a id="71d6a98de13839ac"></a>
#### 구문 규칙 및 파라미터

<a id="49f7fe6349f789b8"></a>
##### &lt;select list&gt;

&lt;asterisk&gt;나 &lt;select sublist&gt;를 갖는다.

<a id="423e3ba3a971f94f"></a>
##### &lt;asterisk&gt;

- &lt;asterisk&gt;는 &lt;select list&gt;에 단독으로만 쓰일 수 있다.
    - (O) SELECT * FROM t1;
    - (X) SELECT *, c1 FROM t1;

<a id="b7d0daaf99478e21"></a>
##### &lt;select sublist&gt;

- &lt;derived column&gt; 또는 &lt;qualified asterisk&gt;를 갖는다.
    - SELECT c1, c2 FROM t1;
    - SELECT t1.* FROM t1;
- &lt;derived column&gt;은 AS를 사용하여 출력 이름을 변경할 수 있으며, AS는 생략할 수 있다.
    - SELECT c1 AS col1, c2 AS col2 AS FROM t1;
    - SELECT c1 col1, c2 col2 FROM t1;
- 둘 이상의 &lt;select sublist&gt;를 기술할 경우, 각 &lt;select sublist&gt;를 콤마 (,)로 구분해야 한다.
    - (O) SELECT c1, c2 FROM t1;
    - (O) SELECT c1, c2, t1.* FROM t1;
    - (X) SELECT c1 c2 FROM t1;
        - c2는 ALIAS로 처리
    - (X) SELECT c1 c2 c3 FROM t1;

<a id="ba38728fb800b7a1"></a>
#### 설명

<a id="970789035fef84d4"></a>
##### &lt;select list&gt;

&lt;select list&gt;는 결과 집합에 포함될 column들을 기술한다.

<a id="0df3944e00e733c1"></a>
##### &lt;asterisk&gt;

&lt;asterisk&gt;는 &lt;from clause&gt;에 있는 모든 column들을 select list로 설정한다.

<a id="54397160be07a300"></a>
##### &lt;select sublist&gt;

&lt;select sublist&gt;는 &lt;derived column&gt; 또는 &lt;qualified asterisk&gt;를 갖는다.

- &lt;qualified asterisk&gt;
    - 특정 table이나 view에 속하는 모든 column들을 select list로 설정한다.
- &lt;derived column&gt;
    - column 또는 &lt;value expression&gt;을 기술할 수 있다.
    - &lt;as clause&gt;를 사용하여 column name을 변경할 수 있으며, 이 때 AS는 생략할 수 있다.
    - &lt;from clause&gt;에 동일한 column name을 가진 테이블들이 있는 경우, 이 column을 참조하기 위해서는 table name이나 table alias를 반드시 명시해야 한다.
        - SELECT t1.c1, t2.c1 FROM t1, t2;
        - SELECT a.c1, b.c1 FROM t1 a, t2 b;

&lt;select sublist&gt;를 둘 이상 기술할 경우에는 반드시 콤마 (,)로 구분하여야 한다.

<a id="2b3eaba87b2d4477"></a>
##### select list에 설정되는 이름

- &lt;derived column&gt;에 &lt;column name&gt;이 명시된 경우, 해당 이름이 select list 이름으로 설정된다.
    - SELECT i1 AS name FROM t1;
- &lt;derived column&gt;에 &lt;column name&gt;이 명시되지 않은 경우
    - &lt;derived column&gt;이 single column reference인 경우
        - Single column이 가진 column name이 select list 이름으로 설정된다.
        - SELECT i1 FROM t1;
    - &lt;derived column&gt;이 column이 아닌 expression인 경우
        - Select list 이름이 설정되지 않는다.
        - SELECT i1 + 100 FROM t1;
        - CREATE TABLE AS SELECT 구문에 쓰일 경우, column name을 기술해야 한다.
        - CREATE TABLE t2 AS SELECT i1 + 100 AS sum_i1 FROM t1;

<a id="989b9a39cf8fd60d"></a>
#### 사용 예

다음은 &lt;asterisk&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT * FROM supplier;

S_SUPPKEY S_NAME                    S_NATION      S_PHONE
--------- ------------------------- ------------- ---------------
        1 Supplier#1                FRANCE        27-918-335-1736
        2 Supplier#2                KOREA         15-679-861-2259
        3 Supplier#3                GERMANY       11-383-516-1199
        4 Supplier#4                UNITED STATES 25-843-787-7479
        5 Supplier#5                CANADA        21-151-690-3663

5 rows selected.
```

다음은 &lt;select sublist&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT revenue.* FROM revenue;

SUPPLIER_NO TOTAL_REVENUE
----------- -------------
          1      11978.64
          2       20321.5
          3      41844.68

3 rows selected.

gSQL> SELECT supplier_no suppno, total_revenue AS TOTAL FROM revenue;

SUPPNO    TOTAL
------ --------
     1 11978.64
     2  20321.5
     3 41844.68

3 rows selected.

gSQL> SELECT 1, revenue.*, CAST( total_revenue AS NATIVE_INTEGER ) TOTAL FROM revenue;

1 SUPPLIER_NO TOTAL_REVENUE TOTAL
- ----------- ------------- -----
1           1      11978.64 11979
1           2       20321.5 20322
1           3      41844.68 41845

3 rows selected.
```

<a id="70f0dadb1c9ce49b"></a>
#### 참조

관련 내용은 [query specification](#7ad631319ea8ccd2) 을 참조한다.

<a id="d8f9755e05abe1cf"></a>
### from clause

<a id="034ff35bbb326ff9"></a>
#### 기능

하나 이상의 table들로부터 파생된 table을 기술한다.

<a id="48152fd26e1d2a78"></a>
#### 구문

```
<from clause> ::=
    FROM <table reference list>

<table reference list> ::=
    <table reference> [ { , <table reference> } ... ]

<table reference> ::=
      <table factor>
    | <joined table>
    | <table reference> <pivot clause>
    | <table reference> <unpivot clause>

<table factor> ::=
      <table primary> [ <sample clause> ]

<table primary> ::=
      <table name> [ <cluster domain> ] [ [ AS ] <correlation name> ]
    | <derived table> [ <cluster domain> ] [ [ AS ] <correlation name> [ <left paren> <derived column list> <right paren> ] ]
    | <lateral derived table> [ <cluster domain> ] [ [ AS ] <correlation name> [ <left paren> <derived column list> <right paren> ] ]
    | <table function derived table> [ [ AS ] <correlation name> ]
    | <parenthesized joined table>

<derived table> ::=
    <table subquery>

<lateral derived table> ::=
    LATERAL <table subquery>

<parenthesized joined table> ::=
      <left paren> <parenthesized joined table> <right paren>
    | <left paren> <joined table> <right paren>

<derived column list> ::=
    <column name list>

<cluster domain> ::=
    @ <cluster domain name>

<cluster domain name> ::=
      GLOBAL
    | LOCAL
    | LOCAL_OFFLINE
    | <identifier>

<table function derived table> ::=
      TABLE <left paren> <table function expression> <right paren>

<table function expression> ::=
      <table function name> <left paren> [ <table function argument list> ] <right paren>

<table function argument list> ::=
      <value expression> [ <comma> ... ]
```

<a id="de4b8d7c3416c53b"></a>
#### 사용 범위 및 접근 권한

&lt;table reference list&gt;에 기술한 table 또는 view에 대한 접근 권한이 있어야 한다.

<a id="35df56adde31bfab"></a>
#### 구문 규칙 및 파라미터

<a id="a4440bd3c89732c4"></a>
##### &lt;table reference list&gt;

- &lt;table reference list&gt;에는 한 개 이상의 테이블들을 콤마 (,)를 이용하여 기술할 수 있다.
- 두 개 이상의 테이블이 기술된 경우
    - 테이블은 왼쪽에서 오른쪽 방향으로 평가 (evaluation)된다.
    - &lt;select list&gt;에 *를 기술한 경우 왼쪽 테이블의 column부터 오른쪽 테이블의 column까지 순서대로 &lt;select list&gt;에 매핑된다.

<a id="285405ad973fb22c"></a>
##### &lt;table reference&gt;

- &lt;pivot clause&gt;와 &lt;unpivot clause&gt;는 순서에 상관 없이 여러 번 기술할 수 있다.
    - SELECT * FROM t1 PIVOT( COUNT(*) FOR c1 IN( 'a' ) ) UNPIVOT( col_value FOR col_name IN( c2, c3, c4 ) )
    - SELECT * FROM t1 UNPIVOT( col_value FOR col_name IN( c2, c3, c4 ) ) PIVOT( COUNT(*) FOR c1 IN( 'a' ) )
- &lt;pivot clause&gt; 앞에 기술된 &lt;table primary&gt;은 pivot 대상 테이블이다.
- &lt;unpivot clause&gt; 앞에 기술된 &lt;table primary&gt;은 unpivot 대상 테이블이다.
- Pivot에 대한 자세한 내용은 [pivot clause](#fc4e37ea9e697ac1)를 참조한다.
- Unpivot에 대한 자세한 내용은 [unpivot clause](#e4262e566d20f76e)를 참조한다.

<a id="ee2e3f9c32606f88"></a>
##### &lt;table factor&gt;

- 전체 데이터에서 일부를 무작위로 샘플링할 수 있는 &lt;sample clause&gt;를 제공한다.
- Sampling에 대한 자세한 내용은 [sample clause](#778d71bbe6c00108) 를 참조한다.

<a id="ba85c07f521a10c5"></a>
##### &lt;table primary&gt;

- &lt;correlation name&gt;을 사용하여 별칭 (alias name)을 기술할 수 있다.
    - SELECT * FROM t1 AS a, t2 AS b;
    - SELECT * FROM ( SELECT i1 FROM t1 ) AS a;

- &lt;derived table&gt;, 즉 &lt;table subquery&gt;는
    - &lt;correlation name&gt;을 이용하여 별칭 (alias name)을 기술할 수 있다.
        - SELECT * FROM ( SELECT i1, i2, i3 FROM t1 ) AS a;
    - &lt;derived column list&gt;를 기술할 수 있다.
        - SELECT * FROM ( SELECT i1, i2, i3 FROM t1 ) AS a( col1, col2, col3 );
        - &lt;derived column list&gt;의 &lt;column name&gt; 개수는 &lt;table subquery&gt;에 기술한 &lt;select list&gt;의 target 개수와 동일해야 한다.
        - &lt;table subquery&gt;에 기술한 &lt;select list&gt;의 target과 순서대로 1 : 1 매핑된다.
        - 해당 &lt;derived table&gt; 내 &lt;table subquery&gt;의 &lt;select list&gt;를 참조하려면 반드시 &lt;derived column list&gt;에 기술한 &lt;column name&gt;을 사용해야 한다.

```
SELECT col1, col2 
FROM ( SELECT i1, i2 FROM t1 ) AS a( col1, col2 ) 
WHERE col1 = 1 AND col2 = 1;
```

- &lt;lateral derived table&gt; 
    - &lt;table subquery&gt; 앞에 LATERAL을 명시하면 lateral inline view가 된다. 
    - lateral inline view는 &lt;table subquery&gt; 내에 있는 모든 clause에서 main query의 FROM 절에 나열된 table을 참조할 수 있다. 
        - 단, lateral inline view 보다 먼저 명시된 table만 참조할 수 있다. 먼저 명시된 table 이라 하더라도 RIGHT OUTER JOIN, FULL OUTER JOIN 인 경우에는 참조할 수 없다.

- &lt;table function derived table&gt;
    - table function derived table은 table function을 실행한 결과 집합으로 구성된 논리적 테이블이다. table function derived table에 대한 자세한 내용은 [Table Function Derived Table](13-sql-objects.md#1355436653509274)을 참조한다.
    - table function derived table은 TABLE과 실행할 table function 이름을 명시한다.
    - &lt;table function expression&gt;의 &lt;table function argument list&gt;에서는 FROM 절에서 &lt;table function derived table&gt; 이전에 나열한 table의 column을 참조할 수 있다.
        - 단, 먼저 명시한 table이라고 해도 RIGHT OUTER JOIN, FULL OUTER JOIN 인 경우에는 참조할 수 없다.

```
SELECT t1.col1, ft.rf2 
FROM t1, TABLE( tablefunc( t1.col1 ) );
```

<a id="11ab94598f3c6e02"></a>
##### &lt;correlation name&gt;

- &lt;table reference list&gt;에는 동일한 &lt;correlation name&gt;이 두 개 이상 존재할 수 없다.
- &lt;correlation name&gt;이 기술된 경우 해당 &lt;table name&gt;이나 &lt;derived table&gt;을 참조하려면 반드시 &lt;correlation name&gt;을 이용하여야 한다.
    - SELECT a.i1 FROM t1 AS a WHERE a.i1 > 3;
    - (X) SELECT t1.i1 FROM t1 AS a WHERE t1.i1 > 3;
- &lt;correlation name&gt;을 기술할 때 그 앞의 AS는 생략할 수 있다.
    - SELECT a.i1 FROM t1 a;

<a id="301ba5efcc185fcd"></a>
##### &lt;derived column list&gt;

&lt;derived column list&gt;에는 동일한 &lt;column name&gt;이 두 개 이상 존재할 수 없다.

<a id="14811fab77fe801d"></a>
##### &lt;cluster domain&gt;

- &lt;cluster domain&gt;은 table이나 view, table subquery를 대상으로 기술할 수 있다.
    - SELECT * FROM t1@G1;
    - &lt;parenthesized joined table&gt;에는 기술할 수 없다.
        - (X) SELECT * FROM ( t1 INNER JOIN t2 ON t1.sk = t2.sk )@G2;
- 구조나 데이터가 변경될 table이나 view에는 &lt;cluster domain&gt;을 기술할 수 없다.
    - (X) DELETE FROM t2@GLOBAL;
    - (X) UPDATE t1@GLOBAL SET i1 = 1;
    - (X) INSERT INTO t1@GLOBAL VALUES ( 1, 10 );
    - (X) SELECT * FROM t1@GLOBAL FOR UPDATE;
    - (X) CREATE INDEX t1_idx ON t1@GLOBAL( i1 );

<a id="73095fd43a1263bc"></a>
##### &lt;cluster domain name&gt;

&lt;cluster domain name&gt;의 &lt;identifier&gt;에는 cluster group name이나 cluster member name이 올 수 있다.

- cluster group name 
    - SELECT * FROM t1@G1;
- cluster member name
    - SELECT * FROM t1@G1N1;

<a id="f199387968f508ab"></a>
#### 설명

<a id="349ad5f85c75c187"></a>
##### &lt;table reference list&gt;

&lt;table reference list&gt;에는 콤마 (,)를 사용하여 두 개 이상의 테이블들을 기술할 수 있다.

- 두 개 이상의 테이블을 기술하면 해당 테이블들을 왼쪽에서 오른쪽으로 각각 cross join하듯 작동한다.
    - SELECT * FROM t1, t2;
    - &lt;=&gt; SELECT * FROM t1 CROSS JOIN t2;
- &lt;where clause&gt;에 두 테이블의 join 조건이 존재할 경우, &lt;where clause&gt;를 join 조건으로 갖는 inner join처럼 동작한다. 
    - SELECT * FROM t1, t2 WHERE t1.I1 = t2.I1;
    - &lt;=&gt; SELECT * FROM t1 INNER JOIN t2 ON t1.i1 = t2.i1;
- &lt;where clause&gt;에 outer join operator (+)를 사용한 경우, outer join과 동일하게 작동한다.
    - Outer join operator (+)에 대한 자세한 내용은 [OUTER JOIN](12-sql-languages.md#49d2ffc0cfaf35dc) 절을 참조한다.

<a id="e4404b1a64307fc4"></a>
##### &lt;table reference&gt;

단일 table이나 view, table subquery, joined table 등이 &lt;table reference&gt;가 될 수 있다. Joined table을 제외한 나머지는 correlation name을 가질 수 있다.

Joined table에 대한 자세한 내용은 [joined table](#f83c5d9047669788) 절을 참고한다.

<a id="0487bbc03fc72116"></a>
##### &lt;table primary&gt;

Table이나 view, table subquery, &lt;parenthesized joined table&gt;이 &lt;table primary&gt;가 될 수 있다.

Table이나 view, table subquery는 correlation name을 가질 수 있는데, 이 때 AS는 생략할 수 있다. Correlation name이 기술된 경우, &lt;select list&gt;나 &lt;where clause&gt;와 같이 해당 table이나 view, table subquery를 참조하는 모든 경우에 correlation name을 사용해야 한다.

Table subquery는 &lt;derived column list&gt;를 기술할 수 있으며, correlation name과 마찬가지로 해당 table subquery의 column을 참조하는 모든 경우에 &lt;derived column list&gt;에 기술한 이름을 사용하여야 한다. Table subquery에 &lt;derived column list&gt;를 사용하려면 correlation name을 반드시 기술해야 한다.

&lt;parenthesized joined table&gt;은 join 연산에 참여하는 table들의 논리적 join 순서를 기술한다. 이 때 괄호로 묶은 모든 table들에 대한 join이 모두 cross join과 inner join일 경우, optimizer가 join 순서를 변경할 수 있다.

<a id="e11478c113430be9"></a>
##### &lt;cluster domain&gt;

&lt;cluster domain&gt;이 생략된 경우 &lt;cluster domain name&gt;으로 GLOBAL을 사용한 것과 동일한 의미를 갖는다.  
자세한 내용은 [Cluster Domain](12-sql-languages.md#1019ccdf9343fa49)을 참조한다.

<a id="6d9c0340c428411c"></a>
##### &lt;cluster domain name&gt;

&lt;cluster domain name&gt;에 정의된 예약어는 다음과 같은 의미를 가진다.

- GLOBAL
    - 모든 cluster group을 cluster domain으로 선정한다.
- LOCAL
    - 사용자 질의를 수행하는 server만 cluster domain으로 선정한다.
        - G2N1에서 다음 질의를 수행할 때, G2N1의 데이터를 가지고 온다.
        - SELECT * FROM t1@LOCAL;
- LOCAL_OFFLINE
    - Offline 상태의 table 데이터를 조회하기 위해 사용자 질의를 수행하는 server만 cluster domain으로 선정한다.
        - G2N1에서 다음 질의를 수행할 때, offline table T1의 G2N1의 데이터를 가져온다.
        - SELECT * FROM t1@LOCAL_OFFLINE;
    - Online table에 LOCAL_OFFLINE domain을 기술하면 에러가 발생한다.

&lt;cluster domain name&gt;에 &lt;identifier&gt;를 기술한 경우 해당 이름의 cluster group 또는 cluster member를 [Cluster Domain](12-sql-languages.md#1019ccdf9343fa49)으로 선정한다.

<a id="62d74b8f739879b1"></a>
#### 사용 예

다음은 &lt;table name&gt;을 이용하여 단일 table을 검색하는 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, c_nation FROM customer;

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

5 rows selected.
```

다음은 &lt;derived table&gt;을 이용하는 SELECT 구문의 예이다.

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer);

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

5 rows selected.


gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer) AS CUST ("CUSTOMER_NAME", "CUSTOMER_NATION");

CUSTOMER_NAME CUSTOMER_NATION
------------- ---------------
Customer#1    KOREA          
Customer#2    CANADA         
Customer#3    KOREA          
Customer#4    GERMANY        
Customer#5    UNITED STATES  

5 rows selected.
```

다음은 &lt;lateral derived table&gt;을 이용하는 SELECT 구문의 예이다.

```
gSQL> SELECT r_name, n_name
  FROM region, (  SELECT n_name
                    FROM nation
                   WHERE n_regionkey = r_regionkey
               ) v_nation
 WHERE r_name = 'ASIA';

ERR-42000(16036): 'R_REGIONKEY': invalid identifier :
                   WHERE n_regionkey = r_regionkey
                                       *

gSQL> SELECT r_name, n_name
  FROM region, LATERAL (  SELECT n_name 
                            FROM nation
                           WHERE n_regionkey = r_regionkey
                       ) v_nation
 WHERE r_name = 'ASIA';
R_NAME                    N_NAME
------------------------- -------------------------
ASIA                      INDIA
ASIA                      INDONESIA
ASIA                      JAPAN
ASIA                      CHINA
ASIA                      VIETNAM

5 rows selected.
```

다음은 괄호를 이용한 joined table에 대한 SELECT 구문의 예이다.

```
gSQL> SELECT customer.c_name, o_totalprice FROM (customer INNER JOIN orders ON customer.c_custkey = orders.o_custkey);

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#2     46929.18
Customer#4    193846.25
Customer#3     32151.78
Customer#5     144659.2

5 rows selected.
```

다음은 콤마 (,)로 구분한 두 개의 table들을 사용하는 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, o_totalprice FROM customer, orders;

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#1     46929.18
Customer#1    193846.25
Customer#1     32151.78
Customer#1     144659.2
Customer#2    173665.47
Customer#2     46929.18
Customer#2    193846.25
Customer#2     32151.78
Customer#2     144659.2
Customer#3    173665.47
Customer#3     46929.18
Customer#3    193846.25
Customer#3     32151.78
Customer#3     144659.2
Customer#4    173665.47
Customer#4     46929.18
Customer#4    193846.25
Customer#4     32151.78
Customer#4     144659.2

C_NAME     O_TOTALPRICE
---------- ------------
Customer#5    173665.47
Customer#5     46929.18
Customer#5    193846.25
Customer#5     32151.78
Customer#5     144659.2

25 rows selected.
```

다음은 &lt;cluster domain&gt;을 이용하는 SELECT 구문의 예이다.

- GLOBAL 예약어 사용

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer@GLOBAL);

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

5 rows selected.
```

- LOCAL 예약어 사용

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer)@LOCAL;

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA

2 rows selected.
```

- G1이라는 이름의 cluster group name을 사용

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer@G1);

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA

2 rows selected.
```

- G2N1이라는 이름의 cluster member name을 사용

```
gSQL> SELECT * FROM (SELECT c_name, c_nation FROM customer@G2N1);

C_NAME     C_NATION
---------- -------------
Customer#3 KOREA
Customer#4 GERMANY

2 rows selected.
```

<a id="7ee3712b3daf3329"></a>
#### 참조

관련 내용은 [subquery](#d3bc7e8acf2465f9)를 참조한다.

<a id="f83c5d9047669788"></a>
### joined table

<a id="a84d02470e35b940"></a>
#### 기능

Cartesian product, inner join, outer join 등에서 파생되는 table을 기술한다.

<a id="f91ebdee96f3f0a1"></a>
#### 구문

```
<joined table> ::=
      <cross join>
    | <qualified join>
    | <natural join>

<cross join> ::=
    <table reference> CROSS JOIN <table factor>

<qualified join> ::=
    <table reference> [ <join type> ] JOIN <table reference> <join specification>

<natural join> ::=
    <table reference> NATURAL [ <join type> ] JOIN <table factor>

<join specification> ::=
      <join condition>
    | <named columns join>

<join condition> ::=
    ON <search condition>

<named columns join> ::=
    USING ( <join column list> )

<join type> ::=
      INNER
    | { LEFT | RIGHT | FULL } [ OUTER ]

<join column list> ::=
    <column name list>
```

<a id="65e41d85e5703ab6"></a>
#### 사용 범위 및 접근 권한

joined table에 기술된 모든 table 및 view에 대한 접근 권한이 있어야 한다.

<a id="a972f3b89e87f635"></a>
#### 구문 규칙 및 파라미터

<a id="6c47ceba89baf5dc"></a>
##### &lt;cross join&gt;

Join 조건을 명시하는 &lt;join specification&gt;은 &lt;cross join&gt; 위치에 오지 않는다.  
&lt;cross join&gt;의 오른쪽에는 단일 테이블이나 &lt;table subquery&gt;, &lt;parenthesized joined table&gt;이 올 수 있다.

<a id="fdc72b30e9cc3bdf"></a>
##### &lt;qualified join&gt;

- Join 조건을 명시하는 &lt;join specification&gt;을 반드시 기술해야 한다.
    - SELECT * FROM t1 INNER JOIN t2 ON t1.i1 = t2.i1;
    - SELECT * FROM t1 INNER JOIN t2 USING ( i1 );
- &lt;join type&gt;은 생략할 수 있는데 생략할 경우 INNER로 처리한다.
    - SELECT * FROM t1 JOIN t2 ON t1.i1 = t2.i1;
    - &lt;=&gt; SELECT * FROM t1 INNER JOIN t2 ON t1.i1 = t2.i1;
- &lt;join type&gt;에서 OUTER는 생략할 수 있다.
    - SELECT * FROM t1 LEFT JOIN t2 ON t1.i1 = t2.i1;
    - &lt;=&gt; SELECT * FROM t1 LEFT OUTER JOIN t2 ON t1.i1 = t2.i1;
- &lt;join type&gt;이 OUTER JOIN인 경우 &lt;join specification&gt;에는 &lt;join condition&gt;만 올 수 있다. 
    - SELECT * FROM t1 FULL OUTER JOIN t2 ON t1.i1 = t2.i1;
    - (X) SELECT * FROM t1 FULL OUTER JOIN t2 USING ( i1 );

<a id="90da0b51059d6e7b"></a>
##### &lt;natural join&gt;

- Join 조건을 명시하는 &lt;join specification&gt;은 &lt;natural join&gt; 위치에 오지 않는다.
- &lt;natural join&gt; 오른쪽에는 단일 테이블이나 &lt;table subquery&gt;, &lt;parenthesized joined table&gt;이 올 수 있다.
- &lt;join type&gt;은 생략할 수 있는데 생략할 경우 INNER로 처리한다.
    - SELECT * FROM t1 NATURAL JOIN t2;
    - &lt;=&gt; SELECT * FROM t1 NATURAL INNER JOIN t2;
- &lt;join type&gt;에 OUTER를 지원하지 않는다.
    - (X) SELECT * FROM t1 NATURAL LEFT OUTER JOIN t2;
- NATURAL JOIN의 왼쪽 row와 오른쪽 row에 동일한 &lt;column name&gt;이 하나도 없는 경우 &lt;cross join&gt;으로 처리한다.
    - t1( c1 INTEGER, c2 INTEGER );
    - t2( c3 INTEGER, c4 INTEGER );
    - SELECT * FROM t1 NATURAL INNER JOIN t2;
    - &lt;=&gt; SELECT * FROM t1 CROSS JOIN t2;
- NATURAL JOIN의 왼쪽 row와 오른쪽 row에 동일한 &lt;column name&gt;이 있을 경우, USING 구문을 기술한 것과 동일하게 동작한다.
    - t1( c1 INTEGER, c2 INTEGER );
    - t2( c2 INTEGER, c3 INTEGER );
    - SELECT * FROM t1 NATURAL INNER JOIN t2;
    - &lt;=&gt; SELECT * FROM t1 INNER JOIN t2 USING( c2 );

<a id="e9e9afee884fa17d"></a>
##### &lt;join specification&gt;

- &lt;join condition&gt;이나 &lt;named columns join&gt; 중에 하나만 기술할 수 있다.
    - &lt;join condition&gt;
        - SELECT * FROM t1 INNER JOIN t2 ON t1.i1 = t2.i1;
    - &lt;named columns join&gt;
        - SELECT * FROM t1 INNER JOIN t2 USING ( i1 );
- &lt;named columns join&gt;을 기술한 경우
    - &lt;join column list&gt;에는 반드시 하나 이상의 column name을 기술해야 한다.
        - SELECT * FROM t1 INNER JOIN t2 USING ( i1 );
    - Column name은 &lt;table name&gt;.&lt;column name&gt;과 함께 기술할 수 없다.
        - (X) SELECT * FROM t1 INNER JOIN t2 USING ( t1.i1 );
    - &lt;join column list&gt;에 나열된 column들이 JOIN의 왼쪽 row와 오른쪽 row에 반드시 존재해야 하며, 비교 가능해야 한다.
        - t1( c1 INTEGER, c2 INTEGER );
        - t2( c2 INTEGER, c3 INTEGER );
        - SELECT * FROM t1 INNER JOIN t2 USING ( c2 );
    - &lt;select list&gt;에 *를 사용한 경우의 레코드 구성  
      1) &lt;join column list&gt;에 기술된 column들   
      2) 왼쪽 row들 중에서 &lt;join column list&gt;에 해당되지 않는 column들  
      3) 오른쪽 row들 중에서 &lt;join column list&gt;에 해당되지 않는 column들
        - t1( c1 INTEGER, c2 INTEGER );
        - t2( c2 INTEGER, c3 INTEGER );
        - SELECT * FROM t1 INNER JOIN t2 USING ( c2 );
        - 레코드 구성 : C2, C1, C3
    - &lt;join column list&gt;에 기술된 &lt;column name&gt;은 &lt;table name&gt;.&lt;column name&gt;과 함께 참조할 수 없고, &lt;column name&gt;으로만 참조할 수 있다.
        - SELECT c2 FROM t1 INNER JOIN t2 USING ( c2 ) WHERE c2 > 3;
        - (X) SELECT t1.c2 FROM t1 INNER JOIN t2 USING ( c2 );
        - (X) SELECT * FROM t1 INNER JOIN t2 USING ( c2 ) WHERE t1.c2 > 3;
    - &lt;join column list&gt;의 조인 조건 처리
        - &lt;join column list&gt;에 나열된 각 column 들에 대하여
        - &lt;left table name&gt;.&lt;column name&gt; = &lt;right table name&gt;.&lt;column name&gt; 조건이 생성되고
        - 각 &lt;column name&gt;에 대한 조건들을 AND로 처리하는 조건이 생성된다.
        - t1( c1 INTEGER, c2 INTEGER );
        - t2( c1 INTEGER, c2 INTEGER );
        - SELECT * FROM t1 INNER JOIN t2 USING ( c1, c2 );
        - 조인 조건: t1.c1 = t2.c1 AND t1.c2 = t2.c2
    - &lt;select list&gt;에는 특정 테이블의 모든 column을 반환하는 &lt;table name&gt;.* 구문을 사용할 수 없다.
        - (X) SELECT t1.*, t2.* FROM t1 INNER JOIN t2 USING ( c1, c2 );

<a id="10edfe8a245ac460"></a>
#### 설명

<a id="e9e0ca540dc5d25c"></a>
##### &lt;cross join&gt;

&lt;cross join&gt;은 왼쪽의 각 row를 오른쪽의 모든 row들과 결합한 결과를 반환한다.

```
T1 ( 1, 1 ), ( 2, 2 )
T2 ( 2, 2 ), ( 3, 3 )

gSQL> SELECT * FROM t1 CROSS JOIN t2;
C1 C2 C1 C2
-- -- -- --
 1  1  2  2
 1  1  3  3
 2  2  2  2
 2  2  3  3
4 rows selected.
```

&lt;cross join&gt;에는 join 조건을 명시적으로 기술할 수 없지만, &lt;where clause&gt;를 통해 두 table에 대한 join 조건을 기술할 수 있으며, 이 경우 inner join과 동일하게 동작한다.  
• SELECT * FROM t1 CROSS JOIN t2 WHERE t1.c1 = t2.c1;  
• &lt;=&gt; SELECT * FROM t1 INNER JOIN t2 ON t1.c1 = t2.c1;

```
T1 ( 1, 1 ), ( 2, 2 )
T2 ( 2, 2 ), ( 3, 3 )

gSQL> SELECT * FROM t1 CROSS JOIN t2 WHERE t1.c1 = t2.c1;
C1 C2 C1 C2
-- -- -- --
 2  2  2  2
1 row selected.
```

<a id="4a038657c31387fa"></a>
##### &lt;qualified join&gt;

&lt;qualified join&gt;은 왼쪽의 각 row들을 오른쪽의 모든 row들과 결합한 후 join 조건을 만족하는 row들만 결과로 반환한다.

&lt;table expression&gt;에 &lt;where clause&gt;가 존재할 경우, &lt;qualified join&gt;의 결과 집합에 &lt;where clause&gt; 조건들을 적용한다.

Inner join은 &lt;where clause&gt;에 존재하는 조건들을 join 조건처럼 처리해도 결과가 동일하지만, outer join은 &lt;where clause&gt;에 존재하는 조건들을 join 조건처럼 처리하면 결과가 달라진다.

- **INNER JOIN:** 

```
t1 ( 1, 1 ), ( 2, 2 ), ( 3, 3 ), ( 4, 4 ), ( 5, 5 )
t2 ( 2, 2 ), ( 3, 3 )
```

- ON 절에만 조건이 있는 경우

```
gSQL> SELECT * FROM t1 INNER JOIN t2 ON t1.c1 = t2.c1 AND t1.c2 = t2.c2;
C1 C2 C1 C2
-- -- -- --
 2  2  2  2
 3  3  3  3
2 rows selected.
```

- ON 절과 WHERE 절에 조건이 있는 경우 
    - JOIN 조건 ON t1.c1 = t2.c1을 적용한 결과 집합에 WHERE 조건 t1.c2 = t2.c2를 적용

```
gSQL> SELECT * FROM t1 INNER JOIN t2 ON t1.c1 = t2.c1 WHERE t1.c2 = t2.c2;
C1 C2 C1 C2
-- -- -- --
 2  2  2  2
 3  3  3  3
2 rows selected.
```

    - JOIN 조건 ON t1.c1 = t2.c1을 적용한 결과 집합 → WHERE 조건 t1.c2 = t2.c2를 적용

```
( 2,  2,    2,    2 )                        ( 2,  2,    2,    2 )
  ( 3,  3,    3,    3 )                   →   ( 3,  3,    3,    3 )
```

- **OUTER JOIN:** 

```
t1 ( 1, 1 ), ( 2, 2 ), ( 3, 3 ), ( 4, 4 ), ( 5, 5 )
t2 ( 2, 2 ), ( 3, 3 )
```

- ON 절에만 조건이 있는 경우

```
gSQL> SELECT * FROM t1 LEFT OUTER JOIN t2 ON t1.c1 = t2.c1 AND t1.c2 = t2.c2;
C1 C2   C1   C2
-- -- ---- ----
 1  1 null null
 2  2    2    2
 3  3    3    3
 4  4 null null
 5  5 null null
5 rows selected.
```

- ON 절과 WHERE 절에 조건이 있는 경우 
    - JOIN 조건 ON t1.c1 = t2.c1을 적용한 결과 집합에 WHERE 조건 t1.c2 = t2.c2를 적용

```
gSQL> SELECT * FROM t1 LEFT OUTER JOIN t2 ON t1.c1 = t2.c1 WHERE t1.c2 = t2.c2;
C1 C2 C1 C2
-- -- -- --
 2  2  2  2
 3  3  3  3
2 rows selected.
```

    - JOIN 조건 ON t1.c1 = t2.c1을 적용한 결과 집합 → WHERE 조건 t1.c2 = t2.c2를 적용

```
( 1,  1, null, null )
  ( 2,  2,    2,    2 )                        ( 2,  2,    2,    2 )
  ( 3,  3,    3,    3 )                   →   ( 3,  3,    3,    3 ) 
  ( 4,  4, null, null )
  ( 5,  5, null, null )
```

Left outer join은 왼쪽 row에 대한 join 조건을 만족하는 오른쪽 row가 있을 경우, 해당 row들을 결합한 row를 결과로 반환한다. Join 조건을 만족하는 오른쪽 row가 존재하지 않을 경우, 왼쪽 row의 값은 그대로 유지하고 오른쪽 row의 값은 모두 NULL로 채운 row를 결과로 반환한다.

- **LEFT OUTER JOIN:** 

```
t1 ( 1, 1 ), ( 2, 2 )
t2 ( 2, 2 ), ( 3, 3 )

gSQL> SELECT * FROM t1 LEFT OUTER JOIN t2 ON t1.c1 = t2.c1;
C1 C2   C1   C2
-- -- ---- ----
 1  1 null null
 2  2    2    2
2 rows selected.
```

Right outer join은 left outer join과 정확히 반대로 동작한다.

```
RIGHT OUTER JOIN

t1 ( 1, 1 ), ( 2, 2 )
t2 ( 2, 2 ), ( 3, 3 )

gSQL> SELECT * FROM t1 RIGHT OUTER JOIN t2 ON t1.c1 = t2.c1;
  C1   C2 C1 C2
---- ---- -- --
   2    2  2  2
null null  3  3
2 rows selected.
```

Full outer join은 left outer join의 결과와 함께 join 조건을 만족하지 않는 모든 오른쪽 row에 대해 왼쪽 row의 값을 NULL로 채운 row들을 결과로 반환한다.

```
FULL OUTER JOIN

t1 ( 1, 1 ), ( 2, 2 )
t2 ( 2, 2 ), ( 3, 3 )

gSQL> SELECT * FROM t1 FULL OUTER JOIN t2 ON t1.c1 = t2.c1;
  C1   C2   C1   C2
---- ---- ---- ----
   1    1 null null
   2    2    2    2
null null    3    3
3 rows selected.
```

<a id="361dc51228591485"></a>
##### &lt;natural join&gt;

&lt;natural join&gt;은 join에 참여하는 두 table에서 동일한 이름을 갖는 모든 column들을 각각 equal 조건으로 join 한다. 즉, join에 참여하는 두 table에서 동일한 이름을 갖는 모든 column들을 inner join에서 USING 구문에 기술한 것과 동일하다.

```
t1 ( C1 INTEGER, C2 INTEGER )
t2 ( C1 INTEGER, C3 INTEGER )

t1 ( 1, 10 ), ( 2, 20 ), ( 3, 30 )
t2 ( 1, 100 ), ( 2, 200 ), ( 3, 300 )

gSQL> SELECT * FROM t1 NATURAL JOIN t2; 
C1 C2  C3
-- -- ---
 1 10 100
 2 20 200
 3 30 300
3 rows selected.

gSQL> SELECT * FROM t1 INNER JOIN t2 USING ( c1 );
C1 C2  C3
-- -- ---
 1 10 100
 2 20 200
 3 30 300
3 rows selected.
```

<a id="6e4cfa57161cd68b"></a>
##### &lt;join specification&gt;

조인 조건을 기술한다.  
&lt;join condition&gt;은 join 구문의 왼쪽 row와 오른쪽 row를 조인할 조건을 기술한다.  
&lt;named columns join&gt;은 왼쪽 row와 오른쪽 row에 대해 동일한 &lt;column name&gt;이 존재하는 경우 이를 나열하여 조인 조건을 기술한다.

```
t1 ( C1 INTEGER, C2 INTEGER )
t2 ( C1 INTEGER, C3 INTEGER )

t1 ( 1, 10 ), ( 2, 20 ), ( 3, 30 )
t2 ( 1, 100 ), ( 2, 200 ), ( 3, 300 )

• <join condition>
gSQL> SELECT * FROM t1 INNER JOIN t2 ON t1.c1 = t2.c1;
C1 C2 C1  C3
-- -- -- ---
 1 10  1 100
 2 20  2 200
 3 30  3 300
3 rows selected.

• <named columns join>
gSQL> SELECT * FROM t1 INNER JOIN t2 USING ( c1 );
C1 C2  C3
-- -- ---
 1 10 100
 2 20 200
 3 30 300
3 rows selected.
```

<a id="9224f4e5f341c054"></a>
#### 사용 예

다음은 &lt;cross join&gt;을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, o_totalprice FROM customer CROSS JOIN orders;

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#1     46929.18
Customer#1    193846.25
Customer#1     32151.78
Customer#1     144659.2
Customer#2    173665.47
Customer#2     46929.18
Customer#2    193846.25
Customer#2     32151.78
Customer#2     144659.2
Customer#3    173665.47
Customer#3     46929.18
Customer#3    193846.25
Customer#3     32151.78
Customer#3     144659.2
Customer#4    173665.47
Customer#4     46929.18
Customer#4    193846.25
Customer#4     32151.78
Customer#4     144659.2

C_NAME     O_TOTALPRICE
---------- ------------
Customer#5    173665.47
Customer#5     46929.18
Customer#5    193846.25
Customer#5     32151.78
Customer#5     144659.2

25 rows selected.
```

다음은 inner join을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, o_totalprice FROM customer INNER JOIN orders ON c_custkey = o_custkey;

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#2     46929.18
Customer#4    193846.25
Customer#3     32151.78
Customer#5     144659.2

5 rows selected.
```

다음은 outer join을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, o_totalprice FROM customer LEFT OUTER JOIN orders ON c_custkey = o_custkey AND o_orderdate < '1996-01-01';

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1         null
Customer#2         null
Customer#3     32151.78
Customer#4    193846.25
Customer#5     144659.2

5 rows selected.

gSQL> SELECT c_name, o_totalprice FROM customer RIGHT OUTER JOIN orders ON c_custkey = o_custkey AND c_nation = 'KOREA';

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
null           46929.18
null          193846.25
Customer#3     32151.78
null           144659.2

5 rows selected.

gSQL> SELECT c_name, o_totalprice FROM customer FULL OUTER JOIN orders ON c_custkey = o_custkey AND c_nation = 'KOREA' AND o_orderdate < '1996-01-01';

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1         null
Customer#2         null
Customer#3     32151.78
Customer#4         null
Customer#5         null
null          173665.47
null           46929.18
null          193846.25
null           144659.2

9 rows selected.
```

다음은 natural join을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, o_totalprice FROM (SELECT c_custkey custkey, c_name FROM customer) NATURAL JOIN (SELECT o_custkey custkey, o_totalprice FROM orders);

C_NAME     O_TOTALPRICE
---------- ------------
Customer#1    173665.47
Customer#2     46929.18
Customer#4    193846.25
Customer#3     32151.78
Customer#5     144659.2

5 rows selected.
```

<a id="efcd3d77f3678ceb"></a>
#### 호환성

**SQL 표준 호환성**

<a id="52e0f264186a5e98"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F401 | Extended joined table | O |
| F402 | Named column joins for LOBs, arrays, and multisets | X |
| F403 | Partitioned join tables | X |

<a id="99844e5ae33e22fb"></a>
#### 참조

관련 내용은 [from clause](#d8f9755e05abe1cf)를 참조한다.

<a id="fc4e37ea9e697ac1"></a>
### pivot clause

<a id="cd05c3269f1378da"></a>
#### 기능

Row (value)를 column으로 변환하는 cross table을 기술한다.

<a id="45051c2eec4ba6cf"></a>
#### 구문

```
<pivot clause> ::=
    PIVOT
    <left paren>
       <aggregation function> [[AS] alias]
       [, <aggregation function> [[AS] alias]] ...
       <pivot for clause>
       <pivot in clause>
    <right paren>

<pivot for clause> ::=
      FOR column
    | FOR <left paren> column [, column] ... <right paren>

<pivot in clause> ::=
    IN
    <left paren>
    { <pivot value list> [[AS] alias] [, <pivot value list> [[AS] alias]] ... }
    <right paren>

<pivot value list> ::=
      expr
    | <left paren> expr [, expr] ... <right paren>
```

<a id="fd30bf96b672c941"></a>
#### 구문 규칙 및 파라미터

<a id="79366d1777de6038"></a>
##### &lt;pivot clause&gt;

&lt;aggregation function&gt;에서 중첩된 집계 함수를 사용할 수 없다.

```
gSQL> SELECT *
        FROM t1 PIVOT(
                       SUM( SUM( c2 ) ) 
                       FOR c1
                       IN (
                             1
                           , 2
                          )
                        );

ERR-42000(16160): group function is nested too deeply : 
                 SUM( SUM( c2 ) ) 
                      *
ERROR at line 3:
```

&lt;pivot for clause&gt;에 기술된 column의 개수와 &lt;pivot value list&gt;의 expr의 개수는 일치하여야 한다.

```
gSQL> SELECT *
        FROM t1 PIVOT(
                       SUM( 1 ) 
                       FOR ( c1, c2 )
                       IN (
                             ( 1, 2 )
                           , ( 3 )
                          )
                        );

ERR-42000(16606): the number of elements in pivot values mismatch the pivot columns : 
                           , ( 3 )
                             *
ERROR at line 7:
```

<a id="27e3dfba7c782ee2"></a>
##### &lt;pivot for clause&gt;

&lt;pivot for clause&gt; 내 column은 column_name만 명시할 수 있다.

```
gSQL> SELECT *
        FROM t1 PIVOT(
                       SUM( 1 ) 
                       FOR 1
                       IN (
                             1
                           , 2
                          )
                        );

    2     3     4     5     6     7     8     9 
ERR-42000(40000): syntax error: 
                       FOR 1
                           ^
Error at line 4


gSQL> SELECT *
        FROM t1 PIVOT(
                       SUM( 1 ) 
                       FOR c1 + 1
                       IN (
                             1
                           , 2
                          )
                        );

    2     3     4     5     6     7     8     9 
ERR-42000(40000): syntax error: 
                       FOR c1 + 1
                              ^
Error at line 4
```

<a id="b26fa3e0ff43850c"></a>
##### &lt;pivot in clause&gt;

&lt;pivot in clause&gt; 내 expr은 상수만 지원한다.

```
gSQL> SELECT *
        FROM t1 PIVOT(
                       SUM( 1 ) 
                       FOR c1
                       IN (
                             c1
                           , 2
                          )
                        );

    2     3     4     5     6     7     8     9 
ERR-42000(16608): non-constant expression is not allowed for pivot|unpivot values : 
                             c1
                             *
ERROR at line 6:


gSQL> SELECT *
        FROM t1 PIVOT(
                       SUM( 1 ) 
                       FOR c1
                       IN (
                             CLOCK_DATE()
                           , 2
                          )
                        );

    2     3     4     5     6     7     8     9 
ERR-42000(16608): non-constant expression is not allowed for pivot|unpivot values : 
                             CLOCK_DATE()
                             *
ERROR at line 6:
```

각 레코드마다 값이 달라지는 expression이나 매번 평가값이 달라지는 expression은 지원하지 않는다.

```
gSQL> SELECT *
        FROM t1 PIVOT(
                       SUM( 1 ) 
                       FOR c1
                       IN (
                             RANDOM( 1, 2 )
                           , 2
                          )
                        );

    2     3     4     5     6     7     8     9 
ERR-42000(16608): non-constant expression is not allowed for pivot|unpivot values : 
                             RANDOM( 1, 2 )
                             *
ERROR at line 6:
```

<a id="be7dd8fb95788dc8"></a>
#### 설명

<a id="c49e8d387d3cdffc"></a>
##### &lt;pivot clause&gt;

&lt;pivot clause&gt; 구문은 source relation을 이용하여 새로운 cross table을 정의한다.

```
gSQL> SELECT T_PIVOT.*
        FROM t1
                PIVOT(                  -- new cross table
                       SUM( c2 ) 
                       FOR c1
                       IN (
                             1
                           , 2
                          )
                        ) AS T_PIVOT;

1 2
- -
1 3

1 row selected.
```

&lt;pivot clause&gt; 구문 앞에 기술된 relation은 cross table의 source relation이다.

```
gSQL> SELECT *
        FROM t1                  -- source relation
                PIVOT(
                       SUM( c2 ) 
                       FOR c1
                       IN (
                             1
                           , 2
                          )
                        );


1 2
- -
1 3

1 row selected.
```

<a id="e93b8e6b3071925d"></a>
##### &lt;pivot for clause&gt;

&lt;pivot for clause&gt; 구문은 pivot 대상 column을 정의한다.

```
gSQL> SELECT c1 FROM t1;

C1
--
 1
 2
 2

3 rows selected.



gSQL> SELECT *
        FROM t1 
                PIVOT(
                       SUM( c2 ) 
                       FOR c1      -- t1.c1
                       IN (
                             1     -- t1.c1 = 1 인 경우
                           , 2     -- t1.c1 = 2 인 경우
                          )
                        );


1 2
- -
1 3

1 row selected.
```

<a id="4ec2745ab26bd08e"></a>
##### Pivot Column

Cross table의 새로운 pivot column은 &lt;pivot in clause&gt;에서 나열한 값과 &lt;aggregation function&gt;의 조합 개수만큼 구성한다.

```
gSQL> SELECT *
        FROM t1
                PIVOT(
                       SUM( c2 )    -- aggregation #1
                       FOR c1
                       IN (
                             1      -- row #1
                           , 2      -- row #2
                          )
                        );

1 2
- -
1 3

1 row selected.


gSQL> SELECT *
        FROM t1
                PIVOT(
                       SUM( c2 )    -- aggregation #1
                     , COUNT(*)     -- aggregation #2
                       FOR c1
                       IN (
                             1      -- row #1
                           , 2      -- row #2
                          )
                        );
1 1 2 2
- - - -
1 1 3 2

1 row selected.
```

Source relation의 column 중에 &lt;pivot clause&gt; 구문 내에서 참조되지 않은 모든 column은 cross table의 column으로 구성한다.

```
gSQL> \DESC t1

COLUMN_NAME TYPE         IS_NULLABLE
----------- ------------ -----------
C1          NUMBER(10,0) TRUE       
C2          NUMBER(10,0) TRUE  


gSQL> SELECT *
        FROM t1
                PIVOT(
                       SUM( 1 ) 
                       FOR c1      -- t1.c1 참조
                       IN (
                             1
                           , 2
                          )
                        );

C2    1 2
-- ---- -
 1    1 1
 2 null 1

2 rows selected.


gSQL> SELECT *
        FROM t1
                PIVOT(
                       SUM( c2 )   -- t1.c2 참조
                       FOR c1      -- t1.c1 참조
                       IN (
                             1
                           , 2
                          )
                        );

1 2
- -
1 3

1 row selected.
```

<a id="7e0b97e8ce86e3f5"></a>
##### Pivot Column Name

pivot column name은 pivot column name prefix와 pivot column name suffix 사이에 '_'를 붙여 구성한다.

```
gSQL> SELECT *
        FROM t1
                PIVOT(
                       SUM( c2 ) AS TOTAL     -- suffix
                       FOR c1
                       IN (
                             1   AS ONE       -- prefix #1
                           , 2   AS TWO       -- prefix #2
                          )
                        );

ONE_TOTAL TWO_TOTAL
--------- ---------
        1         3

gSQL> SELECT *
        FROM t1
                PIVOT(
                       SUM( c2 ) AS TOTAL     -- suffix #1
                     , COUNT(*)  AS CNT       -- suffix #2
                       FOR c1
                       IN (
                             1   AS ONE       -- prefix #1
                           , 2   AS TWO       -- prefix #2
                          )
                        );

ONE_TOTAL ONE_CNT TWO_TOTAL TWO_CNT
--------- ------- --------- -------
        1       1         3       2

1 row selected.
```

<a id="28ccdbec512b7467"></a>
###### **Pivot Column Name Prefix**

&lt;pivot value list&gt; 내에서 나열된 expr에 대한 display name은 pivot column name의 prefix로 사용된다.

```
gSQL> SELECT *
        FROM t1
                PIVOT(
                       SUM( c2 ) AS TOTAL     -- suffix
                       FOR c1
                       IN (
                             1                -- prefix #1
                           , '2'              -- prefix #2
                          )
                        );


1_TOTAL '2'_TOTAL
------- ---------
      1         3

1 row selected.


gSQL> SELECT *
        FROM t1
                PIVOT(
                       SUM( c2 ) AS TOTAL     -- suffix #1
                     , COUNT(*)  AS CNT       -- suffix #2
                       FOR c1
                       IN (
                             1                -- prefix #1
                           , '2'              -- prefix #2
                          )
                        );

1_TOTAL 1_CNT '2'_TOTAL '2'_CNT
------- ----- --------- -------
      1     1         3       2

1 row selected.
```

&lt;pivot value list&gt;에서 둘 이상의 expr이 사용된 경우 각 expr의 display name을 '_'로 연결한다.

```
gSQL> SELECT *
        FROM t1
                PIVOT(
                       COUNT(*)
                       FOR ( c1, c2 )
                       IN (
                             ( 1, 2 )      -- prefix #1
                           , ( '3', '4' )  -- prefix #2
                          )
                        );

1_2 '3'_'4'
--- -------
  0       0

1 row selected.



gSQL> SELECT *
        FROM t1
                PIVOT(
                       COUNT(*) AS CNT     -- suffix
                       FOR ( c1, c2 )
                       IN (
                             ( 1, 2 )      -- prefix #1
                           , ( '3', '4' )  -- prefix #2
                          )
                        );

1_2_CNT '3'_'4'_CNT
------- -----------
      0           0

1 row selected.
```

&lt;pivot value list&gt;에 alias를 명시한 경우 pivot column name의 prefix는 alias로 대체한다.

```
gSQL> SELECT *
        FROM t1
                PIVOT(
                       SUM( c2 )
                       FOR c1
                       IN (
                             1    AS ONE     -- prefix #1
                           , '2'  AS TWO     -- prefix #2
                          )
                        );

ONE TWO
--- ---
  1   3

1 row selected.


gSQL> SELECT *
        FROM t1
                PIVOT(
                       SUM( c2 ) AS TOTAL    -- suffix
                       FOR c1
                       IN (
                             1    AS ONE     -- prefix #1
                           , '2'  AS TWO     -- prefix #2
                          )
                        );

ONE_TOTAL TWO_TOTAL
--------- ---------
        1         3

1 row selected.
```

<a id="30442bc024b3eff2"></a>
###### **Pivot Column Name Suffix**

&lt;aggregation function&gt;에 집계값에 대한 alias를 부여할 수 있는데, 이 때 alias는 pivot column name의 suffix로 적용된다.

```
gSQL> SELECT *
        FROM t1
                PIVOT(
                       SUM( c2 ) AS TOTAL    -- suffix #1
                     , COUNT(*)  AS CNT      -- suffix #2
                       FOR c1
                       IN (
                             1    AS ONE     -- prefix
                          )
                        );

ONE_TOTAL ONE_CNT
--------- -------
        1       1

1 row selected.
```

&lt;aggregation function&gt;에 alias를 부여하지 않은 경우 pivot column name의 suffix는 존재하지 않는다.

```
gSQL> SELECT *
        FROM t1
                PIVOT(
                       SUM( c2 )             -- suffix #1 (empty)
                     , COUNT(*)  AS CNT      -- suffix #2
                       FOR c1
                       IN (
                             1    AS ONE     -- prefix
                          )
                        );

ONE ONE_CNT
--- -------
  1       1

1 row selected.
```

<a id="6cfe9b164943d5d7"></a>
#### 사용 예

다음은 &lt;pivot clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT * FROM sales;

ITEM   REGION PRICE AMOUNT
------ ------ ----- ------
apple  seoul  30000     10
apple  seoul  30000     30
kiwi   seoul  20000     15
mango  seoul  40000     20
orange seoul  25000      5
apple  busan  25000      5
mango  busan  35000     20
mango  busan  45000     10
orange busan  30000     15
apple  daegu  25000     30
kiwi   daegu  25000     10
kiwi   daegu  15000     20
apple  jeju   25000     30
apple  jeju   35000      5
kiwi   jeju   15000     10
kiwi   jeju   15000     10
mango  jeju   45000     10

17 rows selected.


--# 지역별로 판매한 과일 종류별 매출 집계는?
gSQL> SELECT *
        FROM sales PIVOT(
                          SUM( price * amount ) FOR item IN (  'apple'  PC_APPLE
                                                             , 'kiwi'   PC_KIWI
                                                             , 'mango'  PC_MANGO
                                                             , 'orange' PC_ORANGE )
                        );

REGION PC_APPLE PC_KIWI PC_MANGO PC_ORANGE
------ -------- ------- -------- ---------
seoul   1200000  300000   800000    125000
daegu    750000  550000     null      null
busan    125000    null  1150000    450000
jeju     925000  300000   450000      null

4 rows selected.
```

<a id="e51aafd8c28e402a"></a>
#### 호환성

SQL 표준에서는 pivot에 대한 개념을 정의하지 않고 있다.

<a id="5774ddffb50ff2f7"></a>
#### 참조

관련 내용은 [from clause](#d8f9755e05abe1cf)를 참조한다.

<a id="e4262e566d20f76e"></a>
### unpivot clause

<a id="7bd27db43337b183"></a>
#### 기능

Column을 row (value)로 변환하는 cross table을 기술한다.

<a id="c87d537a756d7b8f"></a>
#### 구문

```
<unpivot clause> ::=
    UNPIVOT [ INCLUDE NULLS | EXCLUDE NULLS ]
    <left paren>
       <unpivot value column list>
       <unpivot for clause>
       <unpivot in clause>
    <right paren>

<unpivot value column list> ::=
       name
     | <left paren> name [, name] ... <right paren>
       
<unpivot for clause> ::=
      FOR name
    | FOR <left paren> name [, name] ... <right paren>

<unpivot in clause> ::=
    IN
    <left paren>
        <columns of unpivot in clause> [, <columns of unpivot in clause>] ...
    <right paren>

<columns of unpivot in clause> ::=
    {
        column
      | <left paren> column [, column] ... <right paren>
    }
    [ AS
         {
             expr
         }
    ]
```

<a id="0c9fdfc43f7f8d3b"></a>
#### 구문 규칙 및 파라미터

<a id="3710069836d28702"></a>
##### &lt;unpivot clause&gt;

&lt;unpivot clause&gt; 구문에 [ INCLUDE NULLS | EXCLUDE NULLS ]을 기술하지 않은 경우 EXCLUDE NULLS와 동일하게 동작한다.

```
gSQL> SELECT * FROM result;

STUDENT ENGLISH MATH SCIENCE HISTORY
------- ------- ---- ------- -------
David        70   70      80      90
Linda        90   60      80      70
Tom          90 null    null      70

3 rows selected.


gSQL> SELECT *
        FROM result
              UNPIVOT INCLUDE NULLS      -- INCLUDE NULLS
                     (
                       uc_score
                       FOR uc_subject
                       IN (
                             english
                           , math
                           , science
                           , history
                          )
                     );

STUDENT UC_SUBJECT UC_SCORE
------- ---------- --------
David   ENGLISH          70
Linda   ENGLISH          90
Tom     ENGLISH          90
David   MATH             70
Linda   MATH             60
Tom     MATH           null
David   SCIENCE          80
Linda   SCIENCE          80
Tom     SCIENCE        null
David   HISTORY          90
Linda   HISTORY          70
Tom     HISTORY          70

12 rows selected.

12 rows selected.


gSQL> SELECT *
        FROM result
              UNPIVOT EXCLUDE NULLS      -- EXCLUDE NULLS
                     (
                       uc_score
                       FOR uc_subject
                       IN (
                             english
                           , math
                           , science
                           , history
                          )
                     );

STUDENT UC_SUBJECT UC_SCORE
------- ---------- --------
David   ENGLISH          70
Linda   ENGLISH          90
Tom     ENGLISH          90
David   MATH             70
Linda   MATH             60
David   SCIENCE          80
Linda   SCIENCE          80
David   HISTORY          90
Linda   HISTORY          70
Tom     HISTORY          70

10 rows selected.


gSQL> SELECT *
        FROM result
              UNPIVOT                     -- NULLS Treatment 생략
                     (
                       uc_score
                       FOR uc_subject
                       IN (
                             english
                           , math
                           , science
                           , history
                          )
                     );

STUDENT UC_SUBJECT UC_SCORE
------- ---------- --------
David   ENGLISH          70
Linda   ENGLISH          90
Tom     ENGLISH          90
David   MATH             70
Linda   MATH             60
David   SCIENCE          80
Linda   SCIENCE          80
David   HISTORY          90
Linda   HISTORY          70
Tom     HISTORY          70

10 rows selected.
```

<a id="6147ed4b041b7bdd"></a>
##### &lt;unpivot in clause&gt;

&lt;unpivot in clause&gt; 내의 column은 column_name만 명시할 수 있다.

```
gSQL> SELECT *
        FROM result
              UNPIVOT
                     (
                       uc_score
                       FOR uc_subject
                       IN (
                             'aaa'
                          )
                     );

ERR-42000(40000): syntax error: 
                             'aaa'
                             ^   ^
Error at line 8


gSQL> SELECT *
        FROM result
              UNPIVOT
                     (
                       uc_score
                       FOR uc_subject
                       IN (
                             xxx
                          )
                     );

ERR-42000(16036): 'XXX': invalid identifier : 
                             xxx
                             *
ERROR at line 8:
```

&lt;unpivot value column list&gt; 내의 name 개수와 &lt;columns of unpivot in clause&gt; 내의 column 개수는 일치하여야 한다.

```
gSQL> SELECT *
        FROM result
              UNPIVOT
                     (
                       uc_score                    -- <unpivot value column list>
                       FOR uc_subject
                       IN (
                             english               -- <columns of unpivot in clause> #1
                           , ( math, science )     -- <columns of unpivot in clause> #2
                          )
                     );

ERR-42000(16607): the number of elements in unpivot values mismatch the unpivot columns : 
                           , ( math, science )     -- <columns of unpivot in clause> #2
                                     *
ERROR at line 9:


gSQL> SELECT *
        FROM result
              UNPIVOT
                     (
                       ( uc_score_1, uc_score_2 )  -- <unpivot value column list>
                       FOR uc_subject
                       IN (
                             english               -- <columns of unpivot in clause> #1
                           , ( math, science )     -- <columns of unpivot in clause> #2
                          )
                     );

ERR-42000(16607): the number of elements in unpivot values mismatch the unpivot columns : 
                             english               -- <columns of unpivot in clause> #1
                             *
ERROR at line 8:
```

&lt;columns of unpivot in clause&gt;의 AS 키워드 다음에 기술되는 expr은 unpivot 대상 relation의 column을 참조할 수 없다.

```
gSQL> SELECT *
        FROM result
              UNPIVOT
                     (
                       uc_score
                       FOR uc_subject
                       IN (
                             english AS english    -- result.column
                          )
                     );

ERR-42000(16036): 'ENGLISH': invalid identifier : 
                             english AS english
                                        *
ERROR at line 8:


gSQL> SELECT *
        FROM result
              UNPIVOT
                     (
                       uc_score
                       FOR uc_subject
                       IN (
                             english AS student    -- result.column
                          )
                     );

ERR-42000(16036): 'STUDENT': invalid identifier : 
                             english AS student
                                        *
ERROR at line 8:


gSQL> SELECT *
        FROM dual
       WHERE EXISTS(
                     SELECT *
                       FROM result
                             UNPIVOT
                                    (
                                      uc_score
                                      FOR uc_subject
                                      IN (
                                            english AS dummy  -- dual.dummy (outer query's column)
                                         )
                                    )
                    );

DUMMY
-----
X    

1 row selected.
```

<a id="39a7ac1a6ac09738"></a>
#### 설명

<a id="da2234c6451e5d95"></a>
##### &lt;unpivot clause&gt;

&lt;unpivot clause&gt; 구문은 source relation을 이용하여 새로운 cross table을 정의한다.

```
gSQL> SELECT T_UNPIVOT.*
        FROM result
              UNPIVOT                       -- new cross table
                     (
                       uc_score
                       FOR uc_subject
                       IN (
                             english
                           , math
                           , science
                           , history
                          )
                     ) T_UNPIVOT;

STUDENT UC_SUBJECT UC_SCORE
------- ---------- --------
David   ENGLISH          70
Linda   ENGLISH          90
Tom     ENGLISH          90
David   MATH             70
Linda   MATH             60
David   SCIENCE          80
Linda   SCIENCE          80
David   HISTORY          90
Linda   HISTORY          70
Tom     HISTORY          70

10 rows selected.
```

&lt;unpivot clause&gt; 구문 앞에 기술된 relation은 cross table의 source relation이다.

```
gSQL> SELECT * 
        FROM result                  -- source relation
              UNPIVOT 
                     (
                       uc_score
                       FOR uc_subject
                       IN (
                             english
                           , math
                           , science
                           , history
                          )
                     );

STUDENT UC_SUBJECT UC_SCORE
------- ---------- --------
David   ENGLISH          70
Linda   ENGLISH          90
Tom     ENGLISH          90
David   MATH             70
Linda   MATH             60
David   SCIENCE          80
Linda   SCIENCE          80
David   HISTORY          90
Linda   HISTORY          70
Tom     HISTORY          70

10 rows selected.
```

&lt;unpivot clause&gt;에 INCLUDE NULLS을 명시한 경우 unpivot에 의해 생성된 모든 레코드를 결과로 반환한다.

```
gSQL> SELECT * 
        FROM result
              UNPIVOT INCLUDE NULLS
                     (
                       uc_score
                       FOR uc_subject
                       IN (
                             english
                           , math
                           , science
                           , history
                          )
                     );

STUDENT UC_SUBJECT UC_SCORE
------- ---------- --------
David   ENGLISH          70
Linda   ENGLISH          90
Tom     ENGLISH          90
David   MATH             70
Linda   MATH             60
Tom     MATH           null
David   SCIENCE          80
Linda   SCIENCE          80
Tom     SCIENCE        null
David   HISTORY          90
Linda   HISTORY          70
Tom     HISTORY          70

12 rows selected.
```

&lt;unpivot clause&gt;에 EXCLUDE NULLS을 명시한 경우 unpivot에 의해 생성된 레코드 중 unpivot column이 모두 null 인 레코드를 제외한 나머지 레코드들을 결과로 반환한다.

```
--# unpivot column 이 모두 null 인 경우

gSQL> SELECT * 
        FROM result
              UNPIVOT EXCLUDE NULLS   -- uc_score column값이 null인 row는 제거
                     (
                       uc_score        
                       FOR uc_subject
                       IN (
                             english
                           , math
                           , science
                           , history
                          )
                     );

STUDENT UC_SUBJECT UC_SCORE
------- ---------- --------
David   ENGLISH          70
Linda   ENGLISH          90
Tom     ENGLISH          90
David   MATH             70
Linda   MATH             60
David   SCIENCE          80
Linda   SCIENCE          80
David   HISTORY          90
Linda   HISTORY          70
Tom     HISTORY          70

10 rows selected.
```

```
--# unpivot column 이 일부만 null 인 경우

gSQL> SELECT * 
        FROM result
              UNPIVOT INCLUDE NULLS
                     (
                       ( uc_score_1, uc_score_2 )
                       FOR uc_subject
                       IN (
                             ( english, math )
                           , ( science, history )
                          )
                     );

STUDENT UC_SUBJECT      UC_SCORE_1 UC_SCORE_2
------- --------------- ---------- ----------
David   ENGLISH_MATH            70         70
Linda   ENGLISH_MATH            90         60
Tom     ENGLISH_MATH            90       null
David   SCIENCE_HISTORY         80         90
Linda   SCIENCE_HISTORY         80         70
Tom     SCIENCE_HISTORY       null         70

6 rows selected.


gSQL> SELECT * 
        FROM result
              UNPIVOT EXCLUDE NULLS   -- uc_score_1, uc_score_2 모두 null값인 row는 제거
                     (
                       ( uc_score_1, uc_score_2 )
                       FOR uc_subject
                       IN (
                             ( english, math )
                           , ( science, history )
                          )
                     );

STUDENT UC_SUBJECT      UC_SCORE_1 UC_SCORE_2
------- --------------- ---------- ----------
David   ENGLISH_MATH            70         70
Linda   ENGLISH_MATH            90         60
Tom     ENGLISH_MATH            90       null
David   SCIENCE_HISTORY         80         90
Linda   SCIENCE_HISTORY         80         70
Tom     SCIENCE_HISTORY       null         70

6 rows selected.
```

```
--# unpivot column 이 모두 null 인 경우

gSQL> SELECT * 
        FROM result
              UNPIVOT INCLUDE NULLS
                     (
                       ( uc_score_1, uc_score_2 )
                       FOR uc_subject
                       IN (
                             ( english, history )
                           , ( math, science )
                          )
                     );

STUDENT UC_SUBJECT      UC_SCORE_1 UC_SCORE_2
------- --------------- ---------- ----------
David   ENGLISH_HISTORY         70         90
Linda   ENGLISH_HISTORY         90         70
Tom     ENGLISH_HISTORY         90         70
David   MATH_SCIENCE            70         80
Linda   MATH_SCIENCE            60         80
Tom     MATH_SCIENCE          null       null

6 rows selected.


gSQL> SELECT * 
        FROM result
              UNPIVOT EXCLUDE NULLS   -- uc_score_1, uc_score_2 모두 null값인 row는 제거

                     (
                       ( uc_score_1, uc_score_2 )
                       FOR uc_subject
                       IN (
                             ( english, history )
                           , ( math, science )
                          )
                     );

STUDENT UC_SUBJECT      UC_SCORE_1 UC_SCORE_2
------- --------------- ---------- ----------
David   ENGLISH_HISTORY         70         90
Linda   ENGLISH_HISTORY         90         70
Tom     ENGLISH_HISTORY         90         70
David   MATH_SCIENCE            70         80
Linda   MATH_SCIENCE            60         80

5 rows selected.
```

<a id="4c06ffabe0d994d3"></a>
##### Source Relation의 Column 정보로 구성된 Unpivot Column

&lt;unpivot for clause&gt; 구문은 unpivot 대상 column에 대한 정보로 구성된 새로운 unpivot column을 구성한다.

```
gSQL> SELECT * 
        FROM result
              UNPIVOT INCLUDE NULLS
                     (
                       uc_score
                       FOR uc_subject    -- value is column's name in <columns of unpivot in clause>
                       IN (
                             english     -- <columns of unpivot in clause> #1
                           , math        -- <columns of unpivot in clause> #2
                           , science     -- <columns of unpivot in clause> #3
                           , history     -- <columns of unpivot in clause> #4
                          )
                     );

STUDENT UC_SUBJECT UC_SCORE
------- ---------- --------
David   ENGLISH          70
Linda   ENGLISH          90
Tom     ENGLISH          90
David   MATH             70
Linda   MATH             60
Tom     MATH           null
David   SCIENCE          80
Linda   SCIENCE          80
Tom     SCIENCE        null
David   HISTORY          90
Linda   HISTORY          70
Tom     HISTORY          70

12 rows selected.
```

&lt;unpivot for clause&gt; 내의 name은 새로운 unpivot column의 column name이다.

```
gSQL> SELECT T_UNPIVOT.* 
        FROM result
              UNPIVOT INCLUDE NULLS
                     (
                       uc_score
                       FOR english    -- T_UNPIVOT's column
                       IN (
                             english
                          )
                     ) T_UNPIVOT;

STUDENT MATH SCIENCE HISTORY ENGLISH UC_SCORE
------- ---- ------- ------- ------- --------
David     70      80      90 ENGLISH       70
Linda     60      80      70 ENGLISH       90
Tom     null    null      70 ENGLISH       90

3 rows selected.
```

&lt;unpivot for clause&gt; 내에 기술된 name 개수만큼 새로운 unpivot column이 구성한다.

```
gSQL> SELECT * 
        FROM result
              UNPIVOT INCLUDE NULLS
                     (
                       uc_score
                       FOR (
                              uc_subject_1  -- <unpivot for clause> unpivot column #1
                            , uc_subject_2  -- <unpivot for clause> unpivot column #2
                            )
                       IN (
                             english
                           , math
                           , science
                           , history
                          )
                     );

STUDENT UC_SUBJECT_1 UC_SUBJECT_2 UC_SCORE
------- ------------ ------------ --------
David   ENGLISH      ENGLISH            70
Linda   ENGLISH      ENGLISH            90
Tom     ENGLISH      ENGLISH            90
David   MATH         MATH               70
Linda   MATH         MATH               60
Tom     MATH         MATH             null
David   SCIENCE      SCIENCE            80
Linda   SCIENCE      SCIENCE            80
Tom     SCIENCE      SCIENCE          null
David   HISTORY      HISTORY            90
Linda   HISTORY      HISTORY            70
Tom     HISTORY      HISTORY            70

12 rows selected.
```

&lt;columns of unpivot in clause&gt; 내에 기술된 column들의 display name를 '_'로 연결하여 새로운 string value를 구성한다.

구성된 string value는 &lt;unpivot for clause&gt;에 의해 생성된 unpivot column의 값이다.

```
gSQL> SELECT * 
        FROM result
              UNPIVOT INCLUDE NULLS
                     (
                       ( uc_score_1, uc_score_2 )
                       FOR uc_subject               -- value is column's name in <columns of unpivot in clause>
                       IN (
                             ( english, math )      -- <columns of unpivot in clause> #1
                           , ( science, history )   -- <columns of unpivot in clause> #2
                          )
                     );

STUDENT UC_SUBJECT      UC_SCORE_1 UC_SCORE_2
------- --------------- ---------- ----------
David   ENGLISH_MATH            70         70
Linda   ENGLISH_MATH            90         60
Tom     ENGLISH_MATH            90       null
David   SCIENCE_HISTORY         80         90
Linda   SCIENCE_HISTORY         80         70
Tom     SCIENCE_HISTORY       null         70

6 rows selected.
```

Unpivot table의 각 레코드 내 &lt;unpivot for clause&gt;에 의해 구성된 unpivot column들은 모두 같은 값을 가진다.

```
gSQL> SELECT * 
        FROM result
              UNPIVOT INCLUDE NULLS
                     (
                       ( uc_score_1, uc_score_2 )
                       FOR (
                             uc_subject_1               -- value is column's name in <columns of unpivot in clause>
                           , uc_subject_2               -- value is column's name in <columns of unpivot in clause>
                           )
                       IN (
                             ( english, math )      -- <columns of unpivot in clause> #1
                           , ( science, history )   -- <columns of unpivot in clause> #2
                          )
                     );

STUDENT UC_SUBJECT_1    UC_SUBJECT_2    UC_SCORE_1 UC_SCORE_2
------- --------------- --------------- ---------- ----------
David   ENGLISH_MATH    ENGLISH_MATH            70         70
Linda   ENGLISH_MATH    ENGLISH_MATH            90         60
Tom     ENGLISH_MATH    ENGLISH_MATH            90       null
David   SCIENCE_HISTORY SCIENCE_HISTORY         80         90
Linda   SCIENCE_HISTORY SCIENCE_HISTORY         80         70
Tom     SCIENCE_HISTORY SCIENCE_HISTORY       null         70

6 rows selected.
```

<a id="1fe99982fbd333a5"></a>
##### Source Relation의 Column Value로 구성된 Unpivot Column

&lt;unpivot value column list&gt; 구문은 unpivot 대상 column의 값을 가지는 새로운 unpivot column을 정의한다.

&lt;columns of unpivot in clause&gt;의 column들의 값은 &lt;unpivot value column list&gt;에 의해 생성된 unpivot column의 값으로 설정된다.

```
gSQL> SELECT * 
        FROM result
              UNPIVOT INCLUDE NULLS
                     (
                       uc_score        -- value is column's value in <columns of unpivot in clause>
                       FOR uc_subject
                       IN (
                             english   -- <columns of unpivot in clause> #1
                           , math      -- <columns of unpivot in clause> #2
                           , science   -- <columns of unpivot in clause> #3
                           , history   -- <columns of unpivot in clause> #4
                          )
                     );

STUDENT UC_SUBJECT UC_SCORE
------- ---------- --------
David   ENGLISH          70
Linda   ENGLISH          90
Tom     ENGLISH          90
David   MATH             70
Linda   MATH             60
Tom     MATH           null
David   SCIENCE          80
Linda   SCIENCE          80
Tom     SCIENCE        null
David   HISTORY          90
Linda   HISTORY          70
Tom     HISTORY          70

12 rows selected.
```

&lt;unpivot in clause&gt; 구문은 unpivot 대상 column을 정의한다.

```
gSQL> SELECT * 
        FROM result
              UNPIVOT INCLUDE NULLS
                     (
                       uc_score
                       FOR uc_subject
                       IN (
                             english   -- english is result.english
                           , math      -- math is result.math
                           , science   -- science is result.science
                           , history   -- history is result.history
                          )
                     );

STUDENT UC_SUBJECT UC_SCORE
------- ---------- --------
David   ENGLISH          70
Linda   ENGLISH          90
Tom     ENGLISH          90
David   MATH             70
Linda   MATH             60
Tom     MATH           null
David   SCIENCE          80
Linda   SCIENCE          80
Tom     SCIENCE        null
David   HISTORY          90
Linda   HISTORY          70
Tom     HISTORY          70

12 rows selected.
```

<a id="57d2d772c4ce3619"></a>
#### 사용 예

다음은 &lt;unpivot clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT * FROM result;

STUDENT ENGLISH MATH SCIENCE HISTORY
------- ------- ---- ------- -------
David        70   70      80      90
James        80   90      60      60
Mary         70   90      50      80
Linda        90   60      80      70
Tom          90 null    null      70
null       null null    null    null

6 rows selected.


--# 전체 학생에 대한 과목별 점수 조회
gSQL> SELECT *
  FROM result
             UNPIVOT
                     (
                       uc_score
                       FOR uc_subject
                       IN (
                             english
                           , math
                           , science
                           , history
                          )
                     );

STUDENT UC_SUBJECT UC_SCORE
------- ---------- --------
David   ENGLISH          70
James   ENGLISH          80
Mary    ENGLISH          70
Linda   ENGLISH          90
Tom     ENGLISH          90
David   MATH             70
James   MATH             90
Mary    MATH             90
Linda   MATH             60
David   SCIENCE          80
James   SCIENCE          60
Mary    SCIENCE          50
Linda   SCIENCE          80
David   HISTORY          90
James   HISTORY          60
Mary    HISTORY          80
Linda   HISTORY          70
Tom     HISTORY          70

18 rows selected.
```

<a id="11e6402682aa6004"></a>
#### 호환성

SQL 표준에서는 unpivot에 대한 개념을 정의하지 않고 있다.

<a id="04908f3eaa7e2447"></a>
#### 참조

관련 내용은 [from clause](#d8f9755e05abe1cf)를 참조한다.

<a id="778d71bbe6c00108"></a>
### sample clause

<a id="b8a9d3a4ed98ca51"></a>
#### 기능

&lt;table primary&gt;에 무작위 sampling을 적용한다.

<a id="4cac2b7b3559cb21"></a>
#### 구문

```
<sample clause> ::=
      TABLESAMPLE <left paren> percent_value [ PERCENT ROWS | PERCENT PAGES ] <right paren> [ <repeatable clause> ]

<repeatable clause> ::=
    REPEATABLE <left paren> seed_value <right paren>
```

<a id="1a01798254c08d5f"></a>
#### 구문 규칙 및 파라미터

<a id="cfb55c11fedc45a2"></a>
##### &lt;sample clause&gt;

percent_value는 0보다 크고 100 이하인 실수만 허용한다.

```
gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 0 PERCENT ROWS );

ERR-42000(16664): table sampling rate must be greater than 0 and less than or equal to 100 : 
SELECT COUNT(*) FROM t1 TABLESAMPLE( 0 PERCENT ROWS )
                                     *
ERROR at line 1:


gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 200 PERCENT ROWS );

ERR-42000(16664): table sampling rate must be greater than 0 and less than or equal to 100 : 
SELECT COUNT(*) FROM t1 TABLESAMPLE( 200 PERCENT ROWS )
                                     *
ERROR at line 1:


gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 100 PERCENT ROWS );

COUNT(*)
--------
 1000000

1 row selected.


gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS );

COUNT(*)
--------
   99854

1 row selected.
```

PERCENT ROWS나 PERCENT PAGES를 명시하지 않은 경우, PERCENT ROWS를 적용한다.

```
gSQL> \EXPLAIN PLAN SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 );

COUNT(*)
--------
   99791

1 row selected.

>>>  start print plan

< Execution Plan >
==================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    ROWS |
--------------------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                       1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                       1 |
|    2  |      TABLE ACCESS ("T1")                                     |                       1 |
==================================================================================================

     1  -  TARGET : COUNT(*)
     2  -  ROW SAMPLING ( 10.00 % )
           READ COLUMN : NOTHING
           AGGREGATION : COUNT(*)

<<<  end print plan
```

percent_value는 소수점 이하 두 자리까지의 값을 table sampling rate로 사용한다.

```
gSQL> \EXPLAIN PLAN SELECT COUNT(*) FROM t1 TABLESAMPLE( 12.345678 );

COUNT(*)
--------
  123804

1 row selected.

>>>  start print plan

< Execution Plan >
==================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    ROWS |
--------------------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                       1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                       1 |
|    2  |      TABLE ACCESS ("T1")                                     |                       1 |
==================================================================================================

     1  -  TARGET : COUNT(*)
     2  -  ROW SAMPLING ( 12.34 % )
           READ COLUMN : NOTHING
           AGGREGATION : COUNT(*)

<<<  end print plan
```

<a id="33fd8241eee9c988"></a>
##### &lt;repeatable clause&gt;

seed_value는 native integer type이다.

```
gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS ) REPEATABLE ( 10000000000 );

ERR-22003(12075): data is outside the range of the data type to which the number is being converted


gSQL> \EXPLAIN PLAN SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS ) REPEATABLE ( 100000000 );

COUNT(*)
--------
   99967

1 row selected.

>>>  start print plan

< Execution Plan >
==================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    ROWS |
--------------------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                       1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                       1 |
|    2  |      TABLE ACCESS ("T1")                                     |                       1 |
==================================================================================================

     1  -  TARGET : COUNT(*)
     2  -  ROW SAMPLING ( 10.00 % ) REPEATABLE( 100000000 )
           READ COLUMN : NOTHING
           AGGREGATION : COUNT(*)

<<<  end print plan


gSQL> \EXPLAIN PLAN SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS ) REPEATABLE ( -100000000 );

COUNT(*)
--------
  100109

1 row selected.

>>>  start print plan

< Execution Plan >
==================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    ROWS |
--------------------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                       1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                       1 |
|    2  |      TABLE ACCESS ("T1")                                     |                       1 |
==================================================================================================

     1  -  TARGET : COUNT(*)
     2  -  ROW SAMPLING ( 10.00 % ) REPEATABLE( -100000000 )
           READ COLUMN : NOTHING
           AGGREGATION : COUNT(*)

<<<  end print plan
```

<a id="efac2db689f1fe99"></a>
#### 설명

&lt;sample clause&gt;은 SQL에서 base table 이나 global temporary table의 일부 샘플 데이터만 추출하여 질의를 수행할 수 있게 해주는 기능이다.

```
gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS );

COUNT(*)
--------
  100415

1 row selected.


gSQL> SELECT COUNT(*) FROM ( SELECT * FROM t1 ) TABLESAMPLE( 10 PERCENT ROWS );

ERR-42000(16663): table sampling can only be performed on a single base table or temporary table : 
SELECT COUNT(*) FROM ( SELECT * FROM t1 ) TABLESAMPLE( 10 PERCENT ROWS )
                       *
ERROR at line 1:


gSQL> SELECT COUNT(*) FROM v1 TABLESAMPLE( 10 PERCENT ROWS );

ERR-42000(16663): table sampling can only be performed on a single base table or temporary table : 
SELECT COUNT(*) FROM v1 TABLESAMPLE( 10 PERCENT ROWS )
                     *
ERROR at line 1:
```

PERCENT ROWS를 지정한 경우, percent_value의 확률로 row 단위 샘플링이 수행되며, PERCENT PAGES를 지정한 경우에는 percent_value의 확률로 page 단위 샘플링이 수행된다.

```
gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS );

COUNT(*)
--------
  100415

1 row selected.

gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS );

COUNT(*)
--------
  100173

1 row selected.

gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 20 PERCENT ROWS );

COUNT(*)
--------
  200285

1 row selected.

gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT PAGES );

COUNT(*)
--------
   96768

1 row selected.

gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 20 PERCENT PAGES );

COUNT(*)
--------
  202368

1 row selected.
```

&lt;sample clause&gt;은 정확한 결과 row 수를 보장을 하지 않으며, 인덱스를 무시하고 테이블에 직접 접근하여 평가를 수행한다.

```
gSQL> \EXPLAIN PLAN SELECT /*+ INDEX( t1 ) */ COUNT(*) FROM t1;

COUNT(*)
--------
 1000000

1 row selected.

>>>  start print plan

< Execution Plan >
==================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    ROWS |
--------------------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                       1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                       1 |
|    2  |      INDEX ACCESS ("T1", "IDX_T1")                           | (   1000000)          1 |
==================================================================================================

     1  -  TARGET : COUNT(*)
     2  -  READ INDEX COLUMN : NOTHING
           AGGREGATION : COUNT(*)

<<<  end print plan


gSQL> \EXPLAIN PLAN SELECT /*+ INDEX( t1 ) */ COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS );

COUNT(*)
--------
  100081

1 row selected.

>>>  start print plan

< Execution Plan >
==================================================================================================
|  IDX  |  NODE DESCRIPTION                                            |                    ROWS |
--------------------------------------------------------------------------------------------------
|    0  |  SELECT STATEMENT                                            |                       1 |
|    1  |    QUERY BLOCK ("$QB_IDX_2")                                 |                       1 |
|    2  |      TABLE ACCESS ("T1")                                     |                       1 |
==================================================================================================

     1  -  TARGET : COUNT(*)
     2  -  ROW SAMPLING ( 10.00 % )
           READ COLUMN : NOTHING
           AGGREGATION : COUNT(*)

<<<  end print plan
```

&lt;sample clause&gt;는 무작위 샘플링을 수행하므로, REPEATABLE 구문 없이 실행할 경우 매번 다른 결과가 나올 수 있다.

```
gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS );

COUNT(*)
--------
  100167

1 row selected.

gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS );

COUNT(*)
--------
   99802

1 row selected.

gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS );

COUNT(*)
--------
   99732

1 row selected.
```

&lt;repeatable clause&gt;의 seed_value가 다를 경우, 서로 다른 결과가 나올 수 있다.

```
gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS ) REPEATABLE ( 1 );

COUNT(*)
--------
   99756

1 row selected.

gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS ) REPEATABLE ( 1 );

COUNT(*)
--------
   99756

1 row selected.

gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS ) REPEATABLE ( 2 );

COUNT(*)
--------
  100361

1 row selected.
```

<a id="0fbca9eee5e4f202"></a>
#### 사용 예

다음은 &lt;sample clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT COUNT(*) FROM t1 TABLESAMPLE( 10 PERCENT ROWS ) WHERE c1 >= c2;

COUNT(*)
--------
  100290

1 row selected.

gSQL> SELECT COUNT(*) FROM t1 A TABLESAMPLE( 1 PERCENT ROWS ), t1 B TABLESAMPLE( 2 PERCENT ROWS ) WHERE A.c1 = B.c1;

COUNT(*)
--------
 2012379

1 row selected.
```

<a id="b5b152654467c513"></a>
#### 호환성

**SQL 표준 호환성**

<a id="927fa9ed2f94ddc4"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T613 | Sampling | O |

<a id="ed4cb025d685edfb"></a>
#### 참조

관련 내용은 [query specification](#7ad631319ea8ccd2) 을 참조한다.

<a id="74a33d522dd6bfcc"></a>
### where clause

<a id="801466ffecbf127f"></a>
#### 기능

&lt;from clause&gt; 결과에 &lt;search condition&gt;을 적용한다.

<a id="7d2615944c4d51a0"></a>
#### 구문

```
<where clause> ::=
    WHERE <search condition>
```

<a id="75bfe75ec78de204"></a>
#### 구문 규칙 및 파라미터

<a id="5f040690a2ef1054"></a>
##### &lt;where clause&gt;

WHERE 키워드 뒤에는 boolean type을 반환하는 &lt;search condition&gt;이 와야 한다.

<a id="0124407d534eb272"></a>
#### 설명

&lt;where clause&gt;에 대한 자세한 내용은 [Conditions](11-sql-elements.md#15df5544af4a1a35)을 참고한다.

<a id="082ca84479cd3b69"></a>
#### 사용 예

다음은 &lt;where clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT s_name, s_nation FROM supplier WHERE s_nation = 'KOREA';

S_NAME                    S_NATION
------------------------- --------
Supplier#2                KOREA

1 row selected.

gSQL> SELECT s_name, ps_availqty, ps_supplycost FROM supplier, partsupp WHERE s_nation = 'KOREA' AND s_suppkey = ps_suppkey;

S_NAME                    PS_AVAILQTY PS_SUPPLYCOST
------------------------- ----------- -------------
Supplier#2                       8076        993.49
Supplier#2                       4069        357.84

2 rows selected.
```

<a id="3aca4379eb1a5f57"></a>
#### 호환성

**SQL 표준 호환성**

<a id="b10a92f1afac1206"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F441 | Extended set function support | O |

<a id="261a19827f77c3e3"></a>
#### 참조

관련 내용은 [query specification](#7ad631319ea8ccd2) 을 참조한다.

<a id="263f6cdbec620b99"></a>
### hierarchical query clause

<a id="e70ce4e9fda91846"></a>
#### 기능

계층 모델 데이터를 계층 구조로 검색하도록 기술한다.   
시작 조건과 하위 연결 조건을 이용하여 테이블의 레코드들을 depth-first 순서의 계층 구조로 반환한다.

<a id="3ee3ece3f62bf32e"></a>
#### 구문

```
<hierarchical query clause> ::= 
    <start with connect by clause> [ <order siblings by clause> ]

<start with connect by clause> ::= 
    <start with clause> <connect by clause>
    | <connect by clause> <start with clause>
    | <connect by clause>

<start with clause> ::=
    START WITH <start_with_condition>

<connect by clause> ::=
    CONNECT BY [NOCYCLE] <connect_by_condition>

<order siblings by clause> ::=
    ORDER SIBLINGS BY <ordering element> [ { <comma> <ordering element> }... ]

<ordering element> ::=
    <value expression> [ASC | DESC] [NULLS FIRST | NULLS LAST]

<hierarchy expression> ::=
    LEVEL
    | CONNECT_BY_ISCYCLE
    | CONNECT_BY_ISLEAF
    | PRIOR <value expression>
    | CONNECT_BY_ROOT <value expression>
    | SYS_CONNECT_BY_PATH <left paren> <value expression> <comma> <character string literal> <right paren>
```

<a id="df9bf53b35b3f36a"></a>
#### 사용 범위 및 접근 권한

&lt;query specification&gt; 구문에서 지원되며, 이를 수행하기 위해 사용자는 &lt;query specification&gt;의 접근 권한을 만족해야 한다.  
자세한 내용은 [query specification](#7ad631319ea8ccd2) 을 참조한다.

<a id="0af876885a17b1e8"></a>
#### 구문 규칙 및 파라미터

<a id="a54f278e6080e3ad"></a>
##### &lt;hierarchical query clause&gt;

&lt;connect by clause&gt;는 반드시 기술되어야  한다.   
&lt;start with clause&gt;나 &lt;order siblings by clause&gt;는 필요한 경우 기술한다.

<a id="ec7a4bc7e7b416ca"></a>
##### &lt;start with clause&gt;

데이터 계층에서 root (최상위) 레코드의 조건을 기술한다.  
기술되지 않았을 경우는 from 절의 모든 레코드가 root 레코드 대상이 된다.  
SELECT 구문 내에서 한 번만 기술할 수 있다.

<a id="62086f327456f092"></a>
##### &lt;connect by clause&gt;

상위 (parent) 레코드와 하위 (child) 레코드의 관계를 기술한다.  
상위 레코드의 column 값을 나타내는 PRIOR operator를 이용하여 상위 레코드와 하위 레코드의 관계를 표현한다.   
PRIOR operator로 상위 레코드와 하위 레코드의 연결 조건을 기술하지 않을 경우, 무한루프가 발생할 수 있다.  
SELECT 구문 내에서 한 번만 기술할 수 있다.

- NOCYCLE
    - NOCYCLE 옵션이 기술되지 않은 경우
        - Cycle이 발생했을 때 해당 질의는 error를 발생시키고 실행이 중단된다.
    - NOCYCLE 옵션을 기술한 경우
        - Cycle이 발생했을 때 해당 질의는 에러를 내지 않는다.
        - Cycle을 유발한 레코드는 하위 레코드 검색을 멈추고 결과 레코드에도 포함되지 않는다.
        - Cycle이 발생하지 않은 형제행들에 대해서는 질의가 계속 수행된다.
        - Cycle을 유발한 레코드의 상위 레코드의 CONNECT_BY_ISCYCLE에는 1이 저장된다.
        - Cycle이 발생하지 않은 레코드의 상위 레코드에는 CONNECT_BY_ISCYCLE에 0이 저장된다.

<a id="b9883d5a00322ab5"></a>
##### &lt;order siblings by clause&gt;

같은 상위 (parent) 레코드를 가지는 형제 (sibling) 레코드들 간의 fetch 순서를 지정한다.

- 정렬순서 
    - ASC 
    - DESC
    - 명시하지 않은 경우, 기본값은 ASC 이다.

- Null ordering
    - NULLS FIRST 
    - NULLS LAST
    - 명시하지 않은 경우, 기본값은 NULLS LAST 이다.

<a id="ed8585a1971ef7e1"></a>
##### &lt;hierarchy expression&gt;

- Hierarchy query를 구성할 경우 다음과 같은 hierarchy 정보를 획득할 수 있다. 
    - LEVEL
    - CONNECT_BY_ISCYCLE
    - CONNECT_BY_ISLEAF
    - PRIOR
    - CONNECT_BY_ROOT
    - SYS_CONNECT_BY_PATH

**&lt;hierarchy expression&gt;의 결과 타입**

<a id="c904eb186ae4dac6"></a>
| Expression | Result DataType |
| --- | --- |
| LEVEL | NATIVE_BIGINT |
| CONNECT_BY_ISCYCLE | NATIVE_BIGINT |
| CONNECT_BY_ISLEAF | NATIVE_BIGINT |
| PRIOR expr | expr의 DataType |
| CONNECT_BY_ROOT expr | expr의 DataType |
| SYS_CONNECT_BY_PATH( expr, literal ) | VARCHAR(4000 characters) |

&lt;hierarchy expression&gt;을 기술할 수 있는 구문은 다음과 같다.

<a id="f2303aebe82f7732"></a>
| Expression\clause | FROM | START WITH | CONNECT BY | ORDER SIBLINGS BY | WHERE/ GROUP BY/ HAVING | ORDER BY/ SELECT TARGET |
| --- | --- | --- | --- | --- | --- | --- |
| LEVEL | X | O | O | X | O | O |
| CONNECT_BY_ISCYCLE | X | X | X | X | O | O |
| CONNECT_BY_ISLEAF | X | X | X | X | O | O |
| PRIOR | X | X | O | X | O | O |
| CONNECT_BY_ROOT | X | X | X | X | O | O |
| SYS_CONNECT_BY_PATH | X | X | X | X | O | O |

&lt;hierarchy expression&gt;의 인자로 &lt;hierarchy expression&gt;을 사용할 수 있는지 여부는 다음과 같다.

<a id="d48669f997eafb6c"></a>
| Expression\Argument(expr) | LEVEL | CONNECT_BY_ISCYCLE | CONNECT_BY_ISLEAF | PRIOR | CONNECT_BY_ROOT | SYS_CONNECT_BY_PARTH |
| --- | --- | --- | --- | --- | --- | --- |
| PRIOR expr | X | X | X | X | X | X |
| CONNECT_BY_ROOT expr | X | X | X | X | X | X |
| SYS_CONNECT_BY_PARTH(expr,literal) | O | O | O | O | O | O |

<a id="0d03d2557872511e"></a>
#### 설명

&lt;hierarchical query clause&gt;는 계층 모델 데이터를 계층 구조로 검색하는 구문이다.   
시작 조건과 하위 연결 조건을 이용하여 테이블의 레코드들을 depth-first 순서의 계층 구조로 반환한다.

SELECT에 &lt;hierarchical query clause&gt;를 기술한 경우 다음과 같은 순서로 처리된다.

1. FROM 절의 ON 조건
2. START WITH
3. CONNECT BY
4. WHERE

- From 절에 단일 테이블만 존재하는 경우

```
SELECT *
 FROM r_region
WHERE r_population > 10000000             ❸ WHERE 절의 조건
START WITH r_name = 'EARTH'               ❶ START WITH
CONNECT BY r_domain = PRIOR r_name        ❷ CONNECT BY
```

- From 절에 여러 개의 테이블들로 구성된 join 조건이 존재하는 경우

    - Join 조건을 FROM 절의 ON 절에 기술한 경우

```
SELECT *
  FROM r_region INNER JOIN s_region 
       ON r_id = s_id                      ❶ ON 절의 join 조건
 WHERE r_population > 10000000             ❹ WHERE 절의 조건
START WITH r_name = 'EARTH'                ❷ START WITH
CONNECT BY r_domain = PRIOR r_name         ❸ CONNECT BY
```

    - Join 조건을 WHERE 절에 기술한 경우

```
SELECT *
  FROM r_region, s_region
 WHERE r_population > 10000000             ❸ WHERE 절의 조건
   AND r_id = s_id                         ❸ WHERE 절의 join 조건
START WITH r_name = 'EARTH'                ❶ START WITH
CONNECT BY r_domain = PRIOR r_name         ❷ CONNECT BY
```

    - Join 조건을 FROM의 ON 절과 WHERE 절에 모두 기술한 경우

```
SELECT *
  FROM r_region INNER JOIN s_region
       ON r_name = s_name                   ❶ ON 절의 join 조건
 WHERE r_population > 10000000              ❹ WHERE 절의 조건
   AND r_id = s_id                          ❹ WHERE 절의 join 조건
START WITH r_name = 'EARTH'                 ❷ START WITH
CONNECT BY r_domain = PRIOR r_name          ❸ CONNECT BY
```

<a id="680492d1de680c74"></a>
##### &lt;order siblings by clause&gt;

&lt;hierarchical query clause&gt; 내에서 같은 상위 (parent) 레코드를 가지는 형제 (sibling) 레코드들간의 fetch 순서를 지정한다.  
&lt;order siblings by clause&gt;는 &lt;order by clause&gt;와는 별개의 구문이다.

```
gSQL> 
SELECT * FROM t1;

I1  I2
--- ----
A   null
AA  A   
AB  A   
fAA AA  
eAA AA  
bAA AA  
dAB AB  
cAB AB  
aAB AB  

9 rows selected.
```

- 다음은 같은 상위 레코드를 가지는 형제 레코드들간의 fetch 순서를 지정하는 예이다.

```
gSQL> 
SELECT LEVEL, i1, i2
  FROM t1
START WITH i1 = 'A' 
CONNECT BY i2 = PRIOR i1
ORDER SIBLINGS BY i1;

LEVEL I1  I2
----- --- ----
    1 A   null
    2 AA  A   
    3 bAA AA  
    3 eAA AA  
    3 fAA AA  
    2 AB  A   
    3 aAB AB  
    3 cAB AB  
    3 dAB AB  

9 rows selected.
```

    - 다음은 계층 구조로 검색된 전체 결과에 대해 ORDER BY 절을 이용해 LEVEL 순으로 정렬하는 예이다.

```
gSQL> 
SELECT LEVEL, i1, i2
  FROM t1
START WITH i1 = 'A'
CONNECT BY i2 = PRIOR i1
ORDER SIBLINGS BY i1
ORDER BY LEVEL;

LEVEL I1  I2  
----- --- ----
    1 A   null
    2 AA  A   
    2 AB  A   
    3 bAA AA  
    3 eAA AA  
    3 fAA AA  
    3 aAB AB  
    3 cAB AB  
    3 dAB AB  

9 rows selected.
```

<a id="25aed7e538954445"></a>
##### &lt;hierarchy expression&gt;

hierarchy expression의 기능은 다음과 같다.

- PRIOR
    - 현재 레코드의 상위 레코드를 기반으로 정보를 얻는다. 
    - PRIOR는 단항 연산자이며, 단항 연산자 +,-와 같은 우선순위를 가진다.

```
gSQL>
SELECT i1, i2
  FROM t1
START WITH i1 = 'X'
CONNECT BY i2 = PRIOR i1;

I1    I2  
----- ----
X     null
XA    X   
XXA   XA  
XXXA  XXA 
XXXXA XXXA

5 rows selected.
```

- LEVEL
    - 레코드가 속한 계층 값 
    - root 레코드의 LEVEL은 1이고, root의 하위 (child) 레코드 LEVEL은 2 이다.
    - 하위 (child) 레코드로 갈수록 LEVEL이 1씩 증가한다.

```
gSQL> 
SELECT LEVEL, i1, i2
  FROM t1
START WITH i1 = 'X'
CONNECT BY i2 = prior i1;

LEVEL I1    I2  
----- ----- ----
   1 X     null
   2 XA    X   
   3 XXA   XA  
   4 XXXA  XXA 
   5 XXXXA XXXA

5 rows selected.
```

- CONNECT_BY_ISCYCLE
    - 현재 레코드와 관련된 하위 레코드들 중에 cycle을 발생시키는 레코드가 존재하는지에 대한 정보를 얻는다.
    - CONNECT BY 구문에 NOCYCLE이 있을 때만 사용할 수 있다.

```
gSQL> 
SELECT * FROM t1;

I1 I2  
-- ----
A  null
AA A   
AB A   
AC A   
AA AA  
AB AA  

6 rows selected.

gSQL> 
SELECT i1, i2, CONNECT_BY_ISCYCLE 
  FROM t1
START WITH i1 = 'A'
CONNECT BY NOCYCLE i2 = prior i1;

I1 I2   CONNECT_BY_ISCYCLE
-- ---- ------------------
A  null                  0
AA A                     1
AB AA                    0
AB A                     0
AC A                     0

5 rows selected.
```

- CONNECT_BY_ISLEAF
    - 현재 레코드와 관련된 하위 레코드가 존재하는지에 대한 정보를 얻는다.
    - 현재 레코드와 관련된 하위 레코드가 존재하지 않으면 1이 반환된다.

```
gSQL> 
SELECT i1, i2, CONNECT_BY_ISLEAF
  FROM t1
START WITH i1 = 'X'
CONNECT BY i2 = prior i1; 

I1    I2   CONNECT_BY_ISLEAF
----- ---- -----------------
X     null                 0
XA    X                    0
XXA   XA                   0
XXXA  XXA                  0
XXXXA XXXA                 1

5 rows selected.
```

- CONNECT_BY_ROOT
    - 현재 레코드의 최상위 레코드를 기반으로 정보를 얻는다.

```
gSQL> 
SELECT i1, i2, CONNECT_BY_ROOT i1
  FROM t1
START WITH i1 = 'X'
CONNECT BY i2 = prior i1;

I1    I2   CONNECT_BY_ROOT I1
----- ---- ------------------
X     null X                 
XA    X    X                 
XXA   XA   X                 
XXXA  XXA  X                 
XXXXA XXXA X                 

5 rows selected.
```

- SYS_CONNECT_BY_PATH
    - 현재 레코드의 상위 레코드를 따라 재귀적으로 탐색하며 정보를 얻는다.

```
gSQL> 
SELECT i1, i2, SYS_CONNECT_BY_PATH( i1, '/' )
  FROM t1
START WITH i1 = 'X'
CONNECT BY i2 = prior i1;

I1    I2   SYS_CONNECT_BY_PATH( I1, '/' )
----- ---- ------------------------------
X     null /X                            
XA    X    /X/XA                         
XXA   XA   /X/XA/XXA                     
XXXA  XXA  /X/XA/XXA/XXXA                
XXXXA XXXA /X/XA/XXA/XXXA/XXXXA          

5 rows selected.
```

<a id="866033e2135a91ac"></a>
#### 사용 예

다음은 hierarchical query clause 예제에 사용될 emp 테이블의 레코드 검색 결과이다.

```
gSQL> 
SELECT * FROM emp;

NAME    MGR    
------- -------
Kelly   null   
Bill    Kelly  
Jackson Kelly  
Joe     Kelly  
Scott   Bill   
Larry   Bill   
Paul    Jackson
Bill    Bill   

8 rows selected.
```

다음은 cycle이 발생하는 예이다.

```
gSQL> 
SELECT *
  FROM emp
START WITH mgr IS NULL
CONNECT BY mgr = PRIOR name
ORDER SIBLINGS BY name;

ERR-42000(16511): cycle detected while executing recursive WITH query
```

다음은 CONNECT BY NOCYCLE 구문으로 질의를 수행하는 예이다.

```
gSQL> 
SELECT *
  FROM emp
START WITH mgr IS NULL
CONNECT BY NOCYCLE mgr = PRIOR name
ORDER SIBLINGS BY name;

NAME    MGR    
------- -------
Kelly   null   
Bill    Kelly  
Larry   Bill   
Scott   Bill   
Jackson Kelly  
Paul    Jackson
Joe     Kelly  

7 rows selected.
```

다음은 hierarchy expression을 이용해 계층 구조 데이터의 정보를 조회하는 예이다.

```
gSQL> 
SELECT name, 
       mgr, 
       PRIOR name AS prior_mgr,
       LEVEL,
       CONNECT_BY_ISCYCLE AS iscycle,
       CONNECT_BY_ISLEAF AS isleaf,
       CONNECT_BY_ROOT mgr AS root_mgr,
       SYS_CONNECT_BY_PATH( mgr, '/' ) AS path
  FROM emp
START WITH mgr IS NULL
CONNECT BY NOCYCLE mgr = PRIOR name
ORDER SIBLINGS BY name;

NAME    MGR     PRIOR_MGR LEVEL ISCYCLE ISLEAF ROOT_MGR PATH           
------- ------- --------- ----- ------- ------ -------- ---------------
Kelly   null    null          1       0      0 null     /              
Bill    Kelly   Kelly         2       1      0 null     //Kelly        
Larry   Bill    Bill          3       0      1 null     //Kelly/Bill   
Scott   Bill    Bill          3       0      1 null     //Kelly/Bill   
Jackson Kelly   Kelly         2       0      0 null     //Kelly        
Paul    Jackson Jackson       3       0      1 null     //Kelly/Jackson
Joe     Kelly   Kelly         2       0      1 null     //Kelly        

7 rows selected.
```

<a id="14659507262e5348"></a>
### group by clause

<a id="2bdd5dc87257b705"></a>
#### 기능

이전 구문들이 처리한 결과에 &lt;group by clause&gt;를 적용한 grouped table을 기술한다.

<a id="38dd09a758f73779"></a>
#### 구문

```
<group by clause> ::=
    GROUP BY [<set quantifier>] <grouping element list>

<set quantifier> ::=
    ALL
    | DISTINCT

<grouping element list> ::=
    <grouping element> [ { , <grouping element> } ... ]

<grouping element> ::=
      <ordinary grouping set>
    | <rollup list>
    | <cube list>
    | <grouping sets specification>
    | <empty grouping set>

<ordinary grouping set> ::=
      <grouping column reference>
    | <left paren> <grouping column reference list> <right paren>

<grouping column reference> ::=
    <column reference>
    | <select list alias>
    | <value expression>

<grouping column reference list> ::=
    <grouping column reference> [ { , <grouping column reference> }... ]

<empty grouping set> ::=
    <left paren> <right paren>

<rollup list> ::=
    ROLLUP <left paren> <ordinary grouping set list> <right paren>

<ordinary grouping set list> ::=
    <ordinary grouping set> [ { , <ordinary grouping set> }... ]

<cube list> ::=
    CUBE <left paren> <ordinary grouping set list> <right paren>

<grouping sets specification> ::=
    GROUPING SETS <left paren> <grouping set list> <right paren>

<grouping set list> ::=
    <grouping set> [ { , <grouping set> }... ]

<grouping set> ::=
    <ordinary grouping set>
  | <rollup list>
  | <cube list>
  | <grouping sets specification>
  | <empty grouping set>
```

<a id="64a1f10eeb8f8858"></a>
#### 사용 범위 및 접근 권한

&lt;group by clause&gt;를 수행하기 위해 별도의 접근 권한이 필요한 것은 아니다.

<a id="0faac58acfc6db95"></a>
#### 구문 규칙 및 파라미터

<a id="4aa112a2942c7331"></a>
##### &lt;ordinary grouping set&gt;

하나 이상의 &lt;grouping column reference&gt;로 구성한다.  
LONG type (LONG VARCHAR, LONG VARBINARY)은 지원하지 않는다.  

• SELECT c1, sum(c2) FROM t1 GROUP BY c1;  
• SELECT sum(c1) FROM t1 GROUP BY NULL;

<a id="128dd93d9a29e468"></a>
##### &lt;empty grouping set&gt;

괄호만 사용하여 기술할 수 있다.  

• SELECT sum(c1) FROM t1 GROUP BY ();

<a id="84cb7a1b86ded62f"></a>
#### 설명

<a id="2cbab0a044057d52"></a>
##### &lt;set quantifier&gt;

ALL 또는 DISTINCT 이며, &lt;set quantifier&gt;가 지정되지 않으면 ALL을 의미한다.   
DISTINCT가 기술된 경우, 중복 정의된 그룹을 제거한다.

- GROUP BY ALL ROLLUP (a,b), ROLLUP(a,c)
    - (a,b,c)
    - (a,b)
    - (a,b)
    - (a,c)
    - (a,c)
    - (a)
    - (a)
    - (a)
    - ()
- GROUP BY DISTINCT ROLLUP (a,b), ROLLUP(a,c)
    - (a,b,c)
    - (a,b)
    - (a,c)
    - (a)
    - ()

<a id="bd06cd957ef61cc1"></a>
##### &lt;grouping element list&gt;

&lt;group by clause&gt;에 기술된 &lt;grouping element list&gt;를 하나의 GROUPING SET으로 만드는 grouping을 수행한다. GROUPING SET에 존재하는 모든 &lt;grouping element&gt;들과 값이 일치하면 동일한 group으로 처리한다.

- &lt;group by clause&gt;가 기술된 경우 &lt;select list&gt;에는 다음과 같은 표현식이 올 수 있다.
    - 상수
    - &lt;group by clause&gt;에 기술된 &lt;grouping column reference&gt;
    - &lt;group by clause&gt;에 기술된 &lt;grouping column reference&gt;가 포함된 연산식
    - &lt;group by clause&gt;에 기술되어 있지 않은 column의 집계 함수
    - SELECT c1, sum(c2) FROM t1 GROUP BY c1;

<a id="7fcef7a616a416f0"></a>
##### &lt;ordinary grouping set&gt;

&lt;ordinary grouping set&gt;에는 &lt;grouping column reference&gt; 또는 &lt;left paren&gt;&lt;grouping column reference list&gt;&lt;right paren&gt;이 올 수 있다.

&lt;group column reference list&gt;는 &lt;grouping column reference&gt;의 list 이며, &lt;grouping column reference&gt;에는 &lt;column reference&gt; 또는 &lt;value expression&gt;이 올 수 있다.

- &lt;column reference&gt;
    - &lt;query specification&gt;의 &lt;from clause&gt;에 속하는 column들만 참조할 수 있다.
        - SELECT c1 FROM t1 GROUP BY c1;
    - 동일한 column 이름이 존재하는 경우 table 이름 등을 사용하여 column 이름을 명확하게 기술하여야 한다.
        - SELECT t1.c1, t2.c1 FROM t1, t2 GROUP BY t1.c1, t2.c1;

- &lt;select list alias&gt;
    - &lt;select list&gt;에 포함된 &lt;derived column&gt;의 &lt;as clause&gt;에 명시된 &lt;column name&gt;만 참조할 수 있다.
        - SELECT COUNT(*), t1.c1 AS A1 FROM t1 GROUP BY A1;
    - 동일한 &lt;column name&gt; 이름이 여러 개 존재하는 경우에는 &lt;select list alias&gt;를 명확히 식별할 수 없다.
        - (X) SELECT t1.c1 AS A1, t1.c2 AS A1 FROM t1 GROUP BY A1;
    - 동일한 이름의 &lt;column reference&gt;와 &lt;select list alias&gt;가 하나씩 존재하는 경우, &lt;grouping column reference&gt;은 &lt;column reference&gt;를 의미한다.
        - SELECT t1.c1, t1.c1 AS c1 FROM t1 GROUP BY c1;
        - 상위 질의는 하위 질의와 동일하다.
        - SELECT t1.c1, t1.c1 AS c1 FROM t1 GROUP BY t1.c1;

- &lt;value expression&gt;
    - &lt;column reference&gt;를 포함하는 expression 이다.
        - &lt;column reference&gt;를 사용하여 여러 group으로 구분할 수 있다.
        - SELECT sum(c2) FROM t1 GROUP BY c1 + 10;
    - &lt;column reference&gt;를 포함하지 않는 expression 이다.
        - &lt;value expression&gt;의 값이 모두 동일한 상수값이기 때문에 모든 레코드가 단일 group으로 구성된다.
        - &lt;value expression&gt;에 null 값을 기술할 경우, null 값들은 동일한 값으로 취급되어 모든 레코드가 단일 group으로 구성된다.
        - SELECT sum(c1), sum(c2) FROM t1 GROUP BY NULL;

<a id="43b29e866857c790"></a>
##### &lt;rollup list&gt;

ROLLUP 구문은 &lt;ordinary grouping set list&gt;와 함께 사용된다. &lt;ordinary grouping set list&gt;에 나열된   &lt;ordinary grouping set&gt; 개수가 n개일 경우, &lt;ordinary grouping set&gt;를 n개로 grouping 한 후, &lt;ordinary grouping set&gt;를 n-1개로 grouping 하고 그 다음은  n-2개로 grouping 하는 식으로 계속 grouping 하다가 마지막에는 &lt;empty grouping sets&gt;로 grouping 한 결과를 반환한다.   
따라서 총 ( n + 1 )개의 그룹이 생성된다.   
SUM과 함께 사용하는 경우, ROLLUP은 가장 세부적인 수준의 부분 합부터 총합까지 구할 수 있게 된다.

<a id="8d7e3bba13bafeed"></a>
##### &lt;cube list&gt;

CUBE 구문은 &lt;ordinary grouping set list&gt;와 함께 사용된다. &lt;ordinary grouping set&gt;을 모든 조합으로 grouping 한다. &lt;ordinary grouping set&gt; 개수가 n개 일 경우 총 2<sup>n</sup> 개의 그룹이 생성된다.

<a id="c45b535de264719a"></a>
##### &lt;grouping sets specification&gt;

GROUPING SETS는 필요한 그룹의 조합을 모두 명시할 수 있다. ROLLUP 이나 CUBE는 각 구문에 맞게 그룹의 조합을 구한다. 그러나 GROUPING SETS는 필요한 그룹의 조합만 선택할 수 있다.

<a id="23f5114f9ded6083"></a>
##### &lt;empty grouping set&gt;

&lt;empty grouping set&gt;의 모든 레코드는 단일 group으로 구성된다.  
• SELECT sum(c1), sum(c2) FROM t1 GROUP BY ();

<a id="168ce7b89c645868"></a>
#### 사용 예

다음은 GROUP BY를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_nation, COUNT(c_name) FROM customer GROUP BY c_nation;

C_NATION      COUNT(C_NAME)
------------- -------------
UNITED STATES             1
CANADA                    1
KOREA                     2
GERMANY                   1

4 rows selected.

gSQL> SELECT COUNT(c_name) FROM customer GROUP BY NULL;

COUNT(C_NAME)
-------------
            5

1 row selected.

gSQL> SELECT COUNT(c_name) FROM customer GROUP BY ();

COUNT(C_NAME)
-------------
            5

1 row selected.
```

다음은 grouping key로 &lt;select list alias&gt;를 사용한 예이다.

```
gSQL> SELECT o_orderdate || ' : ' || o_custkey AS date_cust, COUNT(*) 
        FROM orders 
       GROUP BY date_cust 
      HAVING COUNT(*) > 2;


DATE_CUST           COUNT(*)
------------------- --------
1995-06-22 : 114637        3
1994-09-22 : 61855         3
1994-10-26 : 90070         3
1992-09-10 : 108091        3
1992-12-24 : 131530        3
1995-05-12 : 64672         3
1997-09-20 : 8098          3
1997-04-29 : 22942         3
1992-05-31 : 130456        3
1993-04-15 : 10405         3
1992-02-21 : 11939         3
1996-03-31 : 98120         3

12 rows selected.
```

다음은 GROUP BY ROLLUP을 사용한 SELECT 구문의 예이다.

```
SELECT 
       calendar_year as year 
     , calendar_quarter_desc as quarter
     , calendar_month_desc as month
     , SUM(amount_sold) as sum 
  FROM sales, times
 WHERE sales.time_id=times.time_id 
   AND times.calendar_year = 2001
   AND sales.cust_id < 1000 AND sales.prod_id > 142 AND sales.channel_id > 2
 GROUP BY ROLLUP(calendar_year, calendar_quarter_desc, calendar_month_desc)
 ORDER BY 1, 2, 3;

YEAR QUARTER MONTH        SUM
---- ------- ------- --------
2001 2001-01 2001-01  1631.26
2001 2001-01 2001-02   922.03
2001 2001-01 2001-03  1625.59
2001 2001-01 null     4178.88
2001 2001-02 2001-04  2087.83
2001 2001-02 2001-05  1168.99
2001 2001-02 2001-06  1778.76
2001 2001-02 null     5035.58
2001 2001-03 2001-07  1604.74
2001 2001-03 2001-08  1841.42
2001 2001-03 2001-09  1953.56
2001 2001-03 null     5399.72
2001 2001-04 2001-10  2117.61
2001 2001-04 2001-11  1862.95
2001 2001-04 2001-12  1880.53
2001 2001-04 null     5861.09
2001 null    null    20475.27
null null    null    20475.27
```

다음은 GROUP BY CUBE를 사용한 SELECT 구문의 예이다.

```
\EXPLAIN PLAN
SELECT 
       channels.channel_desc as channel 
     , countries.country_iso_code as country
     , SUM(amount_sold) as sold_sum
  FROM sales, customers, times, channels, countries
 WHERE sales.time_id = times.time_id 
   AND sales.cust_id = customers.cust_id 
   AND sales.channel_id = channels.channel_id 
   AND customers.country_id = countries.country_id
   AND channels.channel_desc IN ('Direct Sales', 'Internet')
   AND times.calendar_month_desc ='2001-09'
   AND countries.country_iso_code IN ('US','FR')
   AND sales.cust_id < 1000 AND sales.prod_id > 142 AND sales.channel_id > 2
   AND customers.cust_id < 1000
 GROUP BY CUBE(channels.channel_desc, countries.country_iso_code)
 ORDER BY 1,2;

CHANNEL      COUNTRY SOLD_SUM
------------ ------- --------
Direct Sales FR         59.91
Direct Sales US        662.47
Direct Sales null      722.38
Internet     FR         29.62
Internet     US        382.56
Internet     null      412.18
null         FR         89.53
null         US       1045.03
null         null     1134.56

9 rows selected.
```

다음은 GROUP BY GROUPING SETS를 사용한 SELECT 구문의 예이다.

```
\EXPLAIN PLAN
SELECT 
       calendar_year as year 
     , calendar_quarter_desc as quarter
     , calendar_month_desc as month
     , SUM(amount_sold) as sum 
  FROM sales, times
 WHERE sales.time_id=times.time_id 
   AND times.calendar_year = 2001
   AND sales.cust_id < 1000 AND sales.prod_id > 142 AND sales.channel_id > 2
 GROUP BY GROUPING SETS( (calendar_year, calendar_quarter_desc, calendar_month_desc),
                         (calendar_year),
                                ()
                              )
 ORDER BY 1, 2, 3;  

YEAR QUARTER MONTH        SUM
---- ------- ------- --------
2001 2001-01 2001-01  1631.26
2001 2001-01 2001-02   922.03
2001 2001-01 2001-03  1625.59
2001 2001-02 2001-04  2087.83
2001 2001-02 2001-05  1168.99
2001 2001-02 2001-06  1778.76
2001 2001-03 2001-07  1604.74
2001 2001-03 2001-08  1841.42
2001 2001-03 2001-09  1953.56
2001 2001-04 2001-10  2117.61
2001 2001-04 2001-11  1862.95
2001 2001-04 2001-12  1880.53
2001 null    null    20475.27
null null    null    20475.27

14 rows selected.
```

<a id="6e5c9e2785028b07"></a>
#### 호환성

**SQL 표준 호환성**

<a id="69279b9103cab9c8"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T431 | Extended grouping capabilities | O |
| T432 | Nested and concatenated GROUPING SETS | O |
| T434 | GROUP BY DISTINCT | O |

<a id="ad3f5db32ef0f10d"></a>
#### 참조

관련 내용은 다음을 참조한다.

- [having clause](#e8e681b7980f3e0f)
- [query specification](#7ad631319ea8ccd2)

<a id="e8e681b7980f3e0f"></a>
### having clause

<a id="249476871e231a40"></a>
#### 기능

&lt;search condition&gt;을 만족하지 않는 group을 제거한 grouped table을 기술한다.

<a id="7ed067622268f8fd"></a>
#### 구문

```
<having clause> ::=
    HAVING <search condition>
```

<a id="c2d1a151b9485295"></a>
#### 사용 범위 및 접근 권한

&lt;having clause&gt;를 수행하기 위해 별도의 접근 권한이 필요한 것은 아니다.

<a id="4c699c9c761ee7f0"></a>
#### 구문 규칙 및 파라미터

<a id="421fc214ef77df02"></a>
##### &lt;having clause&gt;

- &lt;grouping column reference&gt;의 &lt;select list alias&gt;는 &lt;having clause&gt;에서 참조할 수 없다.
    - (X) SELECT c1, count(c2) AS A1 FROM t1 GROUP BY c1 HAVING A1 > 3;
- &lt;group by clause&gt;에 기술된 &lt;grouping column reference&gt;만 &lt;search condition&gt;에 집계 함수 없이 사용할 수 있다.
    - SELECT c1, sum(c2) FROM t1 GROUP BY c1 HAVING c1 > 3;
- &lt;group by clause&gt;에 기술되지 않은 column은 집계 함수를 사용하여 기술할 수 있다.
    - SELECT c1, sum(c2) FROM t1 GROUP BY c1 HAVING sum(c2) > 100;

<a id="0357583618392a50"></a>
#### 설명

<a id="def67fd594039c50"></a>
##### &lt;having clause&gt;

&lt;having clause&gt;는 grouping 된 데이터들에 대한 검색 조건을 기술한다.

일반적으로 &lt;group by clause&gt;와 함께 사용되며, &lt;group by clause&gt; 없이 &lt;having clause&gt;를 사용할 경우에는 &lt;empty grouping set&gt;이 있는 것으로 간주한다.

- SELECT sum(c1), sum(c2) FROM t1 HAVING sum(c1) > 0;
- &lt;=&gt; SELECT sum(c1), sum(c2) FROM t1 GROUP BY () HAVING sum(c1) > 0;

&lt;having clause&gt;에는 &lt;group by clause&gt;에 기술된 &lt;column reference&gt;를 기술할 수 있다.  
&lt;group by clause&gt;에 기술되지 않은 column은 집계 함수를 사용하여 기술할 수 있다.

- SELECT c1, sum(c2) FROM t1 GROUP BY c1 HAVING c1 > 3 AND sum(c2) > 100;

<a id="83306b2d806b6567"></a>
#### 사용 예

다음은 &lt;having clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_nation, COUNT(c_name) FROM customer GROUP BY c_nation HAVING COUNT(c_name) > 1;

C_NATION COUNT(C_NAME)
-------- -------------
KOREA                2

1 row selected.

gSQL> SELECT COUNT(c_name) FROM customer HAVING COUNT(c_name) > 1;

COUNT(C_NAME)
-------------
            5

1 row selected.
```

<a id="f5a7abea3b2870da"></a>
#### 호환성

**SQL 표준 호환성**

<a id="37cf827001931d0b"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T301 | Functional dependencies | O |

<a id="8dabf421a0c448e9"></a>
#### 참조

관련 내용은 다음을 참조한다.

- [group by clause](#14659507262e5348)
- [Conditions](11-sql-elements.md#15df5544af4a1a35)

<a id="f9eea6d4ba5feccc"></a>
### window clause

<a id="01769086c1cb32f7"></a>
#### 기능

select list와 order by clause에 기술된 window function의 수행 범위를 정의한다.

<a id="b8c0b6698c1680f5"></a>
#### 구문

```
<window clause> ::=
     WINDOW <window definition list>

<window definition list> ::=
     <window definition> [ { <comma> <window definition> }... ]

<window definition> ::=
     <new window name> AS <window specification>

<new window name> ::=
     <window name>

<window specification> ::=
     <left paren> <window specification details> <right paren>

<window specification details> ::=
     [ <existing window name> ]
          [ <window partition clause> ]
          [ <window order clause> ]
          [ <window frame clause> ]

<existing window name> ::=
     <window name>

<window partition clause> ::=
     PARTITION BY <window partition column reference list>

<window partition column reference list> ::=
     <window partition column reference>
          [ { <comma> <window partition column reference> }... ]

<window partition column reference> ::=
     <column reference>

<window order clause> ::=
     ORDER BY <sort specification list>

<sort specification list> ::=
     <sort specification> [ { <comma> <sort specification> }... ]

<sort specification> ::=
     <sort key> [ <ordering specification> ] [ <null ordering> ]

<sort key> ::=
     <value expression>

<ordering specification> ::=
       ASC
     | DESC

<null ordering> ::=
      NULLS FIRST
    | NULLS LAST

<window frame clause> ::=
     <window frame units> <window frame extent>
          [ <window frame exclusion> ]

<window frame units> ::=
       ROWS
     | RANGE
     | GROUPS

<window frame extent> ::=
       <window frame start>
     | <window frame between>

<window frame start> ::=
       UNBOUNDED PRECEDING
     | <window frame preceding>
     | CURRENT ROW

<window frame preceding> ::=
     <unsigned value specification> PRECEDING

<window frame between> ::=
     BETWEEN <window frame bound 1> AND <window frame bound 2>

<window frame bound 1> ::=
     <window frame bound>

<window frame bound 2> ::=
     <window frame bound>

<window frame bound> ::=
       <window frame start>
     | UNBOUNDED FOLLOWING
     | <window frame following>

<window frame following> ::=
     <unsigned value specification> FOLLOWING

<window frame exclusion> ::=
       EXCLUDE CURRENT ROW
     | EXCLUDE GROUP
     | EXCLUDE TIES
     | EXCLUDE NO OTHERS
```

<a id="a4603aa9de0666ca"></a>
#### 사용 범위 및 접근 권한

window clause에 column이 존재하는 경우 column에 대한 접근 권한이 있어야 한다.

<a id="c0626b284de1657f"></a>
#### 구문 규칙 및 파라미터

<a id="23bf63981fa8d982"></a>
##### &lt;window clause&gt;

window clause에는 window function을 기술할 수 없다.

<a id="b00082566019c56b"></a>
##### &lt;window definition list&gt;

여러 개의 &lt;window definition&gt;을 정의할 수 있다.

<a id="387c17cd6715e094"></a>
##### &lt;window definition&gt;

&lt;new window name&gt;으로 window function의 수행 범위를 기술한다.

&lt;new window name&gt;은 &lt;window clause&gt; 내에서 중복되지 않아야 한다.   
&lt;new window name&gt;은 window function의 over 절에서 참조될 수 있다.

```
SELECT SUM(i2) OVER w1
  FROM t1
WINDOW w1 AS ( PARTITION BY i1 ORDER BY i2 );
```

<a id="ad96b908cfa5649d"></a>
##### &lt;window specification&gt;

Window function의 수행 범위를 정의한다.

&lt;existing window name&gt;을 참조하여, 기존에 정의된 정보에 더하여 &lt;window specification&gt;을 재정의 할 수 있다.  
&lt;existing window name&gt;은 &lt;window definition list&gt;에 이미 정의된 &lt;new window name&gt;만 참조할 수 있다.

```
• window 절에서 참조

SELECT SUM(i2) OVER w2
  FROM t1
WINDOW w1 AS ( PARTITION BY i1
               ORDER BY i2 ),
       w2 AS ( w1 ROWS BETWEEN UNBOUNDED PRECEDING  <---
                           AND CURRENT ROW );

• window function의 over 절에서 참조

SELECT SUM(i2) OVER ( w1 ROWS BETWEEN UNBOUNDED PRECEDING  <---
                                  AND CURRENT ROW )
  FROM t1
WINDOW w1 AS ( PARTITION BY i1
               ORDER BY i2 );
```

&lt;existing window name&gt;을 참조하여 &lt;window specification&gt;을 재정의 할 경우

```
• 재정의 되는 부분에 <window partition clause>를 기술할 수 없다.

SELECT SUM(i2) OVER ( w1 PARTITION BY i1 )  <--- ( X )
  FROM t1
WINDOW w1 AS ( );

• <existing window name> 에 order by clause가 기술된 경우, 
  재정의 되는 부분에 order by clause를 기술할 수 없다.

SELECT SUM(i2) OVER ( w1 ORDER BY i3 ) <--- ( X )
  FROM t1
WINDOW w1 AS ( PARTITION BY i1
               ORDER BY i2 );

• <existing window name>에 window frame clause를 기술할 수 없다.

SELECT SUM(i2) OVER ( w1 )
  FROM t1
WINDOW w1 AS ( PARTITION BY i1
               ORDER BY i2
               ROWS BETWEEN UNBOUNDED PRECEDING  <--- ( X )
                        AND CURRENT ROW );
```

<a id="2c29aad870758926"></a>
##### &lt;window frame start&gt;

frame end가 생략된 경우 &lt;window frame start&gt;는 &lt;window frame start&gt; AND CURRENT ROW와 동일하다.

- UNBOUNDED PRECEDING
    - UNBOUNDED PRECEDING AND CURRENT ROW
- *offset* PRECEDING
    - *offset* PRECEDING AND CURRENT ROW
        - 3 PRECEDING AND CURRENT ROW
- CURRENT ROW
    - CURRENT ROW AND CURRENT ROW

<a id="11146ff17e007efc"></a>
##### &lt;window frame between&gt;

- frame start에 UNBOUNDED FOLLOWING를 기술할 수 없다.
    - BETWEEN *UNBOUNDED FOLLOWING* AND UNBOUNDED FOLLOWING ( X )
- frame end에 UNBOUNDED PRECEDING을 기술할 수 없다.
    - BETWEEN UNBOUNDED PRECEDING AND *UNBOUNDED PRECEDING* ( X ) 
- frame start가 CURRENT ROW인 경우, frame end에는 &lt;window frame preceding&gt;을 기술할 수 없다.
    - BETWEEN CURRENT ROW AND *1 PRECEDING* ( X )
- frame start가 &lt;window frame following&gt;인 경우, frame end에는 &lt;window frame preceding&gt; 이나 CURRENT ROW를 기술할 수 없다.
    - BETWEEN 3 FOLLOWING AND *1 PRECEDING* ( X )
    - BETWEEN 3 FOLLOWING AND *CURRENT ROW* ( X )

<a id="15f8476b852b6f7a"></a>
##### &lt;window frame following&gt; / &lt;window frame preceding&gt;

*offset* PRECEDING / *offset* FOLLOWING

- offset에 음수나 NULL을 기술할 수 없다.
    - *NULL* PRECEDING ( X )
    - *-1* PRECEDING ( X )
    - *NULL* FOLLOWING ( X )
    - *-1 *FOLLOWING ( X )

- frame unit이 RANGE 인 경우
    - window ORDER BY의 sort key가 숫자형이면 offset에 숫자형을 기술한다.
        - ORDER BY orderkey RANGE BETWEEN 3 PRECEDING AND 5 FOLLOWING 
    - window ORDER BY의 sort key가 datetime 또는 interval 타입이면 offset에 interval 타입을 기술한다.
        - ORDER BY orderdate RANGE BETWEEN INTERVAL'3'DAY PRECEDING AND INTERVAL'5'day FOLLOWING 
- frame unit이 ROWS/GROUPS인 경우 offset에 정수형 숫자를 기술한다.
    - ORDER BY orderkey ROWS BETWEEN 3 PRECEDING AND 5 FOLLOWING 
    - ORDER BY orderkey GROUPS BETWEEN 3 PRECEDING AND 5 FOLLOWING

<a id="c6583dcae6a0446d"></a>
#### 설명

WINDOW clause는 select list와 order by clause에 기술되는 window function의 수행 범위를 기술한다.

&lt;window partition clause&gt;로 그룹을 나누고  
&lt;window order clause&gt;로 그룹 내 레코드를 정렬하며  
&lt;window frame clause&gt;로 그룹 내에 정렬된 레코드에 대해 window function의 대상이 되는 레코드 범위를 정의한다.

WINDOW clause는 FROM, WHERE, GROUP BY, HAVING 절이 수행된 후의 결과 집합에 대해 수행된다.  
쿼리에 aggregate, GROUP BY, HAVING 절을 사용할 경우, WINDOW 절에는 원래 테이블의 column 대신 그룹 column을 기술해야 한다.

<a id="a82e99281f41e2a4"></a>
##### &lt;window specification&gt;

각 레코드에 대한 window function의 수행 범위를 기술한다.

&lt;existing window name&gt;을 참조하여, 기존에 정의된 정보에 더하여 &lt;window specification&gt;을 재정의 할 수 있다.

```
SELECT SUM(i2) OVER ( w1 
                      ORDER BY i2
                      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW )
  FROM t1
WINDOW w1 AS ( PARTITION BY i1 ),
       w2 AS ( w1 ORDER BY i3 );

   → 동일한 구문이다.

SELECT SUM(i2) OVER ( PARTITION BY i1 
                      ORDER BY i2
                      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW )
  FROM t1
WINDOW w1 AS ( PARTITION BY i1 ),
       w2 AS ( PARTITION BY i1
               ORDER BY i3 );
```

Window function OVER 절에서 &lt;window name&gt; wname을 참조할 경우, OVER wname과 OVER ( wname )은 동일하지 않다.

- OVER wname

```
* wname으로 정의된 <window specification> 정보 참조

예: w1 참조
SELECT SUM(i2) OVER w1 
  FROM t1
WINDOW w1 AS ( PARTITION BY i1
               ORDER BY i2
               ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW );
```

- OVER( wname )

```
* 기존에 정의된 정보에 더하여 <window specification>을 재정의하며,
  기존 정보에 <window frame clause>를 정의할 수 없다.

예: w1 참조 
SELECT SUM(i2) OVER ( w1 ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW ) 
  FROM t1
WINDOW w1 AS ( PARTITION BY i1
               ORDER BY i2 );

예: w1 참조 ( 오류 상황 : 기존 정보에 <window frame clause>를 정의할 수 없다. )
SELECT SUM(i2) OVER ( w1 ) 
  FROM t1
WINDOW w1 AS ( PARTITION BY i1
               ORDER BY i2
               ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW );  <---
```

<a id="5a80f1536fe1be3c"></a>
##### &lt;window partition clause&gt;

PARTITION BY를 사용하여 &lt;window partition column reference list&gt;을 기반으로 쿼리 결과 집합을 그룹으로 분할한다.  
이 절을 생략하면 함수는 쿼리 결과 집합의 모든 row를 단일 그룹으로 처리한다.

- &lt;window partition clause&gt;를 기술한 경우

```
gSQL> 
SELECT orderdate,
       orderkey,
       totalprice, 
       SUM( totalprice ) OVER( PARTITION BY orderdate ) AS SUM_OVER_RESULT
FROM orders;

ORDERDATE  ORDERKEY TOTALPRICE SUM_OVER_RESULT
---------- -------- ---------- ---------------
1998-07-24     1730     204656          520630  
1998-07-24    17056     289620          520630  
1998-07-24    19937      26354          520630      partition ❶
----------------------------------------------------------------------
1998-07-25     2400     150304          368523  
1998-07-25    11204      27165          368523  
1998-07-25    11938     191054          368523      partition ❷ 
----------------------------------------------------------------------
1998-07-26    35655      13698          362691  
1998-07-26    53377     185930          362691  
1998-07-26    55010     163063          362691      partition ❸ 
----------------------------------------------------------------------

9 rows selected.
```

- &lt;window partition clause&gt;를 생략한 경우

```
gSQL> 
SELECT orderdate,
       orderkey,
       totalprice,
       SUM( totalprice ) OVER() AS SUM_OVER_RESULT 
  FROM orders;

ORDERDATE  ORDERKEY TOTALPRICE SUM_OVER_RESULT
---------- -------- ---------- ---------------
1998-07-24     1730     204656         1251844  
1998-07-24    17056     289620         1251844  
1998-07-24    19937      26354         1251844  
1998-07-25     2400     150304         1251844  
1998-07-25    11204      27165         1251844  
1998-07-25    11938     191054         1251844  
1998-07-26    35655      13698         1251844  
1998-07-26    53377     185930         1251844  
1998-07-26    55010     163063         1251844      partition ❶ 
----------------------------------------------------------------------

9 rows selected.
```

<a id="5956c4349ec94e87"></a>
##### &lt;window order clause&gt;

ORDER BY를 사용하여 &lt;sort specification list&gt;를 기반으로 파티션 내에서 데이터가 정렬되는 방식을 지정한다.

- &lt;ordering specification&gt;
    - 오름차순 또는 내림차순 정렬을 지정할 수 있다.
        - ASC
        - DESC
        - 명시하지 않은 경우, 기본값은 ASC이다.

- &lt;null ordering&gt;
    - NULL 값과 NULL이 아닌 값의 순서를 지정할 수 있다.
        - NULLS FIRST
        - NULLS LAST
        - 명시하지 않은 경우, 기본값은 NULLS LAST이다.

- &lt;window frame clause&gt;의 &lt;window frame units&gt;이 RANGE 일 때,
    - offset PRECEDING 또는 offset FOLLOWING을 기술할 경우 sort key를 하나만 지정할 수 있다.
        - ORDER BY I1 RANGE 3 PRECEDING 
        - ORDER BY I1 RANGE BETWEEN CURRENT ROW AND 3 FOLLOWING 
    - 그 외의 경우에는 sort key를 여러 개 지정할 수 있다.
        - ORDER BY I1, I2 RANGE UNBOUNDED PRECEDING 
        - ORDER BY I1, I2 RANGE CURRENT ROW 
        - ORDER BY I1, i2 RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING 
        - ORDER BY I1, i2 RANGE BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING

<a id="3eaab1f22a0f6a6d"></a>
##### &lt;window frame clause&gt;

Window function의 대상이 되는 레코드 범위인 window frame을 지정한다.

window frame은 쿼리의 각 row (current row)와 관련된 레코드 범위이다.  
window frame의 대상은 현재 파티션 내에 정렬된 레코드이다.   
window frame은 적용할 단위 (ROWS/ RANGE/ GROUPS), 시작 지점과 끝 지점, 제외할 레코드를 정의할 수 있다.

생략할 경우, RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW가 적용된다.

- RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    - 시작 지점: 파티션 시작 레코드부터
    - 끝 지점: 현재 레코드의 모든 peer 레코드까지

- peer: window ORDER BY 절의 정렬 순서가 같은 레코드

```
gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey ) AS SUM_OVER_RESULT
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE SUM_OVER_RESULT
---------- ----- ------- ---------- ---------------
2000-01-01   101 3088161     180000          180000
2000-01-01   102 3088163      42000          269000   <- peer ( custkey 값 동일 )
2000-01-01   103 3088163      47000          269000      peer
2000-01-01   104 3088165     217000          486000
2000-01-01   105 3088167     108000          734000   <- peer ( custkey 값 동일 )
2000-01-01   106 3088167      60000          734000      peer
2000-01-01   107 3088167      80000          734000      peer
...
15 rows selected.
```

- &lt;window frame clause&gt;를 생략할 경우

```
gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶     180000 ❶ 
2000-01-01   102 3088163      42000 ❷     269000 ❶+❷+❸
2000-01-01   103 3088163      47000 ❸     269000 ❶+❷+❸
2000-01-01   104 3088165     217000 ❹     486000 ❶+❷+❸+❹ 
2000-01-01   105 3088167     108000 ❺     734000 ❶+❷+❸+❹+❺+❻+❼
2000-01-01   106 3088167      60000 ❻     734000 ❶+❷+❸+❹+❺+❻+❼
2000-01-01   107 3088167      80000 ❼     734000 ❶+❷+❸+❹+❺+❻+❼
2000-01-01   108 3088169      32000 ❽     766000 ❶+❷+❸+❹+❺+❻+❼+❽ 
2000-01-01   109 3088170      30000 ❾     816000 ❶+❷+❸+❹+❺+❻+❼+❽+❾+❿
2000-01-01   110 3088170      20000 ❿     816000 ❶+❷+❸+❹+❺+❻+❼+❽+❾+❿
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶     222000 ❶+❷
2000-03-03   302 3088161      42000 ❷     222000 ❶+❷
2000-03-03   303 3088165      47000 ❸     269000 ❶+❷+❸
2000-03-03   304 3088167     217000 ❹     594000 ❶+❷+❸+❹+❺
2000-03-03   305 3088167     108000 ❺     594000 ❶+❷+❸+❹+❺

15 rows selected.
```

<a id="08db939bafc66642"></a>
##### &lt;window frame units&gt;

ROWS/ RANGE/ GROUPS는 window frame을 적용하는 단위이다.

<a id="7974b5d12db88d4c"></a>
##### &lt;window frame extent&gt;

window frame start (시작 지점)와 window frame end (끝지점)을 정의한다.

- UNBOUNDED PRECEDING
    - 파티션 시작 레코드부터
- UNBOUNDED FOLLOWING
    - 파티션 마지막 레코드까지
- CURRENT ROW
    - &lt;window frame units&gt; ROWS인 경우
        - 현재 레코드 
    - &lt;window frame units&gt; RANGE/ GROUPS인 경우
        - 현재 레코드의 모든 peer 레코드 
- offset PRECEDING/ offset FOLLOWING
    - &lt;window frame units&gt; ROWS인 경우
        - 현재 레코드 전/후 offset 레코드 개수 범위
    - &lt;window frame units&gt; GROUPS인 경우
        - 현재 레코드 group 전/후 offset group 개수 범위
    - &lt;window frame units&gt; RANGE인 경우
        - 현재 레코드 전/후 offset 값의 범위 
        - ORDER BY column을 ASC 방식으로 정렬할 경우
        - … offset PRECEDING → ( 현재 레코드의 sort key value - offset ) 이상인 value의 레코드
        - … offset FOLLOWING → ( 현재 레코드의 sort key value + offset ) 이하인 value의 레코드
        - ORDER BY column을 DESC 방식으로 정렬할 경우
        - … offset PRECEDING → ( 현재 레코드의 sort key value + offset ) 이하인 value의 레코드
        - … offset FOLLOWING → ( 현재 레코드의 sort key value - offset ) 이상인 value의 레코드
- 자세한 내용은 [&lt;window frame extent&gt; 사용 예](#3e2a97897a200bd5)를 참조한다.

<a id="042eeaf7379770ea"></a>
##### &lt;window frame exclusion&gt;

window frame에서 제외할 레코드를 정의한다.

- EXCLUDE CURRENT ROW: 현재 레코드를 제외한다.
- EXCLUDE GROUP: 현재 레코드와 모든 peer 레코드를 제외한다.
- EXCLUDE TIES: 현재 레코드는 유지하되 모든 peer 레코드는 제외한다.
- EXCLUDE NO OTHERS: 어떤 레코드도 제외하지 않는다.
- 명시하지 않은 경우, 기본값은 EXCLUDE NO OTHERS 이다.
- 자세한 내용은 [&lt;window frame exclusion&gt; 사용 예](#726a99dd0a772e21)를 참조한다.

<a id="3e2a97897a200bd5"></a>
##### &lt;window frame extent&gt; 사용 예

- BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW

```
# ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               ROWS BETWEEN UNBOUNDED PRECEDING 
                                        AND CURRENT ROW ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶     180000 ❶ 
2000-01-01   102 3088163      42000 ❷     222000 ❶+❷ 
2000-01-01   103 3088163      47000 ❸     269000 ❶+❷+❸ 
2000-01-01   104 3088165     217000 ❹     486000 ❶+❷+❸+❹ 
2000-01-01   105 3088167     108000 ❺     594000 ❶+❷+❸+❹+❺
2000-01-01   106 3088167      60000 ❻     654000 ❶+❷+❸+❹+❺+❻ 
2000-01-01   107 3088167      80000 ❼     734000 ❶+❷+❸+❹+❺+❻+❼ 
2000-01-01   108 3088169      32000 ❽     766000 ❶+❷+❸+❹+❺+❻+❼+❽ 
2000-01-01   109 3088170      30000 ❾     796000 ❶+❷+❸+❹+❺+❻+❼+❽+❾ 
2000-01-01   110 3088170      20000 ❿     816000 ❶+❷+❸+❹+❺+❻+❼+❽+❾+❿ 
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶     180000 ❶
2000-03-03   302 3088161      42000 ❷     222000 ❶+❷
2000-03-03   303 3088165      47000 ❸     269000 ❶+❷+❸
2000-03-03   304 3088167     217000 ❹     486000 ❶+❷+❸+❹
2000-03-03   305 3088167     108000 ❺     594000 ❶+❷+❸+❹+❺

15 rows selected.
```

```
# RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               RANGE BETWEEN UNBOUNDED PRECEDING 
                                         AND CURRENT ROW ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶     180000 ❶ 
2000-01-01   102 3088163      42000 ❷     269000 ❶+❷+❸
2000-01-01   103 3088163      47000 ❸     269000 ❶+❷+❸
2000-01-01   104 3088165     217000 ❹     486000 ❶+❷+❸+❹ 
2000-01-01   105 3088167     108000 ❺     734000 ❶+❷+❸+❹+❺+❻+❼
2000-01-01   106 3088167      60000 ❻     734000 ❶+❷+❸+❹+❺+❻+❼
2000-01-01   107 3088167      80000 ❼     734000 ❶+❷+❸+❹+❺+❻+❼
2000-01-01   108 3088169      32000 ❽     766000 ❶+❷+❸+❹+❺+❻+❼+❽ 
2000-01-01   109 3088170      30000 ❾     816000 ❶+❷+❸+❹+❺+❻+❼+❽+❾+❿
2000-01-01   110 3088170      20000 ❿     816000 ❶+❷+❸+❹+❺+❻+❼+❽+❾+❿
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶     222000 ❶+❷
2000-03-03   302 3088161      42000 ❷     222000 ❶+❷
2000-03-03   303 3088165      47000 ❸     269000 ❶+❷+❸
2000-03-03   304 3088167     217000 ❹     594000 ❶+❷+❸+❹+❺
2000-03-03   305 3088167     108000 ❺     594000 ❶+❷+❸+❹+❺

15 rows selected.
```

```
# GROUPS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               GROUPS BETWEEN UNBOUNDED PRECEDING 
                                          AND CURRENT ROW ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶     180000 ❶ 
2000-01-01   102 3088163      42000 ❷     269000 ❶+❷+❸
2000-01-01   103 3088163      47000 ❸     269000 ❶+❷+❸
2000-01-01   104 3088165     217000 ❹     486000 ❶+❷+❸+❹ 
2000-01-01   105 3088167     108000 ❺     734000 ❶+❷+❸+❹+❺+❻+❼
2000-01-01   106 3088167      60000 ❻     734000 ❶+❷+❸+❹+❺+❻+❼
2000-01-01   107 3088167      80000 ❼     734000 ❶+❷+❸+❹+❺+❻+❼
2000-01-01   108 3088169      32000 ❽     766000 ❶+❷+❸+❹+❺+❻+❼+❽ 
2000-01-01   109 3088170      30000 ❾     816000 ❶+❷+❸+❹+❺+❻+❼+❽+❾+❿
2000-01-01   110 3088170      20000 ❿     816000 ❶+❷+❸+❹+❺+❻+❼+❽+❾+❿
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶     222000 ❶+❷
2000-03-03   302 3088161      42000 ❷     222000 ❶+❷
2000-03-03   303 3088165      47000 ❸     269000 ❶+❷+❸
2000-03-03   304 3088167     217000 ❹     594000 ❶+❷+❸+❹+❺
2000-03-03   305 3088167     108000 ❺     594000 ❶+❷+❸+❹+❺

15 rows selected.
```

- BETWEEN offset PRECEDING AND offset FOLLOWING

```
# ROWS BETWEEN 1 PRECEDING AND 2 FOLLOWING

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               ROWS BETWEEN 1 PRECEDING 
                                        AND 2 FOLLOWING ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶     269000 ❶+❷+❸ 
2000-01-01   102 3088163      42000 ❷     486000 ❶+❷+❸+❹ 
2000-01-01   103 3088163      47000 ❸     414000 ❷+❸+❹+❺ 
2000-01-01   104 3088165     217000 ❹     432000 ❸+❹+❺+❻ 
2000-01-01   105 3088167     108000 ❺     465000 ❹+❺+❻+❼ 
2000-01-01   106 3088167      60000 ❻     280000 ❺+❻+❼+❽ 
2000-01-01   107 3088167      80000 ❼     202000 ❻+❼+❽+❾ 
2000-01-01   108 3088169      32000 ❽     162000 ❼+❽+❾+❿ 
2000-01-01   109 3088170      30000 ❾      82000 ❽+❾+❿
2000-01-01   110 3088170      20000 ❿      50000 ❾+❿
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶     269000 ❶+❷+❸ 
2000-03-03   302 3088161      42000 ❷     486000 ❶+❷+❸+❹ 
2000-03-03   303 3088165      47000 ❸     414000 ❷+❸+❹+❺ 
2000-03-03   304 3088167     217000 ❹     372000 ❸+❹+❺ 
2000-03-03   305 3088167     108000 ❺     325000 ❹+❺ 

15 rows selected.
```

```
# RANGE BETWEEN 1 PRECEDING AND 2 FOLLOWING

#####################################################
# ORDER BY column을 ASC 방식으로 정렬할 경우 
#####################################################

 • 1 PRECEDING 
   -->   ( current row의 sortkey value - 1 ) 이상인 value
       = ( custkey - 1 ) 이상인 value

 • 2 FOLLOWING
   -->   ( current row의 sortkey value + 2 ) 이하인 value
       = ( custkey + 2 ) 이하인 value

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               RANGE BETWEEN 1 PRECEDING 
                                         AND 2 FOLLOWING ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶     269000 ❶+❷+❸ 
2000-01-01   102 3088163      42000 ❷     306000 ❷+❸+❹
2000-01-01   103 3088163      47000 ❸     306000 ❷+❸+❹
2000-01-01   104 3088165     217000 ❹     465000 ❹+❺+❻+❼ 
2000-01-01   105 3088167     108000 ❺     280000 ❺+❻+❼+❽
2000-01-01   106 3088167      60000 ❻     280000 ❺+❻+❼+❽
2000-01-01   107 3088167      80000 ❼     280000 ❺+❻+❼+❽
2000-01-01   108 3088169      32000 ❽      82000 ❽+❾+❿ 
2000-01-01   109 3088170      30000 ❾      82000 ❽+❾+❿
2000-01-01   110 3088170      20000 ❿      82000 ❽+❾+❿
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶     222000 ❶+❷
2000-03-03   302 3088161      42000 ❷     222000 ❶+❷
2000-03-03   303 3088165      47000 ❸     372000 ❸+❹+❺ 
2000-03-03   304 3088167     217000 ❹     325000 ❹+❺
2000-03-03   305 3088167     108000 ❺     325000 ❹+❺

15 rows selected.


#####################################################
# ORDER BY column을 DESC 방식으로 정렬할 경우 
#####################################################

 • 1 PRECEDING 
   -->   ( current row의 sortkey value + 1 ) 이하인 value
       = ( custkey + 1 ) 이하인 value

 • 2 FOLLOWING
   -->   ( current row의 sortkey value - 2 ) 이상인 value
       = ( custkey - 2 ) 이상인 value

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey DESC
                               RANGE BETWEEN 1 PRECEDING 
                                         AND 2 FOLLOWING ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   109 3088170      30000 ❶      82000 ❶+❷+❸
2000-01-01   110 3088170      20000 ❷      82000 ❶+❷+❸
2000-01-01   108 3088169      32000 ❸     330000 ❶+❷+❸+❹+❺+❻ 
2000-01-01   105 3088167     108000 ❹     465000 ❹+❺+❻+❼
2000-01-01   106 3088167      60000 ❺     465000 ❹+❺+❻+❼
2000-01-01   107 3088167      80000 ❻     465000 ❹+❺+❻+❼
2000-01-01   104 3088165     217000 ❼     306000 ❼+❽+❾ 
2000-01-01   102 3088163      42000 ❽     269000 ❽+❾+❿
2000-01-01   103 3088163      47000 ❾     269000 ❽+❾+❿
2000-01-01   101 3088161     180000 ❿     180000 ❿ 
-------------------------------------------------------------------------
2000-03-03   304 3088167     217000 ❶     372000 ❶+❷+❸
2000-03-03   305 3088167     108000 ❷     372000 ❶+❷+❸
2000-03-03   303 3088165      47000 ❸      47000 ❸ 
2000-03-03   301 3088161     180000 ❹     222000 ❹+❺
2000-03-03   302 3088161      42000 ❺     222000 ❹+❺

15 rows selected.
```

```
# GROUPS BETWEEN 1 PRECEDING AND 2 FOLLOWING

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               GROUPS BETWEEN 1 PRECEDING 
                                          AND 2 FOLLOWING ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶     486000 ❶+❷+❸+❹ 
2000-01-01   102 3088163      42000 ❷     734000 ❶+❷+❸+❹+❺+❻+❼
2000-01-01   103 3088163      47000 ❸     734000 ❶+❷+❸+❹+❺+❻+❼
2000-01-01   104 3088165     217000 ❹     586000 ❷+❸+❹+❺+❻+❼+❽ 
2000-01-01   105 3088167     108000 ❺     547000 ❹+❺+❻+❼+❽+❾+❿
2000-01-01   106 3088167      60000 ❻     547000 ❹+❺+❻+❼+❽+❾+❿
2000-01-01   107 3088167      80000 ❼     547000 ❹+❺+❻+❼+❽+❾+❿
2000-01-01   108 3088169      32000 ❽     330000 ❺+❻+❼+❽+❾+❿ 
2000-01-01   109 3088170      30000 ❾      82000 ❽+❾+❿
2000-01-01   110 3088170      20000 ❿      82000 ❽+❾+❿
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶     594000 ❶+❷+❸+❹+❺
2000-03-03   302 3088161      42000 ❷     594000 ❶+❷+❸+❹+❺
2000-03-03   303 3088165      47000 ❸     594000 ❶+❷+❸+❹+❺ 
2000-03-03   304 3088167     217000 ❹     372000 ❸+❹+❺
2000-03-03   305 3088167     108000 ❺     372000 ❸+❹+❺

15 rows selected.
```

- BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING

```
# ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               ROWS BETWEEN CURRENT ROW 
                                        AND UNBOUNDED FOLLOWING ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE SUM_OVER_RESULT
---------- ----- ------- ---------- ---------------
2000-01-01   101 3088161     180000          816000
2000-01-01   102 3088163      42000          636000
2000-01-01   103 3088163      47000          594000
2000-01-01   104 3088165     217000          547000
2000-01-01   105 3088167     108000          330000
2000-01-01   106 3088167      60000          222000
2000-01-01   107 3088167      80000          162000
2000-01-01   108 3088169      32000           82000
2000-01-01   109 3088170      30000           50000
2000-01-01   110 3088170      20000           20000
2000-03-03   301 3088161     180000          594000
2000-03-03   302 3088161      42000          414000
2000-03-03   303 3088165      47000          372000
2000-03-03   304 3088167     217000          325000
2000-03-03   305 3088167     108000          108000

15 rows selected.
```

```
# RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               RANGE BETWEEN CURRENT ROW 
                                         AND UNBOUNDED FOLLOWING ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE SUM_OVER_RESULT
---------- ----- ------- ---------- ---------------
2000-01-01   101 3088161     180000          816000
2000-01-01   102 3088163      42000          636000
2000-01-01   103 3088163      47000          636000
2000-01-01   104 3088165     217000          547000
2000-01-01   105 3088167     108000          330000
2000-01-01   106 3088167      60000          330000
2000-01-01   107 3088167      80000          330000
2000-01-01   108 3088169      32000           82000
2000-01-01   109 3088170      30000           50000
2000-01-01   110 3088170      20000           50000
2000-03-03   301 3088161     180000          594000
2000-03-03   302 3088161      42000          594000
2000-03-03   303 3088165      47000          372000
2000-03-03   304 3088167     217000          325000
2000-03-03   305 3088167     108000          325000

15 rows selected.
```

```
# GROUPS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               GROUPS BETWEEN CURRENT ROW 
                                          AND UNBOUNDED FOLLOWING ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE SUM_OVER_RESULT
---------- ----- ------- ---------- ---------------
2000-01-01   101 3088161     180000          816000
2000-01-01   102 3088163      42000          636000
2000-01-01   103 3088163      47000          636000
2000-01-01   104 3088165     217000          547000
2000-01-01   105 3088167     108000          330000
2000-01-01   106 3088167      60000          330000
2000-01-01   107 3088167      80000          330000
2000-01-01   108 3088169      32000           82000
2000-01-01   109 3088170      30000           50000
2000-01-01   110 3088170      20000           50000
2000-03-03   301 3088161     180000          594000
2000-03-03   302 3088161      42000          594000
2000-03-03   303 3088165      47000          372000
2000-03-03   304 3088167     217000          325000
2000-03-03   305 3088167     108000          325000

15 rows selected.
```

<a id="726a99dd0a772e21"></a>
##### &lt;window frame exclusion&gt; 사용 예

- EXCLUDE CURRENT ROW

```
# ROWS

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               ROWS BETWEEN UNBOUNDED PRECEDING 
                                        AND CURRENT ROW
                               EXCLUDE CURRENT ROW ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶       null 
2000-01-01   102 3088163      42000 ❷     180000 ❶ 
2000-01-01   103 3088163      47000 ❸     222000 ❶+❷ 
2000-01-01   104 3088165     217000 ❹     269000 ❶+❷+❸ 
2000-01-01   105 3088167     108000 ❺     486000 ❶+❷+❸+❹ 
2000-01-01   106 3088167      60000 ❻     594000 ❶+❷+❸+❹+❺ 
2000-01-01   107 3088167      80000 ❼     654000 ❶+❷+❸+❹+❺+❻ 
2000-01-01   108 3088169      32000 ❽     734000 ❶+❷+❸+❹+❺+❻+❼ 
2000-01-01   109 3088170      30000 ❾     766000 ❶+❷+❸+❹+❺+❻+❼+❽ 
2000-01-01   110 3088170      20000 ❿     796000 ❶+❷+❸+❹+❺+❻+❼+❽+❾ 
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶       null
2000-03-03   302 3088161      42000 ❷     180000 ❶ 
2000-03-03   303 3088165      47000 ❸     222000 ❶+❷ 
2000-03-03   304 3088167     217000 ❹     269000 ❶+❷+❸ 
2000-03-03   305 3088167     108000 ❺     486000 ❶+❷+❸+❹ 

15 rows selected.
```

```
# RANGE

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               RANGE BETWEEN UNBOUNDED PRECEDING 
                                         AND CURRENT ROW
                               EXCLUDE CURRENT ROW ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶       null
2000-01-01   102 3088163      42000 ❷     227000 ❶+❸
2000-01-01   103 3088163      47000 ❸     222000 ❶+❷
2000-01-01   104 3088165     217000 ❹     269000 ❶+❷+❸ 
2000-01-01   105 3088167     108000 ❺     626000 ❶+❷+❸+❹+❻+❼
2000-01-01   106 3088167      60000 ❻     674000 ❶+❷+❸+❹+❺+❼
2000-01-01   107 3088167      80000 ❼     654000 ❶+❷+❸+❹+❺+❻
2000-01-01   108 3088169      32000 ❽     734000 ❶+❷+❸+❹+❺+❻+❼ 
2000-01-01   109 3088170      30000 ❾     786000 ❶+❷+❸+❹+❺+❻+❼+❽+❿
2000-01-01   110 3088170      20000 ❿     796000 ❶+❷+❸+❹+❺+❻+❼+❽+❾
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶      42000 ❷
2000-03-03   302 3088161      42000 ❷     180000 ❶
2000-03-03   303 3088165      47000 ❸     222000 ❶+❷ 
2000-03-03   304 3088167     217000 ❹     377000 ❶+❷+❸+❺
2000-03-03   305 3088167     108000 ❺     486000 ❶+❷+❸+❹

15 rows selected.
```

```
# GROUPS

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               GROUPS BETWEEN UNBOUNDED PRECEDING 
                                          AND CURRENT ROW
                               EXCLUDE CURRENT ROW ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶       null
2000-01-01   102 3088163      42000 ❷     227000 ❶+❸
2000-01-01   103 3088163      47000 ❸     222000 ❶+❷
2000-01-01   104 3088165     217000 ❹     269000 ❶+❷+❸ 
2000-01-01   105 3088167     108000 ❺     626000 ❶+❷+❸+❹+❻+❼
2000-01-01   106 3088167      60000 ❻     674000 ❶+❷+❸+❹+❺+❼
2000-01-01   107 3088167      80000 ❼     654000 ❶+❷+❸+❹+❺+❻
2000-01-01   108 3088169      32000 ❽     734000 ❶+❷+❸+❹+❺+❻+❼ 
2000-01-01   109 3088170      30000 ❾     786000 ❶+❷+❸+❹+❺+❻+❼+❽+❿
2000-01-01   110 3088170      20000 ❿     796000 ❶+❷+❸+❹+❺+❻+❼+❽+❾
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶      42000 ❷
2000-03-03   302 3088161      42000 ❷     180000 ❶
2000-03-03   303 3088165      47000 ❸     222000 ❶+❷ 
2000-03-03   304 3088167     217000 ❹     377000 ❶+❷+❸+❺
2000-03-03   305 3088167     108000 ❺     486000 ❶+❷+❸+❹

15 rows selected.
```

- EXCLUDE GROUP

```
# ROWS

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               ROWS BETWEEN UNBOUNDED PRECEDING 
                                        AND CURRENT ROW
                               EXCLUDE GROUP ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶       null
2000-01-01   102 3088163      42000 ❷     180000 ❶
2000-01-01   103 3088163      47000 ❸     180000 ❶
2000-01-01   104 3088165     217000 ❹     269000 ❶+❷+❸ 
2000-01-01   105 3088167     108000 ❺     486000 ❶+❷+❸+❹
2000-01-01   106 3088167      60000 ❻     486000 ❶+❷+❸+❹
2000-01-01   107 3088167      80000 ❼     486000 ❶+❷+❸+❹
2000-01-01   108 3088169      32000 ❽     734000 ❶+❷+❸+❹+❺+❻+❼ 
2000-01-01   109 3088170      30000 ❾     766000 ❶+❷+❸+❹+❺+❻+❼+❽
2000-01-01   110 3088170      20000 ❿     766000 ❶+❷+❸+❹+❺+❻+❼+❽
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶       null
2000-03-03   302 3088161      42000 ❷       null
2000-03-03   303 3088165      47000 ❸     222000 ❶+❷ 
2000-03-03   304 3088167     217000 ❹     269000 ❶+❷+❸
2000-03-03   305 3088167     108000 ❺     269000 ❶+❷+❸

15 rows selected.
```

```
# RANGE

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               RANGE BETWEEN UNBOUNDED PRECEDING 
                                         AND CURRENT ROW
                               EXCLUDE GROUP ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶       null
2000-01-01   102 3088163      42000 ❷     180000 ❶
2000-01-01   103 3088163      47000 ❸     180000 ❶
2000-01-01   104 3088165     217000 ❹     269000 ❶+❷+❸ 
2000-01-01   105 3088167     108000 ❺     486000 ❶+❷+❸+❹
2000-01-01   106 3088167      60000 ❻     486000 ❶+❷+❸+❹
2000-01-01   107 3088167      80000 ❼     486000 ❶+❷+❸+❹
2000-01-01   108 3088169      32000 ❽     734000 ❶+❷+❸+❹+❺+❻+❼ 
2000-01-01   109 3088170      30000 ❾     766000 ❶+❷+❸+❹+❺+❻+❼+❽
2000-01-01   110 3088170      20000 ❿     766000 ❶+❷+❸+❹+❺+❻+❼+❽
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶       null
2000-03-03   302 3088161      42000 ❷       null
2000-03-03   303 3088165      47000 ❸     222000 ❶+❷ 
2000-03-03   304 3088167     217000 ❹     269000 ❶+❷+❸
2000-03-03   305 3088167     108000 ❺     269000 ❶+❷+❸

15 rows selected.
```

```
# GROUPS

gSQL> SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               GROUPS BETWEEN UNBOUNDED PRECEDING 
                                          AND CURRENT ROW
                               EXCLUDE GROUP ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶       null
2000-01-01   102 3088163      42000 ❷     180000 ❶
2000-01-01   103 3088163      47000 ❸     180000 ❶
2000-01-01   104 3088165     217000 ❹     269000 ❶+❷+❸ 
2000-01-01   105 3088167     108000 ❺     486000 ❶+❷+❸+❹
2000-01-01   106 3088167      60000 ❻     486000 ❶+❷+❸+❹
2000-01-01   107 3088167      80000 ❼     486000 ❶+❷+❸+❹
2000-01-01   108 3088169      32000 ❽     734000 ❶+❷+❸+❹+❺+❻+❼ 
2000-01-01   109 3088170      30000 ❾     766000 ❶+❷+❸+❹+❺+❻+❼+❽
2000-01-01   110 3088170      20000 ❿     766000 ❶+❷+❸+❹+❺+❻+❼+❽
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶       null
2000-03-03   302 3088161      42000 ❷       null
2000-03-03   303 3088165      47000 ❸     222000 ❶+❷ 
2000-03-03   304 3088167     217000 ❹     269000 ❶+❷+❸
2000-03-03   305 3088167     108000 ❺     269000 ❶+❷+❸

15 rows selected.
```

- EXCLUDE TIES

```
# ROWS

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               ROWS BETWEEN UNBOUNDED PRECEDING 
                                        AND CURRENT ROW
                               EXCLUDE TIES ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶     180000 ❶ 
2000-01-01   102 3088163      42000 ❷     222000 ❶+❷
2000-01-01   103 3088163      47000 ❸     227000 ❶+❸
2000-01-01   104 3088165     217000 ❹     486000 ❶+❷+❸+❹ 
2000-01-01   105 3088167     108000 ❺     594000 ❶+❷+❸+❹+❺
2000-01-01   106 3088167      60000 ❻     546000 ❶+❷+❸+❹+❻
2000-01-01   107 3088167      80000 ❼     566000 ❶+❷+❸+❹+❼
2000-01-01   108 3088169      32000 ❽     766000 ❶+❷+❸+❹+❺+❻+❼+❽ 
2000-01-01   109 3088170      30000 ❾     796000 ❶+❷+❸+❹+❺+❻+❼+❽+❾
2000-01-01   110 3088170      20000 ❿     786000 ❶+❷+❸+❹+❺+❻+❼+❽+❿
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶     180000 ❶
2000-03-03   302 3088161      42000 ❷      42000 ❷
2000-03-03   303 3088165      47000 ❸     269000 ❶+❷+❸ 
2000-03-03   304 3088167     217000 ❹     486000 ❶+❷+❸+❹
2000-03-03   305 3088167     108000 ❺     377000 ❶+❷+❸+❺

15 rows selected.
```

```
# RANGE

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               RANGE BETWEEN UNBOUNDED PRECEDING 
                                         AND CURRENT ROW
                               EXCLUDE TIES ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶     180000 ❶ 
2000-01-01   102 3088163      42000 ❷     222000 ❶+❷
2000-01-01   103 3088163      47000 ❸     227000 ❶+❸
2000-01-01   104 3088165     217000 ❹     486000 ❶+❷+❸+❹ 
2000-01-01   105 3088167     108000 ❺     594000 ❶+❷+❸+❹+❺
2000-01-01   106 3088167      60000 ❻     546000 ❶+❷+❸+❹+❻
2000-01-01   107 3088167      80000 ❼     566000 ❶+❷+❸+❹+❼
2000-01-01   108 3088169      32000 ❽     766000 ❶+❷+❸+❹+❺+❻+❼+❽ 
2000-01-01   109 3088170      30000 ❾     796000 ❶+❷+❸+❹+❺+❻+❼+❽+❾
2000-01-01   110 3088170      20000 ❿     786000 ❶+❷+❸+❹+❺+❻+❼+❽+❿
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶     180000 ❶
2000-03-03   302 3088161      42000 ❷      42000 ❷
2000-03-03   303 3088165      47000 ❸     269000 ❶+❷+❸ 
2000-03-03   304 3088167     217000 ❹     486000 ❶+❷+❸+❹
2000-03-03   305 3088167     108000 ❺     377000 ❶+❷+❸+❺

15 rows selected.
```

```
# GROUPS

gSQL> 
SELECT orderdate AS O_DATE,
       orderkey AS O_KEY,
       custkey,
       totalprice,
       SUM( totalprice ) OVER( PARTITION BY orderdate 
                               ORDER BY custkey
                               GROUPS BETWEEN UNBOUNDED PRECEDING 
                                          AND CURRENT ROW
                               EXCLUDE TIES ) AS SUM_OVER_RESULT 
  FROM orders;

O_DATE     O_KEY CUSTKEY TOTALPRICE    SUM_OVER_RESULT
---------- ----- ------- ----------    ---------------
2000-01-01   101 3088161     180000 ❶     180000 ❶ 
2000-01-01   102 3088163      42000 ❷     222000 ❶+❷
2000-01-01   103 3088163      47000 ❸     227000 ❶+❸
2000-01-01   104 3088165     217000 ❹     486000 ❶+❷+❸+❹ 
2000-01-01   105 3088167     108000 ❺     594000 ❶+❷+❸+❹+❺
2000-01-01   106 3088167      60000 ❻     546000 ❶+❷+❸+❹+❻
2000-01-01   107 3088167      80000 ❼     566000 ❶+❷+❸+❹+❼
2000-01-01   108 3088169      32000 ❽     766000 ❶+❷+❸+❹+❺+❻+❼+❽ 
2000-01-01   109 3088170      30000 ❾     796000 ❶+❷+❸+❹+❺+❻+❼+❽+❾
2000-01-01   110 3088170      20000 ❿     786000 ❶+❷+❸+❹+❺+❻+❼+❽+❿
-------------------------------------------------------------------------
2000-03-03   301 3088161     180000 ❶     180000 ❶
2000-03-03   302 3088161      42000 ❷      42000 ❷
2000-03-03   303 3088165      47000 ❸     269000 ❶+❷+❸ 
2000-03-03   304 3088167     217000 ❹     486000 ❶+❷+❸+❹
2000-03-03   305 3088167     108000 ❺     377000 ❶+❷+❸+❺

15 rows selected.
```

<a id="9bdb5ac08435aaf5"></a>
#### 사용 예

```
gSQL> 
SELECT item_no,
       sales_date,
       sales,
       SUM( sales ) OVER W1 cumulative_sales, 
       AVG( sales ) OVER w1 avg_sales
  FROM store
WINDOW w1 AS ( PARTITION BY item_no
               ORDER BY sales_date
               ROWS BETWEEN UNBOUNDED PRECEDING
                        AND CURRENT ROW );

ITEM_NO SALES_DATE SALES CUMULATIVE_SALES AVG_SALES
------- ---------- ----- ---------------- ---------
    100 2001-01-01   150              150       150
    100 2001-01-02   100              250       125
    100 2001-01-03   170              420       140
    100 2001-01-04    90              510     127.5
    100 2001-01-05   200              710       142
    235 2001-01-01    70               70        70
    235 2001-01-02   130              200       100
    235 2001-01-03   190              390       130
    235 2001-01-04   150              540       135
    235 2001-01-05    50              590       118

10 rows selected.
```

<a id="12be7fd8b26c4eea"></a>
#### 호환성

**SQL 표준 호환성**

<a id="0e8a4ce638829314"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T611 | Elementary OLAP operations | X |
| T612 | Advanced OLAP operations | X |
| T301 | Functional dependencies | X |
| T620 | WINDOW clause: GROUPS option | O |

<a id="eef491473b2ceb46"></a>
#### 참조

관련 내용은 다음을 참조한다.

- [group by clause](#14659507262e5348)
- [order by clause](#14bc5c63df59d6ec)
- [Window Function](11-sql-elements.md#87f34e385804bc26)

<a id="14bc5c63df59d6ec"></a>
### order by clause

<a id="952f67c1dd5679ad"></a>
#### 기능

검색 결과의 정렬 순서를 기술한다.

<a id="1b9a226f6f4ca309"></a>
#### 구문

```
<order by clause> ::=
    ORDER BY <sort specification list>

<sort specification list> ::=
    <sort specification> [ { <comma> <sort specification> }... ]

<sort specification> ::=
    <sort key> [ <ordering specification> ] [ <null ordering> ]

<sort key> ::=
    <value expression>

<ordering specification> ::=
      ASC
    | DESC

<null ordering> ::=
      NULLS FIRST
    | NULLS LAST
```

<a id="dba7b0be13b7fbed"></a>
#### 사용 범위 및 접근 권한

정렬하기 위해 기술한 &lt;sort key&gt;에 column이 존재하는 경우 column에 대한 접근 권한이 있어야 한다.

<a id="639b3b7f3254a648"></a>
#### 구문 규칙 및 파라미터

<a id="7d66f9fd8ed5df3b"></a>
##### &lt;order by clause&gt;

- &lt;query specification&gt;에 &lt;set quantifier&gt; DISTINCT가 기술된 경우, &lt;sort key&gt;에는 &lt;select list&gt;에 기술된 expression만 올 수 있다.
    - SELECT DISTINCT c1, c2 FROM t1 ORDER BY c1;
    - (X) SELECT DISTINCT c1, c2 FROM t1 ORDER BY c5;
- &lt;query specification&gt;의 &lt;select list&gt;에 하나 이상의 &lt;set function specification&gt;을 기술한 경우, &lt;sort key&gt;에는 &lt;select list&gt;에 기술된 expression만 올 수 있다.
    - SELECT c1, sum(c2) FROM t1 GROUP BY c1 ORDER BY c1;
    - (X) SELECT c1, sum(c2) FROM t1 GROUP BY c1 ORDER BY c5;
- &lt;set operator&gt; 구문에 &lt;order by clause&gt;를 명시한 경우, 가장 먼저 기술된 &lt;query specification&gt;을 기준으로 &lt;sort key&gt;를 분석한다.
    - SELECT c1, c2 FROM t1 UNION SELECT i1, i2 FROM t3 ORDER BY c1, c2;
    - (X) SELECT c1, c2 FROM t1 UNION SELECT i1, i2 FROM t3 ORDER BY i1, i2;

<a id="f308278390251b6c"></a>
##### &lt;sort specification list&gt;

- &lt;ordering specification&gt;
    - ASC
    - DESC
    - 명시하지 않은 경우, 기본값은 ASC이다. 
- &lt;null ordering&gt;
    - NULLS FIRST
    - NULLS LAST
    - 명시하지 않은 경우, 기본값은 NULLS LAST이다.

<a id="2093f6190dde2967"></a>
##### &lt;sort key&gt;

- &lt;sort key&gt;의 &lt;value expression&gt;이 양의 정수값이면 그 값을 sort key index로 사용한다.
    - 해당 값에 대응되는 &lt;query specification&gt;의 i 번째 &lt;select sublist&gt;를 sort key로 사용한다.
        - SELECT c1, c2 FROM t1 ORDER BY 1;
        - C1을 sort key로 정렬한다.
    - 해당 값에 대응되는 &lt;query specification&gt;의 i 번째 &lt;select sublist&gt;가 존재하지 않는 경우 error를 반환한다.
        - (X) SELECT c1, c2 FROM t1 ORDER BY 3;
- Row subquery나 relation subquery는 &lt;value expression&gt;로 지원되지 않는다.
    - (X) SELECT c1, c2 FROM t1 ORDER BY ( SELECT i1, i2 FROM t2 FETCH FIRST ROW ONLY );
    - T2에 여러 개의 레코드가 존재한다.
        - (X) SELECT c1, c2 FROM t1 ORDER BY ( SELECT i1 FROM t2 );
- 이 외의 &lt;value expression&gt;은 sort key로 사용된다.

<a id="3a2d070208e5b269"></a>
#### 설명

<a id="4d70154b12c3f73e"></a>
##### &lt;order by clause&gt;

&lt;order by clause&gt;는 검색 결과를 정렬하는 방법을 기술한다.

&lt;order by clause&gt;에는 &lt;sort key&gt;들을 콤마 (,) 리스트로 나열할 수 있으며, 나열한 순서대로 각 레코드들의 &lt;sort key&gt;를 비교하여 순서대로 정렬한다.

```
SELECT c1, c2 FROM t1 ORDER BY c1, c2;
```

&lt;sort key&gt;에는 오름차순 정렬 또는 내림차순 정렬을 지정할 수 있는 &lt;ordering specification&gt;을 기술할 수 있는데 생략할 경우에는 오름차순으로 정렬된다.

```
gSQL> SELECT c1 FROM t1;
C1
--
 2
 3
 1
3 rows selected.
```

- 오름 차순 ( ASC )

```
gSQL> SELECT c1 FROM t1 ORDER BY c1;
C1
--
 1
 2
 3
3 rows selected.

gSQL> SELECT c1 FROM t1 ORDER BY c1 ASC;
C1
--
 1
 2
 3
3 rows selected.
```

- 내림 차순 ( DESC )

```
gSQL> SELECT c1 FROM t1 ORDER BY c1 DESC;
C1
--
 3
 2
 1
3 rows selected.
```

&lt;sort key&gt;에는 NULL 값과 NULL이 아닌 값의 순서를 &lt;null ordering&gt;을 사용하여 지정할 수 있는데 생략할 경우에는 NULLS LAST로 정렬된다.

```
gSQL> SELECT c1 FROM t1;
  C1
----
   2
null
   1
3 rows selected.
```

- NULLS LAST

```
gSQL> SELECT c1 FROM t1 ORDER BY c1;    
  C1
----
   1
   2
null
3 rows selected.

gSQL> SELECT c1 FROM t1 ORDER BY c1 NULLS LAST;
  C1
----
   1
   2
null
3 rows selected.
```

- NULLS FIRST

```
gSQL> SELECT c1 FROM t1 ORDER BY c1 NULLS FIRST;
  C1
----
null
   1
   2
3 rows selected.
```

&lt;sort key&gt;에 상수값을 기술할 경우 &lt;select list&gt;에서 해당 값의 순번에 위치한 expression을 &lt;sort key&gt;로 간주한다. 그리고 이 때 기술하는 상수값은 0보다 큰 정수이며, &lt;select list&gt;에 기술한 expression의 전체 개수와 같거나 작아야 한다.

```
gSQL> SELECT c1 FROM t1 ORDER BY 1;
  C1
----
   1
   2
null
3 rows selected.
```

&lt;sort key&gt;에는 LONG type ( LONG VARCHAR, LONG VARBINARY )을 기술할 수 없다.

<a id="62149d59888f70c2"></a>
##### null value와의 비교

- Null value끼리 비교할 경우에는 동일한 값으로 간주한다.
- Null value와 null value가 아닌 값을 비교할 경우에는 다음 규칙을 따른다.
    - NULLS FIRST이고 ASC인 경우: null value < not null value
    - NULLS LAST이고 ASC인 경우: null value > not null value
    - NULLS FIRST이고 DESC인 경우: null value > not null value
    - NULLS LAST이고 DESC인 경우: null value < not null value
- Null value 비교 결과가 UNKNOWN인 경우, 탐색 순서에 따라 정렬한다.

<a id="7878caeacc0bd4c4"></a>
##### 동일한 sort key 값을 가지는 row들의 정렬

Sort key로 구분할 수 없는 row들을 peer라고 하며, peer들은 탐색 순서에 따라 정렬된다.

<a id="2dc6d76d8ed9aad8"></a>
##### &lt;sort key&gt;로 사용되는 &lt;aggregation function&gt;

&lt;query specification&gt;에서 &lt;aggregation function&gt;이 사용되거나 &lt;group by clause&gt;가 기술된 경우, &lt;aggregation function&gt;을 &lt;sort key&gt;로 사용할 수 있다.  
단, &lt;group by clause&gt;가 기술된 경우에만 중첩된 &lt;aggregation function&gt;을 &lt;sort key&gt;로 사용할 수 있다.

```
gSQL> SELECT c1, c2 FROM t1;
C1 C2
-- --
 2  1
 3  5
 1  2
 2 10
 3 10
5 rows selected.

gSQL> SELECT sum(c1) FROM t1 ORDER BY sum(c1);
SUM(C1)
-------
     11
1 row selected.

gSQL> SELECT c1, sum(c2) FROM t1 GROUP BY c1 ORDER BY sum(c2);
C1 SUM(C2)
-- -------
 1       2
 2      11
 3      15
3 rows selected.

gSQL> SELECT sum(c1) FROM t1 GROUP BY c1 ORDER BY sum(sum(c1));
SUM(C1)
-------
      6
1 row selected.
```

<a id="922aebfc948e0978"></a>
#### 사용 예

다음은 ORDER BY를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, c_nation FROM customer ORDER BY c_nation;

C_NAME     C_NATION
---------- -------------
Customer#2 CANADA
Customer#4 GERMANY
Customer#1 KOREA
Customer#3 KOREA
Customer#5 UNITED STATES

5 rows selected.

gSQL> SELECT c_name, c_nation FROM customer ORDER BY c_nation DESC;

C_NAME     C_NATION
---------- -------------
Customer#5 UNITED STATES
Customer#1 KOREA
Customer#3 KOREA
Customer#4 GERMANY
Customer#2 CANADA

5 rows selected.

gSQL> SELECT c_name, c_nation FROM customer ORDER BY 2 DESC;

C_NAME     C_NATION     
---------- -------------
Customer#5 UNITED STATES
Customer#1 KOREA        
Customer#3 KOREA        
Customer#4 GERMANY      
Customer#2 CANADA       

5 rows selected.
```

<a id="2fd2a4126b4710e7"></a>
#### 호환성

**SQL 표준 호환성**

<a id="d1f8611bf1e83257"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F850 | Top-level &lt;order by clause&gt; in &lt;query expression&gt; | O |
| F851 | &lt;order by clause&gt; in subqueries | O |
| F852 | Top-level &lt;order by clause&gt; in views | O |
| F855 | Nested &lt;order by clause&gt; in &lt;query expression&gt; | O |

<a id="28fc8f327e8ce58f"></a>
#### 참조

관련 내용은 [query expression](#f971bccfc0bcab55)을 참조한다.

<a id="4685bb3308f27adc"></a>
### offset limit clause

<a id="42e5815df3f77a8d"></a>
#### 기능

검색 결과에 대하여 skip 할 row의 개수와 fetch 할 row의 개수를 기술한다.

<a id="bf626e37cdef45e7"></a>
#### 구문

```
<offset limit clause> ::=
      <result offset clause>
    | <fetch limit clause>
    | <result offset clause> <fetch limit clause>

<result offset clause> ::=
    OFFSET <offset row count> [ { ROW | ROWS } ]

<fetch limit clause> ::=
      <fetch first clause>
    | <limit clause>

<fetch first clause> ::=
    FETCH [ FIRST | NEXT ] [ <fetch row count> ] [ ROW ONLY | ROWS ONLY ]

<limit clause> ::=
    LIMIT { <fetch row count> | <offset row count> , <fetch row count> | ALL }
```

<a id="0983636672358e55"></a>
#### 사용 범위 및 접근 권한

&lt;offset limit clause&gt;는 접근 권한을 필요로 하지 않는다.

<a id="18090465d4f88598"></a>
#### 구문 규칙 및 파라미터

<a id="4be0330bfc8eaac3"></a>
##### &lt;result offset clause&gt;

- &lt;offset row count&gt; 값은 0과 같거나 큰 양의 정수이어야 한다.
- ROW와 ROWS는 동일한 의미의 키워드로써 생략할 수 있다.
- 구문을 생략할 경우 OFFSET 0 ROWS 라는 의미이다.

<a id="19667a45222b1957"></a>
##### &lt;fetch limit clause&gt;

- 검색 결과 중 fetch 할 row의 개수를 명시한다.
- 구문을 생략할 경우 LIMIT ALL 이라는 의미이다.

<a id="ee7e2a08dfec1b82"></a>
##### &lt;fetch first clause&gt;

- Fetch 할 row의 개수를 명시한다.
- &lt;limit clause&gt;와 함께 사용할 수 없다.
- FIRST와 NEXT는 동일한 의미의 키워드로써 생략할 수 있다.
- ROW ONLY와 ROWS ONLY는 동일한 의미의 키워드로써 생략할 수 있다.
- &lt;fetch row count&gt; 
    - 0 보다 큰 양의 정수이어야 한다.
    - 생략 가능하며 생략할 경우 그 값은 1이다.

<a id="9e55af5b24381989"></a>
##### &lt;limit clause&gt;

- Fetch 할 row의 개수를 지정한다.
- 질의 결과 중 skip 할 row의 개수와 fetch 할 row의 개수를 동시에 지정할 수 있다.
- &lt;fetch first clause&gt;와 함께 사용할 수 없다.
- LIMIT &lt;fetch row count&gt;로 사용한 경우
    - &lt;fetch row count&gt;는 0보다 큰 양의 정수이어야 한다.
    - 이 구문은 FETCH FIRST &lt;fetch row count&gt; ROWS ONLY와 동일한 의미이다.
- LIMIT &lt;offset row count&gt;, &lt;fetch row count&gt;로 사용한 경우
    - &lt;result offset clause&gt;와 동시에 사용할 수 없다.
    - &lt;offset row count&gt;는 0과 같거나 큰 양의 정수이어야 한다.
    - &lt;fetch row count&gt;는 0보다 큰 양의 정수이어야 한다.
    - 이 구문은 OFFSET &lt;offset row count&gt; ROWS FETCH FIRST &lt;fetch row count&gt; ROWS ONLY와 동일한 의미이다.
- LIMIT ALL로 사용한 경우 fetch 할 row의 개수에 제한이 없다.

<a id="91733cb74a757f31"></a>
#### 설명

<a id="a6e19e863a0b8806"></a>
##### &lt;result offset clause&gt;

검색한 결과 중에 &lt;offset row count&gt; 번 째 row부터 fetch 한다. 만일 &lt;offset row count&gt;가 검색한 결과가 row의 개수와 같거나 크면 fetch row 개수는 0이다.

```
gSQL> SELECT c1 FROM t1;
C1
--
 1
 2
 3
3 rows selected.

gSQL> SELECT c1 FROM t1 OFFSET 1;
C1
--
 2
 3
2 rows selected.

gSQL> SELECT c1 FROM t1 OFFSET 3;
no rows selected.
```

<a id="c7d8d41e3bfb062e"></a>
##### &lt;fetch first clause&gt;

검색한 결과 중에 &lt;fetch row count&gt; 개수만큼만 fetch한다.

```
gSQL> SELECT c1 FROM t1;
C1
--
 1
 2
 3
3 rows selected.

gSQL> SELECT c1 FROM t1 FETCH FIRST 2 ROWS ONLY;
C1
--
 1
 2
2 rows selected.
```

<a id="da40b0d07b504b7c"></a>
##### &lt;limit clause&gt;

LIMIT &lt;fetch_row_count&gt;를 사용한 경우, 검색한 결과 중에 &lt;fetch row count&gt; 개수만큼만 fetch한다.

LIMIT &lt;offset row count&gt;, &lt;fetch row count&gt;를 사용한 경우, 검색한 결과 중에 &lt;offset row count&gt;번째 row부터 &lt;fetch row count&gt; 개수만큼만 fetch한다.

LIMIT ALL을 사용한 경우 개수 제한없이 검색한 결과를 fetch한다.

```
gSQL> SELECT c1 FROM t1;
C1
--
 1
 2
 3
3 rows selected.

• LIMIT <fetch_row_count>
gSQL> SELECT c1 FROM t1 LIMIT 2;
C1
--
 1
 2
2 rows selected.

• LIMIT <offset row count>, <fetch_row_count>
gSQL> SELECT c1 FROM t1 LIMIT 1, 1;
C1
--
 2
1 row selected.

• LIMIT ALL
gSQL> SELECT c1 FROM t1 LIMIT ALL;
C1
--
 1
 2
 3
3 rows selected.
```

<a id="7823f2cf61656019"></a>
#### 사용 예

다음은 &lt;result offset clause&gt;을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, c_nation FROM customer OFFSET 1;

C_NAME     C_NATION
---------- -------------
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

4 rows selected.
```

다음은 &lt;fetch first clause&gt;을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, c_nation FROM customer FETCH FIRST ROW ONLY;

C_NAME     C_NATION
---------- --------
Customer#1 KOREA

1 row selected.

gSQL> SELECT c_name, c_nation FROM customer FETCH FIRST 2 ROW ONLY;

C_NAME     C_NATION
---------- --------
Customer#1 KOREA
Customer#2 CANADA

2 rows selected.
```

다음은 &lt;limit clause&gt;을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, c_nation FROM customer LIMIT 1;

C_NAME     C_NATION
---------- --------
Customer#1 KOREA

1 row selected.

gSQL> SELECT c_name, c_nation FROM customer LIMIT 1, 2;

C_NAME     C_NATION
---------- --------
Customer#2 CANADA
Customer#3 KOREA

2 rows selected.

gSQL> SELECT c_name, c_nation FROM customer LIMIT ALL;

C_NAME     C_NATION
---------- -------------
Customer#1 KOREA
Customer#2 CANADA
Customer#3 KOREA
Customer#4 GERMANY
Customer#5 UNITED STATES

5 rows selected.
```

다음은 &lt;result offset clause&gt;과 &lt;fetch limit clause&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_name, c_nation FROM customer OFFSET 1 FETCH 2;

C_NAME     C_NATION
---------- --------
Customer#2 CANADA
Customer#3 KOREA

2 rows selected.

gSQL> SELECT c_name, c_nation FROM customer OFFSET 1 LIMIT 2;

C_NAME     C_NATION
---------- --------
Customer#2 CANADA
Customer#3 KOREA

2 rows selected.
```

<a id="5c80cb41d0c347dc"></a>
#### 호환성

**SQL 표준 호환성**

<a id="12471cbb418ff8f5"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F861 | Top-level &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| F862 | &lt;result offset clause&gt; in subqueries | O |
| F863 | Nested &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| F864 | Top-level &lt;result offset clause&gt; in views | O |
| F865 | dynamic &lt;offset row count&gt; in &lt;result offset clause&gt; | X |

<a id="8fd806f5930143e4"></a>
### set operator

<a id="64d4bc45218a8165"></a>
#### 기능

부질의 (subquery) 결과들에 대한 집합 (set) 연산을 수행한다.

<a id="e432790d488806c6"></a>
#### 구문

```
<set operator> ::=
      <set operator term>
    | <query expression body> UNION [ ALL | DISTINCT ] <set operator term>
    | <query expression body> EXCEPT [ ALL | DISTINCT ] <set operator term>
    | <query expression body> MINUS [ ALL | DISTINCT ] <set operator term>

<set operator term> ::=
      <query term>
    | <set operator term> INTERSECT [ ALL | DISTINCT ] <set operator term>
```

<a id="4072af90b2b58161"></a>
#### 사용 범위 및 접근 권한

&lt;set operator&gt; 구문을 사용하려면 각 &lt;set operator term&gt;에 나타나는 &lt;query expression&gt;에 대한 접근 권한이 있어야 한다.

<a id="6b58b0555e3d60e5"></a>
#### 구문 규칙 및 파라미터

<a id="075d8ce5bd737bbb"></a>
##### &lt;set operator&gt;

- 부질의 (subquery) 간의 집합 연산을 기술한다.
- 각 부질의 (subquery)의 &lt;select list&gt; target 개수가 모두 동일해야 하며, 매칭되는 target들은 모두 동일한 data type group에 속해야 한다.
- 첫 번째 부질의 (subquery)의 &lt;select list&gt; target 이름이 &lt;set operator&gt; 결과 target의 대표 이름이 된다.
    - gSQL> SELECT c1 AS NAME FROM t1 UNION SELECT i1 FROM t2;  
      NAME  
      ----  
      1  
      2  
      2 rows selected.
- 괄호 등을 사용하여 명확하게 수행 순서를 기술하지 않을 경우, 왼쪽에 기술한 부질의 (subquery)에서 오른쪽에 기술한 부질의 (subquery) 순서로 평가하여 처리한다.
- &lt;set operator&gt;의 각 operator는 다음을 의미한다.
    - UNION
        - UNION ALL: 부질의 (subquery) 결과들에서 중복을 제거하지 않고 합집합으로 처리한다.
        - UNION DISTINCT: 부질의 (subquery) 결과들에서 중복을 제거하여 합집합으로 처리한다.
        - ALL/ DISTINCT 중 하나도 기술하지 않을 경우, DISTINCT를 기술한 것과 동일하게 동작한다.
    - EXCEPT
        - EXCEPT ALL: 부질의 (subquery) 결과들에서 중복을 제거하지 않고 차집합으로 처리한다.
        - EXCEPT DISTINCT: 부질의 (subquery) 결과들에서 중복을 제거하여 차집합으로 처리한다.
        - ALL/ DISTINCT 중 하나도 기술하지 않을 경우, DISTINCT를 기술한 것과 동일하게 동작한다.
    - MINUS
        - EXCEPT의 alias로서 EXCEPT와 동일하게 동작한다.
    - INTERSECT
        - INTERSECT ALL: 부질의 (subquery) 결과들에서 중복을 제거하지 않고 교집합으로 처리한다.
        - INTERSECT DISTINCT: 부질의 (subquery) 결과들에서 중복을 제거하여 교집합으로 처리한다.
        - ALL/ DISTINCT 중 하나도 기술하지 않을 경우, DISTINCT를 기술한 것과 동일하게 동작한다.

<a id="bea41174d2282173"></a>
##### &lt;query term&gt;

하나의 부질의 (subquery)를 기술한다.  
자세한 내용은 [query expression](#f971bccfc0bcab55) 절을 참조한다.

<a id="60ade42234a5299f"></a>
#### 설명

<a id="8c8cb5954740f355"></a>
##### &lt;set operator&gt;의 ALL과 DISTINCT의 차이

예를 들어 R1과 R2 table의 데이터가 다음과 같을 경우, 각 &lt;set operator&gt;의 결과는 다음과 같다.

    - TABLE 데이터
        - R1 TABLE = {1, 1, 1, 2, 2, 2, 3, 4, 4, 5}
        - R2 TABLE = {1, 1, 3, 3, 4}
    - SELECT * FROM R1 UNION ALL SELECT * FROM R2;
        - result = {1, 1, 1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4, 4, 5}
    - SELECT * FROM R1 UNION DISTINCT SELECT * FROM R2;
        - result = {1, 2, 3, 4, 5}
    - SELECT * FROM R1 MINUS ALL SELECT * FROM R2;
        - result = {1, 2, 2, 2, 4, 5}
    - SELECT * FROM R1 MINUS DISTINCT SELECT * FROM R2;
        - result = {2, 5}
    - SELECT * FROM R1 INTERSECT ALL SELECT * FROM R2;
        - result = {1, 1, 3, 4}
    - SELECT * FROM R1 INTERSECT DISTINCT SELECT * FROM R2;
        - result = {1, 3, 4}

<a id="2aba3f07cad96353"></a>
![SET 연산 결과](../assets/images/6584a690a27b54f8.png)

<a id="2c19f8de10cafe17"></a>
##### 연산자 우선 순위

&lt;set operator&gt;의 연산자 우선순위는 다음과 같다.

- 괄호 ( ) 우선 
- INTERSECT 우선 
- UNION, EXCEPT는 left-right로 기술한 순서 우선

<a id="bb1004caa68bc00a"></a>
##### &lt;set operator&gt;의 결과 타입

&lt;set operator&gt; 모든 부질의의 i 번째 column은 동일한 계열의 데이터 타입이어야 하며, [결과 타입 조합 규칙](11-sql-elements.md#e881713e04641bea)에 따라 결과 타입이 결정된다.  
단, LONG VARCHAR와 LONG VARBINARY 타입은 UNION ALL만 사용할 수 있다.

<a id="5e1f6422a3df166d"></a>
##### ORDER BY 구문

&lt;set operator&gt;를 ORDER BY와 함께 사용할 때 부질의 간에 column 이름이 다를 경우, 다음과 같이 사용할 수 있다.

- ORDER BY indicator 
    - 결과 column의 순서를 기술한다.   
      SELECT c1 FROM t1   
      UNION ALL   
      SELECT c2 FROM t2   
      ORDER BY 1; 
- ORDER BY left_column_name 
    - 첫 번째 subquery의 column 이름을 기술한다.   
      SELECT c1 FROM t1   
      UNION ALL   
      SELECT c2 FROM t2   
      ORDER BY c1;

<a id="26b6d936d7f4e1ba"></a>
#### 사용 예

다음은 UNION 연산을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT s_nation nation FROM supplier UNION ALL SELECT c_nation FROM customer;

NATION
-------------
FRANCE
KOREA
GERMANY
UNITED STATES
CANADA
KOREA
CANADA
KOREA
GERMANY
UNITED STATES

10 rows selected.

gSQL> SELECT s_nation nation FROM supplier UNION DISTINCT SELECT c_nation FROM customer;

NATION
-------------
UNITED STATES
CANADA
KOREA
GERMANY
FRANCE

5 rows selected.
```

다음은 EXCEPT 연산을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_nation nation FROM customer EXCEPT ALL SELECT s_nation FROM supplier;

NATION
------
KOREA

1 row selected.

gSQL> SELECT c_nation nation FROM customer EXCEPT DISTINCT SELECT s_nation FROM supplier;

no rows selected.
```

다음은 INTERSECT 연산을 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT c_nation nation FROM customer INTERSECT ALL SELECT s_nation FROM supplier;

NATION
-------------
UNITED STATES
CANADA
KOREA
GERMANY

4 rows selected.

gSQL> SELECT c_nation nation FROM customer INTERSECT DISTINCT SELECT s_nation FROM supplier;

NATION
-------------
UNITED STATES
CANADA
KOREA
GERMANY

4 rows selected.
```

<a id="3178d322f9797108"></a>
#### 호환성

**SQL 표준 호환성**

<a id="70d4bc63b7519cc3"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F302 | INTERSECT table operator | O |
| F301 | CORRESPONDING | X |
| T551 | Optional key words for default syntax | O |
| F304 | EXCEPT ALL table operator | O |

<a id="92110033e3698177"></a>
#### 참조

관련 내용은 [query expression](#f971bccfc0bcab55)을 참조한다.

<a id="d3bc7e8acf2465f9"></a>
### subquery

<a id="cfe7bb5eb5346299"></a>
#### 기능

&lt;query expression&gt;에서 파생되는 scalar value, row, table 등을 기술한다.

<a id="bad01149eb9bb3b7"></a>
#### 구문

```
<scalar subquery> ::=
    <subquery>

<row subquery> ::=
    <subquery>

<table subquery> ::=
    <subquery>

<subquery> ::=
    ( <query expression> )
```

<a id="d47e43716cdc21fe"></a>
#### 사용 범위 및 접근 권한

&lt;subquery&gt;에 존재하는 &lt;query expression&gt;에 대한 접근 권한이 있어야 한다.

<a id="3af42d84cd37380e"></a>
#### 구문 규칙 및 파라미터

<a id="b30b50a12d7abfef"></a>
##### &lt;scalar subquery&gt;

- &lt;query expression&gt;에 존재하는 target의 개수는 한 개이어야 한다.
- &lt;query expression&gt;에서 반환된 row의 개수에 따른 결과값은 다음과 같다.
    - 0 개의 row가 반환된 경우, 결과값은 NULL 이다.
    - 한 개의 row가 반환된 경우, 결과값은 해당 row에 포함된 결과값이다.
    - 두 개이상의 row가 반환된 경우, exception error가 발생한다.

<a id="d88c44e586fa9e3f"></a>
##### &lt;row subquery&gt;

- &lt;query expression&gt;에 존재하는 target의 개수는 두 개 이상이어야 한다.
- &lt;query expression&gt;에서 반환된 row의 개수에 따른 결과값은 다음과 같다.
    - 0 개의 row가 반환된 경우, 결과값은 모든 column이 NULL인 row이다.
    - 한 개의 row가 반환된 경우, 결과값은 해당 row이다.
    - 두 개 이상의 row가 반환된 경우, exception error가 발생한다.

<a id="9e165c0c0d935aff"></a>
##### &lt;table subquery&gt;

- &lt;query expression&gt;에 존재하는 target의 개수는 한 개 이상이어야 한다.
- &lt;query expression&gt;에서 반환된 row의 개수에 따른 결과값은 다음과 같다.
    - 0 개의 row가 반환된 경우, 결과값은 no rows이다.
    - 한 개 이상의 row가 반환된 경우, 결과값은 해당 row이다.

<a id="e7d4b524a1ead72e"></a>
#### 설명

<a id="83bc0cd43a0a598e"></a>
##### &lt;scalar subquery&gt;

&lt;scalar subquery&gt;는 결과값으로 한 개의 column을 갖는 한 개의 row를 반환하는 subquery이다. &lt;scalar subquery&gt;의 target은 하나만 존재해야 하며, 결과의 data type은 target의 data type을 따른다.

&lt;scalar subquery&gt;는 &lt;select list&gt;의 target에 단독으로 쓰일 수 있으며, 단일 column만 갖는 연산자에 쓰일 수 있다.

<a id="053496edb450f5b4"></a>
##### &lt;row subquery&gt;

&lt;row subquery&gt;는 결과값으로 두 개 이상의 column을 갖는 한 개의 row를 반환하는 subquery이다. &lt;row subquery&gt;의 target은 두 개 이상 존재해야 하며, 결과의 data type은 target들 각각의 data type을 따른다.

&lt;row subquery&gt;는 &lt;select list&gt;의 target에 단독으로 쓰일 수 없으며, 둘 이상의 column을 갖는 row 연산자에만 쓰일 수 있다.

<a id="25b816444a47b10d"></a>
##### &lt;table subquery&gt;

&lt;table subquery&gt;는 결과값으로 한 개 이상의 column을 갖는 한 개 이상의 row를 반환하는 subquery이다. &lt;table subquery&gt;의 target은 한 개 이상 존재해야 하며, 결과의 data type은 target들 각각의 data type을 따른다.

&lt;table subquery&gt;는 &lt;select list&gt;의 target에 단독으로 쓰일 수 없으며, IN, NOT IN, EXISTS, NOT EXISTS, quantify operator 등의 연산자에 쓰일 수 있다.

<a id="f1eeeaa99de5703b"></a>
#### 사용 예

다음은 &lt;scalar subquery&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT (SELECT c_name FROM dual)  FROM customer;

(SELECT C_NAME FROM DUAL)
-------------------------
Customer#1
Customer#2
Customer#3
Customer#4
Customer#5

5 rows selected.

gSQL> SELECT c_name, c_nation FROM customer WHERE c_nation = (SELECT 'CANADA' FROM dual);

C_NAME     C_NATION
---------- --------
Customer#2 CANADA

1 row selected.
```

다음은 &lt;row subquery&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT p_name, p_brand, p_type FROM part WHERE (p_brand, p_type) = (SELECT 'Brand#1', 'NICKEL' FROM dual);

P_NAME P_BRAND    P_TYPE
------ ---------- ------
Part#2 Brand#1    NICKEL

1 row selected.
```

다음은 &lt;table subquery&gt;를 사용한 SELECT 구문의 예이다.

```
gSQL> SELECT s_name, s_nation FROM supplier WHERE s_nation IN (SELECT c_nation FROM customer);

S_NAME                    S_NATION
------------------------- -------------
Supplier#2                KOREA
Supplier#3                GERMANY
Supplier#4                UNITED STATES
Supplier#5                CANADA

4 rows selected.

gSQL> SELECT * FROM (SELECT s_name, s_nation FROM supplier);

S_NAME                    S_NATION
------------------------- -------------
Supplier#1                FRANCE
Supplier#2                KOREA
Supplier#3                GERMANY
Supplier#4                UNITED STATES
Supplier#5                CANADA

5 rows selected.
```

<a id="7019dfc426c567c6"></a>
#### 호환성

**SQL 표준 호환성**

<a id="f93e3659d6df10ee"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F471 | Scalar subquery values | O |
| F641 | Row and table constructors | X |
| T501 | Enhanced EXISTS predicate | O |
| E061-11 | Subqueries in IN predicate | O |
| E061-12 | Subqueries in quantified comparison predicate | O |
| E061-12 | Correlated subqueries | O |

<a id="63de61a645d000df"></a>
#### 참조

관련 내용은 다음을 참조한다.

- [from clause](#d8f9755e05abe1cf)
- [where clause](#74a33d522dd6bfcc)

<a id="131687c9a5eb9942"></a>
### hint clause

Query를 수행할 때 사용할 hint를 기술한다.  
자세한 내용은 [SQL Hint](15-sql-tuning.md#54d9bce5449eb296)를 참조한다.

<a id="03346f7372e78a74"></a>
## SELECT .. FOR UPDATE

<a id="d0995529e9236e33"></a>
### 기능

SELECT 구문의 결과 집합을 갱신할지 여부를 설정한다.

<a id="6f087547b567add3"></a>
### 구문

```
<select for update statement> ::=
    <query expression>  <updatability clause>
    ;

<updatability clause> ::=
      FOR READ ONLY 
    | FOR UPDATE [ OF <column name list> ] [ <lock wait mode> ]

<lock wait mode> ::=
    | WAIT
    | WAIT second
    | NOWAIT
```

<a id="a2f9e72552ab599b"></a>
### 사용 범위 및 접근 권한

&lt;select for update statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- &lt;query expression&gt; 구문을 수행하려면 구문에 사용된 모든 테이블에 대한 다음 권한 중 하나가 사용자에게 있어야 한다.
    - 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

- FOR UPDATE 구문을 사용할 경우, lock 대상이 되는 테이블에 대한 다음 권한 중 하나가 있어야 한다.
    - 해당 테이블에 대해 (LOCK 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (LOCK TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - LOCK ANY TABLE ON DATABASE

<a id="744f096d173fdfe0"></a>
### 구문 규칙 및 파라미터

<a id="a7ecb404ee7d4f17"></a>
#### &lt;query expression&gt;

SELECT 구문에 INTO 절이 없어야 한다.

FOR UPDATE를 사용하려면 query가 base table의 row 변화를 식별하거나 row에 lock을 획득할 수 있는 updatable query여야 한다.

Updatable query는 다음 조건을 모두 만족해야 한다.

- 최상위 query에 DISTINCT가 존재하지 않아야 한다.
    - (X) SELECT DISTINCT * FROM t1; 
- 최상위 query에 GROUP BY, HAVING, aggregation function이 존재하지 않아야 한다.
    - (X) SELECT MAX(c1) FROM t1; 
- Set 연산자가 존재하지 않아야 한다. 
    - (X) SELECT * FROM t1 UNION ALL SELECT * FROM t2; 
- FROM 절에 나열된 table 들에 하나 이상의 updatable column이 존재해야 한다. 
    - Join에 포함되는 테이블 중 cross join에 해당되지 않는 테이블의 column은 updatable column이 아니다. 
        - FULL OUTER JOIN은 cross join이 아니다. 
        - NATURAL JOIN 은 cross join이 아니다. 
        - INNER JOIN에 USING 구문이 사용된 경우 cross join이 아니다. 
    - 다음과 같은 table들의 column은 updatable column이 아니다. 
        - Dictionary table, fixed table, performance view 
    - View의 column은 updatable table이 아니다.

SELECT 구문에 대한 자세한 내용은 [query expression](#f971bccfc0bcab55)을 참조한다.

<a id="d66a76d806f5005e"></a>
#### &lt;updatability clause&gt;

결과 집합에 대한 row를 변경할지 여부를 지정한다.

- FOR READ ONLY 
    - 읽기 전용 질의임을 선언한다. 
- FOR UPDATE 
    - 쓰기 가능한 질의임를 선언한다. 
    - 질의를 수행할 때 해당 트랜잭션이 종료될 때까지 다른 트랜잭션에 의해 변경되지 않도록 해당 row 들에 대한 x lock을 획득한다. 
    - &lt;query expression&gt;이 updatable query 여야 한다.

<a id="51fbaeb974e06c19"></a>
#### FOR UPDATE OF …

질의를 수행할 때 lock 획득과 관련된 column들을 나열한다.

- FOR UPDATE OF 구문에 나열하는 column 
    - &lt;query expression&gt;의 FROM 절에 나열된 table의 갱신 가능한 column이어야 한다. 
    - 나열된 column의 table에 대해 lock을 획득한다. 
- FOR UPDATE만 사용하는 경우 
    - &lt;query expression&gt;의 FROM 절에 나열된 table들의 모든 갱신 가능한 column을 나열한 것과 동일한 의미이다. 
    - 모든 column의 table에 대해 lock을 획득한다.

<a id="b59785adb05688c6"></a>
#### &lt;lock wait mode&gt;

FOR UPDATE 구문과 함께 사용하며, lock 획득 방법을 지정한다.

- WAIT 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - Lock을 획득할 수 있을 때까지 대기한다. 
- WAIT second 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - 지정한 시간동안 lock을 획득할 수 없을 경우, 에러가 발생한다. 
    - 초 단위이며 0 ~ 1000000000 까지의 값을 사용할 수 있다. 
- NOWAIT 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - 즉시 lock을 획득할 수 없을 경우, 에러가 발생한다.
- 명시하지 않을 경우, 기본값은 WAIT이다.

<a id="cd1a3ba840f88c6f"></a>
### 설명

SELECT 구문은 transaction의 종료 여부와 관계없이 row에 대한 fetch를 지속할 수 있는 반면에, SELECT .. FOR UPDATE 구문은 row들에 대한 lock을 획득하기 때문에 transaction이 종료되면 fetch 할 수 없다.

> Cursor holdability  
> 
> 
> - WITH HOLD
>     - Transaction 종료 여부와 관계없이 fetch를 지속할 수 있다.
>     - Fetch across commit 이라고도 한다.
> 
> 
> 
> - WITHOUT HOLD
>     - Transaction이 종료되면 fetch 할 수 없다.
> 

<a id="d6a7b57adb4f0239"></a>
### 사용 예

다음은 FOR UPDATE 구문을 사용하여 row에 대한 lock을 획득하는 예이다.

```
gSQL> SELECT id, data FROM t1 WHERE id = 3 FOR UPDATE;

ID DATA  
-- ------
 3 data_3

1 row selected.
```

다음과 같이 join과 ORDER BY 구문을 사용하더라도 updatable query이면 FOR UPDATE 구문을 사용할 수 있다.

```
gSQL> SELECT t1.id, t1.name, t2.addr 
        FROM t1, t2
       WHERE t1.id = t2.id
       ORDER BY 1
         FOR UPDATE;

ID NAME    ADDR         
-- ------- -------------
 1 someone somewhere    
 2 anyone  anywhere     
 3 unknown N/A          
 4 leekmo  leekmo's home
 5 mkkim   seoul        

5 rows selected.
```

다음과 같이 updatable query가 아닌 경우에는 FOR UPDATE 구문을 사용할 수 없다.

```
gSQL> SELECT id, COUNT(*)
        FROM t1
       GROUP BY id
         FOR UPDATE;

ERR-42000(16112): query expression is not updatable
```

<a id="d87de34653118c84"></a>
### 호환성

SQL 표준에서는 &lt;select for update statement&gt;를 정의하지 않고 있는데, 이는 [DECLARE cursor_name](19-sql-references-c-g.md#d0200d8897a107da) 구문을 사용하여 정의할 수 있다.

<a id="410ad949d2455fb3"></a>
## SELECT .. INTO

<a id="7523eaf24652b34e"></a>
### 기능

질의를 통해 row 하나를 검색하고, 검색한 row의 값을 호스트 변수로 얻어온다.

<a id="0c93cd47f641f29a"></a>
### 구문

```
<select statement: single row> ::=
    SELECT [ <hint clause> ] [ <set quantifier> ] <select list>
        INTO <select target list>
        <table expression>
    ;

<select target list> ::=
    variable_name [, ...]
```

<a id="1f2078991b784267"></a>
### 사용 범위 및 접근 권한

&lt;select statement: single row&gt; 구문을 수행하려면 사용자에게 구문에 사용된 모든 테이블에 대한 다음 권한 중 하나가 있어야 한다.

- 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
- 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- SELECT ANY TABLE ON DATABASE

<a id="f3626a390a42d8bb"></a>
### 구문 규칙 및 파라미터

<a id="85fb7e617e17ac08"></a>
#### &lt;hint clause&gt;

질의를 수행하기 위한 힌트를 기술한다.  
자세한 내용은 [SELECT](#2070458035e417b9) 구문의 [hint clause](#131687c9a5eb9942) 절을 참조한다.

<a id="5799086b0eac3580"></a>
#### &lt;set quantifier&gt;

질의 결과에서 중복을 제거할지 여부를 기술한다.  
자세한 내용은 [query specification](#7ad631319ea8ccd2) 절을 참조한다.

<a id="28a17c8016c138b0"></a>
#### &lt;select list&gt;

질의 결과로부터 검색할 column을 기술한다.  
자세한 내용은 [select list](#806e99db5dd57a0e) 절을 참조한다.

<a id="736280c29b176cdb"></a>
#### INTO &lt;select target list&gt;

INTO 절에 기술된 변수의 개수는 &lt;select list&gt;에 기술된 expression의 개수와 동일해야 한다.

<a id="d61f447f10084907"></a>
#### &lt;table expression&gt;

검색 조건 등 질의 내용을 기술한다.  
자세한 내용은 [query specification](#7ad631319ea8ccd2)  절을 참조한다.

<a id="907f8f1ff4d55893"></a>
### 설명

검색할 row가 한 건 이하여야 한다.   
두 건 이상의 row가 검색될 경우, 에러가 발생한다.

<a id="3c3acab7703cecb9"></a>
#### SELECT 구문들의 차이점

- &lt;select statement&gt;
    - 조건에 부합하는 다수의 row를 검색하고, 검색한 row를 SQLFetch() 등의 API로 검색할 수 있다. 
    - 예: SELECT c1 FROM t1 WHERE c1 > 0; 
- &lt;select statement: single row&gt;
    - 조건에 부합하는 한 건 이하의 row를 검색할 수 있으며, 검색한 row가 한 건일 경우 INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: SELECT c2 INTO :v1 FROM t1 WHERE c1 = 0;

<a id="46bb5879397edbf6"></a>
### 사용 예

다음은 interactive SQL (gsql)을 사용하여 host 변수에 값을 얻어오는 예이다.

```
gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> SELECT id, data INTO :v_id, :v_data FROM t1 WHERE id = 3;

V_ID V_DATA
---- ------
   3 data_3

1 row selected.
```

<a id="c4e3d3ba65baab2e"></a>
## SELECT .. INTO .. FOR UPDATE

<a id="1ce862b6b77d2fcf"></a>
### 기능

질의를 통해 row 하나를 검색하여 갱신을 수행할지 여부를 설정한 후, 검색한 row의 값을 호스트 변수에 얻어온다.

<a id="c5dfef82f47d8ee3"></a>
### 구문

```
<select for update statement: single row> ::=
    SELECT [ <hint clause> ] [ <set quantifier> ] <select list>
        INTO <select target list>
        <table expression>  <updatability clause>
    ;

<select target list> ::=
    variable_name [, ...]

<updatability clause> ::=
      FOR READ ONLY 
    | FOR UPDATE [ OF <column name list> ] [ <lock wait mode> ]

<lock wait mode> ::=
    | WAIT
    | WAIT second
    | NOWAIT
```

<a id="f967e18830ec7816"></a>
### 사용 범위 및 접근 권한

&lt;select statement: single row&gt; 구문을 수행하려면 사용자에게 구문에 사용된 모든 테이블에 대한 다음 권한 중 하나가 있어야 한다.

- 테이블의 column 중 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
- 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- SELECT ANY TABLE ON DATABASE

FOR UPDATE 구문을 사용할 경우, lock 대상이 되는 테이블에 대해 다음 권한 중 하나가 있어야 한다.

- 해당 테이블에 대해 (LOCK 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (LOCK TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- LOCK ANY TABLE ON DATABASE

<a id="4778769aa9492fb1"></a>
### 구문 규칙 및 파라미터

<a id="f5181560b1f3bb47"></a>
#### &lt;select for update statement: single row&gt;

FOR UPDATE를 사용하려면 query가 base table의 row 변화를 식별하거나 row에 lock을 획득할 수 있는 updatable query여야 한다.

Updatable query는 다음 조건을 모두 만족해야 한다.

- 최상위 query에 DISTINCT가 존재하지 않아야 한다.
    - (X) SELECT DISTINCT * FROM t1; 
- 최상위 query에 GROUP BY, HAVING, aggregation function이 존재하지 않아야 한다. 
    - (X) SELECT MAX(c1) FROM t1; 
- Set 연산자가 존재하지 않아야 한다. 
    - (X) SELECT * FROM t1 UNION ALL SELECT * FROM t2; 
- FROM 절에 나열된 table들에 하나 이상의 updatable column이 존재해야 한다. 
    - Join에 포함되는 테이블 중 cross join에 해당하지 않는 테이블의 column은 updatable column이 아니다. 
        - FULL OUTER JOIN은 cross join이 아니다. 
        - NATURAL JOIN은 cross join이 아니다. 
        - INNER JOIN에 USING 구문이 사용된 경우 cross join이 아니다. 
    - 다음과 같은 table들의 column은 updatable column이 아니다. 
        - Dictionary table, fixed table, performance view 
    - View의 column은 updatable table이 아니다.

<a id="bbcb1ad4cc93d814"></a>
#### &lt;updatability clause&gt;

결과 집합에 대해 row를 변경할지 여부를 지정한다.

- FOR READ ONLY 
    - 읽기 전용 질의임을 선언한다. 
- FOR UPDATE 
    - 쓰기 가능한 질의임를 선언한다. 
    - 질의를 수행할 때 해당 트랜잭션이 종료될 때까지, 다른 트랜잭션에 의해 변경되지 않도록 해당 row들에 대한 x lock을 획득한다. 
    - &lt;query expression&gt;이 updatable query이어야 한다.

<a id="36bc888242c540c3"></a>
#### FOR UPDATE OF …

질의를 수행할 때 lock 획득과 관련된 column을 나열한다.

- FOR UPDATE OF 구문에 나열하는 column 
    - &lt;query expression&gt;의 FROM 절에 나열된 table의 갱신 가능한 column이어야 한다. 
    - 나열된 column의 table에 대해 lock을 획득한다. 
- FOR UPDATE 만 사용하는 경우 
    - &lt;query expression&gt;의 FROM 절에 나열된 table들의 모든 갱신 가능한 column을 나열한 것과 동일한 의미이다. 
    - 모든 column의 table에 대해 lock을 획득한다.

<a id="c65b8b30d294d217"></a>
#### &lt;lock wait mode&gt;

FOR UPDATE 구문과 함께 사용하며, lock 획득 방법을 지정한다.

- WAIT 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - Lock을 획득할 수 있을 때까지 대기한다. 
- WAIT second 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock 을 획득하며 
    - 지정한 시간동안 lock을 획득할 수 없을 경우, 에러가 발생한다. 
    - 초 단위이며 0 ~ 1000000000 까지의 값을 사용할 수 있다. 
- NOWAIT 
    - 질의 결과를 얻기 전에 질의 결과의 모든 row들에 대한 lock을 획득하며 
    - 즉시 lock을 획득할 수 없을 경우, 에러가 발생한다.
- 명시하지 않을 경우, 기본값은 WAIT 이다.

<a id="e8c527bff301fb32"></a>
#### &lt;hint clause&gt;

질의를 수행하기 위한 힌트를 기술한다.  
자세한 내용은 [SELECT](#2070458035e417b9) 구문의 [hint clause](#131687c9a5eb9942) 절을 참조한다.

<a id="0f0c6e3e9d043cb7"></a>
#### &lt;set quantifier&gt;

질의 결과에서 중복을 제거할지 여부를 기술한다.  
자세한 내용은 [query specification](#7ad631319ea8ccd2) 절을 참조한다.

<a id="f5bd6c4782b98cfd"></a>
#### &lt;select list&gt;

질의 결과로부터 검색할 column을 기술한다.  

자세한 내용은 [select list](#806e99db5dd57a0e) 절을 참조한다.

<a id="9674f658a3af230c"></a>
#### INTO &lt;select target list&gt;

INTO 절에 기술된 변수의 개수는 &lt;select list&gt; 에 기술된 expression의 개수와 동일해야 한다.

<a id="281374a13fc2d8b3"></a>
#### &lt;table expression&gt;

검색 조건 등의 질의 내용을 기술한다.  
자세한 내용은 [query specification](#7ad631319ea8ccd2) 절을 참조한다.

<a id="a4093d397d649d0d"></a>
### 설명

검색할 row가 한 건 이하여야 한다.   
두 건 이상의 row가 검색될 경우, 에러가 발생한다.

SELECT 구문은 transaction의 종료 여부와 관계없이 row에 대한 fetch를 지속할 수 있는 반면에, SELECT .. FOR UPDATE 구문은 row들에 대한 lock을 획득하기 때문에 transaction이 종료되면 fetch 할 수 없다.

> Cursor holdability  
> 
> 
> - WITH HOLD
>     - Transaction 종료 여부와 관계없이 fetch를 지속할 수 있다.
>     - Fetch across commit 라고도 한다.
> 
> 
> 
> - WITHOUT HOLD
>     - Transaction이 종료되면 fetch 할 수 없다.
> 

<a id="917b2a3e813aeee8"></a>
#### SELECT 구문들의 차이점

- &lt;select for update statement&gt;
    - 조건에 부합하는 다수의 row를 검색하여 갱신 수행 여부를 설정하고, 검색한 row를 SQLFetch() 등의 API로 검색할 수 있다. 
    - 예: SELECT c1 FROM t1 WHERE c1 > 0 FOR UPDATE; 
- &lt;select for update statement: single row&gt;
    - 조건에 부합하는 한 건 이하의 row를 검색하여 갱신 수행 여부를 설정하고, 검색한 row가 한 건일 경우 INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: SELECT c2 INTO :v1 FROM t1 WHERE c1 = 0 FOR UPDATE;

<a id="eb883d71e886e007"></a>
### 사용 예

다음은 FOR UPDATE 구문을 사용하여 row에 lock을 획득하고, interactive SQL (gsql)을 사용하여 host 변수에 값을 얻어오는 예이다.

```
gSQL> \var v_id   INTEGER
gSQL> \var v_data VARCHAR(128)

gSQL> SELECT id, data INTO :v_id, :v_data FROM t1 WHERE id = 3 FOR UPDATE;

V_ID V_DATA
---- ------
   3 data_3

1 row selected.
```

다음과 같이 join과 ORDER BY 구문을 사용하더라도 updatable query이면 FOR UPDATE 구문을 사용할 수 있다.

```
gSQL> \var v_id   INTEGER
gSQL> \var v_name VARCHAR(128)
gSQL> \var v_addr VARCHAR(128)


gSQL> SELECT t1.id, t1.name, t2.addr 
        INTO :v_id, :v_name, :v_addr
        FROM t1, t2
       WHERE t1.id = t2.id
       ORDER BY 1
       LIMIT 1
         FOR UPDATE;

ID NAME    ADDR         
-- ------- -------------
 1 someone somewhere    

1 row selected.
```

다음과 같이 updatable query가 아닌 경우에는 FOR UPDATE 구문을 사용할 수 없다.

```
gSQL> \var v_id    INTEGER
gSQL> \var v_count INTEGER

gSQL> SELECT id, COUNT(*)
        INTO :v_id, :v_count
        FROM t1
       GROUP BY id
         FOR UPDATE;

ERR-42000(16112): query expression is not updatable
```

<a id="90e087997d7306f3"></a>
### 참조

관련 내용은 다음을 참조한다.

- [SELECT .. FOR UPDATE](#03346f7372e78a74)
- [SELECT .. INTO](#410ad949d2455fb3)

<a id="b6ece05278d045fb"></a>
## SET CONSTRAINTS

<a id="4b5b330323253b0e"></a>
### 기능

트랜잭션 내에서 지연가능한 제약 조건들의 검사 시점을 IMMEDIATE 또는 DEFERRED로 설정한다.

<a id="79af5fd9d76e24ba"></a>
### 구문

```
<set constraints mode statement> ::=
    SET { CONSTRAINT | CONSTRAINTS } <constraint name list> { DEFERRED | IMMEDIATE }
    ;

<constraint name list> ::=
      ALL
    | <constraint name> [, ...]
```

<a id="5e441b6e529e769f"></a>
### 사용 범위 및 접근 권한

SET CONSTRAINTS를 수행하기 위해 별도의 접근 권한이 필요한 것은 아니다.

> Cluster system에서 지원하지 않는다.

<a id="147dc6ac1cfd8814"></a>
### 구문 규칙 및 파라미터

<a id="590953c56aee0f19"></a>
#### CONSTRAINT | CONSTRAINTS

CONSTRAINT와 CONSTRAINTS는 동일한 의미의 키워드인데 SQL 표준은 CONSTRAINTS 이다.

<a id="d6a389668c764298"></a>
#### &lt;constraint name list&gt;

제약 조건 이름 목록을 기술하거나, ALL 키워드를 사용하여 지연 가능한 제약 조건을 모두 명시할 수 있다.   
&lt;constraint name&gt;을 기술할 경우, 제약 조건은 지연 가능해야 한다.   
ALL은 지연 가능한 모든 제약 조건을 의미한다.

<a id="817c35726c6754be"></a>
#### DEFERRED | IMMEDIATE

명시한 지연 가능한 제약 조건들의 검사 시점을 설정한다.

- IMMEDIATE
    - DML을 수행할 때 해당 제약 조건들을 검사한다.
    - 트랜잭션이 해당 제약 조건들을 위반할 경우, 에러가 발생한다
- DEFERRED
    - COMMIT을 수행할 때 해당 제약 조건들을 검사한다.

트랜잭션이 진행 중이면, 검사 시점은 현재 트랜잭션에 설정되며, 트랜잭션이 진행 중이 아닌 경우에는 다음 트랜잭션에 설정된다.   
트랜잭션이 종료되면 다음 트랜잭션에 영향을 미치지 않는다.

<a id="a1c9f23a1a56794b"></a>
### 설명

<a id="df04d828fecd5107"></a>
#### 지연 가능한 제약 조건

지연 가능한 (DEFERRABLE) 제약 조건은 검사 시점을 변경할 수 있다.   
다음은 지연 가능한 제약 조건을 가진 테이블을 생성하고, 데이터를 추가하는 예이다.

```
gSQL> CREATE TABLE t1 
( 
    id   INTEGER, 
    name VARCHAR(128) CONSTRAINT t1_uk UNIQUE 
                      DEFERRABLE INITIALLY IMMEDIATE
);

Table created.

gSQL> COMMIT;

Commit complete.

gSQL> INSERT INTO t1 VALUES ( 1, 'leekmo' );

1 row created.

gSQL> INSERT INTO t1 VALUES ( 2, 'mkkim' );

1 row created.

gSQL> COMMIT;

Commit complete.
```

위의 예에서 name column에 지연 가능한 UNIQUE 제약 조건을 생성하였으며, 초기 검사 시점이 INITIALLY IMMEDIATE로 설정되어 DML을 수행할 때마다 제약 조건을 검사한다.

이 때, 다음과 같이 두 row의 name 값을 서로 교체하려고 하면 검사 시점이 IMMEDIATE라서 모두 제약 조건을 위반하게 된다.

```
gSQL> UPDATE t1 SET name = 'mkkim' WHERE id = 1;

ERR-23000(16057): unique constraint (PUBLIC.T1_UK) violated

gSQL> UPDATE t1 SET name = 'leekmo' WHERE id = 2;

ERR-23000(16057): unique constraint (PUBLIC.T1_UK) violated
```

다음과 같이 검사 시점을 DEFERRED로 변경하면 COMMIT 시점에 제약 조건을 검사하므로 위의 예와 동일한 변경 작업이 모두 성공한다.

```
gSQL> SET CONSTRAINTS t1_uk DEFERRED;

Constraints set.

gSQL> UPDATE t1 SET name = 'mkkim' WHERE id = 1;

1 row updated.

gSQL> UPDATE t1 SET name = 'leekmo' WHERE id = 2;

1 row updated.

gSQL> COMMIT;

Commit complete.
```

검사 시점을 DEFERRED로 설정하면 COMMIT 시점에 제약 조건을 검사하므로 제약 조건을 위반한 상태에서 트랜잭션을 COMMIT 할 경우 다음과 같이 트랜잭션은 실패하고 ROLLBACK 된다.

```
gSQL> SET CONSTRAINTS t1_uk DEFERRED;

Constraints set.

gSQL> INSERT INTO t1 VALUES ( 3, 'leekmo' );

1 row created.

gSQL> COMMIT;

ERR-40002(16291): transaction rollback: integrity constraint violation : PUBLIC.T1_UK(1)
```

<a id="8d927dabf0a6a3e1"></a>
#### 지연 제약 조건을 위반한 트랜잭션

트랜잭션이 DEFFERED로 설정된 제약 조건을 위반한 상태에서 다음 구문들을 수행할 경우 다음과 같은 에러가 발생한다.

- COMMIT
    - 에러가 발생하고, 트랜잭션이 ROLLBACK 된다.
- SET CONSTRAINTS ALL IMMEDIATE
    - 구문 에러가 발생한다.
- DDL
    - 구문 에러가 발생한다.

COMMIT 할 경우 원치 않는 ROLLBACK이 발생할 수 있으므로, SET CONSTRAINTS ALL IMMEDIATE 구문을 수행하여 트랜잭션이 제약 조건을 위반한 상태인지 확인해야 한다.

```
gSQL> SET CONSTRAINTS t1_uk DEFERRED;

Constraints set.

gSQL> INSERT INTO t1 VALUES ( 3, 'leekmo' );

1 row created.

gSQL> SET CONSTRAINTS ALL IMMEDIATE;

ERR-23000(16038): integrity constraint violation : PUBLIC.T1_UK(1)

gSQL> SELECT * FROM t1 ORDER BY id;

ID NAME  
-- ------
 1 mkkim 
 2 leekmo
 3 leekmo

3 rows selected.

gSQL> UPDATE t1 SET name = 'xcom73' WHERE id = 3;

1 row updated.

gSQL> SET CONSTRAINTS ALL IMMEDIATE;

Constraints set.

gSQL> COMMIT;

Commit complete.
```

<a id="b509629cdbc0bdd9"></a>
#### 트랜잭션 제어 언어

SET CONSTRAINTS 구문은 [SAVEPOINT savepoint_specifier](#903816d217929cbc) 구문과 같이 트랜잭션 진행 중에 사용하는 트랜잭션 제어 언어이다.  
SET CONSTRAINTS 구문에는 COMMIT, ROLLBACK, ROLLBACK TO SAVEPOINT 구문 등의 트랜잭션 제어가 적용된다.

다음은 여러 개의 지연 가능한 제약 조건을 가진 테이블의 예이다.

```
CREATE TABLE t1
(
   id1 INTEGER CONSTRAINT t1_uk1 UNIQUE DEFERRABLE INITIALLY IMMEDIATE,
   id2 INTEGER CONSTRAINT t1_uk2 UNIQUE DEFERRABLE INITIALLY IMMEDIATE,
   id3 INTEGER CONSTRAINT t1_uk3 UNIQUE DEFERRABLE INITIALLY IMMEDIATE
);
```

다음과 같이 트랜잭션이 진행되는 중에 &lt;set constraints mode statement&gt; 구문을 수행할 경우, 각 시점에 따라 지연 가능한 제약 조건들의 검사 시점이 변경된다.

- result: success

```
INSERT INTO t1 VALUES ( 1, 1, 1 );

1 row created.

COMMIT;

Commit complete.
```

- result: success

```
SAVEPOINT sp1;

Savepoint created.
```

- result: success
- t1_uk1 constraint is DEFERRED

```
SET CONSTRAINTS t1_uk1 DEFERRED;

Constraints set.
```

- result: success

```
SAVEPOINT sp2;

Savepoint created.
```

- result: success
- t1_uk1, t1_uk2 constraints are DEFERRED

```
SET CONSTRAINTS t1_uk2 DEFERRED;

Constraints set.
```

- result: success

```
SAVEPOINT sp3;

Savepoint created.
```

- result: success
- ALL constraints are DEFERRED

```
SET CONSTRAINTS ALL DEFERRED;

Constraints set.
```

- result: success

```
SAVEPOINT sp4;

Savepoint created.
```

- result: success
- ALL constraints are IMMEDIATE

```
SET CONSTRAINTS ALL IMMEDIATE;

Constraints set.
```

다음과 같이 ROLLBACK TO SAVEPOINT 구문을 사용하여 트랜잭션을 부분 철회할 경우 SET CONSTRAINTS 구문도 함께 부분 철회되어 검사 시점이 변경된다.

- result: error

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK1) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK2) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK3) violated
```

- result: success
- t1_uk1, t1_uk2 constraints are DEFERRED

```
ROLLBACK TO SAVEPOINT sp4;

Rollback complete.
```

- result: success

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

1 row created.
```

- result: success

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

1 row created.
```

- result: success

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

1 row created.
```

- result: success
- t1_uk1, t1_uk2 constraints are DEFERRED

```
ROLLBACK TO SAVEPOINT sp3;

Rollback complete.
```

- result: success

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

1 row created.
```

- result: success

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

1 row created.
```

- result: error

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK3) violated
```

- result: success
- t1_uk1 constraint is DEFERRED

```
ROLLBACK TO SAVEPOINT sp2;

Rollback complete.
```

- result: success

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

1 row created.
```

- result: error

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK2) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK3) violated
```

- result: success
- all constraint are IMMEDIATE

```
ROLLBACK TO SAVEPOINT sp1;

Rollback complete.
```

- result: error

```
INSERT INTO t1 VALUES ( 1, 2, 2 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK1) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 3, 1, 3 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK2) violated
```

- result: error

```
INSERT INTO t1 VALUES ( 4, 4, 1 );

ERR-23000(16057): unique constraint (PUBLIC.T1_UK3) violated
```

- result: 1 row
- 1 1 1

```
SELECT * FROM t1;

ID1 ID2 ID3
--- --- ---
  1   1   1

1 row selected.
```

트랜잭션을 COMMIT 하거나 ROLLBACK 할 경우, SET CONSTRAINTS 구문의 영향은 종료되며, 모든 지연 가능한 제약 조건들은 제약 조건의 특성으로 설정한 INITIALLY IMMEDIATE 또는 INITIALLY DEFERRED 값을 따른다.

<a id="c7e32119d90cff40"></a>
### 사용 예

다음은 제약 조건 이름을 기술하여 검사 시점을 변경하는 예이다.

```
gSQL> SET CONSTRAINTS t1_uk1 DEFERRED;

Constraints set.
```

다음은 모든 지연 가능한 제약 조건의 검사 시점을 변경하는 예이다.

```
gSQL> SET CONSTRAINTS ALL DEFERRED;

Constraints set.
```

<a id="859c4affd3773323"></a>
### 호환성

SQL 표준에서는 CONSTRAINT 키워드 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="5be9dee3aa73f6f9"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F721 | Deferrable constraints | O |

<a id="f300180357caf13e"></a>
### 참조

관련 내용은 다음을 참조한다.

- 제약 조건 생성
    - [CREATE TABLE](19-sql-references-c-g.md#ce6ecbcf1ea593ea)
    - [ALTER TABLE name ADD CONSTRAINT](18-sql-references-a-b.md#b1bf02c95ebfb66d)
    - [ALTER TABLE name ADD COLUMN](18-sql-references-a-b.md#5bf457087cd2404f)
    - [ALTER TABLE name ALTER COLUMN](18-sql-references-a-b.md#0892c59a03976f71)

- 제약 조건 변경: [ALTER TABLE name ALTER CONSTRAINT](18-sql-references-a-b.md#75005eef58445700)

- 제약 조건 검사시점 제어: [SET CONSTRAINTS](#b6ece05278d045fb)

<a id="0af7a3d47e76664e"></a>
## SET ROLE role_name

<a id="59dedd466052995a"></a>
### 기능

Session role과 current role을 변경한다.

<a id="6c28081a96dfc91d"></a>
### 구문

```
<set role statement> ::=
    SET ROLE <role specification> ;

<role specification> ::=
     <role_name>
   | NONE
```

<a id="feca2ca82c2c331d"></a>
### 사용 범위 및 접근 권한

&lt;set role statement&gt; 구문을 수행하려면 다음 조건 중 하나를 만족해야 한다.

- 사용자에게 ACCESS CONTROL ON DATABASE 권한이 있어야 한다.
- 현재 사용자에게 적용할 수 있는 role (applicable role)이어야 한다.

<a id="134ab5917137031e"></a>
### 구문 규칙 및 파라미터

<a id="ae17b92cbe985538"></a>
#### &lt;role specification&gt;

- &lt;role_name&gt;
    - Current role을 변경할 role 이름이다.
- NONE
    - Session에 접속했을 때처럼 current role을 설정하지 않는다.

<a id="75157a8fa4679605"></a>
### 설명

트랜잭션이 활성화된 상태에서는 &lt;set role statement&gt; 구문을 변경할 수 없다.

Session에 처음 접속했을 때의 current role은 NULL이다.

&lt;set role statement&gt;를 수행하여 current role을 변경한다.  
또는 session에 처음 접속했을 때처럼 current role을 설정하지 않는다.

&lt;set role statement&gt; 구문을 수행한 후에는 설정된 current role을 기준으로 모든 구문을 수행한다.

<a id="7b0aeaf3e89de2d1"></a>
### 사용 예

다음은 role을 부여받은 사용자가 current role을 설정하고 해제하는 예이다.

```
gSQL> \connect u1 u1

gSQL> SELECT CURRENT_USER , CURRENT_ROLE FROM dual;

CURRENT_USER CURRENT_ROLE
------------ ------------
U1           null        

1 row selected.

gSQL> SET ROLE role1;

Session set.

gSQL> SELECT CURRENT_USER , CURRENT_ROLE FROM dual;

CURRENT_USER CURRENT_ROLE
------------ ------------
U1           ROLE1       

1 row selected.

gSQL> SET ROLE NONE;

Session set.

gSQL> SELECT CURRENT_USER , CURRENT_ROLE FROM dual;

CURRENT_USER CURRENT_ROLE
------------ ------------
U1           null        

1 row selected.
```

<a id="a7a720f8b5836b12"></a>
### 호환성

**SQL 표준 호환성**

<a id="7f9f94fddf8101b8"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T331 | Basic roles | O |
| T332 | Extended roles | X |

<a id="de7f734a7dde68ea"></a>
## SET SCHEMA schema_name

<a id="79a8be9d0015d39d"></a>
### 기능

현재 session에서 사용할 기본 schema 이름을 설정한다.

<a id="6637a02b1fbea1a3"></a>
### 구문

```
<set schema statement> ::=
    SET SCHEMA schema_name
    ;
```

<a id="e7239e2511d42a8d"></a>
### 사용 범위 및 접근 권한

없음

<a id="5225245c6b9102b5"></a>
### 구문 규칙 및 파라미터

<a id="7dc75f26ee62aa5b"></a>
#### schema_name

현재 session에 설정할 기본 schema 이름이다.

<a id="6523cbe914f59134"></a>
### 설명

현재 session에서 사용할 기본 schema 이름을 설정한다.  
객체의 schema 이름을 명시하지 않으면 현재 session에서 사용할 기본 schema 이름이 된다.

- u1 사용자로 접속한 경우, u1 사용자의 schema path를 이용해 R 릴레이션을 검색한다.

```
% gsql u1 u1
gsql> SELECT * FROM r;
```

- SET SCHEMA 구문을 설정한 경우, NEW_SCHEMA.R을 이용해 R 릴레이션을 검색한다.

```
gsql> SET SCHEMA new_schema;

gsql> SELECT * FROM r;
```

<a id="0bd19d9ac9c8e1ae"></a>
### 사용 예

다음은 u1 사용자가 s1, s2 스키마를 소유한 예이다.

```
CREATE USER u1 IDENTIFIED BY u1 WITHOUT SCHEMA;
CREATE SCHEMA s1 AUTHORIZATION u1;
CREATE SCHEMA s2 AUTHORIZATION u1;
COMMIT;

ALTER USER u1 SCHEMA PATH ( s1, s2 );
GRANT ALL PRIVILEGES TO u1;
COMMIT;

CREATE TABLE s1.t1 ( c1 VARCHAR(32) );
INSERT INTO s1.t1 VALUES ( 'S1.T1' );
COMMIT;

CREATE TABLE s2.t1 ( c1 VARCHAR(32) );
INSERT INTO s2.t1 VALUES ( 'S2.T1' );
COMMIT;
```

최초로 접속할 때 사용자 u1의 schema path를 이용하여 t1 테이블을 해석하여 S1.T1 테이블을 조회한다.

```
% gsql u1 u1

gSQL> SELECT current_schema FROM dual;

CURRENT_SCHEMA
--------------
S1            

1 row selected.


gSQL> SELECT * FROM t1;

C1   
-----
S1.T1

1 row selected.
```

SET SCHEMA 구문을 사용한 후에 session의 schema 이름을 이용하여 t1 테이블을 해석하여 S2.T1 테이블을 조회한다.

```
gSQL> SET SCHEMA s2;

Session set.


gSQL> SELECT current_schema FROM dual;

CURRENT_SCHEMA
--------------
S2            

1 row selected.


gSQL> SELECT * FROM t1;

C1   
-----
S2.T1

1 row selected.
```

<a id="81b5b13c87d9d96e"></a>
### 호환성

**SQL 표준 호환성**

<a id="ea5057efc312fd35"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F761 | Session management | O |

<a id="784d7fcc74c83d43"></a>
## SET SESSION AUTHORIZATION user_identifier

<a id="fadbe7789d0071a4"></a>
### 기능

Session user와 current user를 변경한다.

<a id="8ef786d5b860f9ba"></a>
### 구문

```
<set session user identifier statement> ::=
    SET SESSION AUTHORIZATION user_identifier
    ;
```

<a id="d73326753da9f199"></a>
### 사용 범위 및 접근 권한

&lt;set session user identifier statement&gt; 구문을 수행하려면 logon 사용자에게 ACCESS CONTROL ON DATABASE 권한이 있어야 한다.

사용자 정보는 다음과 같은 세가지 형태로 관리된다.

- Logon user 
    - Login한 user로써 connection을 닫을 때까지 유지된다. 
- Session user 
    - 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다. 
- Current user 
    - 일반적으로 session user와 동일하지만 PSM이나 view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다. 
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="98a8364ac9a4ade7"></a>
### 구문 규칙 및 파라미터

<a id="b59d3a093665570f"></a>
#### user_identifier

변경할 사용자의 이름이다.

<a id="6f4f1913e63380ed"></a>
### 설명

SET SESSION AUTHORIZATION 구문을 수행한 이후의 모든 구문은 session user를 기준으로 수행되므로, session user에 대한 권한을 검사하고 객체를 생성할 때의 소유자 역시 session user가 된다.

<a id="e80ab5044c90ec92"></a>
### 사용 예

다음은 ACCESS CONTROL ON DATABASE 권한을 가진 test 사용자가 session user를 u1 사용자로 변경한 예이다.

```
gSQL> SET SESSION AUTHORIZATION u1;

Session set.

gSQL> SELECT LOGON_USER(), SESSION_USER(), CURRENT_USER FROM dual;

LOGON_USER() SESSION_USER() CURRENT_USER
------------ -------------- ------------
TEST         U1             U1          

1 row selected.
```

<a id="bb70d09798d6d37e"></a>
### 호환성

**SQL 표준 호환성**

<a id="9fdc0f56885aaa56"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F321 | User authorization | O |

<a id="f5827be020a921bc"></a>
## SET SESSION CHARACTERISTICS AS transaction_mode

<a id="20465f886243e2f0"></a>
### 기능

세션의 트랜잭션 속성을 설정한다.

<a id="b161d7e6a91205ca"></a>
### 구문

```
<set session characteristics statement> ::=
    SET SESSION CHARACTERISTICS AS TRANSACTION <transaction_mode>
    ;

<transaction_mode> ::=
    { <transaction_access_mode> | ISOLATION LEVEL < isolation_level > }

<transaction_access_mode> ::=
    READ { ONLY | WRITE }

< isolation_level > ::=
    { READ COMMITTED | SERIALIZABLE }
```

<a id="e8f879cbec62c1c0"></a>
### 구문 규칙 및 파라미터

<a id="69facf8d0c1f2646"></a>
#### &lt;transaction_access_mode&gt;

다음 트랜잭션의 ACCESS MODE 이다.

- READ ONLY 
- READ WRITE

<a id="7d01dc0bb72bd9a4"></a>
#### &lt;isolation_level&gt;

다음 트랜잭션의 ISOLATION LEVEL 이다.

- READ COMMITTED 
- SERIALIZABLE

> SERIALIZABLE 은 cluster 환경에서는 지원되지 않는다.

<a id="617085246f1d4778"></a>
### 설명

SET SESSION CHARACTERISTICS은 세션의 트랜잭션 속성을 설정한다. 즉, session 내에서 생성되는 모든 transaction의 속성이 이를 따른다.

참고로 [SET TRANSACTION transaction_mode](#b1f1b95a2b4bce4e) 구문의 경우, 이후에 수행되는 하나의 transaction 속성만 변경한다.

<a id="20a9bbb2b61712d3"></a>
### 사용 예

다음은 session 내에서 생성될 모든 transaction을 READ ONLY로 설정하는 예이다.

```
gSQL> SET SESSION CHARACTERISTICS AS TRANSACTION READ ONLY;

Session set.
```

다음은 session 내에서 생성될 모든 transaction의 isolation level을 READ COMMITTED로 설정하는 예이다.

```
gSQL> SET SESSION CHARACTERISTICS AS TRANSACTION ISOLATION LEVEL READ COMMITTED;

Session set.
```

<a id="92d2f4fdebc510cb"></a>
### 호환성

**SQL 표준 호환성**

<a id="1f21bb1695f9322d"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F761 | Session management | O |

<a id="cfb0a729c6a54a79"></a>
### 참조

관련 내용은 [SET TRANSACTION transaction_mode](#b1f1b95a2b4bce4e)를 참조한다.

<a id="abedf122216a7d1b"></a>
## SET TIME ZONE

<a id="4e0686a55b452cc6"></a>
### 기능

세션의 TIMEZONE을 설정한다.

<a id="7253b357cad2ab58"></a>
### 구문

```
<set local time zone statement> ::=
    SET TIME ZONE <set time zone value>
    ;

<set time zone value> ::= 
    { '[+|-]hh:mm' | LOCAL }
```

<a id="33aec657c218ad53"></a>
### 구문 규칙 및 파라미터

<a id="7d00d9736d52a386"></a>
#### &lt;set time zone value&gt;

설정할 TIMEZONE 값이다.

- hh:mm: 설정할 TIMEZONE의 GMT OFFSET 이다.
    - Offset 값의 범위는 '-14:00' ~ '+14:00' 이다.
- LOCAL: Session을 생성한 시점의 TIME ZONE 이다.
    - Session을 생성할 때의 TIME ZONE은 client OS의 TIME ZONE으로 설정된다.

<a id="08aa96947093e7d1"></a>
### 설명

Session의 time zone을 변경하면 함수 [CURRENT_TIME](17-built-in-function-references.md#b857364923db6e01), [CURRENT_TIMESTAMP](17-built-in-function-references.md#168559e424362489) 등의 결과값에 영향을 미친다.

<a id="2953adbc2cb7ab10"></a>
### 사용 예

다음은 session의 time zone을 '+09:00' 으로 변경하는 예이다.

```
gSQL> SET TIME ZONE '+09:00';

Session set.
```

<a id="5142a7fb48b22591"></a>
### 호환성

**SQL 표준 호환성**

<a id="100d297b4a1d223b"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F411 | Time zone specification | O |

<a id="b1f1b95a2b4bce4e"></a>
## SET TRANSACTION transaction_mode

<a id="cb5d19352a5aa615"></a>
### 기능

다음 트랜잭션의 속성을 설정한다.

<a id="85985576d714c3e8"></a>
### 구문

```
<set transaction statement> ::=
    SET TRANSACTION <transaction_mode>
    ;

<transaction_mode> ::=
    { <transaction_access_mode> | ISOLATION LEVEL < isolation_level > }

<transaction_access_mode> ::=
    READ { ONLY | WRITE }

< isolation_level > ::=
    { READ COMMITTED | SERIALIZABLE }
```

<a id="cc97d86d801366b2"></a>
### 구문 규칙 및 파라미터

<a id="a5cccde5bf5d2122"></a>
#### &lt;transaction_access_mode&gt;

다음 트랜잭션의 ACCESS MODE 이다.

- READ ONLY 
- READ WRITE

<a id="6244d814539b38cb"></a>
#### &lt;isolation_level&gt;

다음 트랜잭션의 ISOLATION LEVEL 이다.

- READ COMMITTED 
- SERIALIZABLE

> SERIALIZABLE 은 cluster 환경에서는 지원되지 않는다.

<a id="f5c532049bcb89e1"></a>
### 설명

SET TRANSACTION은 다음 트랜잭션의 속성을 설정하며, 다음 트랜잭션이 종료되면 트랜잭션 속성은 기본값으로 복원된다.

<a id="c7fb66f9520599b2"></a>
### 사용 예

다음에 수행될 transaction을 읽기 전용으로 설정한 예이다.

```
gSQL> SET TRANSACTION READ ONLY;

Transaction set.
```

<a id="b977d94b54996e32"></a>
### 호환성

**SQL 표준 호환성**

<a id="b561cf527b2f7510"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T251 | SET TRANSACTION statement: LOCAL option | X |

<a id="c646096c8a862c7d"></a>
### 참조

관련 내용은 [SET SESSION CHARACTERISTICS AS transaction_mode](#f5827be020a921bc)를 참조한다.

<a id="32f7c95aafaed0c2"></a>
## TRUNCATE TABLE

<a id="9e310e1679af2c04"></a>
### 기능

테이블의 모든 row들을 제거한다.

<a id="b45b888123f08f53"></a>
### 구문

```
<truncate table statement> ::= 
    TRUNCATE TABLE table_name 
        [ RESTART IDENTITY | CONTINUE IDENTITY ] 
        [ DROP STORAGE | DROP ALL STORAGE ] 
    ;
```

<a id="98b13cfb56f7e493"></a>
### 사용 범위 및 접근 권한

&lt;truncate table statement&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- 테이블의 소유자 
- 테이블에 대해 CONTROL TABLE ON TABLE 
- 테이블이 속한 스키마에 대해 (DROP TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- DROP ANY TABLE ON DATABASE

<a id="304220b63c253d94"></a>
### 구문 규칙 및 파라미터

<a id="e344017c2892ed0d"></a>
#### table_name

Row들을 제거할 대상 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="322a0f3969d0bb62"></a>
#### [ RESTART IDENTITY | CONTINUE IDENTITY ]

- RESTART IDENTITY 
    - 자동 생성값을 갖는 column (identity column)이 해당 테이블에 존재할 경우 자동으로 값을 재시작한다. 
- CONTINUE IDENTITY 
    - 자동 생성값을 갖는 column (identity column)이 해당 테이블에 존재할 경우 기존값을 변경하지 않는다.
- 명시하지 않을 경우, 기본값은 CONTINUE IDENTITY이다.

<a id="f7548d99e6ddee83"></a>
#### [ DROP STORAGE | DROP ALL STORAGE ]

- DROP STORAGE 
    - 테이블에 할당된 extent 중에 MINSIZE 만큼만 제외하고 나머지 extent들을 제거한다.
- DROP ALL STORAGE 
    - 테이블에 할당된 모든 extent 들을 제거한다.
- 명시하지 않을 경우, 기본값은 DROP STORAGE 이다.

<a id="24fa3139bfd0d287"></a>
### 설명

TRUNCATE TABLE과 같은 Data Definition Language (DDL) 구문도 트랜잭션이 COMMIT 되기 전이라면 ROLLBACK 할 수 있다.

TRUNCATE TABLE 은 DELETE TRIGGER 를 실행하지 않는다.

Foreign key 가 참조하는 parent table 은 TRUNCATE 할 수 없다.

```
CREATE TABLE parent ( pk INTEGER PRIMARY KEY );
CREATE TABLE child ( fk INTEGER CONSTRAINT child_fk REFERENCES parent(pk) );
INSERT INTO parent VALUES ( 1 );
INSERT INTO child  VALUES ( 1 );
COMMIT;

gSQL> TRUNCATE TABLE parent;
ERR-42000(16042): unique/primary keys in table referenced by foreign keys
```

다음과 같이 child table 을 먼저 TRUNCATE 하거나, foreign key 를 제거하거나 NOT ENFORCED 로 변경해야 한다.

- Child TABLE 을 먼저 TRUNCATE

```
gSQL> TRUNCATE TABLE child;
Table truncated.

gSQL> TRUNCATE TABLE parent;
Table truncated.
```

- FOREIGN KEY 를 제거하거나 NOT ENFORCED 로 변경

```
gSQL> ALTER TABLE child ALTER CONSTRAINT child_fk NOT ENFORCED;
Table altered.

gSQL> TRUNCATE TABLE parent;
Table truncated.
```

<a id="1d5be5794908d3fe"></a>
### 사용 예

다음은 TRUNCATE TABLE 구문을 수행하는 예이다.

```
gSQL> TRUNCATE TABLE t1;

Table truncated.
```

다음은 TRUNCATE TABLE을 수행할 때 identity column 값을 재시작하는 예이다.

```
TRUNCATE TABLE t1 RESTART IDENTITY;

Table truncated.
```

<a id="88f5860492ee1998"></a>
### 호환성

SQL 표준에서는 [ DROP STORAGE | DROP ALL STORAGE ] 절을 정의하지 않고 있다.

**SQL 표준 호환성**

<a id="c6c272db0e9b8279"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F200 | TRUNCATE TABLE statement | O |
| F202 | TRUNCATE TABLE: identity column restart option | O |

<a id="d07bac444b3a8009"></a>
## UPDATE

<a id="3685213a964290fb"></a>
### 기능

테이블의 row들을 갱신한다.

<a id="86a74ddbd698e111"></a>
### 구문

```
<update statement: searched> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
    ;

<set clause> ::=
      column_name = { <value expression> | DEFAULT }
    | ( column_name [, ...] ) = ( { <value expression> | DEFAULT } [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )


<result offset clause> ::=
    OFFSET skip_count [ ROW | ROWS ]


<fetch limit clause> ::=
      <fetch first clause>
    | <limit clause>


<fetch first clause> ::=
    FETCH [ FIRST | NEXT ] [ row_count ] [ ROW ONLY | ROWS ONLY ]


<limit clause>
    LIMIT { fetch_row_count | offset_row_count, fetch_row_count | ALL }
```

<a id="d3ddb3f01933a177"></a>
### 사용 범위 및 접근 권한

&lt;update statement: searched&gt; 구문을 수행하려면 사용자에게 다음 권한 중 하나가 있어야 한다.

- Update 대상인 모든 column에 대해 UPDATE(columns) ON TABLE 
- 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE 
- 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
- UPDATE ANY TABLE ON DATABASE

<a id="95f990994b56eaad"></a>
### 구문 규칙 및 파라미터

<a id="5a5b5219378ae8af"></a>
#### table_name

Row를 갱신할 대상 테이블의 이름이다.  
schema_name.table_name과 같이 테이블이 속한 스키마를 정의할 수 있는데 schema_name을 생략할 경우 구문을 수행하는 사용자의 기본 스키마 이름이 사용된다.

<a id="9c0544ad8986a7f3"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="62d20dc31fe68cd2"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.

다음과 같은 방법으로 정의할 수 있다.

- column_name = { &lt;value expression&gt; | DEFAULT }

```
UPDATE table_name 
   SET column1 = value1, column2 = value2, column3 = value3
```

- ( column_name [, ...] ) = ( { &lt;value expression&gt; | DEFAULT } [, ...] )

```
UPDATE table_name 
   SET ( column1, column2, column3 ) = ( value1, value2, value3 )
```

- ( column_name [, ...] ) = ( &lt;query expression&gt; )

```
UPDATE table_name 
   SET column1 = ( SELECT max(value1) FROM other_table_name )
```

&lt;query expression&gt;은 row 하나를 생성하는 질의여야 한다.

Column 값으로 DEFAULT를 사용할 경우, [CREATE TABLE](19-sql-references-c-g.md#ce6ecbcf1ea593ea)을 수행할 때 정의한 기본값 ([&lt;default clause&gt;](19-sql-references-c-g.md#092150e3dd719845) 참조)을 사용하며, 정의되지 않은 경우에는 NULL 값이 할당된다.

<a id="af2afef424348d02"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 갱신한다.  
WHERE 조건을 명시하지 않을 경우, 모든 row들을 갱신한다.  
WHERE 조건에 대한 자세한 내용은 [SELECT](#2070458035e417b9) 구문의 [where clause](#74a33d522dd6bfcc)를 참조한다.

<a id="c4b00e267c185283"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](#2070458035e417b9) 구문의 &lt;[result offset clause&gt;](#4be0330bfc8eaac3)를 참조한다.

<a id="7fa35a16d90ae353"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row의 개수를 명시하는 구문으로써 다음 두 가지 방법을 사용할 수 있다.

- &lt;fetch first clause&gt; 
    - Fetch 할 row의 개수를 명시한다.
    - 자세한 내용은 [SELECT](#2070458035e417b9) 구문의 &lt;[fetch first clause&gt;](#ee7e2a08dfec1b82)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](#2070458035e417b9) 구문의 &lt;[limit clause&gt;](#9e55af5b24381989)를 참조한다.

<a id="96426e485f532fda"></a>
### 설명

<a id="54d6f0a9c322e3cf"></a>
#### UPDATE 관련 구문들의 차이점

- [UPDATE](#d07bac444b3a8009)
    - 조건에 부합하는 다수의 row를 갱신한다. 
    - 예: UPDATE t1 SET c2 = c2 + 1 WHERE c1 > 0; 
- [UPDATE name WHERE CURRENT OF cursor_name](#27bb694ed08b753f)
    - 현재 cursor가 가리키는 row를 갱신한다. 
    - 예: UPDATE t1 WHERE CURRENT OF cursor; 
- [UPDATE name RETURNING](#bef2071ff7bc6b58)
    - 조건에 부합하는 다수의 row를 갱신하며, 갱신한 row들을 [SELECT](#2070458035e417b9) 구문과 동일한 방식 (SQLFetch() 등의 API)으로 검색할 수 있다. 
    - 예: UPDATE t1 SET c2 = c2 + 1 WHERE c1 > 0 RETURNING c2; 
- [UPDATE name RETURNING .. INTO](#4fc5ee649d3baf4f)
    - 한 건 이하의 row를 갱신할 수 있으며, 갱신한 row가 한 건일 경우 RETURNING INTO 절의 호스트 변수에 값을 얻어온다. 
    - 예: UPDATE t1 SET c2 = c2 + 1 WHERE c1 = 0 RETURNING c2 INTO :v1;

<a id="186eac9706c7fe39"></a>
### 사용 예

다음은 조건에 부합하는 다수의 row를 갱신하는 예이다.

```
gSQL> UPDATE lineitem
         SET l_shipdate = CURRENT_DATE
       WHERE l_returnflag = 'R';

5 rows updated.
```

다음은 여러 column의 값을 갱신하는 예이다.

```
gSQL> UPDATE lineitem
         SET l_shipdate   = CURRENT_DATE
           , l_returnflag = 'A'
       WHERE l_returnflag = 'R';

5 rows updated.
```

다음은 여러 column을 괄호로 묶어 갱신하는 예이다.

```
gSQL> UPDATE lineitem
         SET ( l_shipdate  , l_returnflag )
           = ( CURRENT_DATE, 'A' )
       WHERE l_returnflag = 'R';

5 rows updated.
```

다음은 subquery를 사용하여 column의 값을 갱신하는 예이다.

```
gSQL> UPDATE lineitem
         SET l_discount = ( SELECT MAX(l_discount) + 0.01 FROM lineitem )
       WHERE l_returnflag = 'R';

5 rows updated.
```

다음은 OFFSET과 FETCH 절을 사용하여 조건에 부합하는 row들 중 일부만 갱신하는 예이다.

```
gSQL> UPDATE lineitem
         SET l_discount = l_discount + 0.01
       WHERE l_returnflag = 'R'
      OFFSET 3
      FETCH 2;

2 rows updated.
```

<a id="495a83ffeed3f5a0"></a>
### 호환성

SQL 표준은 UPDATE 구문에서 다음 절을 정의하지 않고 있다.

- &lt;result offset clause&gt; 
- &lt;fetch limit clause&gt;

**SQL 표준 호환성**

<a id="3e452eb012d969ba"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F781 | Self-referencing operations | X |
| T111 | Updatable joins, unions, and columns | X |

<a id="bef2071ff7bc6b58"></a>
## UPDATE name RETURNING

<a id="d779b421577147b8"></a>
### 기능

테이블의 row들을 갱신하고, 갱신 전의 row들이나 갱신 후의 row들을 검색한다.

<a id="cb80a6bd2384b6dd"></a>
### 구문

```
<update statement: searched> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
        <returning clause>

<set clause> ::=
      column_name = { <value expression> | DEFAULT }
    | ( column_name [, ...] ) = ( { <value expression> | DEFAULT } [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )


<result offset clause> ::=
    OFFSET skip_count [ ROW | ROWS ]


<fetch limit clause> ::=
      <fetch first clause>
    | <limit clause>


<fetch first clause> ::=
    FETCH [ FIRST | NEXT ] [ row_count ] [ ROW ONLY | ROWS ONLY ]


<limit clause>
    LIMIT { fetch_row_count | offset_row_count, fetch_row_count | ALL }


<returning clause> ::=
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] }
```

<a id="473bfec8d6e951e9"></a>
### 사용 범위 및 접근 권한

&lt;update returning query statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- UPDATE 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Update 대상인 모든 column에 대해 UPDATE(columns) ON TABLE 
    - 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - UPDATE ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="894c2321e7d77add"></a>
### 구문 규칙 및 파라미터

<a id="a6de920868dfb0d6"></a>
#### table_name

Row를 갱신할 대상 테이블의 이름이다.

<a id="b277d405442f659f"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="3a3074924f451e85"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.  
자세한 내용은 [UPDATE](#d07bac444b3a8009) 구문을 참조한다.

<a id="be51097526fae178"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 갱신한다.  
WHERE 조건을 명시하지 않을 경우, 모든 row들을 갱신한다.  
WHERE 조건에 대한 자세한 내용은 [SELECT](#2070458035e417b9) 구문의 [where clause](#74a33d522dd6bfcc)를 참조한다.

<a id="723e0918c6e9614c"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](#2070458035e417b9) 구문의 &lt;[result offset clause&gt;](#4be0330bfc8eaac3)를 참조한다.

<a id="9babfca74a9262d6"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row의 개수를 명시하는 구문으로써 다음 두 가지 방법을 사용할 수 있다.

- &lt;fetch first clause&gt; 
    - Fetch 할 row의 개수를 명시한다. 
    - 자세한 내용은 [SELECT](#2070458035e417b9) 구문의 &lt;[fetch first clause&gt;](#ee7e2a08dfec1b82)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](#2070458035e417b9) 구문의 &lt;[limit clause&gt;](#9e55af5b24381989)를 참조한다.

<a id="fc55fedc0a8fafab"></a>
#### &lt;returning clause&gt;

갱신된 row들을 결과 집합으로 하고, 이들 중에서 검색할 column을 기술한다.

- RETURN과 RETURNING은 동일한 의미의 키워드이다. 
- NEW | OLD 
    - NEW: 갱신된 row들 중에 갱신 후 row를 기준으로 검색한다. 
    - OLD: 갱신된 row들 중에 갱신 전 row를 기준으로 검색한다. 
    - 생략할 경우, 기본값은 NEW 이다. 
- &lt;value expression&gt; 
    - SELECT 구문의 &lt;select list&gt;와 동일하지만 aggregation 등을 사용할 수 없다. 
- [ [AS] alias_name] 
    - AS 절을 사용하여 &lt;value expression&gt;의 이름을 지정할 수 있다.

<a id="2bdf778adaa170e6"></a>
### 설명

자세한 내용은 [UPDATE 관련 구문들의 차이점](#54d6f0a9c322e3cf)을 참조한다.

<a id="7932d242e446722a"></a>
### 사용 예

다음은 RETURNING 절을 사용하여 갱신된 row들의 값을 얻는 예이다.

```
gSQL> UPDATE lineitem 
         SET l_discount = l_discount + 0.01
       WHERE l_returnflag = 'R'
   RETURNING l_orderkey, l_linenumber, l_discount;

L_ORDERKEY L_LINENUMBER L_DISCOUNT
---------- ------------ ----------
         8            1        .07
         9            2        .11
        12            5        .05
        15            1        .03
        16            2        .08

5 rows updated.
```

다음은 RETURNING OLD 절을 사용하여 갱신된 row들의 갱신 전 값을 얻는 예이다.

```
gSQL> UPDATE lineitem 
         SET l_discount = l_discount + 0.01
       WHERE l_returnflag = 'R'
   RETURNING OLD l_orderkey, l_linenumber, l_discount;

L_ORDERKEY L_LINENUMBER L_DISCOUNT
---------- ------------ ----------
         8            1        .06
         9            2         .1
        12            5        .04
        15            1        .02
        16            2        .07

5 rows updated.
```

<a id="6c0e77ff57e1640d"></a>
### 호환성

SQL 표준에는 &lt;update returning query statement&gt; 구문이 존재하지 않는다.

<a id="4fc5ee649d3baf4f"></a>
## UPDATE name RETURNING .. INTO

<a id="2a55320731f184b5"></a>
### 기능

테이블 row 한 개를 갱신하고, 갱신한 row의 값을 호스트 변수에 얻어온다.

<a id="15dc7744d326f3f3"></a>
### 구문

```
<update statement: searched> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        [ WHERE <search condition> ]
        [ <result offset clause> ]
        [ <fetch limit clause> ]
        <returning into clause>
    ;


<set clause> ::=
      column_name = { <value expression> | DEFAULT }
    | ( column_name [, ...] ) = ( { <value expression> | DEFAULT } [, ...] )
    | ( column_name [, ...] ) = ( <query expression> )


<result offset clause> ::=
    OFFSET skip_count [ ROW | ROWS ]


<fetch limit clause> ::=
      <fetch first clause>
    | <limit clause>


<fetch first clause> ::=
    FETCH [ FIRST | NEXT ] [ row_count ] [ ROW ONLY | ROWS ONLY ]


<limit clause>
    LIMIT { fetch_row_count | offset_row_count, fetch_row_count | ALL }


<returning into clause> ::=
    { RETURN | RETURNING } [ NEW | OLD ] { * | { <value expression> [ [AS] alias_name] } [, ...] } INTO variable_name [, ...]
```

<a id="6f5d7acfd0c6e4c4"></a>
### 사용 범위 및 접근 권한

&lt;update returning query statement&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- UPDATE 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Update 대상인 모든 column에 대해 UPDATE(columns) ON TABLE 
    - 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - UPDATE ANY TABLE ON DATABASE

- RETURNING 절에 사용된 모든 column에 대해 다음 권한 중 하나가 있어야 한다.
    - RETURNING 구문에 사용된 모든 column에 대해 SELECT(columns) ON TABLE 
    - 테이블에 대해 (SELECT 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (SELECT TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - SELECT ANY TABLE ON DATABASE

<a id="4408121954edacec"></a>
### 구문 규칙 및 파라미터

<a id="7d7f2ea77326f32e"></a>
#### table_name

Row를 갱신할 대상 테이블의 이름이다.

<a id="3f5282b1e4af38ef"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="ad8a994f6564a0fc"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.  
자세한 내용은 [UPDATE](#d07bac444b3a8009) 구문을 참조한다.

<a id="466107b250caefb7"></a>
#### WHERE &lt;search condition&gt;

WHERE 조건을 만족하는 row를 갱신한다.  
WHERE 조건을 명시하지 않을 경우, 모든 row들을 갱신한다.  
WHERE 조건에 대한 자세한 내용은 [SELECT](#2070458035e417b9) 구문의 [where clause](#74a33d522dd6bfcc)를 참조한다.

<a id="695a03751b307e71"></a>
#### &lt;result offset clause&gt;

질의 결과 중 건너뛸 row의 개수를 명시한다.  
자세한 내용은 [SELECT](#2070458035e417b9) 구문의 &lt;[result offset clause&gt;](#4be0330bfc8eaac3)를 참조한다.

<a id="14f8f67e6a6d7c76"></a>
#### &lt;fetch limit clause&gt;

Fetch 할 row의 개수를 명시하는 구문으로써 다음 두 가지 방법을 사용할 수 있다.

- &lt;fetch first clause&gt; 
    - Fetch 할 row의 개수를 명시한다. 
    - 자세한 내용은 [SELECT](#2070458035e417b9) 구문의 &lt;[fetch first clause&gt;](#ee7e2a08dfec1b82)를 참조한다.
- &lt;limit clause&gt;
    - Fetch 할 row의 개수를 명시하거나 질의 결과 중 건너뛸 row의 개수와 fetch 할 row의 개수를 동시에 명시한다.
    - 자세한 내용은 [SELECT](#2070458035e417b9) 구문의 &lt;[limit clause&gt;](#9e55af5b24381989)를 참조한다.

<a id="b7d5920a440d23bd"></a>
#### RETURNING .. AS ..

갱신된 row들을 결과 집합으로 하고, 이들 중에서 검색할 column을 기술한다.  
자세한 내용은 [UPDATE name RETURNING](#bef2071ff7bc6b58) 구문의 &lt;[returning clause&gt;](#fc55fedc0a8fafab)를 참조한다.

<a id="0429e6752d458347"></a>
#### INTO variable_name [, ...]

INTO 절에 기술된 변수의 개수는 RETURNING 절에 기술된 expression의 개수와 동일해야 한다.   
갱신할 row가 한 건 이하여야 한다.   
Row가 두 건 이상 갱신될 경우, 에러가 발생한다.

<a id="9d23bc9779db99b6"></a>
### 설명

자세한 내용은 [UPDATE 관련 구문들의 차이점](#54d6f0a9c322e3cf)을 참조한다.

<a id="3af46b059dc35d20"></a>
### 사용 예

다음은 갱신한 row의 column 값을 host 변수에 얻어오는 예이다.

- Host 변수를 선언한다.

```
gSQL> \VAR v_discount NUMBER

gSQL> UPDATE lineitem 
         SET l_discount = l_discount + 0.01
       WHERE l_orderkey = 12 AND l_linenumber = 5
   RETURNING l_discount INTO :v_discount;

V_DISCOUNT
----------
       .05

1 row updated.
```

<a id="eb6a40e453905e3c"></a>
### 호환성

SQL 표준에는 &lt;update returning into statement&gt; 구문이 존재하지 않는다.

<a id="27bb694ed08b753f"></a>
## UPDATE name WHERE CURRENT OF cursor_name

<a id="a4bc8194f35f7582"></a>
### 기능

커서가 가리키는 row 하나를 갱신한다.

<a id="89d1a917a3ae4473"></a>
### 구문

```
<update statement: positioned> ::=
    UPDATE table_name [ [ AS ] alias_name ]
        SET <set clause> [, ...]
        WHERE CURRENT OF cursor_name
    ;
```

<a id="69387e2ffce2475a"></a>
### 사용 범위 및 접근 권한

&lt;update statement: positioned&gt; 구문을 수행하려면 사용자가 다음 조건들을 만족해야 한다.

- UPDATE 구문을 수행하려면 다음 권한 중 하나가 있어야 한다.
    - Update 대상인 모든 column에 대해 UPDATE(columns) ON TABLE 
    - 테이블에 대해 (UPDATE 또는 CONTROL TABLE) ON TABLE 
    - 테이블이 속한 스키마에 대해 (UPDATE TABLE 또는 CONTROL SCHEMA) ON SCHEMA 
    - UPDATE ANY TABLE ON DATABASE

<a id="87d08381b8675bd7"></a>
### 구문 규칙 및 파라미터

<a id="66ed92b88a98fa90"></a>
#### table_name

Row를 갱신할 대상 테이블의 이름이다.

<a id="e2c77503d8ee5919"></a>
#### [ AS alias_name ]

table_name의 alias 이다.

<a id="a27e95d81d240e54"></a>
#### &lt;set clause&gt;

갱신할 column과 할당할 값을 정의하며, &lt;set clause&gt;의 column 개수와 값의 개수는 동일해야 한다.  
자세한 내용은 [UPDATE](#d07bac444b3a8009) 구문을 참조한다.

<a id="67462705aa7964cd"></a>
#### cursor_name

cursor_name에 해당하는 커서는 다음 조건들을 만족해야 한다.

- OPEN 된 커서이어야 한다. ([OPEN cursor_name](#674c9a50006ee689) 참조) 
- 커서를 이용해 FETCH 한 row가 있어야 한다. ([FETCH cursor_name](19-sql-references-c-g.md#189c41bd169bad81) 참조) 
- 커서에 사용된 질의가 table_name을 식별할 수 있어야 한다. ([DECLARE cursor_name](19-sql-references-c-g.md#d0200d8897a107da) 참조) 
- table_name에 대해 갱신할 수 있는 커서이어야 한다. ([DECLARE cursor_name](19-sql-references-c-g.md#d0200d8897a107da) 참조)

<a id="bdf9a0c29b5f72e0"></a>
### 설명

자세한 내용은 [UPDATE 관련 구문들의 차이점](#54d6f0a9c322e3cf)을 참조한다.

<a id="98741677faa72b90"></a>
### 사용 예

다음은 interactive SQL (gsql)에서 cursor를 사용하여 &lt;update statement: positioned&gt; 구문을 수행하는 예이다.

- Host 변수를 선언한다.

```
gSQL> \VAR v_discount NUMBER
```

- Cursor를 선언한다.

```
gSQL> DECLARE update_cursor CURSOR FOR 
        SELECT l_discount
          FROM lineitem
         WHERE l_orderkey = 8 AND l_linenumber = 1
           FOR UPDATE;

Cursor declared.
```

- Cursor를 open한다.

```
gSQL> OPEN update_cursor;

Cursor is open.
```

- Row를 fetch한다.

```
gSQL> FETCH update_cursor INTO :v_discount;

V_DISCOUNT
----------
       .06

1 row fetched.
```

- Current row를 update한다.

```
gSQL> UPDATE lineitem 
         SET l_discount = l_discount + 0.01 
       WHERE CURRENT OF update_cursor;

1 row updated.
```

- Cursor를 close한다.

```
gSQL> CLOSE update_cursor;

Cursor closed.

gSQL> COMMIT;

Commit complete.
```

다음은 embedded SQL 프로그램에서 cursor를 사용하여 &lt;update statement: positioned&gt; 구문을 수행하는 예이다.

```
{
    ...
    EXEC SQL BEGIN DECLARE SECTION;
        ...    
        double v_discount;  
        ...   
    EXEC SQL END DECLARE SECTION;
    ...
    EXEC SQL DECLARE update_cursor CURSOR FOR
              SELECT l_discount
                FROM lineitem
               WHERE l_orderkey = 8 AND l_linenumber = 1
                 FOR UPDATE;
    ...
    EXEC SQL OPEN update_cursor;
    ...
    EXEC SQL FETCH NEXT update_cursor INTO :v_discount;
    ...
    EXEC SQL UPDATE lineitem 
                SET l_discount = l_discount + 0.01 
              WHERE CURRENT OF update_cursor;
    ...
    EXEC SQL CLOSE update_cursor;
    ...
    EXEC SQL COMMIT WORK;
    ...
}
```

<a id="8810add1189a6cd1"></a>
### 호환성

**SQL 표준 호환성**

<a id="38ee3af60d38a527"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| F831 | Full cursor update | O |
| B031 | Basic dynamic SQL | O |

<a id="97e84baefba3257f"></a>
### 참조

관련 내용은 [CLOSE cursor_name](19-sql-references-c-g.md#98a34ae5c82860ff)을 참조한다.

---

[← 19. SQL References (C~G)](19-sql-references-c-g.md) · [전체 목차](../README.md) · [21. Overview of PSM →](../part-04-sql-psm-manual/21-overview-of-psm.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
