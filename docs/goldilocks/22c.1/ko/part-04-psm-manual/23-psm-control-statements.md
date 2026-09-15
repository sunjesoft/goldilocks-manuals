<a id="c89a8103d27ef960"></a>

# 23. PSM Control Statements

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/c89a8103d27ef960)  
> 태그: `22c.1_10_tag`

[← 22. PSM DataTypes](22-psm-datatypes.md) · [전체 목차](../README.md) · [24. PSM Cursor Statements →](24-psm-cursor-statements.md)

<a id="408294c009a01065"></a>
## Assignment

Assignment 연산자(':=')를 사용하여 왼쪽 변수에 오른쪽 expression이 계산된 결과 값을 왼쪽 변수에 삽입한다.

<a id="11c9f93d7a226dc0"></a>
### Assignment Target

Assignment 연산자의 왼쪽에는 assignment 대상이 위치하는데 여기에 올 수 있는 item들은 다음과 같다.

- 변수 (IN 타입이 아닌 procedure나 함수의 인자 포함)
- '?' 나 ':V1' 과 같은 바인드 parameter (Anonymous PL block에서만 사용 가능)

<a id="482d8c8c6eadf088"></a>
### Assigning Expression

Assignment 연산자의 오른쪽에는 PSM에서 사용 가능한 expression이 올 수 있다. PSM의 expression에서 사용 가능한 표현식들은 다음과 같다.

- 상수
- GOLDILOCKS SQL에서 제공하는 모든 연산자, built-in 함수 또는 pseudo column들
- IN 또는 IN OUT 타입으로 바인드 된 바인드 parameter (Anonymous PL block에서만 사용 가능 )
- PSM 변수
- PSM nested 함수
- Schema-level 함수

아래는 각 유형별 assignment 구문의 예이다.

```
CREATE OR REPLACE FUNCTION ADD_TEN( A1 INTEGER )
RETURN INTEGER
IS
BEGIN
  RETURN A1 + 10;
END;
/
COMMIT;

DECLARE
  FUNCTION ADD_ONE( A1 INTEGER )
  RETURN INTEGER
  IS
  BEGIN
    RETURN A1 + 1;
  END;
  V_NUM INTEGER;
  V_STR VARCHAR(10);
BEGIN
  V_NUM := 10;                  ❶ Numeric literal
  V_STR := 'ABC';               ❷ String literal
  :V_PARAM := V_STR || 'DEF';   ❸ PSM variable, SQL operator 
  V_NUM := ADD_ONE( 100 ) + ADD_TEN( 1000 );  
                                ❹ Nested function, schema-level function
END;
/
```

다음 표현식들은 PSM의 expression에서 사용할 수 없다.

- 테이블, view나 해당 객체의 column
- 인덱스, 시퀀스, 동의어 (synonym) 등의 SQL 객체
- Subquery
- Nested procedure
- Schema-level procedure

다음은 잘못된 expression을 사용하여 에러가 발생하는 예이다.

```
gSQL> CREATE SEQUENCE SEQ1;

Sequence created.

gSQL> COMMIT;

Commit complete.

gSQL> DECLARE
  V1 INTEGER;
BEGIN
  V1 := SEQ1.NEXTVAL;
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (4:9): ERR-42000(16074): sequence number not allowed here
```

PSM expression에서 사용할 수 없는 종류의 객체 값을 할당하려면 다음과 같이 SELECT INTO 구문을 사용하여야 한다.

```
gSQL> DECLARE
  V1 INTEGER;
BEGIN
  SELECT SEQ1.NEXTVAL INTO V1 FROM DUAL;
END;
/

Anonymous PL block executed.
```

<a id="d50747074cc2c912"></a>
### Assignment 호환성

Assignment 구문의 expression을 사용할 수 있는 구문이라도 target 타입과 expression의 최종 결과 타입에 따라 성공할 수도 있고 실패할 수도 있다. Target의 타입에 따라 사용 가능한 expression 타입은 다음과 같다.

**Assignment 호환성**

<a id="c2dee2ee398fe8ba"></a>
| Target 타입 | Expression 최종 결과 타입 |
| --- | --- |
| Scalar 타입  * Scalar 타입 변수 * 레코드 타입 변수의 특정 필드 * Key값을 가지는 collection 변수의 scalar element | Target의 타입으로 conversion 가능한 값을 가진 scalar 타입인 경우에만 허용된다. |
| Attribute 레코드 타입 (%ROWTYPE) | 필드의 개수가 같고, 각 필드값이 target의 해당 순번의 필드로 conversion 가능한 경우에만 허용된다. |
| 사용자 정의 레코드 타입 | 정확하게 같은 타입만 허용된다. |
| Collection 타입 * Key 값이 명시되지 않은 collection 타입 변수 | 정확하게 같은 타입만 허용된다. |

내부 구조가 같은 사용자 정의 레코드 타입 변수이더라도 타입 이름이 다르면 다음과 같은 오류가 발생한다.

```
gSQL> DECLARE
  TYPE MY_REC1 IS RECORD ( F1 INTEGER := 1, F2 VARCHAR(10) := 'AAA' );
  TYPE MY_REC2 IS RECORD ( F1 INTEGER := 1, F2 VARCHAR(10) := 'AAA' );
  V1 MY_REC1;
  V2 MY_REC2;
BEGIN
  V2 := V1; 
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (7:9): ERR-HY000(17007): invalid expression
```

그 외에 target이 IN 속성으로 정의된 인자 변수이거나 IN 속성으로 바인딩 된 바인드 parameter인 경우에도 오류가 발생한다.

```
gSQL> DECLARE
  FUNCTION ADD_ONE( A1 IN INTEGER )
  RETURN INTEGER
  IS
  BEGIN
    A1 := A1 + 1;
    RETURN A1;
  END;
  V1 INTEGER;
BEGIN
  V1 := ADD_ONE( 10 );
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (6:5): ERR-HY000(17024): (A1) cannot be used as assignment target
```

Assignment 호환성 규칙은 함수나 procedure를 호출하는 중에 actual parameter 값을 formal parameter 변수로 할당할 때도 동일하게 적용된다.

<a id="3be739d885e1b712"></a>
## PL Block

PL block은 PSM을 구성하는 가장 기본적인 단위이다. PL block은 다른 PL block 안에 다시 nested 될 수 있으며, PL block 안에서 선언된 item들은 모두 해당 block의 범위 내에서만 (하위 block 포함) 참조할 수 있다.

<a id="204c1dd525c3f07d"></a>
### PL Block의 구성

