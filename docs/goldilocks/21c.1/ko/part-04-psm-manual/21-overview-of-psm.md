<a id="dc7b24403ddc357d"></a>

# 21. Overview of PSM

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/dc7b24403ddc357d)  
> 태그: `21c.1_35_tag`

[← 20. SQL References (H~Z)](../part-03-sql-manual/20-sql-references-h-z.md) · [전체 목차](../README.md) · [22. PSM DataTypes →](22-psm-datatypes.md)

<a id="59e32504eb2a2813"></a>
## PSM의 특장점

<a id="d9565d21420b3a71"></a>
### SQL과의 긴밀한 연동

GOLIDILOCKS PSM은 GOLDILOCKS SQL과 긴밀하게 연동하여 사용할 수 있다.

- GOLDILOCKS SQL에서 지원하는 모든 데이터 타입을 지원한다.
- Attribute type (%TYPE, %ROWTYPE)을 지원하므로 테이블과 column 타입을 유연하게 사용할 수 있다.
- GOLDILOCKS SQL에서 지원하는 모든 연산자와 built-in 함수를 지원한다.
- GOLDILOCKS SQL에서 지원하는 모든 DML, DCL (COMMIT/ ROLLBACK 등) 들을 지원한다.
- Cursor를 선언하고 OPEN, FETCH, CLOSE 구문을 사용하여 SQL SELECT 구문을 지원한다.
- Dynamic SQL statement 기능을 통해 SQL DDL 구문을 지원한다.

<a id="f2c831ef0166d2f1"></a>
### 성능 향상

GOLDILOCKS PSM은 서버 내부에서만 실행되므로 사용자 응용 프로그램과 DBMS 서버 사이의 통신 횟수를 줄여 전체적인 성능을 향상시킨다.

<a id="c848c0d046a50890"></a>
### 생산성 향상

GOLDILOCKS PSM의 언어는 script 언어와 유사하므로 적은 노력으로 원하는 기능을 위한 코드를 작성할 수 있다. 사용자의 업무 로직을 모듈화하여 procedure/ 함수로 제작하면 client 응용 프로그램들을 작성하는 시간을 줄일 수 있다.

<a id="301290bc714598cf"></a>
### 이식성

GOLDILOCKS PSM으로 작성된 procedure/ 함수는 ODBC, JDBC, embedded SQL 및 다양한 개발 tool 들에서 동일하게 사용할 수 있다. 또한 서버나 client의 platform 종류에 관계없이 동일하게 작동하므로 종류가 다른 platform에도 쉽게 이식할 수 있다.

<a id="7e06fa8e8e6c8d1d"></a>
### 관리의 용이성

GOLDILOCKS PSM은 개별 client에 각각 존재하는 유사 로직을 단 하나의 모듈로 서버에 구현하므로 관리가 용이하며 해당 모듈을 사용하는 도중에 필요에 따라 변경할 수도 있다.

<a id="60587e3b4abcd780"></a>
## Language Elements

<a id="bea23c2b17f096f8"></a>
### Data Types

GOLDILOCKS PSM은 GOLDILOCKS SQL에서 제공하는 모든 built-in data type들을 제공하며, 사용자가 정의하는 record와 collection 타입까지 지원한다.    
자세한 내용은 [PSM DataTypes](22-psm-datatypes.md#532cba9e7e8dd886)를 참조한다.

<a id="4d93b50310ec643b"></a>
### Variables

GOLDILOCKS PSM에서 사용자가 필요에 의해 선언한 변수는 모든 expression에서 사용할 수 있다.

자세한 내용은 다음을 참조한다.  
• [선언부 (Declarative Part)](23-psm-control-statements.md#66fbcd47ef334da1)  
• [Assignment](23-psm-control-statements.md#1af288b08e981d6d)

<a id="493e593a1ec48244"></a>
### Control Structures

GOLDILOCKS PSM은 일반적인 script 언어들이 제공하는 판단 분기문, GOTO와 같은 무조건 분기문, 반복 수행을 위한 loop 구문들을 대부분 지원한다.   
자세한 내용은 [PSM Control Statements](23-psm-control-statements.md#d68b2e1230f9c4f9)를 참조한다.

<a id="ed4507cab2c626c6"></a>
### Subprograms

GOLDILOCKS PSM subprogram은 이름을 가지고 있고 반복적으로 수행될 수 있는 PSM block이다. 인자를 갖는 subprogram의 경우, 호출할 때마다 서로 다른 인자를 주어 실행시킬 수 있다.   
Subprogram은 procedure나 함수 두 가지 형태 중 하나이며 함수 형태는 반환값을 가진다. 또한 특정 block 내에서 선언되고 그 안에서만 사용되는 nested subprogram도 지원한다.    
자세한 내용은 [Using PSM Subprograms](25-using-psm-subprograms.md#4b885340999f65b2)를 참조한다.

<a id="df262b499aae3183"></a>
## Processing Transaction in PSM

데이터베이스 트랜잭션은 한 개 이상의 SQL 문장으로 구성된 분해할 수 없는 작업 단위이다. GOLDILOCKS 데이터베이스에서 트랜잭션을 사용하는 SQL 구문은 다음과 같다.

- SELECT 구문을 제외한 DML들
- 모든 DDL 들

다음과 같은 경우에 트랜잭션이 시작된다.

- 접속 직후에 처음으로 트랜잭션을 사용하는 SQL을 수행할 때
- COMMIT이나 ROLLBACK 이후에 처음으로 트랜잭션을 사용하는 SQL을 수행할 때

사용자가 COMMIT이나 ROLLBACK을 수행하거나 접속을 종료할 경우, 트랜잭션이 종료된다.

GOLDILOCKS PSM으로 작성된 subprogram 모듈은 자체적으로는 트랜잭션을 사용하지 않는 구문이기 때문에 호출될 때 새로운 트랜잭션을 발생시키지 않는다.

다만, SQL statement의 atomicity를 보장하기 위해 해당 subprogram이 호출된 상황에 따라 다음과 같이 subprogram내에서 사용될 수 있는 SQL의 종류가 제한된다.

- 사용자가 직접 CALL 구문을 사용하여 호출하거나 anonymous block을 수행한 경우
    - 상위 statement가 없는 상황이므로, subprogram 내에서 모든 종류의 SQL을 사용할 수 있고 COMMIT이나 ROLLBACK도 가능하다.
- SELECT를 제외한 DML 구문 (INSERT/ UPDATE/ DELETE 등) 내에서 사용되었을 경우
    - 상위 statement가 transaction을 가지기 때문에 subprogram 내에서는 모든 SQL구문을 사용할 수 있지만 상위 statement의 atomicity를 보장하기 위해 COMMIT이나 ROLLBACK은 할 수 없다.
- SELECT 구문 내에서 호출된 경우
    - 상위 statement가 트랜잭션을 사용하지 않기 때문에 호출된 subprogram 내에서도 트랜잭션을 사용하는 모든 SQL을 사용할 수 없고 COMMIT이나 ROLLBACK도 불가능하며 SELECT 구문만 사용할 수 있다.

---

[← 20. SQL References (H~Z)](../part-03-sql-manual/20-sql-references-h-z.md) · [전체 목차](../README.md) · [22. PSM DataTypes →](22-psm-datatypes.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
