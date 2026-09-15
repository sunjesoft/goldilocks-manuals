<a id="22c487869568c7ce"></a>

# 24. PSM Cursor Statements

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/22c487869568c7ce)  
> 태그: `22c.1_10_tag`

[← 23. PSM Control Statements](23-psm-control-statements.md) · [전체 목차](../README.md) · [25. Using PSM Subprograms →](25-using-psm-subprograms.md)

<a id="3b2e2d72b277abdd"></a>
## Implicit Cursor

Implicit cursor는 PSM statement에 의해 데이터베이스 내에서 정의되고 관리되는 커서이다. PSM statement는 SELECT 문이나 DML 문을 실행할 때마다 implicit cursor를 사용한다. 사용자는 implicit cursor를 제어하지는 못하지만 implicit cursor attribute를 통해 질의에 대한 정보를 얻을 수 있다.

<a id="4c6bcb290c415fb0"></a>
### Implicit Cursor Attributes

Implicit cursor attributes는 가장 최근에 실행된 SELECT 문 또는 DML 문의 실행 결과를 참조한다. 가장 최근에 SELECT 문 또는 DML 문이 실행되지 않았을 경우, attributes 값은 NULL 이다.

**Implicit cursor attributes**

<a id="c29676bf1d10ab46"></a>
| Attribute name | 반환 타입 | 설명 |
| --- | --- | --- |
| SQL%ISOPEN | BOOLEAN | 항상 FALSE를 반환한다. 왜냐하면 최근 실행한 SELECT 문이나 DML 문이 항상 종료되기 때문이다. |
| SQL%FOUND | BOOLEAN | 가장 최근에 실행한 SELECT 문이나 DML 문에서 반환된 결과가 있을 경우 TRUE이고, 그렇지 않으면 FALSE 이다. |
| SQL%NOTFOUND | BOOLEAN | SQL%FOUND와 반대되는 값을 갖는다. |
| SQL%ROWCOUNT | INTEGER | 가장 최근에 실행한 SELECT 문이나 DML 문에서 반환된 ROW의 개수이다. |

<a id="2dd81edb7edb5d74"></a>
### 사용 예

- 가장 최근에 실행된 질의가 없는 경우

```
gSQL> 
BEGIN
  DBMS_OUTPUT.PUT_LINE('SQL%ISOPEN   = ' || SQL%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('SQL%FOUND    = ' || SQL%FOUND);
  DBMS_OUTPUT.PUT_LINE('SQL%NOTFOUND = ' || SQL%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('SQL%ROWCOUNT = ' || SQL%ROWCOUNT);
END;
/

SQL%ISOPEN   = FALSE
SQL%FOUND    = 
SQL%NOTFOUND = 
SQL%ROWCOUNT = 
Anonymous PL block executed.
```

- 가장 최근에 실행된 질의가 있는 경우

```
gSQL> 
CREATE TABLE t_month( month_char VARCHAR(15) , month_num INTEGER );
Table created.

gSQL> 
INSERT INTO t_month VALUES( 'JANUARY' , 1 ), ( 'MARCH' , 3 ),
                          ( 'MAY' , 5 ), ( 'JULY' , 7 ),
                          ( 'SEPTEMBER' , 9 ), ( 'NOVEMBER' , 11 );
6 rows created.

gSQL> 
DECLARE
  row_count INTEGER;
BEGIN
  SELECT COUNT(*) INTO row_count FROM t_month;

  DBMS_OUTPUT.PUT_LINE('SQL%ISOPEN   = ' || SQL%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('SQL%FOUND    = ' || SQL%FOUND);
  DBMS_OUTPUT.PUT_LINE('SQL%NOTFOUND = ' || SQL%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('SQL%ROWCOUNT = ' || SQL%ROWCOUNT);
END;
/

SQL%ISOPEN   = FALSE
SQL%FOUND    = TRUE
SQL%NOTFOUND = FALSE
SQL%ROWCOUNT = 1
Anonymous PL block executed.
```

<a id="343c3f287fc9d6d7"></a>
## Explicit Cursor

Explicit cursor는 사용자가 선언 및 정의하고 관리하는 커서이다. 해당 커서는 사용자가 이름을 지정하고, SELECT 문 또는 DML 문에 연결해야 한다.

- Explicit cursor는 다음과 같이 사용한다.
    - 사용자는 open 구문을 통해 explicit cursor를 열고 fetch 구문을 실행하여 질의 결과를 fetch 한다. 그리고 마지막으로 close 구문으로 커서를 닫는다.
    - Explicit cursor는 cursor for loop 구문으로 사용할 수 있다.

Explicit cursor는 expression으로 사용할 수 없다. 즉, 커서에 값을 할당하거나, procedure 또는 routine의 parameter로 사용할 수 없다.

- Explicit Cursor 예

