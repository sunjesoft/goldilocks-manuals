<a id="da0d8f362a709192"></a>

# 24. PSM Cursor Statements

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/da0d8f362a709192)  
> 태그: `21c.1_35_tag`

[← 23. PSM Control Statements](23-psm-control-statements.md) · [전체 목차](../README.md) · [25. Using PSM Subprograms →](25-using-psm-subprograms.md)

<a id="e8d292146bd972b3"></a>
## Declaration

PSM statement를 통해 조회할 경우 데이터베이스로부터 두 개 이상의 결과를 반환 받을 수 없다. 따라서, 두 개 이상의 결과를 조회하려면 cursor를 선언하고 정의하여 사용해야 한다.

- Cursor는 다음과 같이 분류된다.
    - Explicit cursor
        - Cursor declaration/ definition을 통해 사용자가 명시적으로 선언한다.
    - Implicit cursor
        - PSM statement를 통해 데이터베이스 내부적으로 처리되는 cursor로써 사용자가 정의하거나 선언할 수 없다.

Explicit cursor를 사용하기 전에 PSM declare section에서 cursor를 선언하고 (declaration) 정의해야(definition) 한다. (이후의 설명에서 cursor는 explicit cursor를 의미한다.)

- Cursor 선언 (declaration)은 다음 항목들을 정의한다.
    - Cursor 이름
    - Cursor가 갖는 parameter list
    - Cursor의 return type

- Cursor 정의 (definition)는 다음과 같은 항목을 정의한다.
    - Cursor의 이름
    - Cursor가 갖는 parameter list
    - Cursor의 return type
    - Cursor가 수행할 SELECT 및 SELECT .. FOR UPDATE 구문

- Cursor의 선언과 정의에서 사용되는 각 항목은 다음과 같은 특성을 갖는다.
    - Cursor 이름
        - Cursor가 선언된 SCOPE 내에서 유일해야 한다.
        - 이름은 128 byte 보다 작아야 한다.
    - Parameter list
        - Cursor가 실행할 SQL에 PSM 변수나 값을 binding 해야 할 경우에 정의한다. 
    - Return type
        - Cursor가 가진 SQL 문을 validation한 결과 집합의 형태를 엄격하게 정의하고자 할 때 사용한다. 
        - 만일 cursor가 가진 SQL 문의 결과 집합에 대한 정의가 return type의 정의와 다를 경우 오류가 발생한다.

> Cursor 정의는 이전에 선언된 cursor와 동일한 형태 (name, parameter list, return type)이어야 한다.

Cursor의 declaration/ definition에 대해서는 다음을 참조한다.

```
DECLARE
```

- Declaration

```
CURSOR C1 RETURN T1%ROWTYPE;
```

- Declaration & definition

```
CURSOR C2 IS SELECT * FROM T1;
```

- Definition for C1

```
CURSOR C1 RETURN T1%ROWTYPE IS SELECT * FROM T1;
BEGIN
  NULL;
END;
/
```

만일, 동일한 cursor_name을 갖는 Cursor RETURN TYPE의 선언과 정의가 다를 경우, 다음과 같은 오류가 발생할 수 있다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.

gSQL> DECLARE
    TYPE rec IS RECORD (C1 VARCHAR(20), C2 VARCHAR(20));
```

다음 두 개의 cursor return type의 형태는 같지만 다른 type을 사용하는 것으로 인식되기 때문에 동일한 cursor name 사용에 따른 오류가 발생한다.

```
CURSOR C1 RETURN rec;
    CURSOR C1 RETURN T1%ROWTYPE IS SELECT * FROM T1;
BEGIN
    NULL;
END;
/
ERR-HY000(17032): PSM compilation error : 
(1) at (4:12): ERR-HY000(17033): duplicated cursor name
```

Parameter list 항목의 선언과 정의가 다른 경우에도 다음과 같은 오류가 발생한다.

```
DECLARE
```

- Parameter의 선언과 정의가 다르다. (Parameter name)

```
CURSOR C1 (A1 INTEGER, A2 INTEGER DEFAULT 10) RETURN T1%ROWTYPE;
    CURSOR C1 (A1 INTEGER, A3 INTEGER DEFAULT 10) RETURN T1%ROWTYPE IS 
           SELECT * FROM T1;
