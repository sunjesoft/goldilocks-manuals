<a id="eac7b4acbaa9e3a8"></a>

# 18. PSM DataTypes

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/eac7b4acbaa9e3a8)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 17. Overview of PSM](17-overview-of-psm.md) · [전체 목차](../README.md) · [19. PSM Control Statements →](19-psm-control-statements.md)

<a id="17d837902780b888"></a>
## Built-in Data Types

GOLDILOCKS PSM은 GOLDILOCKS SQL에서 제공하는 모든 기본 데이터 타입들을 동일하게 지원한다.   
기본 데이터 타입들의 종류는 다음과 같다.   
자세한 내용은 [Data Type](../part-03-sql-manual/11-sql-elements.md#ff81d005bda1af76)을 참조한다.

<a id="0070664d50abbbc1"></a>
### 숫자 타입

- NUMBER
- NUMERIC
- FLOAT
- NATIVE_INTEGER
- NATIVE_DOUBLE

<a id="632a14f591b3bbf7"></a>
### CHARACTER STRING 타입

- CHARACTER (CHAR)
- CHARACTER VARYING (VARCHAR, VARCHAR2)
- CHARACTER LONG VARYING (LONG VARCHAR)

> 예외적으로 GOLDILOCKS SQL에서는 지원하지 않는 타입 중에 precision이 명시되지 않은 VARCHAR (VARCHAR2, CHAR VARYING, CHARACTER VARYING) 타입도 GOLDILOCKS PSM에서는 다른 데이터베이스와의 호환을 위해 제공한다.   
>   
> 이 타입은 일반 변수를 선언할 때는 사용할 수 없고 subprogram의 인자나 반환 타입, 그리고 커서의 인자 타입을 명시할 때만 사용할 수 있다. 이 타입이 명시되면 해당 인자나 반환 타입은 VARCHAR 타입 중 최대 크기를 가질 수 있는 타입으로 결정된다. (precision = 4000)

<a id="b8a167f9d87dbc21"></a>
### BINARY STRING 타입

- BINARY
- BINARY VARYING (VARBINARY)
- BINARY LONG VARYING (LONG VARBINARY)

<a id="57c5a3ba5ba5d8e4"></a>
### 날짜/시간 타입

- DATE
- TIME [WITH/WITHOUT TIME ZONE]
- TIMESTAMP [WITH/WITHOUT TIME ZONE]

<a id="1ce4b23e11cf9117"></a>
### INTERVAL 타입

- INTERVAL YEAR
- INTERVAL MONTH
- INTERVAL YEAR TO MONTH
- INTERVAL DAY
- INTERVAL HOUR
- INTERVAL MINUTE
- INTERVAL SECOND
- INTERVAL DAY TO HOUR
- INTERVAL DAY TO MINUTE
- INTERVAL DAY TO SECOND
- INTERVAL HOUR TO MINUTE
- INTERVAL HOUR TO SECOND
- INTERVAL MINUTE TO SECOND

<a id="0da667ac77d90fae"></a>
### BOOLEAN 타입

BOOLEAN

<a id="4b3171cb9bf9e1a3"></a>
### ROWID 타입

ROWID

<a id="4ecc640d2caaa954"></a>
### Built-in 데이터 타입 변수 선언

변수는 anonymous block이나 procedure, 함수 내부의 각 선언부 (declaration section)에서 선언할 수 있다.

```
DECLARE
  V_MSG VARCHAR(20) := 'HELLO, WORLD!';
BEGIN
  DBMS_OUTPUT.PUT_LINE( 'My First Message Is : ' || V_MSG );
END;
/
```

자세한 내용은 [Built-in Data Type References](../part-03-sql-manual/11-sql-elements.md#35b61548d50e5866)를 참조한다.

<a id="d9c3094d776b7d3d"></a>
## Attribute Data Types

다른 PSM 변수나 커서, 테이블, 또는 테이블의 특정 column 등의 타입을 명시할 때 사용되는 데이터 타입이다.

Attribute 타입으로 선언된 변수나 함수의 대상 객체 (테이블 등)가 변경되면 PSM (procedure, 함수)은 자동으로 변경된 타입에 맞춰 다시 컴파일 되어 적용된다.

<a id="e0285f1479b9bf4a"></a>
### %TYPE

다른 변수나 특정 테이블의 column 등의 타입을 명시할 때 사용된다. 참조할 수 있는 대상은 다음과 같다.

- Scalar 타입 (built-in 데이터 타입 포함) 변수
- 사용자 정의 레코드 타입 변수
- 레코드 타입 변수의 특정 필드
- Collection 타입 변수
- Collection 타입 변수의 특정 필드
- 테이블의 특정 column

%TYPE은 다음과 같이 사용된다.

```
CREATE TABLE EMP ( ID INTEGER, NAME VARCHAR(32) );
INSERT INTO EMP VALUES ( 1001, 'Tom Jackson' );
COMMIT;

DECLARE
  V_NAME EMP.NAME%TYPE;
BEGIN
  SELECT NAME INTO V_NAME FROM EMP;
  DBMS_OUTPUT.PUT_LINE( 'EMP.NAME = ' || V_NAME );
END;
/
```

<a id="7036485e1abecc35"></a>
### %ROWTYPE

특정 테이블의 구조 또는 특정 커서의 반환 타입과 동일한 레코드 타입을 명시할 때 사용된다. 참조할 수 있는 대상은 다음과 같다.

- 테이블
- Cursor
- Cursor variable

레코드 타입 변수나 collection 타입 변수는 %ROWTYPE의 대상이 될 수 없다.

%ROWTYPE을 사용하는 예는 다음과 같다.

```
DECLARE
  V_EMP EMP%ROWTYPE;
BEGIN
  SELECT * INTO V_EMP FROM EMP WHERE ID = 1001;
  DBMS_OUTPUT.PUT_LINE( 'Name of ID 1001 Is : ' || V_EMP.NAME );
END;
/
```

<a id="18590087b0a5a063"></a>
### Constraint 속성 상속

Attribute 타입으로 선언된 변수들의 constraint 속성은 다음과 같이 참조 대상의 constraint 속성을 상속받는다.

<a id="e38adbf9f48b51e7"></a>
<table class="table column_count_4"><caption>Attribute type의 constraint 상속 유무 </caption><thead><tr><th class="to_center"><div>Attribute type</div></th><th class="to_center"><div>참조 대상</div></th><th class="to_center"><div>NOT NULL</div></th><th class="to_center"><div>Default 값</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="7"><div>%TYPE</div></td><td class="to_middle"><div>Scalar 변수</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>레코드 타입 변수</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>레코드 타입 변수의 특정 필드</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>Collection 타입의 변수 - scalar element</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>Collection 타입의 변수 - 레코드 element</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>O</div></td></tr><tr><td class="to_middle"><div>Collection 타입 변수의 특정 필드</div></td><td class="to_center to_middle"><div>O</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>테이블의 특정 column</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle" rowspan="3"><div>%ROWTYPE</div></td><td class="to_middle"><div>테이블</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>Cursor</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr><tr><td class="to_middle"><div>Cursor variable</div></td><td class="to_center to_middle"><div>X</div></td><td class="to_center to_middle"><div>X</div></td></tr></tbody></table>

<a id="b5920fbcd6dc58b1"></a>
## User-defined Record Type

레코드 타입 변수는 서로 다른 타입의 필드 여러 개로 구성된 복합 구조 타입이다. 레코드 타입 변수는 %ROWTYPE을 사용하여 다른 테이블이나 커서의 타입을 그대로 복사해 오거나 사용자가 특정 용도에 맞는 데이터 구조를 선언하여 생성할 수 있다.

사용자 정의 레코드 타입은 PSM의 선언부에서 TYPE 키워드를 사용하여 다음과 같이 정의할 수 있고 각 필드는 NOT NULL constraint와 기본값을 선택적으로 명시할 수 있다.

```
DECLARE
  TYPE MY_EMP_TYPE IS RECORD
  ( 
    ID INTEGER := 99999,
    NAME VARCHAR(32) NOT NULL DEFAULT 'anonymous'
  );
  V_EMP MY_EMP_TYPE;
BEGIN
  SELECT ID, NAME INTO V_EMP.ID, V_EMP.NAME FROM EMP;
  DBMS_OUTPUT.PUT_LINE('ID = ' || V_EMP.ID);
  DBMS_OUTPUT.PUT_LINE('NAME = ' || V_EMP.NAME);
END;
/
```

다음은 nested procedure나 nested 함수에서 사용하는 예이다.

```
DECLARE
  TYPE MY_EMP_TYPE IS RECORD
  ( 
    ID INTEGER := 99999,
    NAME VARCHAR(32) NOT NULL DEFAULT 'anonymous'
  );
  V_EMP MY_EMP_TYPE;
  PROCEDURE SET_EMP( A_EMP IN OUT MY_EMP_TYPE )
  IS
  BEGIN
    DBMS_OUTPUT.PUT_LINE('ID = ' || A_EMP.ID);
    DBMS_OUTPUT.PUT_LINE('NAME = ' || A_EMP.NAME);
    SELECT ID, NAME INTO A_EMP.ID, A_EMP.NAME FROM EMP;
  END;
BEGIN
  SET_EMP( V_EMP );
  DBMS_OUTPUT.PUT_LINE('ID = ' || V_EMP.ID);
  DBMS_OUTPUT.PUT_LINE('NAME = ' || V_EMP.NAME);
END;
/
```

사용자 정의 레코드 타입은 일반 지역 변수, nested procedure, 또는 nested 함수의 인자나 반환 타입으로 사용할 수 있지만, schema-level procedure나 schema-level 함수의 인자나 반환 타입으로는 사용할 수 없다.

<a id="9839c05387c72451"></a>
## User-defined Collection Type

User-defined collection type은 한 개 이상의 데이터를 저장하는 일종의 array 구조이다. GOLDILOCKS PSM은 collection type 중에 key/ value pair로 저장할 수 있는 associative array 타입을 지원한다.

Associative type을 선언하기 위한 기본 구문은 다음과 같다.

```
TYPE <type_name> IS TABLE OF <element_data_type> INDEX BY <index_key_data_type>
```

- &lt;type_name&gt;은 사용자가 해당 type에 대해 지정하는 이름이다.
- &lt;element_data_type&gt;은 array를 구성하는 value의 data type을 지정한다.
- &lt;index_key_data_type&gt;은 element를 탐색할 index key의 data type을 지정한다.

예를 들어, (번호)에 해당하는 정보가 (이름, 나이) 형식일 경우, 데이터베이스에 다음과 같은 테이블을 생성하고 저장할 수 있다.

```
CREATE TABLE INFO
(
   NO INTEGER,
   NAME VARCHAR(20),
   AGE INTEGER
)
CREATE UNIQUE INDEX IDX_NO ON INFO (NO)
```

- 위와 같은 정보를 associative array로 저장할 경우 다음과 같이 구성된다.
    - Index_key는 번호 (NO)에 해당된다.
    - Element_data는 이름 (NAME), 나이 (AGE)로 구성된다.

실제 PSM 내에서는 이를 저장할 associative array 변수를 다음과 같이 정의할 수 있다.

```
TYPE rec IS RECORD (NAME VARCHAR(20), AGE INTEGER);
TYPE info IS TABLE OF rec INDEX BY INTEGER;
```

자세한 내용은 [COLLECTION Variable Declaration](23-psm-language-element-references.md#7fa00b668e21b11c)을 참조한다.

<a id="d827c8ad10d3d419"></a>
### Associative Array

Associative array type 변수는 index 절에 기술된 data type의 key를 가지며 TABLE OF 절에 기술된 element data type의 value를 key/ value 형태로 한 개 이상 저장할 수 있는 PSM 변수이다.

- GOLDILOCKS PSM의 associative array type의 특징은 다음과 같다.
    - INDEX BY 절에 기술된 data type 형태의 탐색 key를 가지며 자동으로 정렬되어 저장된다.
    - TABLE OF 절에 기술된 element로 구성된다.
    - Collection method라고 불리는 탐색 함수들을 제공한다.
    - 이미 존재하는 index key에 element를 저장할 경우에는 replace 형태로 저장된다.
    - 최대 저장 공간은 사용 가능한 MEMORY_TEMP_TBS_SIZE 크기 이내로 제한된다.

다음은 SQL data type으로 element type을 선언하여 데이터를 삽입하는 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.



gSQL> DECLARE
  TYPE rec IS TABLE OF VARCHAR(20) INDEX BY VARCHAR(10);
  V1 rec;
BEGIN
  V1('aa') := 'Dog';
  V1('bb') := 'Cat';

  INSERT INTO T1 VALUES ( V1('aa'), V1('bb') );
END;
/

Anonymous PL block executed.


gSQL> SELECT * FROM T1;

C1  C2 
--- ---
Dog Cat

1 row selected.
```

다음은 record type을 element로 갖는 예이다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.



gSQL> DECLARE
  TYPE rec IS TABLE OF T1%ROWTYPE INDEX BY VARCHAR(10);
  V1 rec;
BEGIN
  V1('person1').C1 := 'seoul';
  V1('person1').C2 := '12';

  V1('person2').C1 := 'busan';
  V1('person2').C2 := '24';

  INSERT INTO T1 VALUES V1('person1'), V1('person2');
END;
/

Anonymous PL block executed.


gSQL> SELECT * FROM T1;

C1    C2
----- --
seoul 12
busan 24

2 rows selected.
```

- GOLDILOCKS PSM의 associative array의 index key에 지정할 수 있는 데이터 타입은 다음과 같다. 
    - INTEGER
    - LONG
    - CHAR
    - VARCHAR

- GOLDILOCKS PSM의 associative array의 element type으로 사용할 수 있는 데이터 타입은 다음과 같다.
    - SQL data type
    - %TYPE
    - %ROWTYPE
    - User-defined record type

자세한 내용은 [Built-in Data Types](#17d837902780b888), [%TYPE](#e0285f1479b9bf4a), [%ROWTYPE](#7036485e1abecc35), [User-defined Record Type](#b5920fbcd6dc58b1)을 참조한다.

<a id="7b4aa30c677ee6f8"></a>
### Assign Values to Collection Variables

Collection 변수 간의 assign에는 다음 규칙이 적용된다.

- Element assign에는 &lt;Assign Statement&gt;와 동일한 규칙이 적용된다.
- Collection 변수 전체를 assign하려면 collection 변수의 타입이 동일해야만 한다.
- Collection 변수의 element를 assign 할 경우에는 element data type에 따라 다음과 같이 작동한다.
    - User-defined type element의 assign은 동일한 타입 사이에서만 허용된다.
    - 그 외의 경우에는 element를 구성하는 필드의 data type 간의 run-time 시점에 호환이 가능할 때만 assign할 수 있다.

다음은 다른 타입을 assign하여 오류가 발생하는 경우의 예이다.

```
DECLARE
  TYPE udr1 IS RECORD (F1 INTEGER, F2 VARCHAR(20));
  TYPE udr2 IS RECORD (F1 INTEGER, F2 VARCHAR(20));

  TYPE rec1 IS TABLE OF udr1 INDEX BY VARCHAR(10);
  TYPE rec2 IS TABLE OF udr2 INDEX BY VARCHAR(10);

  V1 rec1;
  V2 rec2;
BEGIN
  V2('person1').F1 := 24;
  V2('person1').F2 := 'seoul korea';

  V1 := V2;

END;
/

ERR-HY000(17032): PSM compilation error : 
(1) at (14:9): ERR-HY000(17007): invalid expression
```

위의 예에서 user-defined type으로 구성된 element의 각 필드 구성은 동일하지만 변수의 type이 다르기때문에 assign할 수 없다.

다음은 동일한 type을 사용하여 정상적으로 assign하는 예이다.

```
DECLARE
  TYPE udr1 IS RECORD (F1 INTEGER, F2 VARCHAR(20));

  TYPE rec1 IS TABLE OF udr1 INDEX BY VARCHAR(10);

  V1 rec1;
  V2 rec1;
BEGIN
  V2('person1').F1 := 24;
  V2('person1').F2 := 'seoul korea';

  V1 := V2;

END;
/

Anonymous PL block executed.
```

Associative type을 element 단위로 assign하려면 element의 data type이 호환 가능해야 한다.

다음 예를 참조한다.

```
gSQL> CREATE TABLE T1 
(
  c1 VARCHAR(20), 
  c2 VARCHAR(20)
);

Table created.


gSQL> DECLARE
TYPE record_org1 IS RECORD (f1 VARCHAR(20), f2 VARCHAR(20));

TYPE rec1 IS TABLE OF t1%rowtype INDEX BY VARCHAR(10);
TYPE rec2 IS TABLE OF record_org1 INDEX BY VARCHAR(10);

v1 record_org1;
v2 rec1;
v3 rec2;
v4 t1%rowtype;
BEGIN
   
  -- From record_org1 type to %rowtype
  V2('first') := v1;

  -- From record_org1 type to record_org1 type
  V3('first') := v1;
  
  -- From t1%rowtype to record_org1 type
  V3('second') := V2('first');

END;
/

Anonymous PL block executed.
```

Associative type 변수는 휘발성 메모리 공간에 저장되는데 공간이 부족할 경우 사용자가 접근 가능한 TEMP TABLESPACE를 확장해야 한다. 다음은 공간 부족으로 인해 오류가 발생하는 예이다.

```
DECLARE
TYPE rec IS TABLE OF t1%rowtype INDEX BY varchar(20);
v1 rec;
BEGIN
  BEGIN
    FOR i IN 1 .. 100000
    LOOP
      v1(i).c1 := i;
      v1(i).c2 := i;
      v1(i).c3 := i;
    END LOOP;

    EXCEPTION WHEN OTHERS THEN
                 dbms_output.put_line('error: count=' || v1.count());
                 dbms_output.put_line('sqlcode=' || SQLCODE);
                 dbms_output.put_line('sqlmsg =' || SQLERRM);
  END;
  dbms_output.put_line('v1.count=' || v1.count());
END;
/
error: count=95004
sqlcode=-14015
sqlmsg =[SUNJESOFT][PSM][GOLDILOCKS]there is no extendible datafile in tablespace 'MEM_TEMP_TBS'
v1.count=95004

Anonymous PL block executed.
```

<a id="9546a286fe89c556"></a>
### Collection Method

Collection method는 collection type 변수를 쉽게 operation 할 수 있도록 제공되는 function이나 procedure를 의미한다. Associative array에는 다음과 같은 method가 제공된다.

**Collection method**

<a id="2676989267f0afc2"></a>
| Method | 유형 | 입력 인자 | 반환 타입 | 설명 |
| --- | --- | --- | --- | --- |
| FIRST | Function | X | Index key data type | 첫 번째 index key를 반환한다. |
| LAST | Function | X | Index key data type | 마지막 index key를 반환한다. |
| COUNT | Function | X | INTEGER | Element의 개수를 반환한다. |
| EXISTS | Function | O | BOOLEAN | Index key의 존재 유무를 반환한다. |
| PRIOR | Function | O | Index key data type | 입력된 index key 이전의 index key를 반환한다. |
| NEXT | Function | O | Index key data type | 입력된 index key 이후 index key를 반환한다. |
| DELETE | Procedure | O | N/A | 입력된 index key에 해당하는 element를 삭제한다. |

Collection method는 다음과 같이 사용할 수 있다.

```
gSQL> CREATE TABLE T1 
(
  C1 VARCHAR(20),
  C2 VARCHAR(20)
);

Table created.



gSQL> DECLARE
  TYPE rec IS TABLE OF T1%ROWTYPE INDEX BY VARCHAR(10);
  V1 rec;
BEGIN
  V1('person1').C1 := 'seoul';
  V1('person1').C2 := '12';

  V1('person2').C1 := 'busan';
  V1('person2').C2 := '24';

  V1('person3').C1 := 'Daegu';
  V1('person3').C2 := '36';

  -- First method
  DBMS_OUTPUT.PUT_LINE('First Index Key = ' || V1.first() );

  -- Last method
  DBMS_OUTPUT.PUT_LINE('Last Index Key = ' || V1.last() );

  -- Count method
  DBMS_OUTPUT.PUT_LINE('Count of element = ' || V1.count() );

  -- Prior Method
  DBMS_OUTPUT.PUT_LINE('Prior (person1) = ' || V1.prior('person1') ); -- return NULL
  DBMS_OUTPUT.PUT_LINE('Prior (person3) = ' || V1.prior('person3') );

  -- Next Method
  DBMS_OUTPUT.PUT_LINE('Next (person1) = ' || V1.next('person1') );
  DBMS_OUTPUT.PUT_LINE('Next (person3) = ' || V1.next('person3') ); -- return NULL

  -- Exists Method
  DBMS_OUTPUT.PUT_LINE('Exists (person2) = ' || V1.exists('person2') );

  -- Delete Method
  V1.delete('person2');

  -- Exists Method
  DBMS_OUTPUT.PUT_LINE('After delete, Exists (person2) = ' || V1.exists('person2') );
END;
/
First Index Key = person1
Last Index Key = person3
Count of element = 3
Prior (person1) = 
Prior (person3) = person2
Next (person1) = person2
Next (person3) = 
Exists (person2) = TRUE
After delete, Exists (person2) = FALSE

Anonymous PL block executed.
```

한 개의 element를 제거하는 delete procedure가 입력된 인자에 해당하는 index key를 찾지 못할 경우 다음과 같은 오류가 발생한다.

```
gSQL> DECLARE
  TYPE rec IS TABLE OF T1%ROWTYPE INDEX BY VARCHAR(10);
  V1 rec;
BEGIN
  V1('person1').C1 := 'seoul';
  V1('person1').C2 := '12';

  -- Call delete procedure
  V1.delete('person2');

END;
/

ERR-HY000(17045): no data found : 
  V1.delete('person2');
  *
ERROR at line 9:
Anonymous PL block executed.
```

<a id="ad8c88ee335f1f79"></a>
## SYS_REFCURSOR

SYS_REFCURSOR는 cursor variable에 대한 predefined type이며 cursor variable을 선언하는 용도로 사용된다.

다음과 같은 형태로 cursor variable을 선언할 때 사용된다.

```
cursor_variable_name SYS_REFCURSOR;
```

Cursor variable은 다음과 같이 OPEN FOR, FETCH, CLOSE 구문과 함께 사용할 수 있다.

```
DECLARE
  v1 VARCHAR(20);
  v2 VARCHAR(20);

  cv1 SYS_REFCURSOR;
  cv2 SYS_REFCURSOR;

BEGIN

  OPEN cv1 FOR SELECT * FROM T1;

  cv2 := cv1;

  FETCH cv2 INTO V1, V2;

  DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);
  
END;
/
V1 = Seoul , V2 = 24

Anonymous PL block executed.
```

- SYS_REFCURSOR로 선언된 변수는 다음과 같이 사용된다.
    - 여러 cursor variable 사이에 서로 assign할 수 있다. Assign의 오른쪽에 위치한 cursor variable의 기존에 이미 열려있는 cursor는 더 이상 사용할 수 없다.
    - Explicit cursor를 cursor variable에 assign 할 수 없다.
    - 다른 data type의 변수를 cursor variable에 assign 할 수 없다.
    - Nested function/ procedure 또는 schema-level function/ procedure의 parameter로 사용할 수 있다.

자세한 내용은 [CURSOR VARIABLES](20-psm-cursor-statements.md#f370970b8fe498e7), [Cursor Variable Declaration](23-psm-language-element-references.md#e6d4ef5813d5c256), [OPEN FOR Statement](23-psm-language-element-references.md#e42e171c8ed8be7c)를 참조한다.

---

[← 17. Overview of PSM](17-overview-of-psm.md) · [전체 목차](../README.md) · [19. PSM Control Statements →](19-psm-control-statements.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