한 개의 PL block은 다음과 같이 세 부분으로 나누어진다.  
자세한 내용은 [Block (BEGIN .. END)](28-psm-language-element-references.md#715afecb623f3a43)를 참조한다.

```
[DECLARE 
❶ 선언부 (Declarative Part)]
BEGIN 
❷ Statements
[EXCEPTION 
❸ Handlers]
END;
```

<a id="bb3da87738683b53"></a>
#### 선언부 (Declarative Part)

선언부는 PL block 내부에서 사용할 지역 (local) item들을 선언하는 구역이다. 선언할 지역 변수 등의 item이 없을 경우에는 선언부에 대한 정의 없이 executable part로 시작된다.

선언부에서 선언될 수 있는 지역 item들은 다음과 같다.

- 변수 ([PSM DataTypes](22-psm-datatypes.md#c817fd8d823748a3) 참조)
- 사용자 정의 타입
- 커서
- Nested 함수 또는 procedure (subprogram)
- 사용자 정의 exception

하나의 PL block 내에서 선언된 모든 item들의 이름은 종류에 관계없이 unique 해야 한다. 예를 들어 변수와 같은 이름의 커서는 선언할 수 없다.

```
gSQL> DECLARE
  C1 INTEGER;
  CURSOR C1 IS SELECT * FROM DUAL;
BEGIN
  OPEN C1;
  FETCH C1 INTO C1;
  CLOSE C1;
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (3:10): ERR-HY000(17027): duplicated identifier
(2) at (5:8): ERR-HY000(17031): mismatch identifier type
(3) at (6:9): ERR-HY000(17031): mismatch identifier type
(4) at (7:9): ERR-HY000(17031): mismatch identifier type
```

단, 하위 PL block에서는 상위 PL block에 선언된 item과 이름이 같은 item을 선언할 수 있다. 이 때 해당 이름은 현재 위치에서 상위 block 방향으로 탐색할 때 가장 먼저 발견되는 item을 가리킨다.

```
gSQL> <<PP>>
DECLARE    ❶ Parent scope begin
  V1 VARCHAR(10) := 'AAA';
BEGIN
  <<CC>>
  DECLARE  ❷ Child scope begin
    V1 INTEGER := 99;
  BEGIN
    DBMS_OUTPUT.PUT_LINE( 'PP.V1 = ' || PP.V1 ); 
    DBMS_OUTPUT.PUT_LINE( 'CC.V1 = ' || CC.V1 ); 
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 ); 
  END;     ❸ Child scope end
END;       ❹ Parent scope end
/

PP.V1 = AAA
CC.V1 = 99
V1 = 99

Anonymous PL block executed.
```

<a id="9dd1f1434a52addc"></a>
#### 실행부 (Executable Part)

실행부에서는 선언된 item들을 조작하고, 포함하고 있는 여러 statement들을 수행한다. 실행부에 올 수 있는 statement 종류는 다음과 같다.

- Control statements ([PSM Control Statements](#c89a8103d27ef960) 참조)
- Cursor statements ([PSM Cursor Statements](24-psm-cursor-statements.md#22c487869568c7ce) 참조)
- SQL statements (Static/ dynamic) ([Using SQLs In PSM](26-using-sqls-in-psm.md#62e118512d69c410) 참조)

<a id="56e6e13585ccdc3e"></a>
#### 예외 처리부 (Exception Handling Part)

실행 중 발생되는 여러가지 예외 (exception)들을 처리할 handler들을 정의한다.

실행부의 여러 statement들을 수행하는 도중에 exception이 발생하면 해당 PL block 위치부터 상위 PL block으로 가면서 발생한 exception을 처리할 handler가 등록된 곳이 있는지 탐색한다. 만일 존재할 경우, 해당 handler의 내용을 수행한 후 exception 발생 상태를 초기화한다.

```
DECLARE
  V1 INTEGER;
BEGIN
  SELECT C1 INTO V1 FROM T1 WHERE C1 = 100;
EXCEPTION 
  WHEN NO_DATA_FOUND THEN
    DBMS_OUTPUT.PUT_LINE('SQL%ISOPEN   = ' || SQL%ISOPEN);
    DBMS_OUTPUT.PUT_LINE('SQL%FOUND    = ' || SQL%FOUND);
    DBMS_OUTPUT.PUT_LINE('SQL%NOTFOUND = ' || SQL%NOTFOUND);
    DBMS_OUTPUT.PUT_LINE('SQL%ROWCOUNT = ' || SQL%ROWCOUNT);
END;
/
```

만일 최상위 PL block까지 탐색한 후에도 적당한 handler를 발견하지 못할 경우, 발생한 exception이 caller에게 반환되며 종료된다

```
gSQL> DECLARE
  v1 INTEGER;
BEGIN
  v1 := 1/ 0;
END;
/

ERR-HY000(17007): invalid expression : 
  v1 := 1/ 0;
        *
ERROR at line 4:
ERR-22012(12122): divisor is equal to zero
```

사용자 정의 exception 선언, built-in handler의 종류 및 handler의 설치 등에 대한 자세한 내용은 [Error Handling](#c9b397839c9e89d1)을 참조한다.

<a id="b51120d93c66981a"></a>
## NULL Statement

PSM 내에서 no-op와 같이 아무런 역할도 하지 않는 statement를 명시할 때 사용한다.   
자세한 내용은 [NULL Statement](28-psm-language-element-references.md#1e6426bab08f582c)를 참조한다.

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  IF V1 < 10 THEN
    V1 := V1 + 1;
  ELSE
    NULL;  -- do nothing
  END IF;
END;
/
```

<a id="4ce913a9f6f4aa84"></a>
## Testing Conditions

조건 분기 구문들은 주어진 조건의 TRUE/ FALSE에 따라 statement들을 수행한다. GOLDILOCKS PSM은 IF와 CASE의 두 가지 조건 분기 구문을 제공한다.

<a id="6b8b122c06fe21f6"></a>
### IF

IF 구문은 주어진 expression의 조건들 중 TRUE인 것들에 해당하는 statement들을 수행한다. Expression 조건들은 IF, ELSIF 다음에 기술할 수 있다. 실행할 때 기술된 순서대로 조건을 검사하여 해당 expression의 조건이 TRUE인 경우, THEN 절 이하의 statement들을 수행한다. 모든 IF 조건이나 ELSIF 조건이 거짓이고 ELSE 절이 기술되었을 경우에는 ELSE 절 이하의 statement들이 수행된다.

IF 구문은 항상 END IF 키워드로 종료된다.   
자세한 내용은 [IF Statement](28-psm-language-element-references.md#44c5e8d593928e53)를 참조한다.

```
DECLARE
V1 INTEGER := 1;
BEGIN
  -- IF COND
  IF V1 > 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'IF COND' );
  ELSIF V1 = 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'ELSIF COND' );
  ELSE
    DBMS_OUTPUT.PUT_LINE( 'ELSE COND' );
  END IF; 

  -- ELSIF COND
  IF V1 = 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'IF COND' );
  ELSIF V1 > 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'ELSIF COND' );
  ELSE
    DBMS_OUTPUT.PUT_LINE( 'ELSE COND' );
  END IF; 

  -- ELSE COND
  IF V1 = 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'IF COND' );
  ELSIF V1 < 0 THEN
    DBMS_OUTPUT.PUT_LINE( 'ELSIF COND' );
  ELSE
    DBMS_OUTPUT.PUT_LINE( 'ELSE COND' );
  END IF; 
END;
/
```

ELSIF 절이나 ELSE 절은 선택사항이므로 기술될 수도 있고 기술되지 않을 수도 있다.

ELSE 절이 기술되지 않고 IF나 ELSIF의 모든 조건이 true가 아닐 경우에는 어떤 statement도 수행하지 않고 exception 발생없이 다음 statement로 진행된다.

<a id="ef1fa08ebd089208"></a>
### CASE

CASE 문은 IF 문과 같은 여러 statement들이 배열된 것들 중에서 한 개 배열을 선택하여 수행한다. CASE 문은 END CASE 키워드로 종료되며, ELSE 절은 선택사항이므로 기술될 수도 있고 기술되지 않을 수도 있다.

적당한 조건을 가진 WHEN 절을 찾을 수 없고 ELSE 절이 기술되어 있을 경우, ELSE 절 이하의 statement 배열을 수행한다. 적당한 조건이 없고 ELSE 절이 기술되어 있지 않은 경우, CASE_NOT_FOUND exception이 발생한다.   
자세한 내용은 [CASE Statement](28-psm-language-element-references.md#d646c443f9233d8a)를 참조한다.

CASE의 WHEN 절들은 기술된 순서대로 evaluate되며, 적당한 WHEN 절을 찾아서 해당 WHEN 절의 statement 배열이 수행되면 그 다음에 기술된 모든 WHEN 절은 무시된다.

CASE 문에는 다음과 같은 두 가지 형태가 있다.

- Simple CASE statement
- Searched CASE statement

<a id="46cb57d3fe28cce6"></a>
#### Simple CASE Statement

Simple CASE statement는 CASE 키워드 다음에 기술된 selector expression을 사용하여 WHEN 절 이후에 기술된 expression들 중에 selector expression과 같은 값을 가지는 WHEN절의 statement 배열을 수행한 후 종료한다.

```
DECLARE
V1 VARCHAR(1) := '2';
BEGIN
  CASE V1 WHEN '0' THEN DBMS_OUTPUT.PUT_LINE ('Result = 0');
          WHEN '1' THEN DBMS_OUTPUT.PUT_LINE ('Result = 1');
          WHEN '2' THEN DBMS_OUTPUT.PUT_LINE ('Result = 2');
          ELSE DBMS_OUTPUT.PUT_LINE ('Result = Other');
  END CASE;
END;
/
```

<a id="239e489c0c408f55"></a>
#### Searched CASE Statement

Searched CASE statement에는 selector expression을 가지지 않는 대신 각 WHEN 절마다 boolean 타입으로 evaluate되는 조건 expression이 기술된다. 실행할 때는 각 WHEN 절의 expression을 evaluate하여 TRUE가 되는 첫 WHEN절이 보유한 statement를 배열한 후에 종료한다.

```
DECLARE
V1 VARCHAR(1) := '2';
BEGIN
  CASE WHEN V1 = 0 THEN DBMS_OUTPUT.PUT_LINE ('Result = 0');
       WHEN V1 = 1 THEN DBMS_OUTPUT.PUT_LINE ('Result = 1');
       WHEN V1 = 2 THEN DBMS_OUTPUT.PUT_LINE ('Result = 2');
       ELSE DBMS_OUTPUT.PUT_LINE ('Result = OTHER');
  END CASE;
END;
/
```

<a id="ec8c69af942202d3"></a>
## Iterative Control

Iterative control 구문들은 일련의 statement들을 여러 번 수행한다. GOLDILOCKS PSM에서 제공하는 iterative control 구문의 종류는 다음과 같다.

- Basic loop
- FOR loop
- WHILE loop

<a id="09eef2516c2fe94c"></a>
### Basic Loop

Basic loop 구문은 LOOP와 END LOOP 키워드로 반복 수행할 일련의 statement들을 감싸고 있다. 이 구문은 내부의 statement들을 무한 반복하여 수행하며, sequential control 구문인 EXIT나 GOTO 구문을 이용하여 loop 밖으로 탈출할 수 있다.   
자세한 내용은 [Basic LOOP Statement](28-psm-language-element-references.md#2d30a62c1a28081c)를 참조한다.

다음은 EXIT WHEN 구문을 사용하여 해당 위치에서 가장 가까운 scope를 가지는 basic loop를 탈출하는 예이다.  
자세한 내용은 [EXIT Statement](28-psm-language-element-references.md#ee87bcf9b6f42397)를 참조한다.

```
gSQL> DECLARE
  V1 INTEGER := 1;
BEGIN
  LOOP
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    V1 := V1 + 1;
    EXIT WHEN V1 > 10;   -- Escape Condition
  END LOOP;
END;
/

V1 = 1
V1 = 2
V1 = 3
V1 = 4
V1 = 5
V1 = 6
V1 = 7
V1 = 8
V1 = 9
V1 = 10

Anonymous PL block executed.
```

여러 loop가 중첩되어 있는 상황에서 특정 loop 밖으로 탈출하려면 루프 앞에 label을 명시하고 EXIT 구문에서 해당 label을 target label로 명시하면 된다.

```
gSQL> DECLARE
  V1 INTEGER := 1;
BEGIN
  <<OUTER_LOOP>>
  LOOP
    <<INNER_LOOP>>
    LOOP
      DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
      V1 := V1 + 1;
      EXIT OUTER_LOOP WHEN V1 > 5;  -- Escape Condition
    END LOOP INNER_LOOP;
    DBMS_OUTPUT.PUT_LINE( 'END OF INNER LOOP' );
    V1 := V1 + 5;
  END LOOP OUTER_LOOP;
  DBMS_OUTPUT.PUT_LINE( 'END OF OUTER LOOP' );
END;
/

V1 = 1
V1 = 2
V1 = 3
V1 = 4
V1 = 5
END OF OUTER LOOP

Anonymous PL block executed.
```

<a id="02c3f3c7f96c8b37"></a>
### FOR Loop

FOR loop 구문은 주어진 범위의 정수 개수 만큼 일련의 statement들을 반복 수행한다.   
자세한 내용은 [FOR LOOP Statement](28-psm-language-element-references.md#93d148b1c6bc7048)를 참조한다.

사용자가 FOR 키워드 뒤에 명시한 이름으로 인덱스 변수를 생성한다.  
그리고 IN 키워드 뒤의 범위 연산자 (..) 왼쪽에 명시된 하한값을 그 인덱스 변수의 초기값으로 하여 범위 연산자 (..) 오른쪽에 명시된 상한값과 같아질 때까지 loop 한 번당 인덱스 변수를 1씩 증가시켜 주어진 일련의 statement들을 수행한다.

```
BEGIN
  FOR I IN 0 .. 2 LOOP
    DBMS_OUTPUT.PUT_LINE( 'I = ' || I );
  END LOOP;
END;
/

I = 0
I = 1
I = 2

Anonymous PL block executed.
```

REVERSE 키워드를 명시할 경우, 범위 연산자 (..) 오른쪽에 명시된 상한값을 인덱스 변수의 초기값으로 하여, 범위 연산자 (..) 왼쪽에 명시된 하한값과 같아질 때까지 인덱스 변수를 1씩 감소시키며 loop를 수행한다.

```
BEGIN
  FOR I IN REVERSE 0 .. 2 LOOP
    DBMS_OUTPUT.PUT_LINE( 'I = ' || I );
  END LOOP;
END;
/

I = 2
I = 1
I = 0

Anonymous PL block executed.
```

<a id="3137be988b2db9c7"></a>
### WHILE Loop

WHILE loop 구문은 주어진 조건이 TRUE인 동안 주어진 일련의 statement들을 반복해서 수행한다.  
자세한 내용은 [WHILE LOOP Statement](28-psm-language-element-references.md#5375d39b7c2ece2a)를 참조한다.

```
DECLARE
V1 integer := 0;
BEGIN
  WHILE V1 < 10 LOOP
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    V1 := V1 + 1;
  END LOOP;
END;
/
```

WHILE loop는 body의 statement들을 수행하기 전에 주어진 조건을 검사하기 때문에 시작 시점부터 조건이 거짓이면 body의 statement들이 한 번도 수행되지 않을 수도 있다.

<a id="da3833cc9de76be6"></a>
## Sequential Control

Sequential control 구문들은 프로그램 수행 위치를 현재 위치에서 다른 위치로 옮긴다.

GOLDILOCKS PSM에서는 다음과 같은 세 가지 sequential control 구문들을 제공한다

- GOTO
- CONTINUE
- EXIT

<a id="77567d421520e8b8"></a>
### GOTO

GOTO 구문은 수행 위치를 주어진 label이 있는 statement로 이동시킨다. Label의 PSM 내 실행 가능한 모든 statement 앞에 명시할 수 있다. GOTO가 이동하는 target label은 GOTO 구문의 이전이나 이후 모두에 존재할 수 있지만 현재 위치에서 visible한 statement인 경우에만 GOTO를 수행할 수 있다.  
자세한 내용은 [GOTO Statement](28-psm-language-element-references.md#f300f93309482f2d)를 참조한다.

Visible한 statement의 조건은 다음과 같다.

- 현재 수행 위치의 앞 뒤에 존재하는 sibling statement들
- 현재 위치의 상위 statement와 그 앞 뒤에 존재하는 sibling statement들

다음은 현재 위치의 sibling statement로 이동하는 예이다.

```
gSQL> BEGIN

  <<PARENT_PREV>>
  DBMS_OUTPUT.PUT_LINE('PARENT PREV');

  <<PARENT>>
  IF 1 > 0 THEN
    <<SIBLING_PREV>>
    DBMS_OUTPUT.PUT_LINE('SIBLING PREV');

    <<CURRENT_POSITION>>
    GOTO SIBLING_NEXT;

    DBMS_OUTPUT.PUT_LINE('SIBLINGS');
    DBMS_OUTPUT.PUT_LINE('SIBLINGS');

    <<SIBLING_NEXT>>
    DBMS_OUTPUT.PUT_LINE('SIBLING NEXT');
  ELSE
    <<NON_SIBLING>>
    DBMS_OUTPUT.PUT_LINE('NON SIBLING');
  END IF;

  <<PARENT_NEXT>>
  DBMS_OUTPUT.PUT_LINE('PARENT NEXT');

END;
/

PARENT PREV
SIBLING PREV
SIBLING NEXT
PARENT NEXT

Anonymous PL block executed.
```

다음은 현재 위치의 상위 statement로 이동하는 예이다.

```
gSQL> BEGIN

  <<PARENT_PREV>>
  DBMS_OUTPUT.PUT_LINE('PARENT PREV');

  <<PARENT>>
  IF 1 > 0 THEN
    <<SIBLING_PREV>>
    DBMS_OUTPUT.PUT_LINE('SIBLING PREV');

    <<CURRENT_POSITION>>
    GOTO PARENT_NEXT;

    DBMS_OUTPUT.PUT_LINE('SIBLINGS');
    DBMS_OUTPUT.PUT_LINE('SIBLINGS');

    <<SIBLING_NEXT>>
    DBMS_OUTPUT.PUT_LINE('SIBLING NEXT');
  ELSE
    <<NON_SIBLING>>
    DBMS_OUTPUT.PUT_LINE('NON SIBLING');
  END IF;

  <<PARENT_NEXT>>
  DBMS_OUTPUT.PUT_LINE('PARENT NEXT');

END;
/

PARENT PREV
SIBLING PREV
PARENT NEXT

Anonymous PL block executed.
```

다음은 sibling이 아닌 statement로 이동하려다 오류가 발생하는 예이다.

```
gSQL> BEGIN

  <<PARENT_PREV>>
  DBMS_OUTPUT.PUT_LINE('PARENT PREV');

  <<PARENT>>
  IF 1 > 0 THEN
    <<SIBLING_PREV>>
    DBMS_OUTPUT.PUT_LINE('SIBLING PREV');

    <<CURRENT_POSITION>>
    GOTO NON_SIBLING;

    DBMS_OUTPUT.PUT_LINE('SIBLINGS');
    DBMS_OUTPUT.PUT_LINE('SIBLINGS');

    <<SIBLING_NEXT>>
    DBMS_OUTPUT.PUT_LINE('SIBLING NEXT');
  ELSE
    <<NON_SIBLING>>
    DBMS_OUTPUT.PUT_LINE('NON SIBLING');
  END IF;

  <<PARENT_NEXT>>
  DBMS_OUTPUT.PUT_LINE('PARENT NEXT');

END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (12:10): ERR-HY000(17010): can not find label name
```

마찬가지로 현재 statement의 상위 sibling이 아닌 statement로 이동하려 해도 오류가 발생한다.

GOTO는 PSM 프로그램 로직을 유연하게 만들어 줄 수 있는 좋은 도구이다. 하지만 다른 언어에서와 마찬가지로 너무 많이 사용할 경우 가독성이 떨어져서 유지 보수가 힘들어질 수 있다. 따라서 일반적인 로직들은 FOR나 WHILE 등의 loop 구문을 사용하고, GOTO는 반드시 필요한 경우에만 사용하는 것이 좋다.

<a id="87d5c144a9f0d263"></a>
### CONTINUE

CONTINUE 구문은 FOR나 WHILE 등의 loop 구문 내에서 현재 iteration을 종료하고 다음 iteration을 시작한다.   
자세한 내용은 [CONTINUE Statement](28-psm-language-element-references.md#cfee583e513f9d6a)를 참조한다.

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  <<AAA>>
  WHILE V1 <= 10 LOOP
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    V1 := V1 + 1;
    IF V1 <= 2 THEN
      DBMS_OUTPUT.PUT_LINE( 'CONTINUE' );
      CONTINUE;
    ELSE
      EXIT;
    END IF;
    DBMS_OUTPUT.PUT_LINE( 'END-OF-WHILE' );
  END LOOP AAA;
END;
/
```

Target label이 기술된 경우에는 해당 label을 가지는 루프의 다음 iteration을 시작하고, 기술되지 않았을 경우에는 가장 가까운 (안쪽의) loop의 다음 iteration을 시작한다.

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  <<AAA>>
  FOR I IN 0..5 LOOP
    <<BBB>>
    WHILE V1 <= 10 LOOP
      DBMS_OUTPUT.PUT_LINE( 'I = ' || I );
      DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
      V1 := V1 + 1;
      IF V1 <= 2 THEN
        CONTINUE BBB;
      ELSE
        EXIT AAA;
      END IF;
    END LOOP BBB;
  END LOOP AAA;
END;
/
```

CONTINUE 구문에는 선택적으로 WHEN 절을 기술할 수 있으며, 이 경우 WHEN 절 다음의 expression이 TRUE일 때만 현재 iteration을 끝내고 다음 iteration을 시작한다.

```
DECLARE
  V1 INTEGER :=0 ;
BEGIN
  LOOP
    V1 := V1 + 1;
    CONTINUE WHEN V1 < 5;
    EXIT;
  END LOOP;
END;
/
```

<a id="278d11f5c0b24297"></a>
### EXIT

EXIT 구문은 현재 loop를 탈출하여 그 다음 statement를 수행한다.   
자세한 내용은 [EXIT Statement](28-psm-language-element-references.md#ee87bcf9b6f42397)를 참조한다.

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  WHILE V1 <= 10 LOOP
    DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    IF V1 > 5 THEN
      EXIT;
    END IF;
    V1 := V1 + 1;
  END LOOP;
END;
/
```

Target loop가 기술된 경우, 해당 label을 가진 loop를 탈출한다.

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  <<AAA>>
  FOR I IN 0..5 LOOP
    <<BBB>>
    WHILE V1 <= 10 LOOP
      DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
      IF V1 >= 5 THEN
        EXIT AAA;
      END IF;
      V1 := V1 + 1;
    END LOOP BBB;
  END LOOP AAA;
END;
/
```

CONTINUE 구문과 마찬가지로 EXIT 구문에도 선택적으로 WHEN 절을 기술할 수 있으며, 이 경우 주어진 조건이 TRUE일 때만 EXIT를 수행한다.

```
DECLARE
  V1 INTEGER := 1;
BEGIN
  <<AAA>>
  FOR I IN 0..5 LOOP
    <<BBB>>
    WHILE V1 <= 10 LOOP
      DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
      EXIT AAA WHEN V1 >= 5;
      V1 := V1 + 1;
    END LOOP BBB;
  END LOOP AAA;
END;
/
```

<a id="c9b397839c9e89d1"></a>
## Error Handling

PSM에서 발생할 수 있는 error의 유형은 발생 시점에 따라 다음과 같이 분류할 수 있다.

- Errors at compile time
- Errors at run-time

<a id="b7a1a85299482bcc"></a>
### Errors at Compile Time

Compile error는 procedure/ function에 기술된 PSM statement를 validation 하는 과정에서 발생하는 오류를 출력한다.

Syntax 오류의 경우, 다음과 같이 첫 번째 발견된 syntax 오류의 위치만 출력하기 때문에 사용자는 수정 후에 다시 컴파일해서 다른 오류가 없는지 확인해야 한다.

```
CREATE OR REPLACE PROCEDURE PROC1
IS
BEGIN
  V1 = 1;
  V2 = 1;
END;
/

ERR-42000(40000): syntax error: 
  V1 = 1;
.....^
Error at line 4
```

Syntax 오류가 없으면 GOLDILOCKS가 PSM statement를 compile 하는 동안 validation 하는데 이 때 발생하는 오류들은 다음과 같이 출력된다.

```
CREATE OR REPLACE PROCEDURE PROC1
IS
BEGIN
  V1 := 1;
  V2 := 2;
END;
/

ERR-01000(16409): Warning: Routine definition has compilation errors
ERR-HY000(17032): PSM compilation error : 
(1) at (4:3): ERR-HY000(17006): unknown variable or column name (V1)
(2) at (5:3): ERR-HY000(17006): unknown variable or column name (V2)
Procedure created.
```

Compile error들은 GOLDILOCKS 자체의 에러 출력 버퍼가 허용하는 size 이내에서 오류 내역을 출력한다. 따라서, 출력되지 않은 오류가 있을 수 있다. 이 경우, 출력되지 않은 오류가 더 있다는 것을 다음과 같은 형태로 출력한다.

```
CREATE OR REPLACE PROCEDURE PROC1
IS
BEGIN
V1 := 1;
V2 := 2;
V3 := 2;
V4 := 2;
V5 := 2;
V6 := 2;
V7 := 2;
V8 := 2;
V10 := 2;
END;
/

ERR-01000(16409): Warning: Routine definition has compilation errors
ERR-HY000(17032): PSM compilation error :
(1) at (4:3): ERR-HY000(17006): unknown variable or column name (V1)
(2) at (5:3): ERR-HY000(17006): unknown variable or column name (V2)
(3) at (6:3): ERR-HY000(17006): unknown variable or column name (V3)
(4) at (7:3): ERR-HY000(17006): unknown variable or column name (V4)
(5) at (8:3): ERR-HY000(17006): unknown variable or column name (V5)
(6) at (9:3): ERR-HY000(17006): unknown variable or column name (V6)
(7) at (10:3): ERR-HY000(17006): unknown variable or column name (V7)
2 more errors...
```

에러 메시지는 다음과 같은 형태로 출력된다.

```
(Index) at (Line_Number : Column_Position): ERR-SQLState( Internal_ErrorCode): Detail_Error_Message
```

- Index
    - 에러가 발생한 순서를 의미한다.
- Line_Number
    - 에러가 발생한 source의 line 위치를 의미한다.
- Column_Position
    - 에러가 발생한 source의 column 위치를 의미한다.
- ERR-SQLState
    - 표준 SQLState를 의미한다.
- Internal_ErrorCode
    - 내부 에러코드이다.
- Detail_Error_Message
    - 에러 메시지의 상세 내역이다.

<a id="21ef0b7d75089755"></a>
### Errors at Run-time

정상적으로 PSM이 적용된 실행 시점에서도 다양한 이유로 PSM statement에서 오류가 발생할 수 있다. 이 경우 GOLDILOCKS는 exception handling 등을 제공하여 사용자가 오류를 제어할 수 있도록 한다.

다음은 실행 시점에 오류가 발생하는 예이다. GOLDILOCKS PMS 실행 시점에 오류가 발생하면 다음과 같이 에러가 발생한 위치와 함께 PSM 오류와 internal error를 함께 출력한다. 즉, 발생한 오류가 한 개 이상일 수 있으므로 사용자가 ODBC와 같은 개발 과정에서 정확한 오류 메시지를 확인하려면 SQLGetDiagRec와 같은 함수를 통해 모든 에러를 데이터베이스로부터 읽어들여야 한다.

```
DECLARE
  V1 INTEGER;
BEGIN
  V1 := 1 / 0;
END;
/

ERR-HY000(17007): invalid expression : 
  V1 := 1 / 0;
        *
ERROR at line 4:
ERR-22012(12122): divisor is equal to zero
```

PSM은 실행 시점에 오류가 발생하면 즉시 중단되고 사용자에게 오류를 알린다. 그러나 사용자가 이러한 오류를 직접 제어하고 프로그램을 계속 실행하고자 할 경우에는 exception handling을 해야 한다.

다음은 오류가 발생하는 위치를 exception handling을 하여 중단없이 사용자 프로그램이 수행되도록 정의한 예이다.

```
DECLARE
  V1 INTEGER;
BEGIN
  BEGIN
    V1 := 1 / 0;
  EXCEPTION WHEN OTHERS 
            THEN DBMS_OUTPUT.PUT_LINE('SQLCODE = ' || SQLCODE);
                 DBMS_OUTPUT.PUT_LINE('SQLERRM = ' || SQLERRM);
  END;
  
  DBMS_OUTPUT.PUT_LINE('next code');
END;
/
SQLCODE = -12122
SQLERRM = [SUNJESOFT][PSM][GOLDILOCKS]divisor is equal to zero
next code

Anonymous PL block executed.
```

자세한 내용은 [EXCEPTION Handling](#e3d3c92a2833b44e), [SQLCODE Function](28-psm-language-element-references.md#a3c80e9aecc87896), [SQLERRM Function](28-psm-language-element-references.md#2f66033fa0f14be9)을 참조한다.

<a id="227f3e995d1ec269"></a>
### Cursor Attributes

Cursor attributes는 PSM을 처리하는 과정에서 데이터베이스 내부나 사용자가 명시한 cursor의 상태를 알 수 있도록 제공되는 속성 (변수)을 의미한다.

- Cursor는 다음과 같이 분류된다.
    - Implicit cursor
        - 데이터베이스 내부에서 필요할 때 OPEN/ FETCH/ CLOSE 되는 cursor
    - Explicit cursor
        - 사용자가 명시적으로 declaration/ definition 한 후에 OPEN/ FETCH/ CLOSE 하는 cursor

<a id="8a6bb04ec3a2714d"></a>
#### Implicit Cursor Attributes

PSM에서 implicit cursor attributes는 직전에 수행한 SQL 문의 처리 상태를 알기 위해 사용된다. Attributes의 각 값들은 조건식과 같은 expression에 사용할 수 있기 때문에 사용자가 해당 값을 통해 프로그램의 로직을 분기하는 등의 제어가 가능하다.   
각 속성에 대한 자세한 내용은 다음 표를 참조한다.

**Implicit cursor attributes**

<a id="08615502ca1d5c92"></a>
| Attribute name | 반환 타입 | 설명 |
| --- | --- | --- |
| ISOPEN | BOOLEAN | 내부적으로 close 되므로 항상 FALSE 이다. |
| FOUND | BOOLEAN | 직전 statement에 의해 데이터가 반환된 경우에는 TRUE이고, 그렇지 않을 경우에는 FALSE 이다. |
| NOTFOUND | BOOLEAN | FOUND와 반대되는 값을 갖는다. |
| ROWCOUNT | INTEGER | 직전 statement에 의해 영향 받은 row의 개수이다. |

사용하는 구문의 형태는 다음과 같다.

```
SQL%Attribute_name

Attribute_name := ISOPEN | FOUND | NOTFOUND | ROWCOUNT
```

다음 예와 같이 각 속성을 확인할 수 있다.

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

gSQL> BEGIN
    UPDATE T1 SET C2 = C2 + 1;
  
    DBMS_OUTPUT.PUT_LINE('ISOPEN   = ' || SQL%ISOPEN );
    DBMS_OUTPUT.PUT_LINE('FOUND    = ' || SQL%FOUND );
    DBMS_OUTPUT.PUT_LINE('NOTFOUND = ' || SQL%NOTFOUND );
    DBMS_OUTPUT.PUT_LINE('ROWCOUNT = ' || SQL%ROWCOUNT );
END;
/
ISOPEN   = FALSE
FOUND    = TRUE
NOTFOUND = FALSE
ROWCOUNT = 2

Anonymous PL block executed.
```

<a id="2843e2fa5c4fc946"></a>
#### Explicit Cursor Attributes

Explicit cursor attributes는 explicit cursor의 상태를 조회하기 위해 사용된다.   
각 속성에 대한 자세한 내용은 다음 표를 참조한다.

**Cursor attributes**

<a id="a2a267629705d338"></a>
| 속성 | 반환 타입 | 설명 |
| --- | --- | --- |
| %ISOPEN | BOOLEAN | Cursor가 정상적으로 열려진 경우에만 TRUE이고 그 외에는 FALSE이다. |
| %FOUND | BOOLEAN | FETCH 이전에는 NULL이고 FETCH가 정상적으로 수행된 경우에는 TRUE이며 데이터가 없는 경우에는 FALSE이다. CLOSE 이후에는 NULL이다. |
| %NOTFOUND | BOOLEAN | %FOUND와 반대되는 값을 갖는다. |
| %ROWCOUNT | INTEGER | OPEN 이전에는 NULL이고 정상적으로 OPEN한 경우 0이며 FETCH가 성공할 때마다 1씩 증가한다. |

PSM 내에서는 다음과 같이 사용한다.

```
Cursor_Name % Attribute_name
Attribute_name :=  ISOPEN
                 | FOUND
                 | NOTFOUND
                 | ROWCOUNT
```

다음은 explicit cursor attribute를 사용하는 예이다.

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
  CURSOR C1 IS SELECT * FROM T1;
  v1 c1%ROWTYPE;
BEGIN
```

- ISOPEN을 통해 cursor가 열려 있는 상태인지 확인한다.

```
IF C1%ISOPEN = FALSE
  THEN
      OPEN C1;
  END IF;


  LOOP
      FETCH C1 INTO v1;
```

- NOTFOUND을 통해 더 이상 데이터가 없는지 확인한다.

```
EXIT WHEN C1%NOTFOUND;
```

- ROWCOUNT를 통해 fetch 된 row의 개수를 확인한다.

```
DBMS_OUTPUT.PUT_LINE('COUNT = ' || C1%ROWCOUNT );
  END LOOP;

  CLOSE C1;
  
END;
/
COUNT = 1
COUNT = 2

Anonymous PL block executed.
```

<a id="e3d3c92a2833b44e"></a>
### EXCEPTION Handling

PSM 내의 exception은 사용자가 PSM을 실행하는 과정에서 발생하는 다양한 오류를 정의한 것이다. PSM 실행 과정에서 오류가 발생하면 즉시 중단하고 사용자에게 오류를 반환한다. EXCEPTION handling은 사용자가 EXCEPTION 상황을 제어하고 중단없이 프로그램을 진행하도록 하기 위해 제공하는 기능이다.

<a id="aa13f94f6a5e7c1b"></a>
#### Exception Handler

다음과 같이 PSM BLOCK에 정의된 exception handler를 통해 에러 상황을 제어할 수 있다.

```
DECLARE
  V1 INTEGER;
BEGIN
  BEGIN
    V1 := 1 / 0;
```

- Exception handler

```
EXCEPTION WHEN OTHERS 
            THEN DBMS_OUTPUT.PUT_LINE('SQLCODE = ' || SQLCODE);
                 DBMS_OUTPUT.PUT_LINE('SQLERRM = ' || SQLERRM);
  END;
  
  DBMS_OUTPUT.PUT_LINE('next code');
END;
/
SQLCODE = -12122
SQLERRM = [SUNJESOFT][PSM][GOLDILOCKS]divisor is equal to zero
next code
```

위의 예에서 실행 시점에 divide by zero에 의해 프로그램이 중단된다. 그러나 exception handler에 의해 에러가 발생한 경우, 해당 BLOCK만 중단하고 다음 위치부터 계속 수행한다.

Exception handler는 다음과 같이 기술한다.

```
BEGIN
EXCEPTION WHEN exception_name, [exception_name, ...] THEN pl_statements;
         [WHEN exception_name, [exception_name, ...] THEN pl_statements;
END
```

- Exception handler의 특징은 다음과 같다.
    - 한 개의 exception handler를 BLOCK에 기술한다.
    - Exception handler 내에는 한 개 이상의 Exception_Name을 지정하고 해당 동작을 정의할 수 있다.
    - Exception handler 내의 Exception_name은 중복되면 안된다.
    - Exception handler가 기술된 PL BLOCK SCOPE 내에서 발생한 오류에 대해서만 동작한다.
    - 모든 예외 상황을 가리키는 OTHERS는 유일해야 하며 가장 마지막에 기술되어야 한다.
    - Exception handler에서 정상적으로 완료되면 이전에 발생한 오류는 clear 된다. 필요한 경우 사용자가 별도의 PSM 변수에 저장해야 한다.

Exception은 GOLDILOCKS에서 다음 표와 같은 특성을 갖는다.

**EXCEPTION 유형**

<a id="0bd16521172f53bf"></a>
| 유형 | Definer | Error code | Name | Raise implicitly | Raise explicitly |
| --- | --- | --- | --- | --- | --- |
| Predefined | Database | O | O | O | Optionally |
| User-defined | User | 사용자가 지정 | 사용자가 지정 | X | O |

> GOLDILOCKS에서 제공하는 predefined exception이나 user-defined exception에 대한 자세한 내용은 [Exception Declaration](28-psm-language-element-references.md#66923260ebd17e4d)을 참조한다.

<a id="d27dfe1ff441e995"></a>
#### Exception 전파

Exception이 발생했을 때 현재 BLOCK 내에 적절한 exception handler가 없으면 exception이 처리될 때까지 상위 BLOCK의 exception handler로 전파된다.

다음과 같은 코드의 LINE_1에서 오류가 난 경우 exception handler의 동작 여부에 따라 수행 결과가 달라진다.

```
BEGIN
  ...
  BEGIN
    LINE_1
    EXCEPTION HANDLER_1
  END;
  LINE_2
  EXCEPTION HANDLER_2
END;
/
```

- EXCEPTION_HANDLER_1에서 처리된 경우
    - Handler 동작을 정상적으로 완료하면 LINE_2부터 수행한다.
- EXCEPTION_HANDLER_1에 적절한 handler가 없는 경우
    - LINE_2는 수행할 수 없으며 현재 발생한 EXCEPTION은 EXCEPTION_HANDLER_2로 전달된다.
        - EXCEPTION_HANDLER_2에 적절한 handler가 존재하는 경우 handler 동작을 정상적으로 완료하면 프로그램이 종료된다.
        - EXCEPTION_HANDLER_2에 handler가 없는 경우 프로그램 진행이 중단되며 현재 발생한 오류 상황을 사용자에게 전달한다.

> Exception을 처리하던 exception handler에 오류가 발생하면 그 오류 코드가 상위 BLOCK으로 전파된다.

```
DECLARE
  V1 INTEGER;
  E1 EXCEPTION;
  E2 EXCEPTION;
BEGIN
  BEGIN
    RAISE E1;
  EXCEPTION WHEN E1 THEN V1 := 1 / 0;   ❶ 새로운 오류가 발생한다.
  END;

  EXCEPTION WHEN E1 
            THEN DBMS_OUTPUT.PUT_LINE('User Exception');
            WHEN ZERO_DIVIDE           
            THEN DBMS_OUTPUT.PUT_LINE('Zero divide');
END;
/
Zero divide

Anonymous PL block executed.
```

<a id="52a66291f9f033e7"></a>
#### User-defined Exception

User-defined exception은 predefined 외에 사용자가 exception name과 error-code를 설정하여 사용하는 exception이다. User-defined exception은 implicite하게 발생할 수 없으며 사용자가 명시적으로 RAISE statment를 사용하여 발생시켜야 한다.

다음은 RAISE statement를 이용하여 exception을 발생시키는 예이다.

```
DECLARE
  V1   INTEGER;
  high EXCEPTION;
  low  EXCEPTION;
BEGIN

  BEGIN
      V1 := 10;

      IF V1 > 10 
      THEN
          RAISE high;
      ELSE
          RAISE low;
      END IF;

  EXCEPTION WHEN high 
            THEN DBMS_OUTPUT.PUT_LINE('High');
            WHEN low
            THEN DBMS_OUTPUT.PUT_LINE('Low');
  END;
END;
/
Low
```

- User-defined exception은 다음 두 가지 경우로 나뉘어 처리된다.
    - Error code를 설정한 경우
    - Error code를 설정하지 않은 경우

사용자가 에러 코드를 설정한 경우에는 다음과 같이 동작한다.

```
DECLARE
  V1 INTEGER;
  E1 EXCEPTION;
  PRAGMA EXCEPTION_INIT( E1, -12122);
BEGIN
  BEGIN
    V1 := 1 / 0;
  EXCEPTION WHEN E1
            THEN DBMS_OUTPUT.PUT_LINE('SQLCODE = ' || SQLCODE);
                 DBMS_OUTPUT.PUT_LINE('SQLERRM = ' || SQLERRM);
  END;
END;
/
SQLCODE = -12122
SQLERRM = [SUNJESOFT][PSM][GOLDILOCKS]divisor is equal to zero
```

ZERO_DIVIDE predefined exception이 존재하지만 사용자가 오류 코드를 E1 exception으로 설정하여 handler를 설정한다. 위와 같이 서로 다른 오류 코드를 가진 벤더 간의 프로그램 호환성을 위해 사용자가 직접 exception의 오류 코드를 재설정한 exception handler를 사용할 수 있다.

Error code가 설정되지 않은 user-defined exception은 exception handler에서 다음과 같은 오류코드와 메시지로 설정된다.

```
DECLARE
  V1 INTEGER;
  E1 EXCEPTION;
BEGIN
  BEGIN
    RAISE E1;
  EXCEPTION WHEN E1
            THEN DBMS_OUTPUT.PUT_LINE('SQLCODE = ' || SQLCODE);
                 DBMS_OUTPUT.PUT_LINE('SQLERRM = ' || SQLERRM);
  END;
END;
/
SQLCODE = 1
SQLERRM = [SUNJESOFT][PSM][GOLDILOCKS]User-Defined Exception

Anonymous PL block executed.
```

User-defined exception의 전파 과정은 predefined exception의 전파 과정과 동일하다. 단, user-defined exception에 error code가 설정되지 않은 경우, 상위 BLOCK으로 전파되는 시점에 unhandled user exception 오류로 전달된다.

```
DECLARE
  V1 INTEGER;
  E1 EXCEPTION;
  E2 EXCEPTION;
BEGIN
  BEGIN
    RAISE E1;
  EXCEPTION WHEN E2
            THEN DBMS_OUTPUT.PUT_LINE('SQLCODE = ' || SQLCODE);
                 DBMS_OUTPUT.PUT_LINE('SQLERRM = ' || SQLERRM);
  END;
END;
/

ERR-HY000(17017): Unhandled user exception : 
    RAISE E1;
          *
ERROR at line 7:
```

Unhandled user exception은 exception handler 내에 user-defined exception을 기술하거나 predefined exception인 OTHERS를 사용하여 catch할 수 있다.

<a id="109daa67ab40b91f"></a>
### PRAGMA EXCEPTION_INIT

User-defined exception을 사용할 때 사용자가 특정 DBMS 에러 코드를 설정하기 위해 사용한다. DBMS 오류 코드는 벤더마다 다르기 때문에 PSM code의 exception handler 호환성을 위해 사용할 수도 있다.

그 문법은 다음과 같다.

```
<PRAGMA EXCEPTION_INIT> ::= 
    PARAGMA EXCEPTION_INIT ( exception_name, internal_errorcode )
```

- 다음과 같은 제약이 있다.
    - exception_name은 미리 선언되어 있어야 한다.
    - exception_name은 predefined exception을 사용할 수 없다.
    - internal_errorcode는 GOLDILOCKS의 internal error code만 가능하다.
    - SUCCESS를 의미하는 0 값을 설정할 수 없다.

다음은 NOT NULL constraints가 적용된 PSM 변수인 V1에 NULL을 assign할 경우의 exception을 user-defined exception으로 handling 하는 예이다.

```
DECLARE
  V1 VARCHAR(20) NOT NULL := 10;
  USER_EXCEPT EXCEPTION;
```

- PSM NOT NULL constrainst 오류를 사용자 정의 exception으로 선언한다.

```
PRAGMA EXCEPTION_INIT( USER_EXCEPT, -17009 );
BEGIN
```

- Exception 상황을 발생시킨다.

```
V1 := NULL;

  EXCEPTION WHEN USER_EXCEPT THEN DBMS_OUTPUT.PUT_LINE('Check Value');
END;
/
Check Value

Anonymous PL block executed.
```

GOLDILOCKS의 internal error code가 아닌 값을 설정할 경우 다음과 같은 오류가 발생한다.

```
DECLARE
  E1 EXCEPTION;
  PRAGMA EXCEPTION_INIT( E1, 99999);
BEGIN
    NULL;
END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (3:30): ERR-HY000(17021): Invalid error number for PRAGMA EXCEPTION_INIT
```

<a id="1434a724146cea99"></a>
### DBMS_STANDARD.RAISE_APPLICATION_ERROR

명시적으로 사용자 exception을 정의하지 않고 임의로 사용자 에러 코드와 메시지를 통해 간단하게 exception을 발생시키고 싶을 때 사용한다. DBMS_STANDARD 모듈에 속하며, 이 모듈의 루틴들은 해당 모듈명을 생략해도 호출할 수 있다.

다음과 같은 세 가지 인자가 있다.

**RAISE_APPLICATION_ERROR**

<a id="5ebc33710dee46be"></a>
| 인자 | 설명 |
| --- | --- |
| error_code IN NATIVE_INTEGER | 임의로 발생시킬 에러 코드 값이다. -20000 ~ -20999 범위의 값만 사용할 수 있다. |
| error_message IN VARCHAR(4000) | 에러가 발생할 때 SQLERRM에 저장될 메시지이다. |
| stack_flag IN BOOLEAN := FALSE | 기존 에러들 위에 쌓을 것인지 (TRUE), 기존 에러를 모두 대체할 것인지 (FALSE)에 관한 flag이다. 기본값은 FALSE이다. |

다음은 간단한 사용 예이다.

```
CREATE OR REPLACE PROCEDURE PROC1
IS
BEGIN
  RAISE_APPLICATION_ERROR (-20000, 'USER DEFINED ERROR TEST');
END;
/

Procedure created.

BEGIN
  PROC1;
EXCEPTION WHEN OTHERS THEN
  DBMS_OUTPUT.PUT_LINE( 'SQLCODE : ' || SQLCODE || ' SQLERRM : ' || SQLERRM );
END;
/
SQLCODE : -20000 SQLERRM : [SUNJESOFT][PSM][GOLDILOCKS]USER DEFINED ERROR TEST

Anonymous PL block executed.
```

---

[← 22. PSM DataTypes](22-psm-datatypes.md) · [전체 목차](../README.md) · [24. PSM Cursor Statements →](24-psm-cursor-statements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