BEGIN
    NULL;
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (3:12): ERR-HY000(17033): duplicated cursor name
```

Cursor에 정의된 SQL 문을 run-time 시점에 PSM 변수등을 참조하여 수행해야 할 경우, cursor의 parameter로 정의할 수 있다.

```
DECLARE
  cursor c1 (a1 varchar ) return t1%rowtype; 
  cursor c2 (a1 varchar(20) ) return t1%rowtype;
BEGIN
  NULL;
END;
/
```

DEFAULT 절을 정의한 경우 cursor를 실행하는 시점에 parameter 정의를 생략할 수 있다.   
다음은 parameter를 모두 입력하여 수행하는 경우와 DEFAULT 절에 parameter 정의를 생략하여 수행하는 경우의 예이다

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);
Table created.

gSQL> INSERT INTO T1 VALUES ('Seoul', '24');
1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');
1 row created.

gSQL> DECLARE
    V1 VARCHAR(20);
    V2 VARCHAR(20);

    CURSOR C1 (A1 INTEGER, A2 INTEGER DEFAULT 10)
        IS SELECT * FROM T1 WHERE C2 >= A1 AND C2 <= A2;
BEGIN
```

- Parameter를 모두 입력하여 수행한다.

```
OPEN C1 (10, 50);
    FETCH C1 INTO V1, V2;

    DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);
    CLOSE C1;
```

- (A2) default parameter를 생략하고 수행한다.

```
OPEN C1 (10);
    FETCH C1 INTO V1, V2;
    IF C1%NOTFOUND = TRUE 
    THEN
        DBMS_OUTPUT.PUT_LINE('NO DATA');
    END IF;
    CLOSE C1;
END;
/
V1 = Seoul , V2 = 24
NO DATA

Anonymous PL block executed.
```

<a id="b74ac20125391a3c"></a>
## OPEN

Explicit cursor를 declaration/ definition한 후에는 OPEN statement를 통해 cursor의 select statement를 수행할 수 있다. 만일, SELECT .. FOR UPDATE 문인 경우에는 결과 집합의 row를 lock 한다.

Cursor가 정상적으로 OPEN 된 CURSOR를 다시 OPEN하면 오류가 발생한다.

```
DECLARE
  V1 VARCHAR(20);
  V2 VARCHAR(20);

  CURSOR C1 IS SELECT * FROM T1;
BEGIN
  
  OPEN C1;
  OPEN C1;

END;
/

ERR-HY000(17037): cursor is already open : 
  OPEN C1;
       *
ERROR at line 9:
```

Explicit cursor가 parameter를 가질 경우, 다음과 같이 사용할 수 있다.

```
DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);

  cursor c1 (a1 varchar(20) ) return t1%rowtype;
  cursor c1 (a1 varchar(20) ) return t1%rowtype 
    is select * from t1 where c1 = a1;
BEGIN

  OPEN c1( 'Seoul' );

  FETCH c1 INTO V1, V2;

  DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);
  
END;
/
V1 = Seoul , V2 = 24

Anonymous PL block executed.
```

자세한 내용은 [OPEN Statement](28-psm-language-element-references.md#ab5c2db9d72f3ce2)를 참조한다.

<a id="1425a5bb050876e0"></a>
## FETCH

Explicit cursor를 정상적으로 OPEN 한 경우, FETCH statement를 통해 결과를 PSM 변수로 저장할 수 있다.

- 결과는 다음과 같은 PSM 변수에 저장할 수 있다.
    - SQL data type 변수
    - Single row를 저장할 수 있는 record type 변수
    - Single row를 저장할 수 있는 key가 명시된 associative array type 변수

다음은 SQL data type의 변수를 이용하거나 %ROWTYPE을 통해 fetch 하는 예이다.

```
DECLARE

V1 VARCHAR(20);
V2 VARCHAR(20);
V3 T1%ROWTYPE;

CURSOR C1 IS SELECT * FROM T1;
BEGIN

OPEN C1;
```

- List of SQL type variables

```
FETCH C1 INTO V1, V2;
DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);
```

- Single record variables

```
FETCH C1 INTO V3;

DBMS_OUTPUT.PUT_LINE('V3.C1 = ' || V3.C1 || ' , V3.C2 = ' || V3.C2);

END;
/
V1 = Seoul , V2 = 24
V3.C1 = Pusan , V3.C2 = 44
```

FETCH에서 사용되는 record type 변수는 단독으로 쓰여야 하며 다른 유형의 변수와 함께 사용할 경우 다음과 같이 오류가 발생한다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);
Table created.

