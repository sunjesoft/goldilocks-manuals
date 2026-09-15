<a id="e33e66504e603815"></a>

# 25. PSM Packages

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/e33e66504e603815)  
> 태그: `20c.1_30_tag`

[← 24. Using SQLs in PSM](24-using-sqls-in-psm.md) · [전체 목차](../README.md) · [26. PSM Language Element References →](26-psm-language-element-references.md)

본 장에서는 package를 이용하여 여러 응용 프로그램에서 공통으로 사용되는 데이터와 PSM 코드를 모듈화하는 방법에 대해 설명한다.

<a id="bc11a80f80ccb464"></a>
## 정의

Package는 논리적으로 관련이 있는 PSM 타입, 변수, subprogram, 커서, 예외 등의 항목을 묶어 놓은 스키마 객체이다. Package는 컴파일 과정을 거쳐 데이터베이스에 저장되는데 이는 다른 프로그램 (다른 package, 프로시저, 외부 프로그램 등)에서 package 항목을 참조, 공유, 실행할 수 있도록 하기 위함이다.

모든 package에는 참조 가능하도록 공개된 여러 item들과 subprogram들의 목록이 기술된 specification이 있다.   
만일 공개된 item 중에 cursor가 존재하거나 공개된 subprogram이 존재하는 경우, 해당 package는 package body를 가질 수 있다. Body는 다음과 같은 내용들을 포함한다.

- 공개된 커서가 수행할 SQL 구문이나 공개된 subprogram이 수행할 PSM code 
- 공개되지 않고 내부적으로만 사용되는 여러 변수, 타입 등의 item이나 subprogram들
- Package가 처음으로 사용될 때 (instantiation) 한 번만 수행되는 공개 item 초기화 code (Initialization part)

Package specification의 AUTHID 구문은 해당 package를 invoker 권한으로 수행할지 definer 권한으로 수행할지 (Default: definer) 여부와 함께 unqualified 객체를 참조할 때 invoker로써 해석할지 definer로써 해석할지를 지정한다.

Package specification 정의 구문은 해당 package 소유자와 EXECUTE PACKAGE 권한을 부여받은 사용자들만 검색할 수 있다. 반면에 package body 정의 구문은 해당 package의 소유자만 검색할 수 있다.

<a id="90d9a85da8f5ca12"></a>
## 특장점

Package의 다음 기능들은 응용 프로그램 개발자와 운영자에게 높은 신뢰도와 재사용성을 제공한다.

- 모듈화 기능 
    - 관련된 item과 subprogram들을 하나로 모아둔 덕분에 데이터 베이스를 관리하고 그 구조를 이해하기 쉽다.
- 프로그램 설계의 용이성 
    - Specification만 정의하면 body를 정의하지 않더라도 관련 응용 프로그램을 설계할 수 있다.
- 캡슐화 
    - Package 내부 구현 사항인 body의 내용을 package 사용자들이 볼 수 없게 숨길 수 있다.
    - 해당 package를 사용하는 SQL과 응용 프로그램을 recompile 하지 않고도 구현 내용인 body를 변경할 수 있다.
- 성능 최적화
    - 메모리에 package 전체가 한 번에 로딩되므로 메모리 내부의 subprogram을 빠르게 호출할 수 있다. 
- 권한 관리의 용이성
    - Package 안에 포함된 모든 공개 item들과 subprogram들 각각에 대한 사용 권한을 package 전체에 대한 권한 하나로 묶을 수 있다.

Package는 subprogram overloading을 지원하지 않으므로 이름이 같은 함수들을 동일한 block scope 내에 정의할 수 없다.

<a id="ae788414516ff62f"></a>
## Specification

Package specification에 선언할 수 있는 공개 item들은 다음과 같다.

- 사용자 정의 타입
    - Record or collection (Associative array)
    - Package 안에 선언된 사용자 정의 타입은 PSM 계열 statement 내에서만 사용될 수 있다.
- 변수
    - 변수를 직접 참조하지 않도록 하기 위해 각 변수에 대해 get/ set subprogram을 정의할 것을 권장한다.
- Subprogram
    - 프로시져 (Procedure)
    - 함수 (Function)
- 명시적 커서 (Explicit cursor)
    - 이름과 반환 타입만 package specification에 정의한 후 커서가 수행할 SQL 구문은 body에 정의할 수도 있다.
    - 커서 변수 (cursor variable)는 package의 공개 item으로 정의할 수 없다.
- 사용자 정의 예외 (Exception)

<a id="b90217271a894010"></a>
### Package Specification 생성

CREATE PACKAGE 구문을 사용하여 package specification을 생성한다.

```
CREATE OR REPLACE PACKAGE MY_PKG
IS
  TYPE MY_REC IS RECORD (F1 INTEGER, F2 INTEGER );
END;
/

Package created.
```

정의된 package의 공개 item들은 다음과 같이 package 이름과 같이 명시하여 package 외부에서 참조 가능하게 할 수 있다.