```
gSQL>
CREATE TABLE t_month( month_char VARCHAR(15), month_num INTEGER );
Table created.

gSQL>
INSERT INTO t_month VALUES( 'FEBRUARY' , 2 ), ( 'APRIL' , 4 ), 
                          ( 'JUNE' , 6 ), ( 'AUGUST' , 8 ),
                          ( 'OCTOBER' , 10 ), ( 'DECEMBER' , 12 );
6 rows created.

gSQL>
DECLARE
  CURSOR cur_month IS SELECT * FROM t_month;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN cur_month;                                         ❶ OPEN explicit cursor.
  
  LOOP                                                   ❷ Loop를 활용하여 여러 ROW fetch
    FETCH cur_month INTO v_month_char, v_month_num;      ❸ FETCH explicit cursor.
     
    EXIT WHEN cur_month%NOTFOUND;                        ❹ 결과 집합에 있는 ROW를 전부 fetch 했는지 확인
    
    DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );
  END LOOP;
    
  CLOSE cur_month;                                       ❺ CLOSE explicit cursor.
END;
/

v_month_char : FEBRUARY , v_month_num : 2
v_month_char : APRIL , v_month_num : 4
v_month_char : JUNE , v_month_num : 6
v_month_char : AUGUST , v_month_num : 8
v_month_char : OCTOBER , v_month_num : 10
v_month_char : DECEMBER , v_month_num : 12
Anonymous PL block executed.
```

<a id="f83d34698dd3496e"></a>
### Declaring and Defining Explicit Cursors