gSQL> INSERT INTO T1 VALUES ('Seoul', '24');
1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');
1 row created.

gSQL> DECLARE
    V1 VARCHAR(20);
    V2 VARCHAR(20);
    V3 T1%ROWTYPE;

    CURSOR C1 (A1 INTEGER, A2 INTEGER DEFAULT 10)
        IS SELECT * FROM T1 WHERE C2 >= A1 AND C2 <= A2;
BEGIN
    OPEN C1 (10, 50);
```

V3는 record type이고 scalar type return 결과를 record type에 저장할 수 없으므로 오류가 발생한다.

```
FETCH C1 INTO V1, V3;

    CLOSE C1;
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (10:23): ERR-HY000(17007): invalid expression
```

자세한 내용은 [FETCH Statement](28-psm-language-element-references.md#f182af65649d3610)를 참조한다.

<a id="6db789a14ae7e06d"></a>
## CLOSE

정상적으로 OPEN 된 cursor를 close 한다. Close 된 cursor로부터는 결과나 cursor-attributes를 얻을 수 없다. CLOSE된 cursor에 접근하여 fetch등을 수행할 경우 다음과 같이 INVALID_CURSOR exception이 발생한다.

```
DECLARE

  V1 VARCHAR(20);
  V2 VARCHAR(20);

  CURSOR C1 IS SELECT * FROM T1;
BEGIN
  
  OPEN C1;
  CLOSE C1;

  BEGIN
    FETCH C1 INTO V1, V2;
  EXCEPTION WHEN INVALID_CURSOR 
            THEN DBMS_OUTPUT.PUT_LINE('invalid cursor exception');
  END;

END;
/
invalid cursor exception

Anonymous PL block executed.
```

자세한 내용은 [CLOSE Statement](28-psm-language-element-references.md#69270ed5b2e896c8)를 참조한다.

<a id="b03582f3ace246e0"></a>
## EXPLICIT CURSOR ATTRIBUTES

Explicit cursor attributes는 explicit cursor의 현재 상태 정보를 가지고 있다. 이 속성들은 expression과 조건식 모두에 사용할 수 있다.

Explicit cursor attribute는 다음 구문과 같이 사용되며 각 속성에 대한 자세한 정보는 다음 표를 참조한다.

```
Cursor_Name % Attribute_name
Attribute_name :=  ISOPEN
                 | FOUND
                 | NOTFOUND
                 | ROWCOUNT
```

**Cursor attributes**

<a id="a1e12bb4f7f2aae8"></a>
| 속성 | 반환 타입 | 설명 |
| --- | --- | --- |
| %ISOPEN | BOOLEAN | Cursor가 정상적으로 열린 경우에만 TRUE이다. 그 외에는 FALSE이다. |
| %FOUND | BOOLEAN | FETCH 이전에는 NULL, FETCH가 정상적으로 수행된 경우 TRUE이고, 데이터가 없는 경우에는 FALSE이며, CLOSE 이후에는 NULL이다. |
| %NOTFOUND | BOOLEAN | %FOUND와 반대되는 값을 갖는다. |
| %ROWCOUNT | INTEGER | OPEN 이전까지는 NULL이고, 정상적으로 OPEN 한 경우 0이며 FETCH가 성공할 때마다 1씩 증가한다. |

다음은 각 cursor attribute에 대하여 단계별로 값이 어떻게 변화하는지 보여주는 예이다.

```
DECLARE

  V1 VARCHAR(20);
  V2 VARCHAR(20);

  CURSOR C1 IS SELECT * FROM T1;