```
DECLARE
V1 MY_PKG.MY_REC;
BEGIN
    V1.F1 := 10;
    V1.F2 := 20;
    DBMS_OUTPUT.PUT_LINE( 'V1.F1 = ' || V1.F1 || ', V1.F2 = ' || V1.F2 );
END;
/
V1.F1 = 10, V1.F2 = 20
Anonymous PL block executed.
```

<a id="4e9eb4dde13879a0"></a>
### Package Body 생성

Package에 공개된 커서 또는 subprogram이 있거나 초기화 코드가 필요한 경우에는 body를 선언해야 할 수 있다. 그 외의 경우에 body는 선택적으로 선언한다.

Package body에는 다음과 같은 제약사항이 있다.

- Package body는 package specification과 동일한 스키마에 생성되어야 한다.
- Package body는 package specification과 동일한 이름을 가져야 한다.
- Package specification에 선언된 공개 커서 중에 SQL 구문이 지정되지 않은 커서가 있을 경우, 반드시 그것과 이름, 레코드 타입, 인자들이 동일한 커서에 SQL을 명시하여 body에 정의해야 한다.
- Package specification에 선언된 공개 subprogram의 이름, 인자, 반환 타입과 동일한 subprogram이 body에도 동일하게 정의되어야 한다.
- Package body에는 package specification에 정의된 변수, 타입, 예외와 동일한 이름의 변수, 타입, 예외를 선언할 수 없다.

다음과 같이 package body를 생성한다.

```
CREATE TABLE emp( empno NUMBER, sal NUMBER, comm NUMBER );
Table created.

INSERT INTO emp VALUES( 3548, 6000, 1000 );
1 row created.

INSERT INTO emp VALUES( 9369, 5000, NULL );
1 row created.

INSERT INTO emp VALUES( 7294, 4000, 500 );
1 row created.

COMMIT;
Commit complete.


CREATE OR REPLACE PACKAGE emp_mgmt
IS
  PROCEDURE adjust_sal(v_flag VARCHAR, v_empno NUMBER, v_pct NUMBER);
  FUNCTION get_annual_sal(v_empno NUMBER) RETURN NUMBER;
END;
/

Package created.


CREATE OR REPLACE PACKAGE BODY emp_mgmt
IS
  PROCEDURE adjust_sal(v_flag VARCHAR, v_empno NUMBER, v_pct NUMBER) IS
  BEGIN
    IF v_flag = 'INCREASE' THEN
      UPDATE emp SET sal = sal + (sal * (v_pct / 100)) WHERE empno = v_empno;
    ELSE
      UPDATE emp SET sal = sal - (sal * (v_pct / 100)) WHERE empno = v_empno;
    END IF;
  END;
  FUNCTION get_annual_sal (v_empno NUMBER) RETURN NUMBER
  IS
    v_sal NUMBER;
  BEGIN
    SELECT (sal + NVL(comm,0)) * 12 INTO v_sal FROM emp WHERE empno = v_empno;
    RETURN v_sal;
  END;
END;
/

Package created.
```

다음과 같이 생성된 package body의 subprogram들을 호출할 수 있다.

```
call emp_mgmt.adjust_sal('INCREASE',7369, 10);

Procedure Call complete.


SELECT emp_mgmt.get_annual_sal(7294) FROM DUAL;
EMP_MGMT.GET_ANNUAL_SAL(7294)
-----------------------------
                        54000
1 row selected.
```

<a id="4e8bbe2d6e84ebe1"></a>
### Package 상태

Package는 각 session에서 처음으로 참조되거나 호출되었을 때 instance화 (instantiation) 되는데 이 때 다음과 같은 작업이 발생한다.

- 공개된 변수를 선언할 때 명시한 초기값 설정
- Body에 초기화 코드가 정의되어 있을 경우, 해당 코드 실행

Package specification에 하나 이상의 공개된 변수나 커서가 존재하는 package를 stateful package 라고 하고 그렇지 않은 package는 stateless package 라고 한다.

일반적으로 package 상태는 session의 lifetime과 동일하게 유지되지만 stateful package의 경우, 다음과 같은 경우에 invalidate되어 instance가 초기화된다.

- ALTER PACKAGE 구문을 실행하여 package specification이 recompile 된 경우
- Package specification이 참조한 객체들 중 어느 하나에라도 package instance의 형상에 영향을 줄 수 있는 변경 (DDL) 작업이 발생한 경우
    - 예를 들어 변수 타입을 선언하기 위해 참조한 table에 대해 CREATE INDEX를 실행할 때는 invalidate 되지 않지만 ADD COLUMN을 실행할 때는 경우에 따라 invalidate 될 수 있다.
- Session 내에 instance화 된 package들 중 하나라도 invalidate 될 경우

Stateless package는 상태를 가지지 않기 때문에 관련 객체의 형상이 변경되더라도 자동으로 recompile 되어 수행할 수 있지만 stateful package에는 instance가 invalidate 될 수 있다. 따라서 응용 프로그램에서 package를 사용할 때는 이런 상황에 따른 예외 처리에 유의해야 한다.

---

[← 24. Using SQLs in PSM](24-using-sqls-in-psm.md) · [전체 목차](../README.md) · [26. PSM Language Element References →](26-psm-language-element-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