Explicit cursor를 사용하기 위해 PSM declare section에서 선언 (declaration) 및 정의 (definition) 한다. Explicit cursor를 선언할 (declaration) 때의 cursor name, parameter 정보, return type은 정의 (definition) 할 때에도 동일해야 한다. Explicit cursor의 syntax 및 자세한 설명은 [Explicit Cursor Declaration and Definition](28-psm-language-element-references.md#4b4c67d5cfe44688)을 참조한다.

<a id="8429ecea08b8baae"></a>
#### Explicit Cursor 선언 (declaration) 및 정의 (definition) 예

```
gSQL>
DECLARE
  CURSOR cur_month1( p1 INTEGER ) RETURN t_month%rowtype;
  CURSOR cur_month1( p1 INTEGER ) RETURN t_month%rowtype IS SELECT * FROM t_month WHERE month_num = p1;

  CURSOR cur_month2 IS SELECT * FROM t_month;
BEGIN
  NULL;
END;
/

Anonymous PL block executed.
```

<a id="34f06cff941631bc"></a>
### Opening and Closing Explicit Cursors

- Explicit cursor를 선언 (declaration)하고 정의 (definition) 한 후에는 [OPEN Statement](28-psm-language-element-references.md#0e2282272361b688)를 실행하여 cursor query를 수행한다.
- Explicit cursor의 질의가 SELECT ... FOR UPDATE 문이면 결과 집합의 ROW에 LOCK을 잡는다.
- Explicit cursor의 질의가 explicit cursor parameter나 PSM variable을 참조할 경우, 질의 결과에 영향을 준다.
- Explicit cursor를 사용한 후에는 [CLOSE Statement](28-psm-language-element-references.md#5dd511f3fe54ad01)를 실행하여 닫을 수 있다. Explicit cursor가 닫힌 후에는 결과 집합에서 레코드를 가져올 수 없다.
- Explicit cursor가 OPEN 된 후로는 다시 OPEN할 수 없으며, 다시 OPEN 하려면 CLOSE를 먼저 수행한 후에 OPEN 해야 한다.

<a id="ba1c014b0df3cdcd"></a>
#### Explicit Cursor OPEN과 CLOSE 예

```
gSQL>
DECLARE
  CURSOR cur_month( p1 INTEGER ) IS SELECT * FROM t_month WHERE month_num = p1;
BEGIN
  OPEN cur_month( 2 );      -- Explicit Cursor OPEN

  CLOSE cur_month;          -- Explicit Cursor CLOSE
END;
/

Anonymous PL block executed.
```

<a id="80907f9ca05b617c"></a>
### Fetching Data with Explicit Cursors

- Explicit cursor를 OPEN 한 후에 [FETCH Statement](28-psm-language-element-references.md#31aa8d8b5c8ba1f0)를 실행하여 결과 집합의 row를 가져올 수 있다.
- Fetch statement는 결과 집합의 현재 ROW를 검색하고 해당 ROW 값을 PSM variable 또는 record type variable에 저장하고 커서를 다음 ROW로 이동시킨다.
- PSM [FETCH Statement](28-psm-language-element-references.md#31aa8d8b5c8ba1f0)는 fetch 된 ROW가 없더라도 예외를 발생시키지 않는다.
- [Basic LOOP Statement](28-psm-language-element-references.md#2d30a62c1a28081c)에서 FETCH를 수행할 경우 종료 조건을 감지하기 위해 %NOTFOUND 속성을 활용한다.

<a id="4f28fb5d16232cad"></a>
#### Explicit Cursor의 FETCH 예

```
gSQL>
DECLARE
  CURSOR cur_month IS SELECT * FROM t_month;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN cur_month;
  
  LOOP
    FETCH cur_month INTO v_month_char, v_month_num;
    
    EXIT WHEN cur_month%NOTFOUND;
    
    DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );
  END LOOP;
    
  CLOSE cur_month;
END;
/

v_month_char : FEBRUARY , v_month_num : 2
v_month_char : APRIL , v_month_num : 4
v_month_char : JUNE , v_month_num : 6
v_month_char : AUGUST , v_month_num : 8
v_month_char : OCTOBER , v_month_num : 10
v_month_char : DECEMBER , v_month_num : 12
Anonymous PL block executed.
```

<a id="89ecda8a7c6b7b03"></a>
### When Explicit Cursor Queries Need Column Aliases

Explicit cursor의 질의에 expression이 포함된 경우, 해당 column에는 항상 별칭 (alias name)이 있어야 한다. Explicit cursor를 참조하여 만든 %ROWTYPE variable에 fetch 된 결과를 저장해놓고, 참조할 때 이를 사용할 수 있다.

<a id="01e1b345a52b6616"></a>
#### Explicit Cursor의 질의에서 별칭을 사용하는 예

```
gSQL>
DECLARE
  CURSOR cur_month IS SELECT month_char, ( ' == ' || month_num ) as equal_month_num FROM t_month;
  var cur_month%rowtype;
BEGIN
  OPEN cur_month;
  
  LOOP
    FETCH cur_month INTO var; 
    
    EXIT WHEN cur_month%NOTFOUND;
    
    DBMS_OUTPUT.PUT_LINE( var.month_char || var.equal_month_num );
  END LOOP;

  CLOSE cur_month;
END;
/

FEBRUARY == 2
APRIL == 4
JUNE == 6
AUGUST == 8
OCTOBER == 10
DECEMBER == 12
Anonymous PL block executed.
```

<a id="635ab6c30e149f7c"></a>
### Explicit Cursors that Accept Parameters

Parameter가 있는 explicit cursor를 선언 (declaration)하고 정의 (definition) 할 수 있다.

- Explicit cursor의 parameter
    - IN bind type만 허용한다.
    - DEFAULT value를 가질 수 있다. Argument는 명시하지 않아도 된다.
    - Cursor의 질의에서 참조할 수 있다.
    - Explicit cursor의 범위 밖에서는 explicit cursor의 parameter를 참조할 수 없다.

<a id="eeadc68cb8b8e2f4"></a>
#### Explicit Cursor Parameter 사용 예

```
gSQL>
DECLARE
  CURSOR cur_month( p1 IN INTEGER ) IS SELECT month_char, month_num FROM t_month WHERE month_num = p1;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN cur_month(4);
  
  FETCH cur_month INTO v_month_char, v_month_num;      
  DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );
gSQL> 
  CLOSE cur_month;
END;
/ 

v_month_char : APRIL , v_month_num : 4
Anonymous PL block executed.
```

- Explicit cursor parameter의 DEFAULT value 예

```
gSQL>
DECLARE
  CURSOR cur_month( p1 INTEGER DEFAULT 2 ) IS SELECT month_char, month_num FROM t_month WHERE month_num = p1;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN cur_month;                    ❶ Actual parameter는 생략할 수 있다.
   
  FETCH cur_month INTO v_month_char, v_month_num;      
  DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );

  CLOSE cur_month;
  
  OPEN cur_month(4);               ❷ Actual parameter를 명시하여 OPEN 할 수 있다.
  
  FETCH cur_month INTO v_month_char, v_month_num;      
  DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );

  CLOSE cur_month;
END;
/

v_month_char : FEBRUARY , v_month_num : 2
v_month_char : APRIL , v_month_num : 4
Anonymous PL block executed.
```

<a id="70e1cdd1d95eff09"></a>
### Explicit Cursor Attributes

Explicit cursor 속성은 explicit cursor의 상태 정보를 나타낸다. Cursor name 뒤에 속성을 붙여서 explicit cursor 속성으로 사용할 수 있다.

**Explicit cursor attributes**

<a id="8bfc0414806fdb57"></a>
| Attribute name | 반환 타입 | 설명 |
| --- | --- | --- |
| explicit_cursor_name%ISOPEN | BOOLEAN | Explicit cursor가 정상적으로 OPEN 된 경우 TRUE, 그 외에는 FALSE이다. |
| explicit_cursor_name%FOUND | BOOLEAN | Explicit cursor FETCH 이전에는 NULL, 데이터가 있는 경우 TRUE, 데이터가 없는 경우 FALSE, CLOSE 이후에는 NULL이다. |
| explicit_cursor_name%NOTFOUND | BOOLEAN | explicit_cursor_name%FOUND와 반대되는 값을 갖는다. |
| explicit_cursor_name%ROWCOUNT | INTEGER | Explicit cursor OPEN 이전에는 NULL, 정상적으로 OPEN 되었다면 0 이다. FETCH를 수행할 때마다 1씩 증가하는데 CLOSE 이후에는 NULL이다. |

<a id="86f8bf2ceacb0332"></a>
#### Explicit Cursor Parameter 사용 예

- Explicit cursor OPEN 전

```
gSQL> 
DECLARE
  CURSOR cur_month IS SELECT month_char, month_num FROM t_month;
BEGIN
  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);
END;
/

cur_month%ISOPEN   = FALSE
cur_month%FOUND    = 
cur_month%NOTFOUND = 
cur_month%ROWCOUNT = 
Anonymous PL block executed.
```

- Explicit cursor OPEN 후

```
gSQL> 
DECLARE
  CURSOR cur_month IS SELECT month_char, month_num FROM t_month;
BEGIN
  OPEN cur_month;
  
  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);

  CLOSE cur_month;
END;
/

cur_month%ISOPEN   = TRUE
cur_month%FOUND    = 
cur_month%NOTFOUND = 
cur_month%ROWCOUNT = 0
Anonymous PL block executed.
```

- Explicit cursor FETCH 후

```
gSQL>
DECLARE
  CURSOR cur_month IS SELECT month_char, month_num FROM t_month LIMIT 3;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN cur_month;


  DBMS_OUTPUT.PUT_LINE( '[ First Fetch ]' );
  
  FETCH cur_month INTO v_month_char, v_month_num;      

  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);


  DBMS_OUTPUT.PUT_LINE( '[ Second Fetch ]' );

  FETCH cur_month INTO v_month_char, v_month_num;      

  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);


  DBMS_OUTPUT.PUT_LINE( '[ Last Fetch ]' );
  
  FETCH cur_month INTO v_month_char, v_month_num;
  
  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);


  DBMS_OUTPUT.PUT_LINE( '[ Over Last Fetch ]' );

  FETCH cur_month INTO v_month_char, v_month_num;            

  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);


  CLOSE cur_month;
END;
/

[ First Fetch ]
cur_month%ISOPEN   = TRUE
cur_month%FOUND    = TRUE
cur_month%NOTFOUND = FALSE
cur_month%ROWCOUNT = 1
[ Second Fetch ]
cur_month%ISOPEN   = TRUE
cur_month%FOUND    = TRUE
cur_month%NOTFOUND = FALSE
cur_month%ROWCOUNT = 2
[ Last Fetch ]
cur_month%ISOPEN   = TRUE
cur_month%FOUND    = TRUE
cur_month%NOTFOUND = FALSE
cur_month%ROWCOUNT = 3
[ Over Last Fetch ]
cur_month%ISOPEN   = TRUE
cur_month%FOUND    = FALSE
cur_month%NOTFOUND = TRUE
cur_month%ROWCOUNT = 3
Anonymous PL block executed.
```

- Explicit cursor CLOSE 후

```
gSQL>
DECLARE
  CURSOR cur_month IS SELECT month_char, month_num FROM t_month;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN cur_month;
  
  FETCH cur_month INTO v_month_char, v_month_num;      

  CLOSE cur_month;

  DBMS_OUTPUT.PUT_LINE('cur_month%ISOPEN   = ' || cur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('cur_month%FOUND    = ' || cur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%NOTFOUND = ' || cur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('cur_month%ROWCOUNT = ' || cur_month%ROWCOUNT);
END;
/

cur_month%ISOPEN   = FALSE
cur_month%FOUND    = 
cur_month%NOTFOUND = 
cur_month%ROWCOUNT = 
Anonymous PL block executed.
```

<a id="c966cf3ff87d8368"></a>
## Cursor Variable

<a id="bb03cf3d79c9223b"></a>
### Create Cursor Variables

Cursor variable을 생성하려면 미리 정의된 SYS_REFCURSOR type의 variable을 선언하거나 REF CURSOR TYPE을 정의하여 해당 유형의 variable을 선언한다. 자세한 내용은 [Cursor Variable Declaration](28-psm-language-element-references.md#92b929c62f63ee43)을 참조한다.

- REF CURSOR type은 다음과 같다.
    - Strong REF CURSOR type
        - REF CURSOR type을 정의할 때 return_type을 명시한 경우, strong REF CURSOR type 이다.
        - Strong REF CURSOR type variable은 정의한 return_type과 동일한 유형을 질의 집합으로 가지는 질의만 CURSOR VARIABLE의 질의로 연결할 수 있다.
        - Strong REF CURSOR type variable 할당은 정의한 return_type이 동일할 경우에 가능하다.
    - Weak REF CURSOR type
        - REF CURSOR type을 정의할 때 return_type을 명시하지 않은 경우, weak REF CURSOR type 이다.
        - SYS_REFCURSOR type도 weak REF CURSOR type 이다.
        - Strong REF CURSOR variable보다 유연하게 사용할 수 있다.
        - Weak REF CURSOR type variable에서 SYS_REFCURSOR type variable로 할당할 수 있고, 반대로 SYS_REFCURSOR type variable에서 weak REF CURSOR type variable로 할당할 수도 있다.

<a id="3e4c041c50bd1c5e"></a>
#### Create Cursor Variable 예

- REF CURSOR type 정의 (definition)

```
gSQL>
DECLARE
  TYPE strong_refcur IS REF CURSOR RETURN t_month%ROWTYPE;   ❶ strong ref cursor type
  TYPE weak_refcur IS REF CURSOR;                            ❷ weak ref cursor type
BEGIN
  NULL;
END;
/

Anonymous PL block executed.
```

- CURSOR VARIABLE 선언 (declaration)

```
gSQL>
DECLARE
  TYPE strong_refcur IS REF CURSOR RETURN t_month%ROWTYPE;   ❶ strong ref cursor type
  TYPE weak_refcur IS REF CURSOR;                            ❷ weak ref cursor type

  v_sys_refcursor     SYS_REFCURSOR;                         ❸ weak ref cursor type variable
  v_strong_refcursor  strong_refcur;                         ❹ strong ref cursor type variable
  v_weak_refcursor    weak_refcur;                           ❺ weak ref cursor type variable
BEGIN
  NULL;
END;
/

Anonymous PL block executed.
```

<a id="d82dca6601c9f06a"></a>
### Opening and Closing Cursor Variables

- Cursor variable을 선언한 후에 [OPEN FOR Statement](28-psm-language-element-references.md#a04f79d8641839a1)를 수행하여 cursor variable과 수행할 SELECT 문 또는 DML 문을 연결한다.
- Cursor 질의에는 OPEN FOR 문의 using 절에 명시된 값을 지정하는 bind variable이 있을 수 있다.
- Cursor 질의에 FOR UPDATE 문이 있을 경우, 결과 집합의 ROW에 LOCK을 잡는다.
- Cursor variable을 REOPEN 할 경우 CLOSE 하지 않아도 되고, REOPEN 하면 이전 질의와의 연결은 끊어진다.
- Cursor variable 사용이 끝난 경우, [CLOSE Statement](28-psm-language-element-references.md#5dd511f3fe54ad01)를 수행하면 된다.
- CLOSE 된 cursor variable의 질의 결과에 접근하거나, cursor variable 속성을 참조할 수 없다.

<a id="f96c20706a3ff420"></a>
#### Cursor Variable의 OPEN 및 CLOSE 예

```
DECLARE
  v_refcur_month SYS_REFCURSOR;
BEGIN
  OPEN v_refcur_month FOR SELECT * FROM t_month;
  CLOSE v_refcur_month;
END;
/

Anonymous PL block executed.
```

- Using 절을 사용한 cursor variable의 OPEN 예

```
gSQL>
DECLARE
  v_refcur_month SYS_REFCURSOR;
  var            INTEGER;
BEGIN
  var := 1;
  
  OPEN v_refcur_month FOR 'SELECT * FROM t_month WHERE month_num = :v' USING IN var;
END;
/

Anonymous PL block executed.
```

<a id="8bdddae9b8afc05f"></a>
### Fetching Data with Cursor Variables

Cursor variable을 OPEN 한 후에 [FETCH Statement](28-psm-language-element-references.md#31aa8d8b5c8ba1f0)를 실행하여 결과 집합의 row를 가져올 수 있다. Cursor variable이 반환하는 결과는 into 절과 호환되어야 한다.

<a id="340f316a4b31ca8d"></a>
#### Cursor Variable의 FETCH 예

```
gSQL>
DECLARE  
  TYPE ref_month IS REF CURSOR RETURN t_month%ROWTYPE;
  v_refcur_month ref_month;
  
  v_month        t_month%ROWTYPE;  
BEGIN
  OPEN v_refcur_month FOR SELECT * FROM t_month;
  
  LOOP
    FETCH v_refcur_month INTO v_month;
    
    EXIT WHEN v_refcur_month%NOTFOUND;
    
    DBMS_OUTPUT.PUT_LINE( 'v_month.month_char : ' || v_month.month_char || ' , v_month.month_num : ' || v_month.month_num );
  END LOOP;
  
  CLOSE v_refcur_month;
END;
/

v_month.month_char : JANUARY , v_month.month_num : 1
v_month.month_char : MARCH , v_month.month_num : 3
v_month.month_char : MAY , v_month.month_num : 5
v_month.month_char : JULY , v_month.month_num : 7
v_month.month_char : SEPTEMBER , v_month.month_num : 9
v_month.month_char : NOVEMBER , v_month.month_num : 11
Anonymous PL block executed.
```

<a id="554940eae83e9ec8"></a>
### Assigning Value to Cursor Variables

Cursor variable은 다른 cursor variable 이나 host variable 값을 할당할 수 있다. Source cursor variable이 OPEN 된 상태로 target cursor variable에 값을 할당하면 두 cursor variable은 동일한 SQL을 가리킨다. Source cursor variable이 OPEN 되지 않은 상태로 target cursor variable에 값을 할당하면 두 cursor variable은 모두 OPEN 되지 않은 상태이다.

<a id="7fda38994c856c7f"></a>
#### Assign Cursor Variable 예

```
gSQL>
DECLARE  
  source_refcur_month SYS_REFCURSOR;
  target_refcur_month SYS_REFCURSOR;
  v_month_char   VARCHAR(15);
  v_month_num    INTEGER;
BEGIN

  DBMS_OUTPUT.PUT_LINE( 'OPEN source_refcur_month' );
  
  OPEN source_refcur_month FOR SELECT * FROM t_month;

  DBMS_OUTPUT.PUT_LINE( 'source_refcur_month%ISOPEN : ' || source_refcur_month%ISOPEN );
  DBMS_OUTPUT.PUT_LINE( 'target_refcur_month%ISOPEN : ' || target_refcur_month%ISOPEN );


  DBMS_OUTPUT.PUT_LINE( 'Assign source_refcur_month to target_refcur_month' );
  
  target_refcur_month := source_refcur_month;

  DBMS_OUTPUT.PUT_LINE( 'source_refcur_month%ISOPEN : ' || source_refcur_month%ISOPEN );
  DBMS_OUTPUT.PUT_LINE( 'target_refcur_month%ISOPEN : ' || target_refcur_month%ISOPEN );


  DBMS_OUTPUT.PUT_LINE( 'CLOSE source_refcur_month' );  

  CLOSE source_refcur_month;

  DBMS_OUTPUT.PUT_LINE( 'source_refcur_month%ISOPEN : ' || source_refcur_month%ISOPEN );
  DBMS_OUTPUT.PUT_LINE( 'target_refcur_month%ISOPEN : ' || target_refcur_month%ISOPEN );
END;
/

OPEN source_refcur_month
source_refcur_month%ISOPEN : TRUE
target_refcur_month%ISOPEN : FALSE
Assign source_refcur_month to target_refcur_month
source_refcur_month%ISOPEN : TRUE
target_refcur_month%ISOPEN : TRUE
CLOSE source_refcur_month
source_refcur_month%ISOPEN : FALSE
target_refcur_month%ISOPEN : FALSE
Anonymous PL block executed.
```

<a id="5465674f7956e946"></a>
### Cursor Variable Attributes

Cursor variable의 속성은 explicit cursor 속성과 동일하며, cursor variable의 상태 정보를 나타낸다. Cursor variable name 뒤에 속성을 붙여 cursor variable 속성으로 사용할 수 있다. cursor_variable_name%ISOPEN 속성을 제외한 나머지 속성의 경우, cursor variable OPEN 전이나 CLOSE 후에는 'cursor is not defined' 에러가 발생한다.

**Cursor variable attributes**

<a id="9a0d1a7dc203a8ef"></a>
| Attribute name | 반환 타입 | 설명 |
| --- | --- | --- |
| cursor_variable_name%ISOPEN | BOOLEAN | Cursor variable이 OPEN 된 상태라면 TRUE, 그 외에는 FALSE 이다. |
| cursor_variable_name%FOUND | BOOLEAN | FETCH 이후 데이터가 있으면 TRUE 이고 없으면 FALSE 이다. |
| cursor_variable_name%NOTFOUND | BOOLEAN | FETCH 이후 cursor_variable_name%FOUND와 반대되는 값을 갖는다. |
| cursor_variable_name%ROWCOUNT | INTEGER | Cursor variable이 OPEN 된 상태라면 0 이고 FETCH를 수행할 때마다 1씩 증가한다. |

<a id="d5ebab09e56943f6"></a>
#### Cursor Variable Attributes 사용 예

- Cursor variable OPEN 전

```
gSQL> 
DECLARE
  v_refcur_month SYS_REFCURSOR;
BEGIN
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);
END;
/

v_refcur_month%ISOPEN   = FALSE
ERR-2F000(17036): cursor is not defined : 
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
                       *
ERROR at line 5:
```

- Cursor variable OPEN 후

```
gSQL> 
DECLARE
  v_refcur_month SYS_REFCURSOR;
BEGIN
  OPEN v_refcur_month FOR SELECT * FROM t_month;
  
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);

  CLOSE v_refcur_month;
END;
/

v_refcur_month%ISOPEN   = TRUE
v_refcur_month%FOUND    = 
v_refcur_month%NOTFOUND = 
v_refcur_month%ROWCOUNT = 0
Anonymous PL block executed.
```

- Cursor variable FETCH 후

```
gSQL>
DECLARE
  v_refcur_month SYS_REFCURSOR;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN v_refcur_month FOR SELECT * FROM t_month LIMIT 3;


  DBMS_OUTPUT.PUT_LINE( '[ First Fetch ]' );
  
  FETCH v_refcur_month INTO v_month_char, v_month_num;      
 
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);


  DBMS_OUTPUT.PUT_LINE( '[ Second Fetch ]' );
  
  FETCH v_refcur_month INTO v_month_char, v_month_num;      
 
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);


  DBMS_OUTPUT.PUT_LINE( '[ Last Fetch ]' );
  
  FETCH v_refcur_month INTO v_month_char, v_month_num;      
 
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);


  DBMS_OUTPUT.PUT_LINE( '[ Over Last Fetch ]' );
  
  FETCH v_refcur_month INTO v_month_char, v_month_num;      
 
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);


  CLOSE v_refcur_month;
END;
/

[ First Fetch ]
v_refcur_month%ISOPEN   = TRUE
v_refcur_month%FOUND    = TRUE
v_refcur_month%NOTFOUND = FALSE
v_refcur_month%ROWCOUNT = 1
[ Second Fetch ]
v_refcur_month%ISOPEN   = TRUE
v_refcur_month%FOUND    = TRUE
v_refcur_month%NOTFOUND = FALSE
v_refcur_month%ROWCOUNT = 2
[ Last Fetch ]
v_refcur_month%ISOPEN   = TRUE
v_refcur_month%FOUND    = TRUE
v_refcur_month%NOTFOUND = FALSE
v_refcur_month%ROWCOUNT = 3
[ Over Last Fetch ]
v_refcur_month%ISOPEN   = TRUE
v_refcur_month%FOUND    = FALSE
v_refcur_month%NOTFOUND = TRUE
v_refcur_month%ROWCOUNT = 3
Anonymous PL block executed.
```

- Cursor variable CLOSE 후

```
gSQL>
DECLARE
  v_refcur_month SYS_REFCURSOR;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  OPEN v_refcur_month FOR SELECT * FROM t_month LIMIT 3;

  FETCH v_refcur_month INTO v_month_char, v_month_num;      
 
  CLOSE v_refcur_month;
   
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ISOPEN   = ' || v_refcur_month%ISOPEN);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%NOTFOUND = ' || v_refcur_month%NOTFOUND);
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%ROWCOUNT = ' || v_refcur_month%ROWCOUNT);
END;
/

gSQL>
v_refcur_month%ISOPEN   = FALSE
ERR-2F000(17036): cursor is not defined : 
  DBMS_OUTPUT.PUT_LINE('v_refcur_month%FOUND    = ' || v_refcur_month%FOUND);
                       *
ERROR at line 13:
```

<a id="8eb85933d4a745aa"></a>
### Cursor Variable as Routine Parameter

Cursor variable을 routine의 parameter로 사용하면 질의 결과를 전달하는데 유용하다. Procedure나 function에서 cursor variable을 FETCH 하거나 CLOSE 하려면 parameter가 IN 또는 IN OUT type 이어야 한다. Cursor variable을 OPEN 하려면 parameter가 OUT 또는 IN OUT type 이어야 한다. Package에서 ref cursor type을 선언하면 서로 다른 routine에서 cursor variable의 질의 결과를 서로 전달하는데 유용하다.

<a id="b2513a6dc0866082"></a>
#### Parameter로 Cursor Variable을 사용하는 예

- Routine parameter로서의 예

```
gSQL>
CREATE OR REPLACE PROCEDURE p_open( p_refcur_month OUT SYS_REFCURSOR ) AS 
BEGIN
  OPEN p_refcur_month FOR SELECT * FROM t_month;
END;
/

Procedure created.

gSQL>
CREATE OR REPLACE PROCEDURE p_fetch( p_refcur_month IN SYS_REFCURSOR ) AS 
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  FETCH p_refcur_month INTO v_month_char, v_month_num;
  DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );
END;
/

Procedure created.

gSQL>
DECLARE
  v_refcur_month SYS_REFCURSOR;
BEGIN
  p_open( v_refcur_month );
  DBMS_OUTPUT.PUT_LINE( 'v_refcur_month%ISOPEN : ' || v_refcur_month%ISOPEN );
  
  p_fetch( v_refcur_month );
  DBMS_OUTPUT.PUT_LINE( 'v_refcur_month%FOUND : ' || v_refcur_month%FOUND );
  
  CLOSE v_refcur_month;
  DBMS_OUTPUT.PUT_LINE( 'v_refcur_month%ISOPEN : ' || v_refcur_month%ISOPEN );
END;
/

v_refcur_month%ISOPEN : TRUE
v_month_char : JANUARY , v_month_num : 1
v_refcur_month%FOUND : TRUE
v_refcur_month%ISOPEN : FALSE
Anonymous PL block executed.
```

- Package의 ref cursor type 사용 예

```
gSQL>
CREATE OR REPLACE PACKAGE pkg_refcur AS
  TYPE ref_month IS REF CURSOR RETURN t_month%ROWTYPE;
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
  
  PROCEDURE p_open( p_refcur_month OUT ref_month, p_month IN INTEGER );
  PROCEDURE p_fetch( p_refcur_month IN ref_month );
  PROCEDURE p_close( p_refcur_month IN ref_month );
END;
/

Package created.

gSQL>
CREATE OR REPLACE PACKAGE BODY pkg_refcur AS
  PROCEDURE p_open( p_refcur_month OUT ref_month, p_month IN INTEGER ) AS
  BEGIN
    IF p_month = 1 THEN
      OPEN p_refcur_month FOR SELECT * FROM t_month WHERE month_num = 1;
    ELSIF p_month = 3 THEN
      OPEN p_refcur_month FOR SELECT * FROM t_month WHERE month_num = 3;
    ELSIF p_month = 5 THEN
      OPEN p_refcur_month FOR SELECT * FROM t_month WHERE month_num = 5;    
    ELSIF p_month = 7 THEN    
      OPEN p_refcur_month FOR SELECT * FROM t_month WHERE month_num = 7;
    ELSIF p_month = 9 THEN        
      OPEN p_refcur_month FOR SELECT * FROM t_month WHERE month_num = 9;    
    ELSIF p_month = 11 THEN
      OPEN p_refcur_month FOR SELECT * FROM t_month WHERE month_num = 11;    
    ELSE
      DBMS_OUTPUT.PUT_LINE( 'NO ODD MONTH' );
    END IF;
    
    DBMS_OUTPUT.PUT_LINE( 'p_refcur_month%ISOPEN : ' || p_refcur_month%ISOPEN );
  END;
  
  PROCEDURE p_fetch( p_refcur_month IN ref_month ) AS
  BEGIN
    FETCH p_refcur_month INTO v_month_char, v_month_num;
    DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );
  END;
  
  PROCEDURE p_close( p_refcur_month IN ref_month ) AS
  BEGIN
    CLOSE p_refcur_month;
    DBMS_OUTPUT.PUT_LINE( 'p_refcur_month%ISOPEN : ' || p_refcur_month%ISOPEN );    
  END;
END;
/

Package created.

gSQL>
DECLARE
  v_pkg_refcur_month pkg_refcur.ref_month;
BEGIN
  pkg_refcur.p_open( v_pkg_refcur_month, 5 );
  pkg_refcur.p_fetch( v_pkg_refcur_month );
  pkg_refcur.p_close( v_pkg_refcur_month );  
END;
/

p_refcur_month%ISOPEN : TRUE
v_month_char : MAY , v_month_num : 5
p_refcur_month%ISOPEN : FALSE
Anonymous PL block executed.
```

<a id="2a0c2e4c2ba74f54"></a>
### Cursor Variable as Host Variable

Cursor variable은 host variable로 선언할 수 있다. Host cursor variable은 서버와 클라이언트 간에 질의 결과를 전달하는데 유용하며, 서버와 클라이언트 간에 동일한 질의 결과 집합을 공유할 수 있다.

Cursor variable을 host variable로 사용하기 위해서는 REF CURSOR type인 host variable을 선언하고 서버로 전달하여 사용한다. 서버와 클라이언트 간의 cursor variable 호출에는 제한이 없다. 클라이언트에서 cursor variable을 선언하고 서버에서 OPEN 한 후 Fetch 하고, 이 후 클라이언트에서 FETCH 한 후에 닫을 수 있다.

<a id="e147a74fb771f723"></a>
#### Host Cursor Variable 예

```
gSQL>
\var host_refcur_month REFCURSOR

gSQL>
BEGIN
  OPEN :host_refcur_month FOR SELECT * FROM t_month;
END;
/

Anonymous PL block executed.

gSQL>
DECLARE
  v_month_char VARCHAR(15);
  v_month_num  INTEGER;
BEGIN
  FETCH :host_refcur_month INTO v_month_char, v_month_num;
  DBMS_OUTPUT.PUT_LINE( 'v_month_char : ' || v_month_char || ' , v_month_num : ' || v_month_num );  
END;
/

v_month_char : JANUARY , v_month_num : 1
Anonymous PL block executed.

gSQL>
BEGIN
  CLOSE :host_refcur_month;
END;
/

Anonymous PL block executed.
```

---

[← 23. PSM Control Statements](23-psm-control-statements.md) · [전체 목차](../README.md) · [25. Using PSM Subprograms →](25-using-psm-subprograms.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