BEGIN
  
  DBMS_OUTPUT.PUT_LINE('<BEFORE OPEN>');
  DBMS_OUTPUT.PUT_LINE('%ISOPEN   = [' || C1%ISOPEN   || ']');
  DBMS_OUTPUT.PUT_LINE('%FOUND    = [' || C1%FOUND    || ']');
  DBMS_OUTPUT.PUT_LINE('%NOTFOUND = [' || C1%NOTFOUND || ']');
  DBMS_OUTPUT.PUT_LINE('%ROWCOUNT = [' || C1%ROWCOUNT || ']');

  OPEN C1;

  DBMS_OUTPUT.PUT_LINE('<AFTER OPEN>');
  DBMS_OUTPUT.PUT_LINE('%ISOPEN   = [' || C1%ISOPEN   || ']');
  DBMS_OUTPUT.PUT_LINE('%FOUND    = [' || C1%FOUND    || ']');
  DBMS_OUTPUT.PUT_LINE('%NOTFOUND = [' || C1%NOTFOUND || ']');
  DBMS_OUTPUT.PUT_LINE('%ROWCOUNT = [' || C1%ROWCOUNT || ']');

  FETCH C1 INTO V1, V2;

  DBMS_OUTPUT.PUT_LINE('<AFTER FETCH>');
  DBMS_OUTPUT.PUT_LINE('%ISOPEN   = [' || C1%ISOPEN   || ']');
  DBMS_OUTPUT.PUT_LINE('%FOUND    = [' || C1%FOUND    || ']');
  DBMS_OUTPUT.PUT_LINE('%NOTFOUND = [' || C1%NOTFOUND || ']');
  DBMS_OUTPUT.PUT_LINE('%ROWCOUNT = [' || C1%ROWCOUNT || ']');



  CLOSE C1;
  DBMS_OUTPUT.PUT_LINE('<AFTER CLOSE>>');
  DBMS_OUTPUT.PUT_LINE('%ISOPEN   = [' || C1%ISOPEN   || ']');
  DBMS_OUTPUT.PUT_LINE('%FOUND    = [' || C1%FOUND    || ']');
  DBMS_OUTPUT.PUT_LINE('%NOTFOUND = [' || C1%NOTFOUND || ']');
  DBMS_OUTPUT.PUT_LINE('%ROWCOUNT = [' || C1%ROWCOUNT || ']');
END;
/
<BEFORE OPEN>
%ISOPEN   = [FALSE]
%FOUND    = []
%NOTFOUND = []
%ROWCOUNT = []
<AFTER OPEN>
%ISOPEN   = [TRUE]
%FOUND    = []
%NOTFOUND = []
%ROWCOUNT = [0]
<AFTER FETCH>
%ISOPEN   = [TRUE]
%FOUND    = [TRUE]
%NOTFOUND = [FALSE]
%ROWCOUNT = [1]
<AFTER CLOSE>>
%ISOPEN   = [FALSE]
%FOUND    = []
%NOTFOUND = []
%ROWCOUNT = []

Anonymous PL block executed.
```

<a id="f8c33e4aa9bfacf9"></a>
## IMPLICIT_CURSOR_ATTRIBUTES

Implicit cursor는 PSM statement를 통해 데이터베이스 내부적으로 처리된 cursor이며 explicit cursor가 가진 attributes와 이름이 같은 attributes를 가진다.   
자세한 내용은 다음 표를 참조한다.

**Implicit cursor attributes**

<a id="dc4bfdfe70777471"></a>
| Attribute name | 반환 타입 | 설명 |
| --- | --- | --- |
| ISOPEN | BOOLEAN | 내부적으로 close되므로 항상 FALSE이다. |
| FOUND | BOOLEAN | 직전 statement에 의해 데이터가 반환된 경우에는 TRUE이고, 그렇지 않을 경우에는 FALSE이다. |
| NOTFOUND | BOOLEAN | FOUND와 반대되는 값을 갖는다. |
| ROWCOUNT | INTEGER | 직전 statement에 의해 영향 받은 row의 개수이다. |

다음은 implicit cursor attributes의 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.


gSQL> INSERT INTO T1 VALUES ('Seoul', '24');

1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');

1 row created.


gSQL> DECLARE
V1 INTEGER;
BEGIN
    SELECT COUNT(*) INTO V1 FROM T1;
    DBMS_OUTPUT.PUT_LINE('COUNT RET    = ' || V1);
    DBMS_OUTPUT.PUT_LINE('SQL%ISOPEN   = ' || SQL%ISOPEN);
    DBMS_OUTPUT.PUT_LINE('SQL%FOUND    = ' || SQL%FOUND);
    DBMS_OUTPUT.PUT_LINE('SQL%NOTFOUND = ' || SQL%NOTFOUND);
    DBMS_OUTPUT.PUT_LINE('SQL%ROWCOUNT = ' || SQL%ROWCOUNT);
END;
/
COUNT RET    = 2
SQL%ISOPEN   = FALSE
SQL%FOUND    = TRUE
SQL%NOTFOUND = FALSE
SQL%ROWCOUNT = 1

Anonymous PL block executed.
```

<a id="71c2283761c90530"></a>
## CURSOR VARIABLES

