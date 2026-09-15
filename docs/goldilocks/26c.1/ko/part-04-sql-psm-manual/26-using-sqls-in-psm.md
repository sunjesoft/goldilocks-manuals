<a id="bed68c5444868b93"></a>

# 26. Using SQLs in PSM

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/bed68c5444868b93)  
> 태그: `26c.1_0_tag`

[← 25. Using PSM Subprograms](25-using-psm-subprograms.md) · [전체 목차](../README.md) · [27. PSM Packages →](27-psm-packages.md)

<a id="ef17d120325bea28"></a>
## Static SQLs

<a id="71fe5dd533cb0f19"></a>
### 개요

Static SQL은 GOLDILOCKS에서 지원하는 PSM 변수를 사용할 수 있도록 확장된 SQL이다.   
SQL에서 bind parameter를 사용할 수 있는 expression의 모든 곳에서 PSM 변수를 사용할 수 있다.

- SELECT INTO Statement
    - 자세한 내용은 PSM Language Element References의 [SELECT INTO Statement](30-psm-language-element-references.md#ae316b261e4e6598)를 참조한다.
- Data Manipulation Language( DML )
    - INSERT Statement Extension
        - 자세한 내용은 PSM Language Element References의 [INSERT Statement Extension](30-psm-language-element-references.md#bad4432950ae600a)를 참조한다.
    - INSERT INTO ... UPDATE Statement Extension
        - 자세한 내용은 PSM Language Element References의 [INSERT INTO ... UPDATE Statement Extension](30-psm-language-element-references.md#b4fbf41981dfde9d)를 참조한다.
    - UPDATE Statement Extension
        - 자세한 내용은 PSM Language Element References의 [UPDATE Statement Extension](30-psm-language-element-references.md#eef0130cc744e99e)를 참조한다.
    - DELETE Statement Extension
        - 자세한 내용은 PSM Language Element References의 [DELETE Statement Extension](30-psm-language-element-references.md#b7ff64cf994a5599)를 참조한다.
- Transaction Control Language
    - COMMIT
        - 자세한 내용은 SQL References의 [COMMIT](../part-03-sql-manual/19-sql-references-c-g.md#9d9942a1324d8ced)을 참조한다.
    - ROLLBACK
        - 자세한 내용은 SQL References의 [ROLLBACK](../part-03-sql-manual/20-sql-references-h-z.md#1ba3b433854d9411)을 참조한다.
    - SAVEPOINT
        - 자세한 내용은 SQL References의 [SAVEPOINT savepoint_specifier](../part-03-sql-manual/20-sql-references-h-z.md#903816d217929cbc)를 참조한다.
    - LOCK TABLE
        - 자세한 내용은 SQL References의 [LOCK TABLE](../part-03-sql-manual/20-sql-references-h-z.md#aa7af8e829d2f1c4)을 참조한다.

<a id="9567614006ca7122"></a>
#### 사용 예

- Built-in data type인 PSM 변수를 사용하는 경우

```
gSQL> 
DECLARE
  v_id      NUMBER;
  v_name    VARCHAR(50);
BEGIN
  -- SELELECT INTO Statement
  SELECT id , name
    INTO v_id , v_name 
    FROM emp
   WHERE id = 201;

   DBMS_OUTPUT.PUT_LINE( '[SELECT INTO] ' || v_id || ' , ' || v_name );

  -- INSERT Statement Extension
  v_id   := 200;
  v_name := 'Jennifer Whalen';
  INSERT INTO emp VALUES( v_id , v_name );
     
  -- DELETE Statement Extension
  DELETE FROM emp 
   WHERE id = v_id
  RETURNING name INTO v_name;

  DBMS_OUTPUT.PUT_LINE( '[DELETE] ' || v_id || ' , ' || v_name );
 
  -- UPDATE Statement Extension
  UPDATE emp 
     SET id = v_id , name = v_name
   WHERE id = 200;

  -- Commit
  COMMIT;
END;
/

[SELECT INTO] 201 , Michael Hartstein
[DELETE] 200 , Jennifer Whalen
Anonymous PL block executed.
```

- ROW type인 PSM 변수를 사용하는 경우

```
gSQL>
DECLARE
  TYPE rec_emp IS RECORD( f_id emp.id%TYPE , f_name emp.name%TYPE );
  v_rec_emp rec_emp;

BEGIN
  -- SELELECT INTO Statement
  SELECT id , name
    INTO v_rec_emp 
    FROM emp
   WHERE id = 201;

   DBMS_OUTPUT.PUT_LINE( '[SELECT INTO] ' || v_rec_emp.f_id ||
                         ' , ' || v_rec_emp.f_name );

  -- INSERT Statement Extension
  v_rec_emp.f_id   := 200;
  v_rec_emp.f_name := 'Jennifer Whalen';
  INSERT INTO emp VALUES( v_rec_emp.f_id , v_rec_emp.f_name );
     
  -- DELETE Statement Extension
  DELETE FROM emp 
   WHERE id = v_rec_emp.f_id
  RETURNING * INTO v_rec_emp;

   DBMS_OUTPUT.PUT_LINE( '[DELETE] ' || v_rec_emp.f_id ||
                         ' , ' || v_rec_emp.f_name );
 
  -- UPDATE Statement Extension
  UPDATE emp 
     SET ROW = v_rec_emp
   WHERE id = 200;

  -- Commit
  COMMIT;
END;
/

[SELECT INTO] 201 , Michael Hartstein
[DELETE] 200 , Jennifer Whalen
Anonymous PL block executed.
```

<a id="8d93826c36259d0f"></a>
### Processing Query Result Sets

PSM에서는 implicit cursor 또는 explicit cursor를 사용하여 결과 집합을 처리한다.

PSM이 정의하는 implicit cursor는 다음과 같다.

    - SELECT INTO
    - Implicit Cursor FOR LOOP

PSM이 정의하는 explicit cursor는 다음과 같다.

    - Explicit Cursor FOR LOOP
        - 사용자가 정의한 explicit cursor로써 PSM 구문이 실행되는 동안 사용할 수 있다.

<a id="73a52ea28d3a5b49"></a>
#### Processing Query Result Sets with SELECT INTO Statements

Implicit cursor를 사용하여 SELECT INTO statement을 실행하는 방식으로 값을 검색하고 PSM 변수에 저장한다.  
Select into statement의 결과 집합은 항상 single row이다.

<a id="f602058c4b8d6082"></a>
##### 사용 예

```
gSQL>
DECLARE
  v_id   emp.id%TYPE;
  v_name emp.name%TYPE;
BEGIN
  SELECT id , name
    INTO v_id , v_name
    FROM emp
   WHERE id = 201;
   
   DBMS_OUTPUT.PUT_LINE( 'SQL%FOUND = ' || SQL%FOUND );
END;
/

SQL%FOUND = TRUE
Anonymous PL block executed.
```

<a id="a6f01e3d5c2f250c"></a>
#### Processing Query Result Sets with Cursor FOR LOOP Statements

Cursor For LOOP statement는 implicit cursor와 explicit cursor를 실행하여 결과 집합의 row를 반복적으로 반환한다.

SELECT 문을 사용하는 cursor FOR LOOP statement를 implicit cursor FOR LOOP statement라고 한다. Implicit cursor FOR LOOP statement는 select statement를 위한 implicit cursor를 사용하여 결과 집합의 row을 반환한다.

Cursor FOR LOOP statement에는 사용자가 선언한 explicit cursor를 사용할 수 있다.  
사용자가 선언한 explicit cursor는 PSM block의 다른 statement에서도 사용할 수 있다.

Cursor FOR LOOP statement는 cursor가 loop index로 반환하는 유형에 대한 %ROWTYPE 변수를 암시적으로 생성하여 사용한다.  
Loop index는 cursor FOR LOOP statement를 실행하는 동안에만 사용할 수 있는 변수이다.  
Loop 중에 실행되는 PSM statement에서 loop index를 사용하여 레코드와 필드를 참조할 수 있다.

Cursor FOR LOOP statement는 loop index 변수를 생성한 후에 사용자가 지정한 cursor를 열어 실행한다.  
Loop를 반복할 때마다 row 결과를 loop index 변수에 저장한다.  
더 이상 반환되는 row가 없을 경우 cursor가 닫힌다. 또한, 실행 중에 예외가 발생하는 경우에도 cursor가 닫힌다.

<a id="50e2c11f96256e05"></a>
##### 사용 예

- Cursor FOR LOOP statement에서 SELECT statement를 사용하는 경우

```
gSQL> 
BEGIN
  FOR tmp IN ( SELECT id , name , manager_id FROM emp ) LOOP
    DBMS_OUTPUT.PUT_LINE( 'id = ' || tmp.id || 
                          ' , name = ' || tmp.name || 
                          ' , manager_id = ' || tmp.manager_id );
  END LOOP;


END;
/

id = 200 , name = Jennifer Whalen   , manager_id = 101
id = 201 , name = Michael Hartstein , manager_id = 101
id = 202 , name = Pat Fay           , manager_id = 301
id = 203 , name = Susan Mavris      , manager_id = 201
id = 204 , name = Hermann Baer      , manager_id = 201
id = 205 , name = Shelley Higgins   , manager_id = 301
id = 206 , name = William Gietz     , manager_id = 201
Anonymous PL block executed.
```

- Cursor FOR LOOP statement에서 explicit cursor를 사용하는 경우
    - Explicit cursor에 parameter가 없는 경우

```
gSQL>
DECLARE
  CURSOR cur1 IS SELECT id , name , manager_id FROM emp;
BEGIN
  FOR tmp IN cur1 LOOP
    DBMS_OUTPUT.PUT_LINE( 'id = ' || tmp.id || 
                          ' , name = ' || tmp.name || 
                          ' , manager_id = ' || tmp.manager_id );
  END LOOP;
END;
/

id = 200 , name = Jennifer Whalen   , manager_id = 101
id = 201 , name = Michael Hartstein , manager_id = 101
id = 202 , name = Pat Fay           , manager_id = 301
id = 203 , name = Susan Mavris      , manager_id = 201
id = 204 , name = Hermann Baer      , manager_id = 201
id = 205 , name = Shelley Higgins   , manager_id = 301
id = 206 , name = William Gietz     , manager_id = 201
Anonymous PL block executed.
```

    - Explicit cursor에 parameter가 있는 경우

```
gSQL> 
DECLARE
  CURSOR cur1( p1 NUMBER ) IS SELECT id , name , manager_id 
                                FROM emp 
                               WHERE manager_id = p1;
BEGIN
  FOR tmp IN cur1( 201 ) LOOP
    DBMS_OUTPUT.PUT_LINE( 'id = ' || tmp.idgSQL>  || 
                          ' , name = ' || tmp.name || 
                          ' , manager_id = ' || tmp.manager_id );
  END LOOP;
END;
/

id = 203 , name = Susan Mavris      , manager_id = 201
id = 204 , name = Hermann Baer      , manager_id = 201
id = 206 , name = William Gietz     , manager_id = 201
Anonymous PL block executed.
```

<a id="a967c9c4c6a3dd90"></a>
#### Processing Query Result Sets with Explicit Cursors, OPEN, FETCH, and CLOSE

결과 집합을 원하는 대로 제어하기 위해 explicit cursor를 선언하여 사용한다.  
Explicit cursor를 선언한 후에 사용자가 OPEN, FETCH, CLOSE statement를 사용하여 결과 집합을 관리할 수 있다.

이와 같은 PL statement를 사용한 질의는 복잡해 보이더라도 다음과 같이 유연하게 결과 집합을 관리할 수 있다는 장점이 있다.

    - 여러 explicit cursor를 사용하여, 결과 집합을 병렬로 처리할 수 있다.
    - 단일 loop statement에서 결과 집합의 여러 row를 병렬 처리하거나, 특정 row를 건너뛸 수 있다.
    - 또한, 여러 loop statement를 사용하여 결과 집합을 분할하여 처리할 수 있다.

자세한 사항은 [Explicit Cursor](24-psm-cursor-statements.md#b5976a7f6342e62c)를 참조한다.

<a id="1940fa94f2faa74c"></a>
## Dynamic SQL

Dynamic SQL은 static SQL과 달리 syntax가 실행 시점에 결정된다.

PSM에서는 EXECUTE IMMEDIATE나 OPEN FOR 구문을 통해 run-time에 사용자가 작성한 dynamic SQL을 수행할 수 있다.

- 다음과 같은 경우에 dynamic SQL을 사용한다.
    - Compile 할 때 SQL 문을 결정할 수 없는 경우 (예: 조건에 따라 SQL 문이 달라져야 하는 경우)
    - Static SQL에서 지원되지 않는 SQL을 수행하는 경우 (예: DDL)
- Dynamic SQL은 실행 시점까지 syntax를 알 수 없기 때문에 syntax 오류, 대상 object의 존재 여부, 사용자 권한 등의 validation에 따라 run-time 오류가 발생할 수 있다.

- Dynamic SQL은 다음과 같은 PSM statement에서 사용할 수 있다.
    - [EXECUTE IMMEDIATE Statement](30-psm-language-element-references.md#527305bdfcd7c7ed) 
    - [OPEN FOR Statement](30-psm-language-element-references.md#eb4bf8bad6641506)

<a id="d86b4f96e6a55c69"></a>
### EXECUTE IMMEDIATE

EXECUTE IMMEDIATE에서는 다양한 dynamic SQL을 수행할 수 있다. 다만, PSM에서 제공되는 SQL extension 형태의 구문은 사용할 수 없다.

다음과 같은 형태의 구문이 제공된다.

```
EXECUTE IMMEDIATE 'dynamic sql' [ USING [IN | OUT | INOUT] variable_list] [INTO variable_list] [RETURNING INTO variable_list]
```

EXECUTE IMMEDIATE 구문에 제공되는 USING, INTO, RETURNING INTO 구문을 통해 PSM 변수에 저장된 값을 데이터베이스에 적용하거나 데이터베이스로부터 PSM 변수에 값을 저장할 수 있다.   
각 구문의 사용 방법에는 다음과 같은 차이가 있다.

- USING 
    - PSM 변수의 값을 SQL에 적용할 경우 IN-mode를 사용한다.
    - SQL의 처리 결과를 PSM 변수에 저장하고자 할 경우 OUT-mode를 사용한다.
        - 따라서 OUT-mode로 사용된 경우 반드시 PSM 변수로 기술되어야 한다. (Expression 사용 불가)
    - USING 절에 기술된 변수의 binding type이 명시되지 않을 경우 IN-mode가 적용 된다.
    - SELECT의 target을 USING OUT으로 반환받을 경우 SELECT INTO 절을 사용한 것과 동일하게 동작한다.
    - 데이터베이스로부터는 single row만 반환받을 수 있으며 두 개 이상의 결과가 발생하면 오류가 발생한다.
    - USING IN 절의 PSM 변수는 scalar type 형태로만 사용할 수 있다.
    - USING OUT 절의 PSM 변수는 record type도 가능하지만 다른 유형과 섞어서 사용할 수는 없다.
- INTO
    - 데이터베이스 내부적으로 implicit cursor를 사용하여 처리되는 SELECT의 결과를 저장할 경우에 사용한다.
    - SELECT 절을 dynamic SQL 방식으로 실행했을 경우에만 사용할 수 있다. (SELECT INTO 절 사용 불가)
    - PSM 변수는 record-type도 가능하지만 다른 유형과 섞어서 사용할 수 없다.
- RETURING INTO
    - INSERT/ UPDATE/ DELETE에 의해 처리된 데이터의 전/ 후를 저장할 경우에 사용한다.
    - Single row만 저장할 수 있다.
    - PSM 변수는 record type도 가능하지만 다른 유형과 섞어서 사용할 수 없다.

다음은 dynamic SQL을 사용하여 SELECT_INTO 구문의 결과를 출력하는 예이다.

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
BEGIN
  EXECUTE IMMEDIATE 'SELECT * INTO ?, ? FROM T1 WHERE C1 = ''Seoul''' 
  USING OUT V1, OUT V2;

  DBMS_OUTPUT.PUT_LINE('V1 = ' || V1);
  DBMS_OUTPUT.PUT_LINE('V2 = ' || V2);
END;
/
V1 = Seoul
V2 = 24

Anonymous PL block executed.
```

다음은 갱신 연산을 수행하고 갱신되기 이전의 결과를 RETURNING INTO에 기술된 변수로 저장하는 예이다.

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
  V3 VARCHAR(20);
  V4 VARCHAR(20);
BEGIN
  V1 := 'Daegu';
  V2 := '50';

  EXECUTE IMMEDIATE 
      'UPDATE T1 SET C1 = ? ,  C2 = ? WHERE C1 = ''Seoul'' RETURNING OLD * INTO ?, ?' 
  USING V1, V2 RETURNING INTO V3, V4;

  DBMS_OUTPUT.PUT_LINE('V3 = ' || V3);
  DBMS_OUTPUT.PUT_LINE('V4 = ' || V4);
END;
/
V3 = Seoul
V4 = 24

Anonymous PL block executed.
```

자세한 내용은 [EXECUTE IMMEDIATE Statement](30-psm-language-element-references.md#527305bdfcd7c7ed)를 참조한다.

<a id="41167b4dcced30fa"></a>
### OPEN FOR, FETCH and CLOSE

EXECUTE IMMEDIATE를 사용하여 조회를 처리할 경우 한 건 이상을 데이터베이스로부터 반환받을 수 없다. 처리할 SQL이 dynamic SQL이고 cursor와 같이 두 건 이상의 결과 집합을 fetch 해야 할 경우라면 OPEN FOR를 사용할 수 있다.

다음과 같은 형태로 OPEN FOR에 dynamic SQL을 사용할 수 있다.

```
OPEN Cursor_variable FOR dynamic_sql [USING variable_list]
```

다음은 dynmaic SQL을 통해 OPEN FOR를 수행하는 예이다.

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
  v3 VARCHAR(20);

  cv1 SYS_REFCURSOR;
  sqlstr VARCHAR(1024);
BEGIN
   
    sqlstr := 'SELECT * FROM T1 WHERE C1 >= ?';

    v3 := 'AAAA';
    OPEN cv1 FOR sqlstr USING v3;

    FETCH cv1 INTO v1, v2;

    DBMS_OUTPUT.PUT_LINE('V1 = ' || V1 || ' , V2 = ' || V2);

    CLOSE cv1;
END;
/
V1 = Seoul , V2 = 24

Anonymous PL block executed.
```

- OPEN FOR Statement의 USING 절에는 다음과 같은 제한이 있다.
    - Binding mode
        - IN mode만 가능하다.
    - 사용 가능한 항목
        - PSM 변수
        - Scalar type으로 결과가 반환되는 value expression이다.

자세한 내용은 [OPEN FOR Statement](30-psm-language-element-references.md#eb4bf8bad6641506), [FETCH Statement](30-psm-language-element-references.md#2be71b2c548c858e), [CLOSE Statement](30-psm-language-element-references.md#c59c992edb95f702)를 참조한다.

---

[← 25. Using PSM Subprograms](25-using-psm-subprograms.md) · [전체 목차](../README.md) · [27. PSM Packages →](27-psm-packages.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