Cursor variable은 explicit cursor와 유사한 개념이다. 하지만 explicit cursor가 한 개의 statement에 종속적인 반면, cursor variable은 한 개 이상의 cursor를 가리키는 pointer와 같은 역할을 한다. 즉, 한 개의 cursor variable을 이용하여 N 개의 SQL syntax를 변경해가며 cursor를 사용할 수 있다.

- Explicit cursor와의 차이점은 다음과 같다.
    - 한 개 이상의 SELECT 질의를 변경하며 cursor로 처리할 수 있다.
    - Cursor variable 간에 assign 할 수 있다.
    - Expression 내에서 사용할 수 있다.
    - Subprogram과 schema-level procedure/ function의 parameter로 사용할 수 있다.
    - Parameter를 가질 수 없다.

Cursor variable을 통해 open 된 cursor가 선언된 SCOPE를 벗어나면 자동으로 close 된다. 하지만 subprogram과 schema_level procedure/ function의 parameter로 사용된 경우에는, 해당 procedure/ function을 종료하더라도 호출한 곳의 SCOPE를 벗어날 때까지는 유효한 상태를 유지한다.

> Cursor variable을 parameter로 사용하려면 해당 parameter의 binding-mode는 반드시 OUT이나 IN OUT으로 선언되어야 한다.

Cursor variable도 explicit cursor와 동일한 형태의 cursor attributes를 사용할 수 있다.

```
DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);

  cv1 SYS_REFCURSOR;
BEGIN
  DBMS_OUTPUT.PUT_LINE('Before Open');
  DBMS_OUTPUT.PUT_LINE('ISOPEN   = ' || cv1%ISOPEN );
  DBMS_OUTPUT.PUT_LINE('FOUND    = ' || cv1%FOUND );
  DBMS_OUTPUT.PUT_LINE('NOTFOUND = ' || cv1%NOTFOUND );
  DBMS_OUTPUT.PUT_LINE('ROWCOUNT = ' || cv1%ROWCOUNT );

  OPEN cv1 FOR SELECT * FROM T1;

  DBMS_OUTPUT.PUT_LINE('After Open');
  DBMS_OUTPUT.PUT_LINE('ISOPEN   = ' || cv1%ISOPEN );
  DBMS_OUTPUT.PUT_LINE('FOUND    = ' || cv1%FOUND );
  DBMS_OUTPUT.PUT_LINE('NOTFOUND = ' || cv1%NOTFOUND );
  DBMS_OUTPUT.PUT_LINE('ROWCOUNT = ' || cv1%ROWCOUNT );

  FETCH cv1 INTO V1, V2;

  DBMS_OUTPUT.PUT_LINE('After fetch');
  DBMS_OUTPUT.PUT_LINE('ISOPEN   = ' || cv1%ISOPEN );
  DBMS_OUTPUT.PUT_LINE('FOUND    = ' || cv1%FOUND );
  DBMS_OUTPUT.PUT_LINE('NOTFOUND = ' || cv1%NOTFOUND );
  DBMS_OUTPUT.PUT_LINE('ROWCOUNT = ' || cv1%ROWCOUNT );
  
END;
/
Before Open
ISOPEN   = FALSE
FOUND    = 
NOTFOUND = 
ROWCOUNT = 
After Open
ISOPEN   = TRUE
FOUND    = 
NOTFOUND = 
ROWCOUNT = 0
After fetch
ISOPEN   = TRUE
FOUND    = TRUE
NOTFOUND = FALSE
ROWCOUNT = 1

Anonymous PL block executed.
```

Cursor variable은 다음과 같이 subprogram과 schema-level procedure/ function의 parameter로 사용할 수 있다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.


gSQL> INSERT INTO T1 VALUES ('Seoul', '24');

1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');

1 row created.




gSQL> DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);

  cv1 SYS_REFCURSOR;

  PROCEDURE PROC1 ( A_CV1 IN OUT SYS_REFCURSOR )
  IS
  BEGIN
```

- 입력 parameter cursor variable을 사용하여 cursor를 open한다.

```
OPEN A_CV1 FOR SELECT * FROM T1;
  END;

BEGIN

  PROC1( cv1 );
```

- Parameter로 사용된 cursor variable을 이용하여 fetch한다.

```
FETCH cv1 INTO V1, V2;

  DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);
  
END;
/
V1 = Seoul , V2 = 24

Anonymous PL block executed.
```

자세한 내용은 [Cursor Variable Declaration](28-psm-language-element-references.md#f8e7f57ff1b9e79e)을 참조한다.

<a id="2e69168fd9281e3d"></a>
### OPEN and Close Cursor Variables

PSM 내에서 OPEN FOR statement를 사용하면 cursor variable을 통해 cursor를 OPEN 할 수 있다. 또한, explicit cursor와 동일하게 CLOSE statement를 통해 cursor variable의 cursor를 CLOSE 할 수도 있다.

OPEN FOR statement를 통해 cursor를 실행할 시점에 cursor variable에 이미 열려 있는 cursor가 있을 경우, 해당 cursor는 자동으로 close 되며 새로운 상태의 cursor가 OPEN된다.

다음은 cursor variable을 사용하는 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.


gSQL> INSERT INTO T1 VALUES ('Seoul', '24');

1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');

1 row created.


gSQL> DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);

  cv1 SYS_REFCURSOR;
BEGIN
  OPEN cv1 FOR SELECT * FROM T1;
```

- Fetch with cursor-variable

```
FETCH cv1 INTO V1, V2;
  
  DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);

  CLOSE cv1;
END;
/
V1 = Seoul , V2 = 24

Anonymous PL block executed.
```

자세한 내용은 [OPEN FOR Statement](28-psm-language-element-references.md#3ba74406e2b4860c), [CLOSE Statement](28-psm-language-element-references.md#69270ed5b2e896c8)를 참조한다.

<a id="43ddec992f2cf67d"></a>
### Fetching Data With Cursor Variables

Explicit cursor와 동일하게 fetch statement를 통해 데이터베이스에서 처리된 결과를 PSM 변수로 저장할 수 있다.  
자세한 내용은 [FETCH Statement](28-psm-language-element-references.md#f182af65649d3610)를 참조한다.

<a id="008f6d1981947ce2"></a>
### Assign Values to Cursor Variables

Cursor variable은 RETURN-TYPE이 동일한 경우에 서로 assign할 수 있다. Cursor variable type이 아닌 경우에는 오류가 발생한다.

다음과 같은 assign statement로 수행한다.

```
target_cursor_variable := source_cursor_variable
```

Cursor variable을 assign 하면 target_cursor_variable이 가리키는 cursor pointer가 Source_cursor_variable이 가진 cursor를 가리키게 된다. 따라서 정상적으로 assign된 이후에는 target cursor variable에 이미 열려 있는 cursor는 유효하지 않으며 접근도 할 수 없다. 또한 cursor는 cursor variable이 선언된 SCOPE를 벗어날 때 내부적으로 정리된다.

```
DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);

  cv1 SYS_REFCURSOR;
  cv2 SYS_REFCURSOR;

BEGIN
```

- Open cv1

```
OPEN cv1 FOR SELECT * FROM T1;
```

- Assign cv1 to cv2

```
cv2 := cv1;
```

- Fetch from cv2

```
FETCH cv2 INTO V1, V2;

  DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);
  
END;
/
V1 = Seoul , V2 = 24
```

다음은 각각의 cursor variable이 OPEN을 수행한 후에 assign에 의해 동일한 cursor를 사용하는 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);
Table created.

gSQL> INSERT INTO T1 VALUES ('Seoul', '24');
1 row created.

gSQL> INSERT INTO T1 VALUES ('Pusan', '44');
1 row created.

gSQL> DECLARE
  cv1 SYS_REFCURSOR;
  cv2 SYS_REFCURSOR;
  v1 t1%ROWTYPE;
BEGIN
```

- 각각의 cursor variable이 cursor를 OPEN한다.

```
OPEN cv1 FOR select * from t1 where c1 = 'Seoul';
OPEN cv2 FOR select * from t1 where c1 = 'Pusan';
```

- Assign cursor-variable
- cv2의 cursor는 더 이상 유효하지 않다.

```
cv2 := cv1;
```

- cv1의 결과를 fetch한다.

```
FETCH cv2 INTO v1;
  
  DBMS_OUTPUT.PUT_LINE('C1 = ' || V1.C1 || ' , C2 = ' || V1.C2);
END;
/
C1 = Seoul , C2 = 24

Anonymous PL block executed.
```

---

[← 23. PSM Control Statements](23-psm-control-statements.md) · [전체 목차](../README.md) · [25. Using PSM Subprograms →](25-using-psm-subprograms.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
