<a id="eee28d2f6b3bbdc9"></a>

# 17. Built-in Function References

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/eee28d2f6b3bbdc9)  
> 태그: `26c.1_0_tag`

[← 16. Built-in Data Type References](16-built-in-data-type-references.md) · [전체 목차](../README.md) · [18. SQL References (A~B) →](18-sql-references-a-b.md)

<a id="8d66ed492522d26e"></a>
## * (MULTIPLICATION)

<a id="ce11c2bb766abd79"></a>
### 구문

```
expr1 * expr2
```

<a id="51526488f0fa5a39"></a>
### 설명

expr1과 expr2의 곱하기 연산 결과를 반환한다.

곱하기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#d9c1b23c9cbab71c)을 참조한다.

**숫자형 * 연산**

<a id="d125fd8d84c6cfef"></a>
| expr1 (expr2) | expr2 (expr1) | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="6757709f74b4263a"></a>
<table class="table column_count_3"><caption>INTERVAL * 연산 </caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>숫자형 타입</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>숫자형 타입</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_left" colspan="3"><div>자세한 내용은 <a class="reference text" href="#34c6acf523b0524b">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

**표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입**

<a id="34c6acf523b0524b"></a>
<table><thead><tr><th align="center">INTERVAL YEAR TO MONTH</th><th align="center">INTERVAL DAY TO SECOND</th></tr></thead><tbody><tr><td valign="middle"><ul><li>INTERVAL YEAR</li><li>INTERVAL MONTH</li><li>INTERVAL YEAR TO MONTH</li></ul></td><td valign="middle"><ul><li>INTERVAL DAY</li><li>INTERVAL HOUR</li><li>INTERVAL MINUTE</li><li>INTERVAL SECOND</li><li>INTERVAL DAY TO HOUR</li><li>INTERVAL DAY TO MINUTE</li><li>INTERVAL DAY TO SECOND</li><li>INTERVAL HOUR TO MINUTE</li><li>INTERVAL HOUR TO SECOND</li><li>INTERVAL MINUTE TO SECOND</li></ul></td></tr></tbody></table>

<a id="6a7b8379f607fb17"></a>
### 사용 예

```
gSQL> SELECT INTERVAL'1-2'YEAR TO MONTH * 2 AS RESULT FROM DUAL;
RESULT    
----------
+000002-04
1 row selected.

gSQL> SELECT INTERVAL'1 01:02:03.400000'DAY TO SECOND * 2 AS RESULT 
      FROM DUAL;
RESULT                 
-----------------------
+000002 02:04:06.800000
1 row selected.
```

<a id="393f2bd7ac2ec7a5"></a>
## + (ADDITION)

<a id="4586b47f11f09267"></a>
### 구문

```
expr1 + expr2
```

<a id="91a2391b4bf4dfd1"></a>
### 설명

expr1과 expr2의 더하기 연산 결과를 반환한다.

더하기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#d9c1b23c9cbab71c)을 참조한다.

**숫자형 + 연산**

<a id="359a6234eb2e2e58"></a>
| expr1 (expr2) | expr2 (expr1) | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="0bf9681de67b44e3"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) + 연산</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#34c6acf523b0524b">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="7f9059b0d77cf0eb"></a>
### 사용 예

```
gSQL> SELECT TO_DATE( '2012-05-05', 'YYYY-MM-DD' ) + 5 AS RESULT FROM DUAL;
RESULT    
----------
2012-05-10
1 row selected.

gSQL> SELECT 
      TO_DATE( '2012-05-05', 'YYYY-MM-DD' ) + INTERVAL'01-01'YEAR TO MONTH
      AS RESULT 
      FROM DUAL;
RESULT    
----------
2013-06-05
1 row selected.

gSQL> SELECT 
      INTERVAL'01-01'YEAR TO MONTH + INTERVAL'02-10'YEAR TO MONTH 
      AS RESULT 
      FROM DUAL;
RESULT    
----------
+000003-11
1 row selected.
```

<a id="bd714b8df1748510"></a>
## + (POSITIVE)

<a id="4da7e5735213f7bb"></a>
### 구문

```
+ expr
```

<a id="fee9abec16190215"></a>
### 설명

expr에 + 부호를 표시한다.

<a id="685c054748d72495"></a>
### 사용 예

```
gSQL> SELECT +3 AS RESULT1, +(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      3      -3
1 row selected.
```

<a id="fd8f2f96027d5c69"></a>
## - (NEGATIVE)

<a id="bacb9810f3aca1da"></a>
### 구문

```
- expr
```

<a id="c00bc6cae75cbd6e"></a>
### 설명

expr에 - 부호를 표시한다.

<a id="0b91dd89107c60c8"></a>
### 사용 예

```
gSQL> SELECT -3 AS RESULT1, -(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     -3       3
1 row selected.
```

<a id="ef4eebc1388b8004"></a>
## - (SUBTRACTION)

<a id="f42544102cca7ccc"></a>
### 구문

```
expr1 - expr2
```

<a id="b34ad29c669dbebd"></a>
### 설명

expr1과 expr2의 뺄셈 연산 결과를 반환한다.

뺄셈 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#d9c1b23c9cbab71c)을 참조한다.

**숫자형 - 연산**

<a id="5eaf3da66ba477cc"></a>
| expr1 | expr2 | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="fe7574f5349a30ce"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) - 연산</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMBER</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#34c6acf523b0524b">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="523771bf654d7bdd"></a>
### 사용 예

```
gSQL> SELECT 
      TO_DATE( '2012-05-05' ) - TO_DATE( '2012-05-01' ) AS RESULT 
      FROM DUAL;
RESULT
------
     4
1 row selected.

gSQL> SELECT TO_DATE( '2012-05-05' ) - 3 AS RESULT FROM DUAL;
RESULT    
----------
2012-05-02
1 row selected.

gSQL> SELECT 
      TO_DATE( '2012-05-05' ) - INTERVAL'01-02'YEAR TO MONTH AS RESULT 
      FROM DUAL;
RESULT    
----------
2011-03-05
1 row selected.

gSQL> SELECT
      INTERVAL'05-01'YEAR TO MONTH - INTERVAL'02-01'YEAR TO MONTH
      AS RESULT 
      FROM DUAL;
RESULT    
----------
+000003-00
1 row selected.

gSQL> SELECT INTERVAL'15 23:59:59.999999'DAY TO SECOND 
           - INTERVAL'10 23:59:59.999999'DAY TO SECOND AS RESULT 
      FROM DUAL;
RESULT                 
-----------------------
+000005 00:00:00.000000
1 row selected.
```

<a id="296a41984f9582a0"></a>
## / (DIVISION)

<a id="3385b8fb51d41214"></a>
### 구문

```
expr1 / expr2
```

<a id="daf8cb05cfec5c22"></a>
### 설명

expr1과 expr2의 나누기 연산 결과를 반환한다.

나누기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#d9c1b23c9cbab71c)을 참조한다.

**숫자형/ 연산**

<a id="db75b9aec64fa02b"></a>
| expr1 | expr2 | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER | NUMBER |
| NATIVE_DOUBLE | NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="ce41027c2d48276d"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL)/ 연산</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(결과 타입은 interval type 이다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#34c6acf523b0524b">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="2722153ad57a16d3"></a>
### 사용 예

```
gSQL> SELECT INTERVAL'20-10'YEAR TO MONTH / 2 AS RESULT FROM DUAL;
RESULT    
----------
+000010-05
1 row selected.

gSQL> SELECT   INTERVAL'02 02:04:06.800000'DAY TO SECOND / 2 AS RESULT 
      FROM DUAL;
RESULT                 
-----------------------
+000001 01:02:03.400000
1 row selected.
```

<a id="30b41dd69ad4319b"></a>
## || (CONCATENATE)

<a id="d7c1d64fdaf908bb"></a>
### 구문

```
str1 || str2
```

<a id="8387def546e1d024"></a>
### 설명

CONCATENATE는 str1과 str2를 연결한 문자열을 반환한다.

str1과 str2 중 하나가 null인 경우 null이 아닌 나머지 str이 반환되고, str1과 str2가 모두 null인 경우 NULL이 반환된다.

인자로는 character string 타입 또는 binary string 타입으로 변환될 수 있는 타입이 올 수 있다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#d9c1b23c9cbab71c)을 참조한다.

[CONCAT](#9242750a22d6bb53), [CONCATENATE](#f86aa5c3d97dc300)의 alias 이다.

결과 타입은 다음 표와 같다.

**|| (CONCATENATE)의 결과 타입**

<a id="b548d08f610acc94"></a>
| Data type | CHAR | VARCHAR | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR | CHAR | VARCHAR | LONG VARCHAR |
| VARCHAR | VARCHAR | VARCHAR | LONG VARCHAR |
| LONG VARCHAR | LONG VARCHAR | LONG VARCHAR | LONG VARCHAR |
| Data type | BINARY | VARBINARY | LONG VARBINARY |
| BINARY | BINARY | VARBINARY | LONG VARBINARY |
| VARBINARY | VARBINARY | VARBINARY | LONG VARBINARY |
| LONG VARBINARY | LONG VARBINARY | LONG VARBINARY | LONG VARBINARY |

<a id="d8232700ddfbb33a"></a>
### 사용 예

```
gSQL> SELECT 'DATA' || 'BASE' AS RESULT1,
             'DATA' || NULL   AS RESULT2,
               NULL || NULL   AS RESULT3 
       FROM DUAL;
RESULT1  RESULT2 RESULT3
-------- ------- -------
DATABASE DATA    null   
1 row selected.
```

<a id="49e1ba0580f64e62"></a>
## ABS

<a id="14dd566bfd9dc141"></a>
### 구문

```
ABS( num )
```

<a id="2b545a559f6172a0"></a>
### 설명

ABS는 num의 절대값을 반환한다.  

인자 num에는 숫자 타입 또는 숫자로 변환될 수 있는 타입이 올 수 있다.  
num이 NULL이면 NULL을 반환한다.

<a id="8e98026f2915d528"></a>
### 사용 예

```
gSQL> SELECT ABS(-1) AS RESULT1, ABS(1) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1       1
1 row selected.
```

<a id="af8eaec1ed5ab4c0"></a>
## ACOS

<a id="c743c72c81a8fa03"></a>
### 구문

```
ACOS( num )
```

<a id="4ba4030a5b1bdc97"></a>
### 설명

ACOS 함수는 num의 arc cosine 값을 반환한다.  

인자 num은 -1 이상 1 이하의 값이어야 한다.  
num이 NULL이면 NULL을 반환한다.  

0 ~ pi 사이의 라디안 값을 반환한다.

<a id="1cd75055f5fd0cf4"></a>
### 사용 예

```
gSQL> SELECT ACOS( 1 ) FROM DUAL;
ACOS( 1 )
---------
        0
1 row selected.
```

<a id="697ea8afd9a5c84e"></a>
## ADDDATE

<a id="e3fe55c305b82134"></a>
### 구문

```
ADDDATE( date, INTERVAL expr unit  )
ADDDATE( expr, days )
```

<a id="b456d6c64e5d8b20"></a>
### 설명

ADDDATE는 입력받은 첫 번째 인자에 두 번째 인자를 더하기 연산하여 그 결과를 반환한다.  

첫 번째 인자에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있고, 두 번째 인자에는 INTERVAL 또는 숫자 타입이 올 수 있다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.

결과 타입은 [(DATETIME/INTERVAL) + 연산](#0bf9681de67b44e3)과 동일하다.

<a id="d26780ac193488f5"></a>
### 사용 예

```
gSQL> SELECT ADDDATE( TO_DATE( '2012-12-12', 'YYYY-MM-DD' ), 1 ) AS RESULT
        FROM DUAL;
RESULT    
----------
2012-12-13
1 row selected.

gSQL> SELECT ADDDATE( TO_DATE( '2012-11-11', 'YYYY-MM-DD' ),
                      INTERVAL'01-01'YEAR TO MONTH ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2013-12-11
1 row selected.
```

<a id="ae8af9cb0c29ff45"></a>
## ADDTIME

<a id="47fa66831b536c69"></a>
### 구문

```
ADDTIME( expr1, expr2 )
```

<a id="97a8d7a9d76eea33"></a>
### 설명

ADDTIME은 입력받은 expr2를 expr1에 더하여 그 결과를 반환한다.

expr1에는 TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE TYPE이 올 수 있고, expr2에는 INTERVAL DAY TO SECOND TYPE이 올 수 있다.  

expr1이나 expr2가 NULL이면 결과값은 NULL이다.

결과 타입은 [(DATETIME/INTERVAL) + 연산](#0bf9681de67b44e3)과 동일하다.

<a id="75fe6288916a7612"></a>
### 사용 예

```
gSQL> SELECT
      ADDTIME( TO_TIMESTAMP( '2001-05-05 06:00:00', 
                             'YYYY-MM-DD HH24:MI:SS' ),
               INTERVAL'0 00:06:06.666666'DAY TO SECOND ) AS RESULT
      FROM DUAL;
RESULT                    
--------------------------
2001-05-05 06:06:06.666666
1 row selected.
```

<a id="2875ddd3ff069dd3"></a>
## ADD_MONTHS

<a id="dd1a3086c4af2648"></a>
### 구문

```
ADD_MONTHS( date, number )
```

<a id="b31347d753b1fd13"></a>
### 설명

ADD_MONTHS는 date에 number 숫자만큼의 달을 더한 값을 반환한다.  
만약 ADD_MONTHS 연산 후에 날짜가 그 달의 마지막 날보다 큰 경우에는 마지막 날짜로 조정한다.  

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있으며 인자 number에는 숫자타입이 올 수 있다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.

결과 타입은 입력 인자 date 타입과 관계없이 항상 DATE 타입이다.

<a id="20fc85e28cc23ee5"></a>
### 사용 예

```
gSQL> SELECT 
      ADD_MONTHS( TO_DATE( '2001-07-31', 'YYYY-MM-DD' ), 1 ) AS RESULT1,
      ADD_MONTHS( TO_DATE( '2001-07-31', 'YYYY-MM-DD' ), 2 ) AS RESULT2
      FROM DUAL;
RESULT1    RESULT2   
---------- ----------
2001-08-31 2001-09-30
1 row selected.
```

<a id="4bd83f1213792549"></a>
## APPROX_COUNT_DISTINCT

<a id="9e6f9a7d8024ffd5"></a>
### 구문

```
APPROX_COUNT_DISTINCT( expr [, expr, ...] ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="21b4b38a9d850f7d"></a>
### 설명

Aggregation 함수로서, 중복을 제거한 expr 값이 NULL이 아닌 row의 대략적인 개수를 반환한다.  

APPROX_COUNT_DISTINCT 함수는 COUNT(DISTINCT expr)와 거의 동일한 결과를 제공하면서도 훨씬 빠르게 대량의 데이터를 처리할 수 있다.  

FILTER를 지정하면 지정된 condition을 만족하는 값에 대해서만 aggregation을 수행한다.

<a id="56d98d3374d07345"></a>
### 사용 예

```
gSQL> SELECT APPROX_COUNT_DISTINCT( c1 ) FROM t1;

APPROX_COUNT_DISTINCT( C1 )
---------------------------
                         99

1 row selected.

gSQL> SELECT APPROX_COUNT_DISTINCT( c1 ) FILTER ( c2 > 50 ) FROM t1;

APPROX_COUNT_DISTINCT( C1 ) FILTER ( C2 > 50 )
----------------------------------------------
                                            49

1 row selected.
```

> APPROX_COUNT_DISTINCT 함수는 HyperLogLog 알고리즘을 기반으로 고유값의 개수를 추정한다.

<a id="9f1ebbc3fa98c148"></a>
## ASCII

<a id="90cae39a551cb4fc"></a>
### 구문

```
ASCII( char )
```

<a id="31157bd9c14ac29d"></a>
### 설명

char의 첫 번째 문자에 대한 database character set code를 십진수로 반환한다.

char에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있고, 반환되는 타입은 NUMBER 이다.  
char가 NULL이면 NULL을 반환한다.

<a id="402367c6bb985dd4"></a>
### 사용 예

```
gSQL> SELECT ASCII( 'G' ) AS RESULT FROM DUAL;
RESULT
------
    71
1 row selected.
```

<a id="fc3b02e1549e5dab"></a>
## ASIN

<a id="fedbdbefbd411475"></a>
### 구문

```
ASIN( num )
```

<a id="69b2a9de9d288db9"></a>
### 설명

ASIN 함수는 num의 arc sin 값을 반환한다.

인자 num은 -1 이상 1 이하의 값이어야 한다.  
num이 NULL이면 NULL을 반환한다.

-pi/2 ~ pi/2 사이의 라디안 값을 반환한다.

<a id="6d66e4886227ed77"></a>
### 사용 예

```
gSQL> SELECT ASIN( 0 ) FROM DUAL;
ASIN( 0 )
---------
        0
1 row selected.
```

<a id="31056f39ac4ea50f"></a>
## ATAN

<a id="eed6adced032d017"></a>
### 구문

```
ATAN( num )
```

<a id="0744ccaa1ed9aec7"></a>
### 설명

ATAN 함수는 num의 arc tangent 값을 반환한다.

num 값 범위의 제한은 없으며, -pi/2 ~ pi/2 사이의 라디안 값을 반환한다.   
num이 NULL이면 NULL을 반환한다.

<a id="7c08ad665e1e99e4"></a>
### 사용 예

```
gSQL> SELECT ATAN(0.5) FROM DUAL;
       ATAN(0.5)
----------------
.463647609000806
1 row selected.
```

<a id="afe54e7ea18a7c26"></a>
## ATAN2

<a id="3a0350fe76bd979d"></a>
### 구문

```
ATAN2( num1, num2 )
```

<a id="37f32260feaf49f0"></a>
### 설명

ATAN2 함수는 num1과 num2의 arc tangent 값을 반환한다.

인자 num1 값 범위의 제한은 없으며 -pi ~ pi 사이의 라디안 값을 반환한다.   
num1 또는 num2 중 하나라도 NULL이면 NULL을 반환한다.

<a id="5789884413fd2a53"></a>
### 사용 예

```
gSQL> SELECT ATAN2(1,2) FROM DUAL; 
      ATAN2(1,2)
----------------
.463647609000806
1 row selected.
```

<a id="1a081b007cc42414"></a>
## AVG

<a id="82457c003caa48af"></a>
### 구문

```
AVG( [ ALL | DISTINCT ] num ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="acb62bbd5c36b73b"></a>
### 설명

Aggregation 함수로써 expr 들의 평균값을 얻는데 사용된다.

ALL을 명시한 경우, 모든 값들에 대한 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복 제거한 값들에 대한 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

FILTER를 명시한 경우 condition을 만족하는 값들에 한하여 aggregation을 수행한다.

<a id="e4e713b5924b313d"></a>
### 사용 예

```
gSQL> SELECT AVG( c1 ) FROM t1;

AVG(C1)
-------
      2

1 row selected.


gSQL> SELECT AVG( c1 ) FILTER( WHERE c1 > 1 ) FROM t1;

AVG(C1)
-------
      3

1 row selected.
```

<a id="f7ea4f1a7c386ef9"></a>
## AVG() OVER

<a id="3753892c11ec954a"></a>
### 구문

```
AVG ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="2ecebc5b477b1c61"></a>
### 설명

Window function AVG는 expr의 평균값을 구하는 함수이다.  
NULL 값은 연산에서 제외된다.

<a id="58b2d62fb87d3d3a"></a>
### 사용 예

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , AVG( min_price ) OVER ( ORDER BY min_price ) AS "AVG"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE              AVG
--------- ----------------
       73               73
      247              160
      731 350.333333333333
     null 350.333333333333
     null 350.333333333333

5 rows selected.
```

<a id="0fe01d5c696eb761"></a>
## BITAND

<a id="2a26989e11190e25"></a>
### 구문

```
BITAND( num1, num2 )
```

<a id="9d3b428d1209951a"></a>
### 설명

num1과 num2의 비트에 대한 AND 연산 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.

결과 타입은 NATIVE_BIGINT이다.

<a id="ec4eb2a7457af070"></a>
### 사용 예

```
gSQL> SELECT BITAND(2, 4) FROM DUAL;
BITAND(2, 4)
------------
           0
1 row selected.
```

<a id="b7e603a350a417a7"></a>
## BITNOT

<a id="4df753f5aed4d838"></a>
### 구문

```
BITNOT( num )
```

<a id="8f1f9f40076c2ce7"></a>
### 설명

num의 비트에 대해 NOT 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자가 NULL이면 결과값도 NULL이다.

결과 타입은 다음과 같다.  
• 입력 인자가 NATIVE_SMALLINT인 경우, NATIVE_SMALLINT  
• 입력 인자가 NATIVE_INTEGER인 경우, NATIVE_INTEGER  
• 입력 인자가 NATIVE_BIGINT인 경우, NATIVE_BIGINT

<a id="8410259cef8a9c37"></a>
### 사용 예

```
gSQL> SELECT BITNOT( 5 ) AS RESULT FROM DUAL;
RESULT
------
    -6
1 row selected.
```

<a id="d1d1fc67acccbf08"></a>
## BITOR

<a id="e6c60464c93484bc"></a>
### 구문

```
BITOR( num1, num2 )
```

<a id="a26ba60cdf087ba0"></a>
### 설명

num1과 num2의 비트에 대해 OR 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자의 값이 하나라도 NULL이면 결과는 NULL이다.

결과 타입은 NATIVE_BIGINT이다.

<a id="0ea268c85ec34bdc"></a>
### 사용 예

```
gSQL> SELECT BITOR( 2, 4 ) FROM DUAL;
BITOR( 2, 4 )
-------------
            6
1 row selected.
```

<a id="f2d55a750c989c84"></a>
## BITXOR

<a id="e7b99a1e6bf55cbc"></a>
### 구문

```
BITXOR( num1, num2 )
```

<a id="ff6510a47520a7fb"></a>
### 설명

num1과 num2의 비트에 대해 XOR 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자의 값이 하나라도 NULL이면 결과는 NULL이다.

결과 타입은 NATIVE_BIGINT이다.

<a id="500df4d3e60491fb"></a>
### 사용 예

```
gSQL> SELECT BITXOR( 5, 3 ) FROM DUAL;
BITXOR( 5, 3 )
-------------
            6
1 row selected.
```

<a id="ae4da9b7765fd53d"></a>
## BIT_LENGTH

<a id="88ff3b6ae044da07"></a>
### 구문

```
BIT_LENGTH( str )
```

<a id="07865827b357a912"></a>
### 설명

BIT_LENGTH는 str의 비트 수를 반환한다.  
str이 NULL이면 NULL을 반환한다.

<a id="ba3a60ff910de497"></a>
### 사용 예

```
gSQL> SELECT BIT_LENGTH( 'LIKE' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
             32
    1 row selected.
```

<a id="2e9fab2319460d39"></a>
## BYTE_LENGTH

<a id="354745cad341687b"></a>
### 구문

```
BYTE_LENGTH( str )
```

<a id="bd131e31a30c2227"></a>
### 설명

OCTET_LENGTH의 alias이다.  
자세한 내용은 [OCTET_LENGTH](#ebe17e037d8d8ea6), [LENGTHB](#601cb51b0994464d)를 참조한다.

<a id="01f1699428e06eaf"></a>
### 사용 예

- Multi byte character set (예: UTF8): 1 byte character

```
gSQL> SELECT BYTE_LENGTH( 'OCTET_LENGTH' ) AS RESULT_1BYTE_CHARACTERS 
        FROM DUAL;
RESULT_1BYTE_CHARACTERS
-----------------------
                     12
1 row selected.
```

- Multi byte character set (예: UTF8): 2 byte character

```
gSQL> SELECT BYTE_LENGTH( 'αβ' ) AS RESULT_2BYTE_CHARACTERS FROM DUAL;
RESULT_2BYTE_CHARACTERS
-----------------------
                      4
1 row selected.
```

<a id="57df539807682278"></a>
## CASE2

<a id="2f255c1799690e0f"></a>
### 구문

```
CASE2( condition1, result1
      [, condition2, result2
       , ...
       , conditionN, resultN ]
      [, default ] )
```

<a id="d0efa9bafe55a9e3"></a>
### 설명

CASE2는 기술된 순서대로 condition을 평가한다.  
비교 결과가 FALSE이면 TRUE가 나올 때까지 평가한다.  
비교 결과가 TRUE이면 대응되는 result를 반환하고, 이후는 평가하지 않는다.  
비교 결과가 모두 FALSE인 경우에는 default를 반환하고, default가 생략된 경우에는 NULL을 반환한다.

result에 여러 type이 오는 경우, [결과 타입 조합 규칙](11-sql-elements.md#e881713e04641bea)에 따라 result type이 결정된다.

CASE2는 CASE로 동일하게 표현할 수 있다.

- CASE2( condition1, res1, condition2, res2 )

```
CASE WHEN condition1 THEN res1
     WHEN condition2 THEN res2
     ELSE NULL
  END
```

- CASE2( condition1, res1, condition2, res2, default )

```
CASE WHEN condition1 THEN res1
     WHEN condition2 THEN res2
     ELSE default
  END
```

<a id="db15a9f1d2257f47"></a>
### 사용 예

```
gSQL> SELECT I1,
        CASE2( I1 = 1, 'ONE', I1 = 2, 'TWO' ) AS CASE2_RESULT1,
        CASE2( I1 = 1, 'ONE', I1 = 2, 'TWO', 'NUMBER' ) AS CASE2_RESULT2
      FROM T1;
I1 CASE2_RESULT1 CASE2_RESULT2
-- ------------- -------------
 1 ONE           ONE          
 2 TWO           TWO          
 3 null          NUMBER       
3 rows selected.
```

<a id="b61e9231dbfbd8fc"></a>
## CBRT

<a id="21440c3b3538f983"></a>
### 구문

```
CBRT( num )
```

<a id="432ae2f7e7508053"></a>
### 설명

num의 세제곱근을 반환한다.  
num이 NULL이면 결과값도 NULL이 반환된다.

<a id="566ba0fbeb690ae2"></a>
### 사용 예

```
gSQL> SELECT CBRT( 27 ) FROM DUAL;
CBRT( 27 )
----------
         3
1 row selected.
```

<a id="fb759ce74d51cda7"></a>
## CEIL

<a id="6313eeb41d85ade4"></a>
### 구문

```
CEIL( num )
CEILING( num )
```

<a id="7889908fec493a92"></a>
### 설명

CEIL 함수는 num 보다 크거나 같은 가장 작은 정수를 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="dfece7db5ad6c2f1"></a>
### 사용 예

```
gSQL> SELECT CEIL( 3.5 ) AS RESULT1, CEIL( -3.5 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      4      -3
1 row selected.
```

<a id="419a706c1c7cf97a"></a>
## CHAR_LENGTH

<a id="d1af56e88409d170"></a>
### 구문

```
CHAR_LENGTH( str )            
CHARACTER_LENGTH( str )
```

<a id="65f18be3cec5ab75"></a>
### 설명

CHAR_LENGTH는 str에 대해 character set에 따른 문자수를 반환한다.

str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있고, 반환되는 타입은 NATIVE_BIGINT 이다.

str의 타입이 CHARACTER 타입이면 공백문자 (trailing blank)를 포함하여 계산한다.  
str이 NULL이면 NULL이 반환된다.

[LENGTH](#05398af639dccbdf)의 alias이다.

<a id="593631a9fe2f70e4"></a>
### 사용 예

Multi byte character set: (예:UTF8)

```
gSQL> SELECT CHAR_LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="465c03a9b42080cd"></a>
## CHR

<a id="1c0fe6dfaf5685ad"></a>
### 구문

```
CHR( num )
```

<a id="1bcb0318054318ae"></a>
### 설명

num에 대응하는 database character set code 내의 charater를 반환한다.

num은 숫자 타입이다.  
num이 NULL이면 NULL을 반환한다.  

결과 타입은 VARCHAR 이다.

<a id="8288ca8797be63ca"></a>
### 사용 예

```
gSQL> SELECT CHR(71) FROM DUAL;
CHR(71)
-------
G      
1 row selected.
```

<a id="8d4aa10dcf8c0deb"></a>
## CLOCK_DATE

<a id="6df90b30ec21e95a"></a>
### 구문

```
CLOCK_DATE()
```

<a id="d399c5ad3de9045f"></a>
### 설명

함수가 호출될 때마다 현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="cfe376c8c53ae7a0"></a>
### 사용 예

Row 마다 다른 값을 가질 수 있다.

```
gSQL> SELECT CLOCK_DATE() FROM t1;

CLOCK_DATE()
------------
2013-12-12  
2013-12-12  
2013-12-13  

3 rows selected.
```

<a id="a1e867d976dcf8d3"></a>
## CLOCK_LOCALTIME

<a id="fdb0f8f96b6593c3"></a>
### 구문

```
CLOCK_LOCALTIME()
```

<a id="bfab48e4d7cda3d9"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 없는 현재 시간 (TIME WITHOUT TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="360d5a10bf51437d"></a>
### 사용 예

Row 마다 시간값이 다를 수 있다.

```
gSQL> SELECT CLOCK_LOCALTIME() FROM t1;

CLOCK_LOCALTIME()
-----------------
14:42:05.470757  
14:42:05.470759  
14:42:05.470759  

3 rows selected.
```

<a id="c99ee0e195480e4a"></a>
## CLOCK_LOCALTIMESTAMP

<a id="2ac5aaa1c405f7cc"></a>
### 구문

```
CLOCK_LOCALTIMESTAMP()
```

<a id="0a0ab586d428e603"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 없는 현재 TIMESTAMP (TIMESTAMP WITHOUT TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="d4de835aa43bb576"></a>
### 사용 예

Row 마다 값이 다를 수 있다.

```
gSQL> SELECT CLOCK_LOCALTIMESTAMP() FROM t1;

CLOCK_LOCALTIMESTAMP()    
--------------------------
2013-12-12 14:46:17.309206
2013-12-12 14:46:17.309209
2013-12-12 14:46:17.309209
```

<a id="d485c25147ecd847"></a>
## CLOCK_TIME

<a id="6c4399030656831d"></a>
### 구문

```
CLOCK_TIME()
```

<a id="c1ba25f5e3ce8f2a"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="b78abb89bc2d4c41"></a>
### 사용 예

Row 마다 시간값이 다를 수 있다.

```
gSQL> SELECT CLOCK_TIME() FROM t1;

CLOCK_TIME()          
----------------------
14:48:21.052324 +09:00
14:48:21.052326 +09:00
14:48:21.052327 +09:00

3 rows selected.
```

<a id="32b13e69bebe812b"></a>
## CLOCK_TIMESTAMP

<a id="b2644778b81cb734"></a>
### 구문

```
CLOCK_TIMESTAMP()
```

<a id="c8a38f1dea9f75a4"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="d7e454737a7b13db"></a>
### 사용 예

Row 마다 값이 다를 수 있다.

```
gSQL> SELECT CLOCK_TIMESTAMP() FROM t1;

CLOCK_TIMESTAMP()                
---------------------------------
2013-12-12 14:49:45.051709 +09:00
2013-12-12 14:49:45.051714 +09:00
2013-12-12 14:49:45.051714 +09:00

3 rows selected.
```

<a id="04470874956922ee"></a>
## COALESCE

<a id="fb3e4df45095910b"></a>
### 구문

```
COALESCE( expr1, ..., exprN )
```

<a id="5283b7ceda5900e3"></a>
### 설명

expr list들 중에 null이 아닌 첫 번째 expr을 반환한다.  
expr list들이 모두 null인 경우에는 null을 반환한다.  
expr은 두 개 이상이어야 한다.

expr list에 여러 type들이 오는 경우에는 [결과 타입 조합 규칙](11-sql-elements.md#e881713e04641bea)에 따라 result type이 결정된다.

- COALESCE는 CASE를 사용하여 동일하게 표현할 수 있다.

    - COALESCE( expr1, expr2 )

```
CASE WHEN expr1 IS NOT NULL THEN expr1
       ELSE expr2
  END
```

    - COALESCE( expr1, expr2, ..., exprN )

```
CASE WHEN expr1 IS NOT NULL THEN expr1
       ELSE COALESCE( expr2, ..., exprN )
  END
```

<a id="aef4a613b98c094a"></a>
### 사용 예

```
gSQL> SELECT COALESCE( NULL, 1, 2 ) FROM DUAL;
COALESCE( NULL, 1, 2 )
----------------------
                     1
1 row selected.

gSQL> SELECT COALESCE( NULL, NULL, NULL ) FROM DUAL;
COALESCE( NULL, NULL, NULL )
----------------------------
null                        
1 row selected.
```

<a id="9242750a22d6bb53"></a>
## CONCAT

<a id="ddd4d7258d05155d"></a>
### 구문

```
CONCAT( str1, str2, ... )
```

<a id="2240e65a8de2867b"></a>
### 설명

\|| ( CONCATENATE )의 alias 이다.  
CONCAT 함수의 argument로써 2 ~ 254 개까지 설정할 수 있다.  
자세한 내용은 [|| (CONCATENATE)](#30b41dd69ad4319b), [CONCATENATE](#f86aa5c3d97dc300)를 참조한다.

<a id="ae2f3b7aee564527"></a>
### 사용 예

```
gSQL> SELECT CONCAT( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="f86aa5c3d97dc300"></a>
## CONCATENATE

<a id="edc029aa76f8af9b"></a>
### 구문

```
CONCATENATE( str1, str2, ... )
```

<a id="69ccd45be6450d0b"></a>
### 설명

\|| ( CONCATENATE ) 의 alias 이다.  
CONCATENATE 함수의 argument로 2 ~ 254 개까지 설정할 수 있다.  
자세한 내용은 [CONCAT](#9242750a22d6bb53), [|| (CONCATENATE)](#30b41dd69ad4319b)를 참조한다.

<a id="806aea4636b35afb"></a>
### 사용 예

```
gSQL> SELECT CONCATENATE( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="f6965ab879be69b9"></a>
## CORR() OVER

<a id="3946c1617b8b202f"></a>
### 구문

```
CORR( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="7aaa2caf28bd7c88"></a>
### 설명

Window function CORR는 expr 쌍의 상관계수 (coefficient of correlation)를 구하는 함수이다.

expr1 또는 expr2가 NULL일 경우, 계산에서 제외된다.  
expr 쌍의 row 개수가 한 개 이하일 경우, 결과로 NULL을 반환한다.

<a id="2cac515ad8063a53"></a>
### 사용 예

```
gSQL> SELECT employee_id, TO_CHAR( hire_date, 'YYYY' ) AS hire_date, salary,
             CORR( TO_CHAR( hire_date, 'YYYY' ), salary ) OVER ( ORDER BY employee_id ) AS corr
      FROM employees
      WHERE department_id = 60;

EMPLOYEE_ID HIRE_DATE SALARY              CORR
----------- --------- ------ -----------------
        103 1990        9000              null
        104 1991        6000                -1
        105 1997        4800 -.805837379342809
        106 1998        4800 -.840210805972693
        107 1999        4200 -.875185734200534

5 rows selected.
```

<a id="550b8141a8dabe36"></a>
## COS

<a id="1bf9e46af54d4a64"></a>
### 구문

```
COS(num)
```

<a id="ac95cba48558a699"></a>
### 설명

num의 COSINE 값을 반환한다.  
인자값 num이 NULL이면 결과값도 NULL이다.

<a id="98c58e69ae8791d2"></a>
### 사용 예

```
gSQL> SELECT COS( 0 ) FROM DUAL;
COS( 0 )
--------
       1
1 row selected.
```

<a id="23f1271a3371704b"></a>
## COT

<a id="b17af41c97a6a723"></a>
### 구문

```
COT(num)
```

<a id="8ec2792eb24d507d"></a>
### 설명

num의 COTANGENT 값을 반환한다.  
인자값 num이 NULL이면 결과값도 NULL이다.

<a id="477d77cca56ae0b9"></a>
### 사용 예

```
gSQL> SELECT COT( 1 ) FROM DUAL;
        COT( 1 )
----------------
.642092615934331
1 row selected.
```

<a id="afd0d6dd3d81826b"></a>
## COUNT

<a id="7e3f9267b639ee0d"></a>
### 구문

```
COUNT( [ ALL | DISTINCT ] expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="27a81b409f6b24a2"></a>
### 설명

Aggregation 함수로써 expr이 NULL 값이 아닌 row의 개수를 얻는다.

ALL을 명시한 경우, 모든 값들에 대한 aggregation을 수행한다.  
DISTINCT을 명시한 경우, 중복 제거한 값들에 대한 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

FILTER를 명시한 경우 condition을 만족하는 값들에 한하여 aggregation을 수행한다.

<a id="125bf94edf718fd8"></a>
### 사용 예

```
gSQL> SELECT COUNT( c1 ) FROM t1;

COUNT(C1)
---------
        3

1 row selected.


gSQL> SELECT COUNT( c1 ) FILTER( WHERE c1 > 1 ) FROM t1;

COUNT(C1)
---------
        2

1 row selected.
```

<a id="582dda281cd4fe2f"></a>
## COUNT() OVER

<a id="c0449aa022ff1703"></a>
### 구문

```
COUNT ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="cf3ca146ffc154c8"></a>
### 설명

Window function COUNT는 row의 개수를 세는 함수이다.  
NULL 값은 연산에서 제외된다.

<a id="36af5b3016de4e8a"></a>
### 사용 예

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , COUNT( min_price ) OVER ( ORDER BY min_price ) AS "COUNT"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE COUNT
--------- -----
       73     1
      247     2
      731     3
     null     3
     null     3

5 rows selected.
```

<a id="9ba48f32b5d0883b"></a>
## COUNT(*)

<a id="30fba7eedb3b0051"></a>
### 구문

```
COUNT(*) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="a85f077dd9f32f84"></a>
### 설명

Aggregation 함수로써 row의 개수를 얻는다.   
별도의 expression을 지정하지 않으므로 값의 NULL 여부와 무관하다.

FILTER를 명시한 경우 condition을 만족하는 값들에 한하여 aggregation을 수행한다.

<a id="a0005ef32248d323"></a>
### 사용 예

```
gSQL> SELECT COUNT(*) FROM t1;

COUNT(*)
--------
       4

1 row selected.


gSQL> SELECT COUNT(*) FILTER( WHERE c1 > 1 ) FROM t1;

COUNT(*)
--------
       2

1 row selected.
```

<a id="df6e1de4166a2f4e"></a>
## COUNT(*) OVER

<a id="9eed95dc2af782c5"></a>
### 구문

```
COUNT(*) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="9f127a557bca814b"></a>
### 설명

Window function COUNT(*)는 row의 개수를 세는 함수이다.  
별도로 expression을 지정하지 않으므로 값의 NULL 여부와는 무관하다.

<a id="bc3a4e7a03cd30b7"></a>
### 사용 예

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , COUNT(*) OVER ( ORDER BY min_price ) AS "COUNT(*)"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE COUNT(*)
--------- --------
       73        1
      247        2
      731        3
     null        5
     null        5

5 rows selected.
```

<a id="8531f86ea30bc50f"></a>
## COVAR_POP() OVER

<a id="1b46f44e533ce6ca"></a>
### 구문

```
COVAR_POP( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="6107108dc8ac261b"></a>
### 설명

Window function COVAR_POP은 expr 쌍의 모집단 공분산 (population covariance)을 구하는 함수이다.

expr1 또는 expr2가 NULL일 경우, 계산에서 제외된다.   
expr 쌍의 row 개수가 한 개 이하일 경우, 결과로 0을 반환한다.

<a id="f44d97f3eae325d7"></a>
### 사용 예

```
gSQL> SELECT employee_id, TO_CHAR( hire_date, 'YYYY' ) AS hire_date, salary,
             COVAR_POP( TO_CHAR( hire_date, 'YYYY' ), salary ) OVER ( ORDER BY employee_id ) AS covar_pop
      FROM employees
      WHERE department_id = 60;

EMPLOYEE_ID HIRE_DATE SALARY COVAR_POP
----------- --------- ------ ---------
        103 1990        9000         0
        104 1991        6000      -750
        105 1997        4800     -4400
        106 1998        4800     -5100
        107 1999        4200     -5640

5 rows selected.
```

<a id="220b7c02b596f959"></a>
## COVAR_SAMP() OVER

<a id="82ab7397ca9117ec"></a>
### 구문

```
COVAR_SAMP( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="e06207f859259f4a"></a>
### 설명

Window function COVAR_SAMP는 expr 쌍의 표본 공분산 (sample covariance)을 구하는 함수이다.

expr1 또는 expr2가 NULL일 경우, 계산에서 제외된다.  
expr 쌍의 row 개수가 한 개 이하일 경우, 결과로 NULL을 반환한다.

<a id="b290d94c932b93d6"></a>
### 사용 예

```
gSQL> SELECT employee_id, TO_CHAR( hire_date, 'YYYY' ) AS hire_date, salary,
             COVAR_SAMP( TO_CHAR( hire_date, 'YYYY' ), salary ) OVER ( ORDER BY employee_id ) AS covar_samp
      FROM employees
      WHERE department_id = 60;

EMPLOYEE_ID HIRE_DATE SALARY COVAR_SAMP
----------- --------- ------ ----------
        103 1990        9000       null
        104 1991        6000      -1500
        105 1997        4800      -6600
        106 1998        4800      -6800
        107 1999        4200      -7050

5 rows selected.
```

<a id="46ea2ec9c3721407"></a>
## CUME_DIST() OVER

<a id="82b316a9356ebc91"></a>
### 구문

```
CUME_DIST( ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="b6de2534f599ecc9"></a>
### 설명

Window function CUME_DIST는 현재 row 값의 상대적 위치에 따른 누적 분포도를 계산한다.

CUME_DIST 함수의 결과는 0부터 1 사이의 숫자이다.  
Row들의 값이 같을 경우 그 중에 가장 큰 누적 분포 값으로 동일한 결과를 반환한다.

window frame은 사용할 수 없다.

<a id="e4299eb2967ad4b0"></a>
### 사용 예

```
gSQL> SELECT department_id, salary,
             CUME_DIST() OVER ( ORDER BY salary ) AS cume_dist
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY CUME_DIST
------------- ------ ---------
           60   4200        .2
           60   4800        .6
           60   4800        .6
           60   6000        .8
           60   9000         1

5 rows selected.
```

<a id="91d13fe4a6f153de"></a>
## CURRENT_CATALOG

<a id="8d364c889da9d3d4"></a>
### 구문

```
CURRENT_CATALOG [()]
```

<a id="49026258744c39a9"></a>
### 설명

catalog name (database 이름)을 얻는다.

<a id="48df8978ba34f30d"></a>
### 사용 예

```
gSQL> SELECT CURRENT_CATALOG FROM dual;

CURRENT_CATALOG
---------------
TEST_DB        

1 row selected.
```

<a id="072b484139124e1d"></a>
## CURRENT_DATE

<a id="a3ad1635490bacf6"></a>
### 구문

```
CURRENT_DATE [()]
STATEMENT_DATE()
```

<a id="b9efb09604be9fa0"></a>
### 설명

현재 날짜 (DATE type) 값을 얻는다.

CURRENT_DATE는 SQL 표준 함수이다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• CURRENT_DATE, STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="801c5a7375c55cac"></a>
### 사용 예

```
gSQL> SELECT CURRENT_DATE FROM t1;

CURRENT_DATE
------------
2013-12-12  
2013-12-12  
2013-12-12  

3 rows selected.
```

<a id="84f3b85ed9383e58"></a>
## CURRENT_ROLE

<a id="dfa4be67a78abb5d"></a>
### 구문

```
CURRENT_ROLE [()]
```

<a id="eafebb73567667a9"></a>
### 설명

현재 세션의 role을 반환한다.

<a id="250c2f6a5c4f9205"></a>
### 사용 예

```
% gsql sys gliese

gSQL> SELECT current_user, current_role FROM dual;

CURRENT_USER CURRENT_ROLE
------------ ------------
SYS          null        

1 row selected.

gSQL> SET ROLE sysdba;

Session set.

gSQL> SELECT current_user, current_role FROM dual;

CURRENT_USER CURRENT_ROLE
------------ ------------
SYS          SYSDBA      

1 row selected.

gSQL> SET ROLE NONE;

Session set.


gSQL> SELECT current_user, current_role FROM dual;

CURRENT_USER CURRENT_ROLE
------------ ------------
SYS          null        

1 row selected.
```

<a id="4d350b96f9d2a1a4"></a>
## CURRENT_SCHEMA

<a id="c7ae254b9319c164"></a>
### 구문

```
CURRENT_SCHEMA [()]
```

<a id="888b17edaa365f1b"></a>
### 설명

사용자의 현재 SCHEMA를 얻는다.

<a id="f9237d5935cd1231"></a>
### 사용 예

```
gSQL> SELECT CURRENT_SCHEMA FROM dual;

CURRENT_SCHEMA
--------------
PUBLIC        

1 row selected.
```

<a id="b857364923db6e01"></a>
## CURRENT_TIME

<a id="64431506c1ac1fbc"></a>
### 구문

```
CURRENT_TIME [()]
STATEMENT_TIME()
```

<a id="c971972d170be468"></a>
### 설명

Session 시간을 기준으로 현재 TIME WITH TIME ZONE type 값을 얻는다.

CURRENT_TIME은 SQL 표준 함수이다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• CURRENT_TIME, STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="149623d7c1f51b65"></a>
### 사용 예

모든 row가 같은 시간값을 갖는다.

```
gSQL> SELECT CURRENT_TIME FROM t1;

CURRENT_TIME          
----------------------
16:27:10.116396 +09:00
16:27:10.116396 +09:00
16:27:10.116396 +09:00

3 rows selected.
```

<a id="168559e424362489"></a>
## CURRENT_TIMESTAMP

<a id="05b421b2abbcdee2"></a>
### 구문

```
CURRENT_TIMESTAMP [()]
STATEMENT_TIMESTAMP()
```

<a id="9da887524ba53ce9"></a>
### 설명

Session 시간을 기준으로 TIMESTAMP WITH TIME ZONE type 값을 얻는다.

CURRENT_TIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• CURRENT_TIMESTAMP, STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="720dd6db87127042"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT CURRENT_TIMESTAMP FROM t1;

CURRENT_TIMESTAMP                
---------------------------------
2013-12-12 16:34:55.649632 +09:00
2013-12-12 16:34:55.649632 +09:00
2013-12-12 16:34:55.649632 +09:00

3 rows selected.
```

<a id="b74ed317d4b03cd1"></a>
## CURRENT_USER

<a id="ee5e1ff20361ab30"></a>
### 구문

```
CURRENT_USER [()]
```

<a id="a2a454217e9b254e"></a>
### 설명

현재 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다.
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다.
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다.
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="b38ad5e1832991e4"></a>
### 사용 예

```
% gsql sys gliese

gSQL> SET SESSION AUTHORIZATION test;

Session set.

gSQL> SELECT 
        LOGON_USER() AS result1, 
        SESSION_USER() AS result2, 
        CURRENT_USER() AS result3 
      FROM DUAL;

RESULT1 RESULT2 RESULT3
------- ------- -------
SYS     TEST    TEST

1 row selected.
```

<a id="2bee070f9c29bf65"></a>
## CURRVAL

<a id="c20d9ba07f0cedb8"></a>
### 구문

```
seq_name.CURRVAL
CURRVAL(seq_name)
```

<a id="a01dba5697fad47c"></a>
### 설명

시퀀스 객체의 현재 값을 얻는다.

최소 한 번은 NEXTVAL(seq_name) 등으로 시퀀스 값을 설정해야 한다.

<a id="2020092c39247ff6"></a>
### 사용 예

```
gSQL> SELECT seq.CURRVAL FROM dual;

SEQ.CURRVAL
-----------
          1

1 row selected.
```

<a id="64772be178cb6dad"></a>
## DATEADD

<a id="1cde5cf8d38517af"></a>
### 구문

```
DATEADD( datepart, number, date )
```

<a id="02256bfaad9669dd"></a>
### 설명

date의 지정된 datepart에 number를 더한 값을 반환한다.

number가 소수점인 경우 반올림되지 않는다.  
date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE 타입이 올 수 있다.  
number 또는 date가 NULL인 경우에는 결과값도 NULL이다.

인자로 받은 date의 타입과 동일한 결과 타입이 반환된다.

**datepart에 사용 가능한 형식문자열**

<a id="f131a89886fe6ea5"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">설명</th></tr><tr><td>YEAR</td><td>년</td></tr><tr><td>QUARTER</td><td>분기</td></tr><tr><td>MONTH</td><td>월</td></tr><tr><td>DAYOFYEAR</td><td>일</td></tr><tr><td>DAY</td><td>요일</td></tr><tr><td>WEEK</td><td>주</td></tr><tr><td>WEEKDAY</td><td>평일</td></tr><tr><td>HOUR</td><td>시</td></tr><tr><td>MINUTE</td><td>분</td></tr><tr><td>SECOND</td><td>초</td></tr><tr><td>MILLISECOND</td><td>밀리세컨드</td></tr><tr><td>MICROSECOND</td><td>마이크로세컨드</td></tr></tbody></table>

<a id="02b9777ae1f5a87a"></a>
### 사용 예

```
gSQL> SELECT 
      DATEADD( YEAR, 1, TO_DATE( '2013-05-14', 'YYYY-MM-DD' ) ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2014-05-14
1 row selected.

gSQL> SELECT 
      DATEADD( MONTH, 13, TO_DATE('2013-05-14', 'YYYY-MM-DD') ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2014-06-14
1 row selected.

gSQL> SELECT 
      DATEADD( DAY, 397, TO_DATE('2013-05-14', 'YYYY-MM-DD') ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2014-06-15
1 row selected.
```

<a id="2166fdf4962b7a1d"></a>
## DATEDIFF

<a id="99bc9699c0d7ee47"></a>
### 구문

```
DATEDIFF( datepart, startdate, enddate )
```

<a id="ac3cccd28db40a16"></a>
### 설명

enddate에서 startdate를 뺀 값을 지정된 datepart로 반환한다.

startdate와 enddate에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME TYPE이 올 수 있다.  
startdate 또는 enddate가 NULL이면 결과값도 NULL이다.

결과 타입은 NUMBER이다.

**datepart에 사용 가능한 형식문자열**

<a id="2b56292854fbbb14"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">설명</th></tr><tr><td>YEAR</td><td>년</td></tr><tr><td>QUARTER</td><td>분기</td></tr><tr><td>MONTH</td><td>월</td></tr><tr><td>DAYOFYEAR</td><td>일</td></tr><tr><td>DAY</td><td>요일</td></tr><tr><td>HOUR</td><td>시</td></tr><tr><td>MINUTE</td><td>분</td></tr><tr><td>SECOND</td><td>초</td></tr><tr><td>MILLISECOND</td><td>밀리세컨트</td></tr><tr><td>MICROSECOND</td><td>마이크로세컨드</td></tr></tbody></table>

<a id="7fbe6fae2e2747a7"></a>
### 사용 예

```
gSQL>  SELECT 
       DATEDIFF( YEAR, 
                 TO_DATE( '2013-05-14', 'YYYY-MM-DD' ), 
                 TO_DATE( '2014-06-15', 'YYYY-MM-DD' ) ) AS RESULT 
       FROM DUAL;
RESULT
------
     1
1 row selected.

gSQL>  SELECT 
       DATEDIFF( MONTH, 
                 TO_DATE( '2014-05-14', 'YYYY-MM-DD' ), 
                 TO_DATE( '2014-06-15', 'YYYY-MM-DD' ) ) AS RESULT 
       FROM DUAL;
RESULT
------
     1
1 row selected.

gSQL> SELECT 
      DATEDIFF( DAY, 
                TO_DATE( '2013-06-01', 'YYYY-MM-DD' ), 
                TO_DATE( '2013-06-15', 'YYYY-MM-DD' ) ) AS RESULT 
      FROM DUAL;
RESULT
------
    14
1 row selected.
```

<a id="93f2a2ab0fe05576"></a>
## DATE_ADD

<a id="c15f5a8e979cb281"></a>
### 구문

```
DATE_ADD( date, INTERVAL expr unit  )
```

<a id="255451ea81b3b36b"></a>
### 설명

[ADDDATE](#697ea8afd9a5c84e) ( date, INTERVAL expr unit )와 동일한 함수이다.

<a id="5f298591a66d46dd"></a>
### 사용 예

```
gSQL> SELECT 
      DATE_ADD( TO_DATE( '2012-01-02', 'YYYY-MM-DD' ),
                INTERVAL '2-2' YEAR TO MONTH ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2014-03-02
1 row selected.
```

<a id="052dff56ca55ff3f"></a>
## DATE_PART

<a id="a4c69ee08f790288"></a>
### 구문

```
DATE_PART( field, datetime )
```

<a id="dffd20561cf9f705"></a>
### 설명

DATE_PART는 EXTRACT 함수와 결과값이 같은 함수로써 입력한 datetime 타입에서 지정된 field를 찾아 반환한다.

인자 field에는 문자 literal만 올 수 있으며, YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, TIMEZONE_HOUR, TIMEZONE_MINUTE를 문자 literal로 지정할 수 있다.  
인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.

field가 datetime의 범위에 있지 않는 경우 에러를 반환한다.  
또한, DATE 타입인 경우에는 field에 YEAR, MONTH, DAY 만 올 수 있고, 그 외에는 에러를 반환한다.  
datatime이 NULL이면 NULL을 반환한다.  

반환되는 타입은 NUMBER이다.

자세한 내용은 [EXTRACT](#c3ddc90dd21782b7)를 참조한다.

<a id="3d0c68932fd8abf8"></a>
### 사용 예

```
gSQL> SELECT 
      DATE_PART( 'DAY', TO_DATE( '2012-01-02', 'YYYY-MM-DD' ) ) AS RESULT
      FROM DUAL;
RESULT
------
     2
1 row selected.

gSQL> SELECT 
      DATE_PART( 'YEAR', INTERVAL'9-11'YEAR TO MONTH ) AS RESULT 
      FROM DUAL;
RESULT
------
     9
1 row selected.
```

<a id="c951d8e927911955"></a>
## DECODE

<a id="4b68693cf14e5317"></a>
### 구문

```
DECODE( expr, comparison_expr1, result1
           [, comparison_expr2, result2
            , ...
            , comparison_exprN, resultN ]
           [, default ] )
```

<a id="07a355c3e775149c"></a>
### 설명

DECODE 문에 기술된 순서대로 expr과 comparison_expr을 equal 연산으로 평가한다.  
비교 결과가 FALSE이면 TRUE가 나올 때까지 평가한다.  
비교 결과가 TRUE면 대응되는 result를 반환하고 이후는 평가하지 않는다.

expr과 comparison_expr이 같거나, expr과 comparison_expr이 모두 null인 경우, (null = null)에는 TRUE로 평가되어 대응되는 result를 반환한다.  
평가한 결과가 모두 FALSE인 경우에는 default를 반환하고, default가 생략된 경우, NULL을 반환한다.

- expr과 comparison_expr 비교  
  모든 expr, comparison_expr1, ..., comparison_exprN은 comparison_expr1 (첫 번째 comparison_expr)의 데이터 타입으로 변환하여 비교한다.  
  comparison_expr1 (첫 번째 comparison_expr)이 문자형인 경우와 숫자형인 경우, 각각 expr, comparison_expr1, ..., comparison_exprN에 기술된 타입들의 범위를 포함할 수 있는 타입이 된다.  
  expr, comparison_expr1, ..., comparison_exprN에 기술된 타입이 모두 CHAR 타입인 경우, VARCHAR 타입으로 비교가 수행된다.

- 결과 타입  
  결과 타입은 result1 (첫 번째 result)의 데이터 타입이 된다.  
  result1 (첫 번째 result)의 데이터 타입이 숫자형인 경우와 문자형인 경우는 각각 result1, ..., resultN에 기술된 타입들의 범위를 포함할 수 있는 타입이 된다.  
  result1 (첫 번째 result)가 CHAR 타입 또는 NULL인 경우, 결과 타입은 VARCHAR가 된다.

DECODE는 CASE를 사용해 동일하게 표현할 수 있다.

- DECODE( expr, comp_expr1, res1, comp_expr2, res2 )

```
CASE WHEN (expr = comp_expr1) OR (expr IS NULL AND comp_expr1 IS NULL ) THEN res1
     WHEN (expr = comp_expr2) OR (expr IS NULL AND comp_expr2 IS NULL ) THEN res2
     ELSE NULL
  END
```

- DECODE( expr, comp_expr1, res1, comp_expr2, res2, default )

```
CASE WHEN (expr = comp_expr1) OR (expr IS NULL AND comp_expr1 IS NULL ) THEN res1
     WHEN (expr = comp_expr2) OR (expr IS NULL AND comp_expr2 IS NULL ) THEN res2
     ELSE default
  END
```

<a id="5d8fef49bfacf7c6"></a>
### 사용 예

```
gSQL> SELECT I1,
             DECODE( I1, 1, 'ONE', 
                         2, 'TWO', 
                         NULL, 'NULL VALUE', 
                         'DEFAULT VALUE' ) AS DECODE_RESULT
      FROM T1;
  I1 DECODE_RESULT
---- -------------
   1 ONE          
   2 TWO          
null NULL VALUE   
   3 DEFAULT VALUE
4 rows selected.
```

<a id="17a832a9787fdb0e"></a>
## DEGREES

<a id="59e398dc424527ff"></a>
### 구문

```
DEGREES( radians )
```

<a id="eaf00fdde9d3cbf6"></a>
### 설명

라디안 단위로 표시된 각도 radians를 도 단위로 변환한 값을 반환한다.  
radians가 NULL이면 NULL이 반환된다.

<a id="14637a9579cb0b1d"></a>
### 사용 예

```
gSQL> SELECT DEGREES( PI() ) AS RESULT FROM DUAL;
RESULT
------
   180
1 row selected.
```

<a id="d3e8703b5b1b8331"></a>
## DENSE_RANK() OVER

<a id="784e8684e0055b4f"></a>
### 구문

```
DENSE_RANK( ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="18b143614417a049"></a>
### 설명

Window function DENSE_RANK는 순위를 계산하는 함수이다.

순위는 1부터 시작하는 연속적인 정수이고, 값이 같은 row는 순위도 동일하다.  
그러나 RANK와는 다르게 값이 같은 row들이 나와도 순위를 건너뛰지 않는다.

window frame은 사용할 수 없다.

<a id="a85991311bbf63e1"></a>
### 사용 예

```
gSQL> SELECT department_id, salary,
             DENSE_RANK() OVER ( ORDER BY salary ) AS d_rank
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY D_RANK
------------- ------ ------
           60   4200      1
           60   4800      2
           60   4800      2
           60   6000      3
           60   9000      4

5 rows selected.
```

<a id="f38a99e71e7b4e26"></a>
## DIGEST

<a id="f40dabe316108f08"></a>
### 구문

```
DIGEST( data, type )
```

<a id="8112435f26d6d117"></a>
### 설명

data를 주어진 type으로 hash한 결과값을 VARBINARY 타입으로 반환한다.

data 타입을 다음 규칙에 따라 입력할 때 implicit conversion이 발생할 수 있다.  

• BINARY, VARBINARY 타입 data는 VARBINARY로 입력한다.  
• LONG VARBINARY 타입 data는 LONG VARBINARY로 입력한다.  
• LONG VARCHAR 타입 data는 LONG VARCHAR로 입력한다.  
• 그 외의 모든 타입 data는 모두 VARCHAR 타입으로 implicit conversion하여 입력한다.

DIGEST 함수가 지원하는 hash type은 다음과 같다.  

• 'SHA1'의 결과는 20 byte varbinary이다.  
• 'SHA224'의 결과는 28 byte varbinary이다.  
• 'SHA256'의 결과는 32 byte varbinary이다.  
• 'SHA384'의 결과는 48 byte varbinary 이다.  
• 'SHA512'의 결과는 64 byte varbinary 이다.

결과를 VARBINARY 타입으로 반환하기 때문에 결과를 hexadecimal 문자로 보려면 HEX 함수를 씌워서 사용해야 하는데 이 경우 그 길이는 원본의 두 배가 된다.

<a id="ad251fb4f681a173"></a>
### 사용 예

```
gSQL> SELECT HEX( DIGEST( 'my password', 'SHA256' ) ) AS RESULT FROM DUAL;

RESULT                                                          
----------------------------------------------------------------
BB14292D91C6D0920A5536BB41F3A50F66351B7B9D94C804DFCE8A96CA1051F2

1 row selected.
```

<a id="47765d9d5b9bf97e"></a>
## DUMP

<a id="13a1affc1370f8d7"></a>
### 구문

```
DUMP( expr )
```

<a id="27f26b1482870d72"></a>
### 설명

DUMP 함수는 expr의 내부 표현정보를 반환한다.  
내부 표현정보는 데이터 타입, 길이 (byte length), 데이터 정보로 보여준다.

expr에는 모든 타입이 가능하다.  
expr이 NULL이면 NULL을 반환한다.  

반환되는 타입은 CHARACTER VARYING이다.

<a id="efc37289b476c1af"></a>
### 사용 예

```
gSQL> SELECT DUMP( 'DUMP' ) AS RESULT FROM DUAL;
RESULT                           
---------------------------------
Type=CHAR Len=4 : Str=68,85,77,80
1 row selected.
```

<a id="652cd3b0ced6bc32"></a>
## EXP

<a id="a28ce12315b91459"></a>
### 구문

```
EXP( num )
```

<a id="c6d013d9ec11d5eb"></a>
### 설명

EXP 함수는 e (자연로그 베이스)의 num의 제곱값을 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="2441d31b7bb0c3b3"></a>
### 사용 예

```
gSQL> SELECT EXP( 1 ) AS RESULT FROM DUAL;
          RESULT
----------------
2.71828182845905
1 row selected.
```

<a id="c3ddc90dd21782b7"></a>
## EXTRACT

<a id="dcb257dd9eaca0e5"></a>
### 구문

```
EXTRACT( <field> FROM datetime )

<field> ::= 
        YEAR
      | MONTH
      | DAY
      | HOUR
      | MINUTE
      | SECOND
      | TIMEZONE_HOUR
      | TIMEZONE_MINUTE
```

<a id="547d6c76869c9230"></a>
### 설명

EXTRACT는 입력한 datetime 타입에서 지정된 field를 찾아 반환한다.

인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.

field가 datetime의 범위에 있지 않는 경우에는 에러를 반환한다.  
또, DATE 타입인 경우에는 field에 YEAR, MONTH, DAY만 올 수 있고, 그 외의 경우에는 에러를 반환한다.  
반환되는 타입은 NUMBER이다.

EXTRACT 함수의 결과는 [DATE_PART](#052dff56ca55ff3f)와 동일하다.

<a id="c4e2de6dadf87bc6"></a>
### 사용 예

```
gSQL> SELECT 
      EXTRACT( SECOND FROM TO_TIMESTAMP( '2012-12-13 01:23:44.5', 
                                         'YYYY-MM-DD HH24:MI:SS.FF1' )  ) 
              AS RESULT 
      FROM DUAL;
RESULT
------
  44.5
1 row selected.

gSQL> SELECT
      EXTRACT( YEAR FROM CAST('2-3' AS INTERVAL YEAR TO MONTH) ) AS RESULT
      FROM DUAL;
RESULT
------
     2
1 row selected.
```

<a id="96e098f688ced383"></a>
## FACTORIAL

<a id="c8a1f8c094342647"></a>
### 구문

```
FACTORIAL( num )
```

<a id="54f75c22fe8bd156"></a>
### 설명

FACTORIAL 함수는 1 ~ num 까지의 연속된 자연수를 차례로 곱한 값을 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="6ce84b4d54f24625"></a>
### 사용 예

```
gSQL> SELECT FACTORIAL( 5 ) AS RESULT FROM DUAL;
RESULT
------
   120
1 row selected.
```

<a id="4981ab75e0efea25"></a>
## FIRST() OVER

<a id="1ed7a125d2529cc8"></a>
### 구문

```
aggregation_function KEEP ( DENSE_RANK FIRST ORDER BY <sort specification list> ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="b46de05e964d513f"></a>
### 설명

Window function FIRST 함수는 KEEP 절 내 order by에 쓰인 sort specification list를 정렬한 후, DENSE_RANK 순위가 1인 row들의 aggregation function 값을 반환한다.

aggregation_function에 해당하는 함수는 AVG, COUNT, COUNT(*), SUM, MAX, MIN, STDDEV, VARIANCE 이다.

window 절 내에서 order by는 사용할 수 없다.  
window frame은 사용할 수 없다.

<a id="df3b1de64f3ad720"></a>
### 사용 예

```
gSQL> SELECT department_id, salary,
           DENSE_RANK() OVER ( ORDER BY department_id ) AS "DENSE_RANK",
           MAX( salary ) KEEP ( DENSE_RANK FIRST ORDER BY department_id ) OVER () AS "MAX_FIRST"
  FROM employees
 WHERE department_id BETWEEN 90 AND 100;
    
DEPARTMENT_ID SALARY DENSE_RANK MAX_FIRST
------------- ------ ---------- ---------
           90  24000          1     24000
           90  17000          1     24000
           90  17000          1     24000
          100  12000          2     24000
          100   9000          2     24000
          100   8200          2     24000
          100   7700          2     24000
          100   7800          2     24000
          100   6900          2     24000

9 rows selected.
```

<a id="84e97a097c1ee6bf"></a>
## FIRST_VALUE() OVER

<a id="0b0e5d300322274c"></a>
### 구문

```
FIRST_VALUE ( expr ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

FIRST_VALUE ( expr [ RESPECT NULLS | IGNORE NULLS ] ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="fb1e3cbb569aef5f"></a>
### 설명

Window function FIRST_VALUE는 expr의 첫 번째 값을 반환한다.

RESPECT NULLS는 NULL 값을 포함하여 row 중에 가장 첫 번째 값을 반환한다.  
IGNORE NULLS는 NULL이 아닌 row 중에 가장 첫 번째 값을 반환한다.  
명시하지 않으면 기본값은 RESPECT NULLS 이다.

<a id="cfeb5d4b30aea18b"></a>
### 사용 예

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , FIRST_VALUE( min_price ) OVER ( ORDER BY min_price NULLS FIRST ) AS "FIRST_VALUE"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE FIRST_VALUE
--------- -----------
     null        null
     null        null
       73        null
      247        null
      731        null

5 rows selected.
```

다음은 null_treatment에 IGNORE NULLS를 명시한 예이다.

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , FIRST_VALUE( min_price IGNORE NULLS ) OVER ( ORDER BY min_price NULLS FIRST )
                                                       AS "FIRST_VALUE"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE FIRST_VALUE
--------- -----------
     null        null
     null        null
       73          73
      247          73
      731          73

5 rows selected.
```

<a id="37b8b2a8227612bc"></a>
## FLOOR

<a id="5f1e54e7f458067c"></a>
### 구문

```
FLOOR( num )
```

<a id="f7405477108ecf69"></a>
### 설명

FLOOR 함수는 num 보다 크지 않은 가장 큰 정수를 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="10aba734f1d615a0"></a>
### 사용 예

```
gSQL> SELECT FLOOR(42.8) AS RESULT1, FLOOR(-42.8) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     42     -43
1 row selected.
```

<a id="a5fd965acdfbf4d5"></a>
## FROM_BASE64

<a id="919af758216b0099"></a>
### 구문

```
FROM_BASE64( str )
```

<a id="32c4e4cd56a726d6"></a>
### 설명

FROM_BASE64는 base64 인코딩으로 변환된 문자를 입력 받아 디코딩된 binary string을 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 BINARY VARYING 또는 BINARY LONG VARYING과 같은 BINARY 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 base64 문자 범위에 속하지 않는 문자가 포함되면, 에러를 반환한다.  
디코딩 할 때 str의 newline, carriage return, tab, space는 무시된다.

자세한 내용은 [TO_BASE64](#a81b5df21d4b3b16)를 참조한다.

<a id="1b734d5b68f1a0ba"></a>
### 사용 예

```
gSQL> SELECT FROM_BASE64( TO_BASE64( 'abc' ) ),
             FROM_BASE64( TO_BASE64( 'abcd' ) ) 
        FROM DUAL;
FROM_BASE64( TO_BASE64( 'abc' ) ) FROM_BASE64( TO_BASE64( 'abcd' ) )
--------------------------------- ----------------------------------
616263                            61626364                          
1 row selected.
```

<a id="b8e235f519cbbf4f"></a>
## FROM_TZ

<a id="ee42e2609a03e175"></a>
### 구문

```
FROM_TZ( timestamp, timezone )
```

<a id="87c9037dd3c1d531"></a>
### 설명

FROM_TZ 함수는 timestamp와 정해진 format의 timezone을 TIMESTAMP WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 timestamp는 TIMESTAMP 타입이거나 TIMESTAMP 타입으로 변환이 가능해야 한다.   
인자 timestamp가 NULL이면 결과는 NULL이다.

인자 timezone은 CHARACTER, CHARACTER VARYING와 같은 CHARACTER 문자 타입이어야 하며, format은 'TZH:TZM'이다.   
인자 timezone이 NULL이면 결과는 NULL이다.

결과 타입은 TIMESTAMP(6) WITH TIME ZONE 이다.

<a id="ad52f1dcf00e6b34"></a>
### 사용 예

```
gSQL> SELECT 
      FROM_TZ( TIMESTAMP'2021-01-01 10:10:20.000000', '+06:00' ) AS RESULT
        FROM DUAL;
RESULT
-----------------------------------
2021-01-01 10:10:20.000000 +06:00
1 row selected.
```

<a id="2c4f5032fdd3a378"></a>
## GREATEST

<a id="64bcb1408455fc67"></a>
### 구문

```
GREATEST( expr1 [, expr2, ... exprn ] )
```

<a id="14573d2c569e87da"></a>
### 설명

GREATEST 함수는 인자로 받은 expr들 중에 가장 큰 값을 반환한다.

인자로 받은 expr들 중 하나라도 NULL인 경우, 결과값은 NULL이다.

결과 타입은 expr1 (첫 번째 expr)의 데이터 타입이다.  
expr1 (첫 번째 expr)의 데이터 타입이 숫자형인 경우와 문자형인 경우는 각각 expr1, ..., exprN의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, ..., exprN에 모두 CHAR 타입이 기술된 경우, 모든 expr은 VARCHAR 타입으로 비교되고, 결과 타입은 VARCHAR 타입으로 결정된다.

<a id="f610fd72b5783621"></a>
### 사용 예

```
gSQL> SELECT GREATEST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
   200
1 row selected.
```

<a id="6be942edd0b74700"></a>
## GROUPING

<a id="7405faad5564b295"></a>
### 구문

```
GROUPING( expr [, expr]... )
```

<a id="cb98d70d6a82f145"></a>
### 설명

GROUPING function은 GROUP BY와 함께 사용해야 한다.  
Argument인 expr 하나당 한 개의 bit를 표현하고 그에 해당하는 숫자를 반환한다. GROUPING KEY로 사용되었을 경우에는 0, 그렇지 않은 경우에는 1로 표현된다.   
결과 데이터 타입은 NATIVE_INTEGER 이다. 양의 정수로 표현 가능한 최대 bit 수는 31 개 이므로, GROUPING()의 최대 argument 개수는 31 개로 제한된다.

GROUP BY ROLLUP(a,b)와 함께 쓰였을 때, GROUPING은 다음과 같다.

<a id="0fdb8d21a2f3a52c"></a>
| Grouping Set | Bit vector | GROUPING |
| --- | --- | --- |
| a, b | 0 0 | 0 |
| a | 0 1 | 1 |
| null | 1 1 | 3 |

GROUP BY CUBE(a,b)와 함께 쓰였을 때, GROUPING은 다음과 같다.

<a id="8f69be6c887774b7"></a>
| Grouping Set | Bit vector | GROUPING |
| --- | --- | --- |
| a,b | 0 0 | 0 |
| a | 0 1 | 1 |
| b | 1 0 | 2 |
| null | 1 1 | 3 |

<a id="571daebc587732f2"></a>
### 사용 예

```
\EXPLAIN PLAN
SELECT 
       calendar_year as year 
     , calendar_quarter_desc as quarter
     , calendar_month_desc as month
     , GROUPING( calendar_year, calendar_quarter_desc, calendar_month_desc ) as grouping_id_func
  FROM sales, times
 WHERE sales.time_id=times.time_id 
   AND times.calendar_year = 2001
   AND sales.cust_id < 1000 AND sales.prod_id > 142 AND sales.channel_id > 2
 GROUP BY ROLLUP(calendar_year, calendar_quarter_desc, calendar_month_desc)
 ORDER BY 1, 2, 3;    2     3     4     5     6     7     8     9    10    11    12 

YEAR QUARTER MONTH   GROUPING_ID_FUNC
---- ------- ------- ----------------
2001 2001-01 2001-01                0
2001 2001-01 2001-02                0
2001 2001-01 2001-03                0
2001 2001-01 null                   1
2001 2001-02 2001-04                0
2001 2001-02 2001-05                0
2001 2001-02 2001-06                0
2001 2001-02 null                   1
2001 2001-03 2001-07                0
2001 2001-03 2001-08                0
2001 2001-03 2001-09                0
2001 2001-03 null                   1
2001 2001-04 2001-10                0
2001 2001-04 2001-11                0
2001 2001-04 2001-12                0
2001 2001-04 null                   1
2001 null    null                   3
null null    null                   7

18 rows selected.
```

<a id="34f7482b59045a4e"></a>
## GROUPING_ID

<a id="bddb23979c950698"></a>
### 구문

```
GROUPING_ID( expr [, expr]... )
```

<a id="109fe049b4e7b5d7"></a>
### 설명

GROUPING 함수와 동일하다. 즉 GROUPING의 alias라고 보아도 된다.

<a id="feb86fd78481f03d"></a>
### 사용 예

```
\EXPLAIN PLAN
SELECT 
       calendar_year as year 
     , calendar_quarter_desc as quarter
     , calendar_month_desc as month
     , GROUPING_ID( calendar_year, calendar_quarter_desc, calendar_month_desc ) as grouping_id_func
  FROM sales, times
 WHERE sales.time_id=times.time_id 
   AND times.calendar_year = 2001
   AND sales.cust_id < 1000 AND sales.prod_id > 142 AND sales.channel_id > 2
 GROUP BY ROLLUP(calendar_year, calendar_quarter_desc, calendar_month_desc)
 ORDER BY 1, 2, 3;  

YEAR QUARTER MONTH   GROUPING_ID_FUNC
---- ------- ------- ----------------
2001 2001-01 2001-01                0
2001 2001-01 2001-02                0
2001 2001-01 2001-03                0
2001 2001-01 null                   1
2001 2001-02 2001-04                0
2001 2001-02 2001-05                0
2001 2001-02 2001-06                0
2001 2001-02 null                   1
2001 2001-03 2001-07                0
2001 2001-03 2001-08                0
2001 2001-03 2001-09                0
2001 2001-03 null                   1
2001 2001-04 2001-10                0
2001 2001-04 2001-11                0
2001 2001-04 2001-12                0
2001 2001-04 null                   1
2001 null    null                   3
null null    null                   7

18 rows selected.
```

<a id="07153d77d1b51d4a"></a>
## GSI_PHYSICAL_STATS

<a id="bb23b123bf2a5283"></a>
### 구문

```
GSI_PHYSICAL_STATS( [schema_name.]table_name [,sampling_ratio_value] )
```

<a id="f12d79c54d506b1c"></a>
### 설명

GSI_PHYSICAL_STATS 는 클러스터 환경에서 테이블의 global secondary index 객체에 대한 페이지 단편화 (fragmentation) 정보를 반환하는 함수이다.

입력 인자 table_name은 identifier로 지정해야 하며, 해당 객체가 일반 테이블이 아닌 경우, 에러가 발생한다.

입력 인자 sampling_ratio_value는 객체가 보유한 전체 페이지 중 분석 대상으로 접근할 페이지의 비율 (%) 을 의미한다. 전체 페이지를 모두 처리하지 않고 일부 페이지만 무작위로 샘플링하여 분석함으로써, 작업을 더욱 빠르고 효율적으로 수행할 수 있다. 결과로 출력되는 Used 및 Fragmented는 할당된 전체 페이지가 아니라, 샘플링된 페이지를 기준으로 분석된 크기이다. 이 인자를 생략하면 기본적으로 100%가 적용되어 전체 페이지를 분석한다. 값의 범위는 1~100이며, 범위를 벗어나면 오류가 반환된다.

결과 타입은 VARCHAR 이며, Page, Used, Fragmented 정보를 반환한다.  
• Page: Global secondary index에 할당된 전체 페이지 수이다.  
• Used: 사용된 공간의 크기로서 페이지의 헤더 크기와 저장된 데이터 크기의 합이며, 단위는 byte이다.   
• Fragmented: 단편화 된 공간의 크기로서 단위는 byte 이다.

> Cluster system에서 유효한 정보이다.  
> 클러스터의 모든 노드에서 확인하고자 할 때에는 GLOBAL_DUAL 을 사용할 수 있다.

<a id="262c943d6c5407dd"></a>
### 사용 예

- DUAL 사용 시
    - 접속한 노드의 객체 정보를 반환한다.
    - 클러스터 환경에서는 클러스터 도메인을 지정할 수 있다.

```
gSQL> SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(T1) FROM DUAL;
CLUSTER_MEMBER_NAME GSI_PHYSICAL_STATS(T1)                      
------------------- --------------------------------------------
G1N1                Page: 384, Used: 1703308, Fragmented: 766659
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(PUBLIC.T1) FROM DUAL;
CLUSTER_MEMBER_NAME GSI_PHYSICAL_STATS(PUBLIC.T1)               
------------------- --------------------------------------------
G1N1                Page: 384, Used: 1703308, Fragmented: 766659
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(PUBLIC.T1, 50) FROM DUAL;
CLUSTER_MEMBER_NAME GSI_PHYSICAL_STATS(PUBLIC.T1, 50)          
------------------- -------------------------------------------
G1N1                Page: 384, Used: 821311, Fragmented: 368207
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(T1) FROM DUAL@G1N1
      UNION ALL
      SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(T1) FROM DUAL@G2N1
      UNION ALL
      SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(T1) FROM DUAL@G3N1;
CLUSTER_MEMBER_NAME GSI_PHYSICAL_STATS(T1)                         
------------------- -----------------------------------------------
G1N1                Page: 384, Used: 1703308, Fragmented: 766659   
G2N1                Page: 1088, Used: 5115758, Fragmented: 2300000 
G3N1                Page: 2080, Used: 10226411, Fragmented: 4600000
3 rows selected.
```

- GLOBAL_DUAL 사용 시
    - 클러스터 환경에서 모든 노드의 객체 정보를 반환한다.
    - 클러스터 도메인을 지정할 수 있다.

```
gSQL> SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(PUBLIC.T1, 50)
        FROM GLOBAL_DUAL
      ORDER BY CLUSTER_MEMBER_NAME;
CLUSTER_MEMBER_NAME GSI_PHYSICAL_STATS(PUBLIC.T1, 50)             
------------------- ----------------------------------------------
G1N1                Page: 384, Used: 887714, Fragmented: 398199   
G1N2                Page: 384, Used: 775345, Fragmented: 347438   
G2N1                Page: 1088, Used: 2603073, Fragmented: 1175875
G2N2                Page: 1088, Used: 2669476, Fragmented: 1205867
G3N1                Page: 2080, Used: 5021814, Fragmented: 2265086
G3N2                Page: 2080, Used: 5129068, Fragmented: 2313547
6 rows selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, GSI_PHYSICAL_STATS(PUBLIC.T1, 50)
        FROM GLOBAL_DUAL@G1N1|G2N1|G3N1
      ORDER BY CLUSTER_MEMBER_NAME;
CLUSTER_MEMBER_NAME GSI_PHYSICAL_STATS(PUBLIC.T1, 50)             
------------------- ----------------------------------------------
G1N1                Page: 384, Used: 851955, Fragmented: 382053   
G2N1                Page: 1088, Used: 2700097, Fragmented: 1219736
G3N1                Page: 2080, Used: 5384404, Fragmented: 2428961
3 rows selected.
```

<a id="3b5f99df99c16049"></a>
## HASH32

<a id="39ab7ff52375a627"></a>
### 구문

```
HASH32( expr [, expr]... )
```

<a id="2533fb8bafd229ee"></a>
### 설명

HASH32 함수는 전달된 expr 인자들의 해시값을 계산하여 반환한다.

인자는 최소 1 개 이상, 최대 32 개까지 지정할 수 있다.  
입력 인자 중 하나라도 NULL이 포함되어 있으면 결과 값은 NULL이 된다.

결과 타입은 NATIVE_INTEGER 이다.

<a id="91ba0bd2eebdd5be"></a>
### 사용 예

```
CREATE TABLE t1 ( c_int INTEGER, c_vchar VARCHAR(10), c_date DATE );
INSERT INTO t1 VALUES ( 100, 'GOLDILOCKS', sysdate );
INSERT INTO t1 VALUES ( 200, null, sysdate );

gSQL> SELECT * FROM t1;

C_INT C_VCHAR    C_DATE    
----- ---------- ----------
  100 GOLDILOCKS 2026-02-26
  200 null       2026-02-26

2 rows selected.

gSQL> SELECT HASH32( c_int, c_vchar, c_date ) FROM t1;

HASH32( C_INT, C_VCHAR, C_DATE )
--------------------------------
                      1116649224
                            null

2 rows selected.
```

<a id="de12493c5a02b161"></a>
## HEX

<a id="ad7c1fddbe4d73ad"></a>
### 구문

```
HEX( str )
```

<a id="1cdbe0d4c94c0a51"></a>
### 설명

인자 str을 16진수 문자로 반환한다.  
인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입 또는 문자 타입으로 변환될 수 있는 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.  
결과 타입은 CHARACTER VARYING 또는 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.

HEX 함수의 인자로 숫자타입이 오는 경우에는 에러를 반환한다.  
10진수 숫자를 16진수로 변환하고자 하는 경우에는  'X' number format을 이용한 TO_CHAR() 함수를 사용할 수 있다.  
예: TO_CHAR( 255, 'XX' )

자세한 내용은 [UNHEX](#7f7d06540fb972c9)를 참조한다.

<a id="4df6d95df265b85d"></a>
### 사용 예

```
gSQL> SELECT HEX( 'abc' ) FROM DUAL;
HEX( 'abc' )
------------
616263      
1 row selected.
```

<a id="8ecc511dde1fe96e"></a>
## INDEX_PHYSICAL_STATS

<a id="4f7d14043580cb92"></a>
### 구문

```
INDEX_PHYSICAL_STATS( [schema_name.]index_name [,sampling_ratio_value] )
```

<a id="241d1525f2815d63"></a>
### 설명

INDEX_PHYSICAL_STATS 는 인덱스에 할당된 페이지의 단편화 (fragmentation) 정보를 반환하는 함수이다.

입력 인자 index_name은 identifier로 지정해야 하며, 해당 객체가 인덱스가 아닌 경우, 에러가 발생한다.

입력 인자 sampling_ratio_value는 객체가 보유한 전체 페이지 중 분석 대상으로 접근할 페이지의 비율 (%) 을 의미한다. 전체 페이지를 모두 처리하지 않고 일부 페이지만 무작위로 샘플링하여 분석함으로써, 작업을 더욱 빠르고 효율적으로 수행할 수 있다. 결과로 출력되는 Used 및 Fragmented는 할당된 전체 페이지가 아니라, 샘플링된 페이지를 기준으로 분석된 크기이다. 이 인자를 생략하면 기본적으로 100%가 적용되어 전체 페이지를 분석한다. 값의 범위는 1~100이며, 범위를 벗어나면 오류가 반환된다.

결과 타입은 VARCHAR 이며, Page, Used, Fragmented 정보를 반환한다.  
• Page: Index에 할당된 전체 페이지 수이다.  
• Used: 사용된 공간의 크기로서 페이지의 헤더 크기와 저장된 데이터 크기의 합이며, 단위는 byte이다.  
• Fragmented: 단편화 된 공간의 크기로서 단위는 byte 이다.

> 클러스터의 모든 노드에서 확인하고자 할 때에는 GLOBAL_DUAL 을 사용할 수 있다.

<a id="e5fa6449fb6e89e5"></a>
### 사용 예

- DUAL 사용 시
    - 접속한 노드의 객체 정보를 반환한다.
    - 클러스터 환경에서는 클러스터 도메인을 기술할 수 있다.

```
gSQL> SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(T1_UIDX1) FROM DUAL;
CLUSTER_MEMBER_NAME INDEX_PHYSICAL_STATS(T1_UIDX1)              
------------------- --------------------------------------------
G1N1                Page: 480, Used: 2026050, Fragmented: 892587
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1) FROM DUAL;
CLUSTER_MEMBER_NAME INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1)       
------------------- --------------------------------------------
G1N1                Page: 480, Used: 2026050, Fragmented: 892587
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1, 50) FROM DUAL;
CLUSTER_MEMBER_NAME INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1, 50)   
------------------- --------------------------------------------
G1N1                Page: 480, Used: 1136487, Fragmented: 506293
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(T1_UIDX1) FROM DUAL@G1N1
      UNION ALL
      SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(T1_UIDX1) FROM DUAL@G2N1
      UNION ALL
      SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(T1_UIDX1) FROM DUAL@G3N1;
CLUSTER_MEMBER_NAME INDEX_PHYSICAL_STATS(T1_UIDX1)                 
------------------- -----------------------------------------------
G1N1                Page: 480, Used: 2026050, Fragmented: 892587   
G2N1                Page: 1280, Used: 6097450, Fragmented: 2697980 
G3N1                Page: 2464, Used: 12182935, Fragmented: 5395960
3 rows selected.
```

- GLOBAL_DUAL 사용 시
    - 클러스터 환경에서 모든 노드의 객체 정보를 반환한다.
    - 클러스터 도메인을 기술할 수 있다.

```
gSQL> SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1, 50)
        FROM GLOBAL_DUAL
      ORDER BY CLUSTER_MEMBER_NAME;
CLUSTER_MEMBER_NAME INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1, 50)     
------------------- ----------------------------------------------
G1N1                Page: 480, Used: 1146717, Fragmented: 510879  
G1N2                Page: 480, Used: 1115998, Fragmented: 497144  
G2N1                Page: 1280, Used: 3110836, Fragmented: 1371868
G2N2                Page: 1280, Used: 3142877, Fragmented: 1390133
G3N1                Page: 2464, Used: 6072430, Fragmented: 2687620
G3N2                Page: 2464, Used: 6177784, Fragmented: 2737856
6 rows selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1, 50)
        FROM GLOBAL_DUAL@G1N1|G2N1|G3N1
      ORDER BY CLUSTER_MEMBER_NAME;
CLUSTER_MEMBER_NAME INDEX_PHYSICAL_STATS(PUBLIC.T1_UIDX1, 50)     
------------------- ----------------------------------------------
G1N1                Page: 480, Used: 1213355, Fragmented: 540555  
G2N1                Page: 1280, Used: 3102215, Fragmented: 1369573
G3N1                Page: 2464, Used: 6347994, Fragmented: 2810966
3 rows selected.
```

<a id="405c8f5a4181712d"></a>
## INITCAP

<a id="ff1cb6cb0b5f9e08"></a>
### 구문

```
INITCAP( str )
```

<a id="0226165c3fcfb241"></a>
### 설명

INITCAP 함수는 주어진 문자열 str의 각 단어들의 첫 번째 문자를 대문자로 변환하고 첫 번째 문자 이후의 문자를 소문자로 변환하여 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.

문자열의 각 단어는 white space, 알파벳 또는 숫자가 아닌 문자로 구분한다.  
str이 NULL이면 결과값도 NULL이다.

인자로 받는 str의 타입과 동일한 타입이 반환된다.

<a id="75a7765b4a727cef"></a>
### 사용 예

```
gSQL> SELECT INITCAP( 'hi GLIESE' ) AS RESULT FROM DUAL;
RESULT   
---------
Hi Gliese
1 row selected.
```

<a id="95f0d155a49249e9"></a>
## INSTR

<a id="5de486015bbfda1a"></a>
### 구문

```
INSTR( str, substr [, position [, occurrence ] ] )
```

<a id="2e5c1c83e589d80e"></a>
### 설명

INSTR 함수는 str의 position부터 시작해서 occurrence 번째의 substr을 찾아 그 위치를 반환한다.

인자 str, substr에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

인자 position, occurrence에는 숫자 타입이 올 수 있다.

position과 occurrence가 생략된 경우, default 값은 1이다.  
position과 occurrence는 1부터 시작하며, character set에 따른 문자 단위로 계산된다. (byte 단위가 아님)

position은 str에서 substr 검색을 시작할 처음 위치를 의미하며, 0이 아닌 정수값이어야 한다.

- 양수인 경우: str의 앞부분에서부터 오른쪽으로 계속 비교해나가면서 substr을 찾을 때까지 position 위치를 검색한다.
- 음수인 경우: str의 뒷부분에서부터 왼쪽으로 계속 비교해나가면서 substr을 찾을 때까지 position 위치를 검색한다.
- 0인 경우: 결과값은 0이다.

occurrence는 str에서 substr이 반복된 횟수를 의미하며, 양의 정수이어야 한다.

입력 인자 중 하나라도 NULL이면 결과값도 NULL이다.

<a id="d8c777802ca8b240"></a>
### 사용 예

```
gSQL> SELECT INSTR( 'ABCD ABCD ABCDABCD', 'BC' ) AS RESULT1,
             INSTR( 'ABCD ABCD ABCDABCD', 'BC', 4 ) AS RESULT2
      FROM DUAL;
RESULT1 RESULT2
------- -------
      2       7
1 row selected.

gSQL> SELECT INSTR( 'ABCD ABCD ABCDABCD', 'BC', 5 , 3 ) AS RESULT1,
             INSTR( 'ABCD ABCD ABCDABCD', 'BC', -5,  3 ) AS RESULT2
      FROM DUAL;
RESULT1 RESULT2
------- -------
     16       2
1 row selected.
```

<a id="de97ba0a4d32a2af"></a>
## JSON_ARRAY

<a id="bf718d34efcdc62f"></a>
### 구문

```
JSON_ARRAY( [ value_expression [, ...] ]
            [<JSON constructor null clause>]
            [<JSON output clause>]
          )
```

&lt; JSON constructor null clause &gt;에 대한 자세한 내용은 [JSON Constructor Null Clause](11-sql-elements.md#80e8f502383fbf61)를 참조한다.

&lt; JSON output clause &gt;에 대한 자세한 내용은 [JSON Output Clause](11-sql-elements.md#d8ec54a70fd9d3a7)를 참조한다.

<a id="322379cae76478d1"></a>
### 설명

JSON_ARRAY는 0개 이상의 expr을 JSON ARRAY 문자열로 반환한다.

JSON constructor null clause는 SQL null 값을 어떻게 처리할지 지정하는 옵션이다.  
명시하지 않으면 기본값은 ABSENT ON NULL이다.

JSON output clause는 함수가 생성하는 문자열의 타입과 출력 형식을 제어할 수 있는 옵션이다.  
Data type을 명시하여 결과 타입을 지정할 수 있다. 명시하지 않으면 기본값은 VARCHAR(4000)이다.  
PRETTY를 명시하여 JSON 문자열 출력 형식을 변경할 수 있다.

<a id="217b1df5a1327d6a"></a>
### 사용 예

```
CREATE TABLE accounts ( name VARCHAR(20), balances INTEGER );
INSERT INTO accounts VALUES ( 'Alice', 50000 );
INSERT INTO accounts VALUES ( 'Bob', NULL );
INSERT INTO accounts VALUES ( 'Chris', 1000 );

gSQL> SELECT JSON_ARRAY( name, balances ) AS res_json_array
        FROM accounts;

RES_JSON_ARRAY 
---------------
["Alice",50000]
["Bob"]        
["Chris",1000] 

3 rows selected.
```

<a id="6a1307addaa8d032"></a>
## JSON_ARRAYAGG

<a id="e8b7b02d98fe55a2"></a>
### 구문

```
JSON_ARRAYAGG( value_expression
               [<JSON array aggregate order by clause>]
               [<JSON constructor null clause>]
               [<JSON output clause>]
             ) [ FILTER ( [ WHERE ] condition )
```

&lt;JSON array aggregate order by clause&gt;에 대한 자세한 내용은 [JSON Array Aggregate Order By Clause](11-sql-elements.md#90516a21bfc51e9b)를 참조한다.

&lt; JSON constructor null clause &gt;에 대한 자세한 내용은 [JSON Constructor Null Clause](11-sql-elements.md#80e8f502383fbf61)를 참조한다.

&lt; JSON output clause &gt;에 대한 자세한 내용은 [JSON Output Clause](11-sql-elements.md#d8ec54a70fd9d3a7)를 참조한다.

FILTER를 지정하면 지정된 condition을 만족하는 값에 대해서만 aggregation을 수행한다.

<a id="7a980e4cc9f1f2b0"></a>
### 설명

JSON_ARRAYAGG는 aggregation 함수로서 value expression을 연결하여 한 개의 JSON array string row를 반환한다.

JSON array aggregate order by clause는 JSON array의 value를 정렬하여 출력하는 옵션이다.

JSON constructor null clause는 SQL null 값을 어떻게 처리할지 지정하는 옵션이다.   
명시하지 않으면 기본값은 ABSENT ON NULL이다.

JSON output clause는 함수가 생성하는 문자열의 타입과 출력 형식을 제어할 수 있는 옵션이다.  
Data type을 명시하여 결과 타입을 지정할 수 있다. 명시하지 않으면 기본값은 VARCHAR(4000)이다.  
PRETTY를 명시하여 JSON 문자열 출력 형식을 변경할 수 있다.

<a id="a87dec5ff025d89a"></a>
### 사용 예

```
CREATE TABLE accounts ( name VARCHAR(20), balances INTEGER );
INSERT INTO accounts VALUES ( 'Alice', 50000 );
INSERT INTO accounts VALUES ( 'Bob', NULL );
INSERT INTO accounts VALUES ( 'Chris', 1000 );

gSQL> SELECT JSON_ARRAYAGG( name ) AS name_arrayagg,
             JSON_ARRAYAGG( balances ) AS balances_arrayagg
        FROM accounts; 

NAME_ARRAYAGG           BALANCES_ARRAYAGG
----------------------- -----------------
["Alice","Bob","Chris"] [50000,1000]     

1 row selected.

gSQL> SELECT JSON_ARRAYAGG( name ) 
             FILTER ( balances > 10000 ) AS name_arrayagg,
             JSON_ARRAYAGG( balances ) 
             FILTER ( balances > 10000 ) AS balances_arrayagg
        FROM accounts; 

NAME_ARRAYAGG BALANCES_ARRAYAGG
------------- -----------------
["Alice"]     [50000]          

1 row selected.
```

<a id="677ae68f770b3e92"></a>
## JSON_ARRAYAGG() OVER

<a id="2d4e5d9a0fdd663a"></a>
### 구문

```
JSON_ARRAYAGG( value_expression
               [<JSON array aggregate order by clause>]
               [<JSON constructor null clause>]
               [<JSON output clause>]
             ) OVER < window name or specification >
```

&lt;JSON array aggregate order by clause&gt;에 대한 자세한 내용은 [JSON Array Aggregate Order By Clause](11-sql-elements.md#90516a21bfc51e9b)를 참조한다.

&lt; JSON constructor null clause &gt;에 대한 자세한 내용은 [JSON Constructor Null Clause](11-sql-elements.md#80e8f502383fbf61)를 참조한다.

&lt; JSON output clause &gt;에 대한 자세한 내용은 [JSON Output Clause](11-sql-elements.md#d8ec54a70fd9d3a7)를 참조한다.

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="3e6c947d0c5009f2"></a>
### 설명

Window function JSON_ARRAYAGG는 window 범위 내의 value expression을 연결하여 JSON array 문자열을 생성하는 함수이다.

JSON array aggregate order by clause는 JSON array의 value를 정렬하여 출력하는 옵션이다.

JSON constructor null clause는 SQL null 값을 어떻게 처리할지 지정하는 옵션이다.  
명시하지 않으면 기본값은 ABSENT ON NULL이다.

JSON output clause는 함수가 생성하는 문자열의 타입과 출력 형식을 제어할 수 있는 옵션이다.  
Data type을 명시하여 결과 타입을 지정할 수 있다. 명시하지 않으면 기본값은 VARCHAR(4000)이다.  
PRETTY를 명시하여 JSON 문자열 출력 형식을 변경할 수 있다.

<a id="4e6c750ad43367c0"></a>
### 사용 예

```
CREATE TABLE accounts ( name VARCHAR(20), balances INTEGER );
INSERT INTO accounts VALUES ( 'Alice', 50000 );
INSERT INTO accounts VALUES ( 'Bob', NULL );
INSERT INTO accounts VALUES ( 'Chris', 1000 );

gSQL> SELECT JSON_ARRAYAGG( name ) OVER ( ORDER BY balances DESC NULLS LAST ) AS name_arrayagg_over,
             JSON_ARRAYAGG( balances ) OVER ( ORDER BY balances DESC NULLS LAST ) AS balances_arrayagg_over
        FROM accounts;

NAME_ARRAYAGG_OVER      BALANCES_ARRAYAGG_OVER
----------------------- ----------------------
["Alice"]               [50000]               
["Alice","Chris"]       [50000,1000]          
["Alice","Chris","Bob"] [50000,1000]          

3 rows selected.
```

<a id="8cd5e69d1f7d5ba9"></a>
## JSON_OBJECT

<a id="367c241494e1f3eb"></a>
### 구문

```
JSON_OBJECT( [ <JSON name and value> [, ...] ]
             [ <JSON constuctor null clause> ]
             [ <JSON key uniqueness constraint> ]
             [ <JSON output clause> ]
           )

<JSON name and value> ::=
    [KEY] <JSON name> VALUE <value_expression>
  | <JSON name> : <value_expression>
```

&lt; JSON constructor null clause &gt;에 대한 자세한 내용은 [JSON Constructor Null Clause](11-sql-elements.md#80e8f502383fbf61)를 참조한다.

&lt; JSON key uniqueness constraint &gt;에 대한 자세한 내용은 [JSON Key Uniqueness Constraint](11-sql-elements.md#2bce9d5d0bac743d)를 참조한다.

&lt; JSON output clause &gt;에 대한 자세한 내용은 [JSON Output Clause](11-sql-elements.md#d8ec54a70fd9d3a7)를 참조한다.

<a id="5f9f46a5f44a2e84"></a>
### 설명

JSON_OBJECT는 0개 이상의 JSON name and value를 JSON object 문자열로 반환한다.  
JSON name은 character string으로 표현할 수 있는 expresssion이어야 한다.

JSON constructor null clause는 SQL null 값을 어떻게 처리할지 지정하는 옵션이다.   
명시하지 않으면 기본값은 NULL ON NULL이다.

JSON key uniqueness constraint는 JSON object의 key field에 중복을 허용할지 여부를 결정하는 옵션이다.   
명시하지 않으면 기본값은 WITHOUT UNIQUE KEYS이다.

JSON output clause는 함수가 생성하는 문자열의 타입과 출력 형식을 제어할 수 있는 옵션이다.  
Data type을 명시하여 결과 타입을 지정할 수 있다. 명시하지 않으면 기본값은 VARCHAR(4000)이다.  
PRETTY를 명시하여 JSON 문자열 출력 형식을 변경할 수 있다.

<a id="89e1bdfd8991dd75"></a>
### 사용 예

```
CREATE TABLE accounts ( name VARCHAR(20), balances INTEGER );
INSERT INTO accounts VALUES ( 'Alice', 50000 );
INSERT INTO accounts VALUES ( 'Bob', NULL );
INSERT INTO accounts VALUES ( 'Chris', 1000 );

gSQL> SELECT JSON_OBJECT( name VALUE balances ) AS res_json_object
       FROM accounts;

RES_JSON_OBJECT
---------------
{"Alice":50000}
{"Bob":null}   
{"Chris":1000} 

3 rows selected.
```

<a id="f2ed9f8209629cd7"></a>
## JSON_OBJECTAGG

<a id="e46edd2e7d0f0b48"></a>
### 구문

```
JSON_OBJECTAGG( <JSON name and value>
                [ <JSON constructor null clause> ]
                [ <JSON key uniqueness constraint> ]
                [ <JSON output clause> ]
              ) [ FILTER ( [ WHERE ] condition ) ]

<JSON name and value> ::=
    [KEY] <JSON name> VALUE <value_expression>
  | <JSON name> : <value_expression>
```

&lt; JSON constructor null clause &gt;에 대한 자세한 내용은 [JSON Constructor Null Clause](11-sql-elements.md#80e8f502383fbf61)를 참조한다.

&lt; JSON key uniqueness constraint &gt;에 대한 자세한 내용은 [JSON Key Uniqueness Constraint](11-sql-elements.md#2bce9d5d0bac743d)를 참조한다.

&lt; JSON output clause &gt;에 대한 자세한 내용은 [JSON Output Clause](11-sql-elements.md#d8ec54a70fd9d3a7)를 참조한다.

FILTER를 지정하면 지정된 condition을 만족하는 값에 대해서만 aggregation을 수행한다.

<a id="ef1c6cd15acf7a1d"></a>
### 설명

JSON_OBJECTAGG는 aggregation 함수로서 JSON name and value 쌍을 연결하여 한 개의 JSON object string row를 반환한다.   
JSON name은 character string으로 표현할 수 있는 expresssion이어야 한다.

JSON constructor null clause는 SQL null 값을 어떻게 처리할지 지정하는 옵션이다.   
명시하지 않으면 기본값은 NULL ON NULL이다.

JSON key uniqueness constraint는 JSON object의 key field에 중복을 허용할지 여부를 결정하는 옵션이다.   
명시하지 않으면 기본값은 WITHOUT UNIQUE KEYS이다.

JSON output clause는 함수가 생성하는 문자열의 타입과 출력 형식을 제어할 수 있는 옵션이다.  
Data type을 명시하여 결과 타입을 지정할 수 있다. 명시하지 않으면 기본값은 VARCHAR(4000)이다.  
PRETTY를 명시하여 JSON 문자열 출력 형식을 변경할 수 있다.

<a id="4e435dacc7a0d091"></a>
### 사용 예

```
CREATE TABLE accounts ( name VARCHAR(20), balances INTEGER );
INSERT INTO accounts VALUES ( 'Alice', 50000 );
INSERT INTO accounts VALUES ( 'Bob', NULL );
INSERT INTO accounts VALUES ( 'Chris', 1000 );

gSQL> SELECT JSON_OBJECTAGG( name VALUE balances ) AS res_json_objectagg
        FROM accounts;

RES_JSON_OBJECTAGG                     
---------------------------------------
{"Alice":50000,"Bob":null,"Chris":1000}

1 row selected.

gSQL> SELECT JSON_OBJECTAGG( name VALUE balances ) 
                    FILTER ( balances > 10000 ) AS res_json_objectagg
       FROM accounts;   

RES_JSON_OBJECTAGG
------------------
{"Alice":50000}   

1 row selected.
```

<a id="4b6cac5f93cac0c0"></a>
## JSON_OBJECTAGG() OVER

<a id="80468c514f894fb2"></a>
### 구문

```
JSON_OBJECTAGG( <JSON name and value>
                [ <JSON constructor null clause> ]
                [ <JSON key uniqueness constraint> ]
                [ <JSON output clause> ]
              ) OVER < window name or specification >

<JSON name and value> ::=
    [KEY] <JSON name> VALUE <value_expression>
  | <JSON name> : <value_expression>
```

&lt; JSON constructor null clause &gt;에 대한 자세한 내용은 [JSON Constructor Null Clause](11-sql-elements.md#80e8f502383fbf61)를 참조한다.

&lt; JSON key uniqueness constraint &gt;에 대한 자세한 내용은 [JSON Key Uniqueness Constraint](11-sql-elements.md#2bce9d5d0bac743d)를 참조한다.

&lt; JSON output clause &gt;에 대한 자세한 내용은 [JSON Output Clause](11-sql-elements.md#d8ec54a70fd9d3a7)를 참조한다.

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#74a33d522dd6bfcc)를 참조한다.

<a id="fbfd8e431033d5ea"></a>
### 설명

Window function JSON_OBJECTAGG는 window 범위 내의 JSON name and value 쌍을 연결하여 JSON object 문자열을 생성하는 함수이다.  
JSON name은 character string으로 표현할 수 있는 expresssion이어야 한다.

JSON constructor null clause는 SQL null 값을 어떻게 처리할지 지정하는 옵션이다.   
명시하지 않으면 기본값은 NULL ON NULL이다.

JSON key uniqueness constraint는 JSON object의 key field에 중복을 허용할지 여부를 결정하는 옵션이다. 명시하지 않으면 기본값은 WITHOUT UNIQUE KEYS이다.

JSON output clause는 함수가 생성하는 문자열의 타입과 출력 형식을 제어할 수 있는 옵션이다.  
Data type을 명시하여 결과 타입을 지정할 수 있다. 명시하지 않으면 기본값은 VARCHAR(4000)이다.  
PRETTY를 명시하여 JSON 문자열 출력 형식을 변경할 수 있다.

<a id="bf262c7d09e66aa1"></a>
### 사용 예

```
CREATE TABLE accounts ( name VARCHAR(20), balances INTEGER );
INSERT INTO accounts VALUES ( 'Alice', 50000 );
INSERT INTO accounts VALUES ( 'Bob', NULL );
INSERT INTO accounts VALUES ( 'Chris', 1000 );

gSQL> SELECT JSON_OBJECTAGG( name VALUE balances ) OVER ( ORDER BY balances DESC NULLS LAST ) AS res_json_objectagg_over
        FROM accounts;
RES_JSON_OBJECTAGG_OVER                
---------------------------------------
{"Alice":50000}                        
{"Alice":50000,"Chris":1000}           
{"Alice":50000,"Chris":1000,"Bob":null}

3 rows selected.
```

<a id="4918b9387a19231b"></a>
## LAG() OVER

<a id="af49afc90324efe2"></a>
### 구문

```
LAG ( expr [, offset [, default ] ] ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

LAG ( expr [ RESPECT NULLS | IGNORE NULLS ] [, offset [, default ] ] ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="4153bd36d161d55c"></a>
### 설명

Window function LAG는 현재 row에서 offset 만큼 이전의 row 값을 반환한다.  
Offset이 window 범위를 벗어나면 default 값을 반환한다.

Offset, default 값을 명시하지 않으면 기본값으로 설정된다.  
Offset 기본값은 1이고, default 기본값은 NULL 이다.

RESPECT NULLS는 NULL 값을 포함하여 offset 만큼 이전의 row 값을 반환한다.  
IGNORE NULLS는 NULL이 아닌 row 중 offset 만큼 이전의 row 값을 반환한다.  
명시하지 않으면 기본값은 RESPECT NULLS이다.

window frame은 사용할 수 없다.

<a id="005631e0305046ce"></a>
### 사용 예

```
gSQL> SELECT department_id, employee_id, manager_id,
             LAG( manager_id ) OVER ( ORDER BY employee_id ) AS lag
        FROM employees
       WHERE department_id = 90;

DEPARTMENT_ID EMPLOYEE_ID MANAGER_ID  LAG
------------- ----------- ---------- ----
           90         100       null null
           90         101        100 null
           90         102        100  100

3 rows selected.
```

다음은 offset을 명시한 예이다.

```
gSQL> SELECT department_id, employee_id, manager_id,
             LAG( manager_id, 2 ) OVER ( ORDER BY employee_id ) AS lag
        FROM employees
       WHERE department_id = 90;

DEPARTMENT_ID EMPLOYEE_ID MANAGER_ID  LAG
------------- ----------- ---------- ----
           90         100       null null
           90         101        100 null
           90         102        100 null

3 rows selected.
```

다음은 offset과 default를 명시한 예이다.

```
gSQL> SELECT department_id, employee_id, manager_id,
             LAG( manager_id, 2, 0 ) OVER ( ORDER BY employee_id ) AS lag
        FROM employees
       WHERE department_id = 90;

DEPARTMENT_ID EMPLOYEE_ID MANAGER_ID  LAG
------------- ----------- ---------- ----
           90         100       null    0
           90         101        100    0
           90         102        100 null

3 rows selected.
```

<a id="76b6d58617b4030b"></a>
## LAST() OVER

<a id="52132c370af6ffdc"></a>
### 구문

```
aggregation_function KEEP ( DENSE_RANK LAST ORDER BY <sort specification list> ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="094eff4b14ad0b15"></a>
### 설명

Window function LAST 함수는 KEEP 절 내 order by에 쓰인 sort specification list를 정렬한 후, DENSE_RANK 순위가 마지막인 row들의 aggregation function 값을 반환한다.

aggregation_function에 해당하는 함수는 AVG, COUNT, COUNT(*), SUM, MAX, MIN, STDDEV, VARIANCE 이다.

window 절 내에서 order by는 사용할 수 없다.  
window frame은 사용할 수 없다.

<a id="95110b9c54d37793"></a>
### 사용 예

```
gSQL> SELECT department_id, salary,
           DENSE_RANK() OVER ( ORDER BY department_id ) AS "DENSE_RANK",
           MAX( salary ) KEEP ( DENSE_RANK LAST ORDER BY department_id ) OVER () AS "MAX_LAST"
  FROM employees
 WHERE department_id BETWEEN 90 AND 100;

DEPARTMENT_ID SALARY DENSE_RANK MAX_LAST
------------- ------ ---------- --------
           90  24000          1    12000
           90  17000          1    12000
           90  17000          1    12000
          100  12000          2    12000
          100   9000          2    12000
          100   8200          2    12000
          100   7700          2    12000
          100   7800          2    12000
          100   6900          2    12000

9 rows selected.
```

<a id="54b97cb12add7e5f"></a>
## LAST_DAY

<a id="5242da99ee332d49"></a>
### 구문

```
LAST_DAY( date )
```

<a id="6e7d27f3e77798ee"></a>
### 설명

LAST_DAY 함수는 date에 포함된 월의 마지막 날짜를 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
반환되는 타입은 인자 date의 타입에 상관없이 항상 DATE이다.  

date가 NULL이면 NULL을 반환한다.

<a id="efaa7bb3893afa61"></a>
### 사용 예

```
gSQL> SELECT 
      LAST_DAY( TO_DATE( '2012-07-10', 'YYYY-MM-DD' ) ) AS RESULT FROM DUAL;
RESULT    
----------
2012-07-31
1 row selected.
```

<a id="0a4be64485ed5393"></a>
## LAST_IDENTITY_VALUE

<a id="77c550441e1b30fc"></a>
### 구문

```
LAST_IDENTITY_VALUE()
```

<a id="265bf92c9c7efa4e"></a>
### 설명

현재 session에서 identity column을 위해 자동으로 생성한 최근 값으로써 결과 타입은 NATIVE_BIGINT 이다.

자동 생성한 값이 없을 경우 null을 반환한다.

MS-SQL의 @@IDENTITY, MySQL의 LAST_INSERT_ID()와 유사한 기능으로, 다수의 테이블에 대해 DML을 수행할 경우 다음과 같이 마지막으로 변경한 테이블에 의해 값이 결정되므로 주의하여 사용하여야 한다.

```
gSQL> INSERT INTO t1(name) VALUES ( 'leekmo' );

1 row created.

gSQL> SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                   12

1 row selected.


gSQL> INSERT INTO t2(name) VALUES ( 'leekmo' );

1 row created.



gSQL> SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                    2

1 row selected.
```

INSERT 할 때 생성된 identity column의 값을 얻으려면 다음과 같이 [INSERT INTO name RETURNING .. INTO](20-sql-references-h-z.md#995e5aa709d17272) 구문을 사용한다.

```
gSQL> CREATE TABLE t1 ( id INTEGER GENERATED BY DEFAULT AS IDENTITY, name VARCHAR(32) );

Table created.

gSQL> \var v1 integer
gSQL> INSERT INTO t1(name) VALUES ( 'leekmo' ) RETURN id INTO :v1;

V1
--
 1

1 row created.
```

<a id="e7922bc931482419"></a>
### 사용 예

다음은 LAST_IDENTITY_VALUE() 함수를 사용하는 예이다.

```
gSQL> CREATE TABLE t1 ( id   INTEGER GENERATED BY DEFAULT AS IDENTITY,
                        name VARCHAR(32) ); 

Table created.

gSQL> COMMIT;

Commit complete.
```

- 현재 session에서 생성한 identity value가 없다.

```
gSQL> SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                 null

1 row selected.
```

- identity value (1)를 자동으로 생성한다.

```
gSQL> INSERT INTO t1(name) VALUES ( 'leekmo' );

1 row created.
```

- Result: 1

```
gSQL> SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                    1

1 row selected.
```

- Default 값으로 identity value (2)가 자동 생성된다.

```
gSQL> UPDATE t1 SET id = DEFAULT;

1 row updated.
```

- Result: 2

```
gSQL> SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                    2

1 row selected.
```

- 사용자가 입력한 값으로 identity value가 자동으로 생성되지 않는다.

```
INSERT INTO t1 VALUES ( 100, 'jhkim' );

1 row updated.
```

- Result: 2

```
SELECT LAST_IDENTITY_VALUE() FROM dual;

LAST_IDENTITY_VALUE()
---------------------
                    2

1 row selected.
```

<a id="1b557a326f8bb6ae"></a>
## LAST_VALUE() OVER

<a id="e215de4af94d4134"></a>
### 구문

```
LAST_VALUE ( expr ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

LAST_VALUE ( expr [ RESPECT NULLS | IGNORE NULLS ] ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="567e4262051085e6"></a>
### 설명

Window function LAST_VALUE는 expr의 마지막 값을 반환한다.

RESPECT NULLS는 NULL 값을 포함하여 row 중 마지막 값을 반환한다.  
IGNORE NULLS는 NULL이 아닌 row 중 마지막 값을 반환한다.  
명시하지 않으면 기본값은 RESPECT NULLS이다.

<a id="3906e1c27730428d"></a>
### 사용 예

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , LAST_VALUE( min_price ) OVER ( ORDER BY min_price ) AS "LAST_VALUE"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE LAST_VALUE
--------- ----------
       73         73
      247        247
      731        731
     null       null
     null       null

5 rows selected.
```

다음은 null_treatment에 IGNORE NULLS를 명시한 예이다.

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , LAST_VALUE( min_price IGNORE NULLS ) OVER ( ORDER BY min_price ) AS "LAST_VALUE"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE LAST_VALUE
--------- ----------
       73         73
      247        247
      731        731
     null        731
     null        731

5 rows selected.
```

<a id="724d528c51441dae"></a>
## LEAD() OVER

<a id="76df81d4777b6b43"></a>
### 구문

```
LEAD ( expr [, offset [, default ] ] ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

LEAD ( expr [ RESPECT NULLS | IGNORE NULLS ] [, offset [, default ] ] ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="8d6ddf234a5f1737"></a>
### 설명

Window function LEAD는 현재 row에서 offset 만큼 이후의 row 값을 반환한다.  
offset이 window 범위를 벗어났을 경우 default 값을 반환한다.

offset, default 값을 명시하지 않으면 기본값으로 설정된다.  
offset의 기본값은 1이고, default의 기본값은 NULL 이다.

RESPECT NULLS는 NULL 값을 포함하여 row 중 offset 만큼 이후의 row 값을 반환한다.  
IGNORE NULLS는 NULL이 아닌 row 중 offset 만큼 이후의 row 값을 반환한다.  
명시하지 않으면 기본값은 RESPECT NULLS이다.

window frame은 사용할 수 없다.

<a id="3b58085fc2b79481"></a>
### 사용 예

```
gSQL> SELECT department_id, employee_id, manager_id,
             LEAD( manager_id ) OVER ( ORDER BY employee_id DESC ) AS lead
        FROM employees
       WHERE department_id = 90;

DEPARTMENT_ID EMPLOYEE_ID MANAGER_ID LEAD
------------- ----------- ---------- ----
           90         102        100  100
           90         101        100 null
           90         100       null null

3 rows selected.
```

다음은 offset을 명시했을 때의 예이다.

```
gSQL> SELECT department_id, employee_id, manager_id,
             LEAD( manager_id, 2 ) OVER ( ORDER BY employee_id DESC ) AS lead
        FROM employees
       WHERE department_id = 90;

DEPARTMENT_ID EMPLOYEE_ID MANAGER_ID LEAD
------------- ----------- ---------- ----
           90         102        100 null
           90         101        100 null
           90         100       null null

3 rows selected.
```

다음은 offset과 default를 명시했을 때의 예이다.

```
gSQL> SELECT department_id, employee_id, manager_id,
             LEAD( manager_id, 2, 0 ) OVER ( ORDER BY employee_id DESC ) AS lead
        FROM employees
       WHERE department_id = 90;

DEPARTMENT_ID EMPLOYEE_ID MANAGER_ID LEAD
------------- ----------- ---------- ----
           90         102        100 null
           90         101        100    0
           90         100       null    0

3 rows selected.
```

<a id="72380c9a67173fb9"></a>
## LEAST

<a id="c83e2220920802f2"></a>
### 구문

```
LEAST( expr1 [, expr2, ... exprn ] )
```

<a id="d3b113fe4a4c5ae8"></a>
### 설명

LEAST 함수는 인자로 받은 expr들 중에 가장 작은 값을 반환한다.

인자로 받은 expr들 중 하나라도 NULL인 경우, 결과값은 NULL이다.

결과 타입은 expr1 (첫 번째 expr)의 데이터 타입에 따라 결정된다.  
expr1 (첫 번째 expr)의 데이터 타입이 숫자형인 경우와 문자형인 경우에는 각각 expr1, ..., exprN의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, ..., exprN에 모두 CHAR 타입이 기술된 경우, 모든 expr은 VARCHAR 타입으로 비교되고, 결과 타입은 VARCHAR 타입이 된다.

<a id="d9502db88575dccb"></a>
### 사용 예

```
gSQL> SELECT LEAST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="05398af639dccbdf"></a>
## LENGTH

<a id="6a59ed3ec26ded2c"></a>
### 구문

```
LENGTH( str )
```

<a id="2d0529baa858db66"></a>
### 설명

[CHAR_LENGTH](#419a706c1c7cf97a)의 alias 이다.

<a id="a9bb6113156c5c4d"></a>
### 사용 예

Multi byte character set: (예: UTF8)

```
gSQL> SELECT LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="601cb51b0994464d"></a>
## LENGTHB

<a id="90353f248837c346"></a>
### 구문

```
LENGTHB( str )
```

<a id="ce70ed8a4bbbb7fc"></a>
### 설명

OCTET_LENGTH의 alias이다.  
자세한 내용은 [OCTET_LENGTH](#ebe17e037d8d8ea6), [BYTE_LENGTH](#2e9fab2319460d39)를 참조한다.

<a id="535866f11bc38335"></a>
### 사용 예

- Multi byte character set (예: UTF8): 1 byte character

```
gSQL> SELECT LENGTHB( 'OCTET_LENGTH' ) AS RESULT_1BYTE_CHARACTERS 
        FROM DUAL;
RESULT_1BYTE_CHARACTERS
-----------------------
                     12
1 row selected.
```

- Multi byte character set (예: UTF8): 2 byte character

```
gSQL> SELECT LENGTHB( 'αβ' ) AS RESULT_2BYTE_CHARACTERS FROM DUAL;
RESULT_2BYTE_CHARACTERS
-----------------------
                      4
1 row selected.
```

<a id="102baf39aaaf238c"></a>
## LISTAGG() OVER

<a id="b4ec75a1501fc45d"></a>
### 구문

```
LISTAGG( str [, delimiter] ) WITHIN GROUP ( ORDER BY <sort specification list> ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="19fb8af6a4104bc0"></a>
### 설명

Window function LISTAGG는 각 그룹 내에서 정렬된 순서대로 str을 연결하는 함수이다.

LISTAGG의 OVER() 절에는 PARTITION BY 절만 기술할 수 있다.  
OVER() 절을 사용하여 쿼리 결과 집합을 그룹으로 분할한다.

WITHIN GROUP ( ORDER BY &lt;sort specification list&gt; )로 그룹 내 레코드를 정렬한다.

각 그룹 내 정렬된 레코드 순서대로 str을 연결한다.   
str이 NULL인 경우에는 제외된다.

delimiter는 str 연결 구분자이며, 생략할 경우 기본값은 NULL 이다.

str에는 character string 또는 binary string이 올 수 있다.   
str이 character string 이면 결과 타입은 varchar 이다.   
str이 binary string 이면 결과 타입은 varbinary 이다.

<a id="a90a1587bce8f504"></a>
### 사용 예

```
gSQL> 
SELECT regionkey,
       name,
       LISTAGG( name ) WITHIN GROUP ( ORDER BY nationkey ) 
                       OVER ( PARTITION BY regionkey ) 
       AS "LISTAGG( name ) RESULT",
       LISTAGG( name, ', ' ) WITHIN GROUP ( ORDER BY nationkey ) 
                             OVER ( PARTITION BY regionkey ) 
       AS "LISTAGG( name, ', ' ) RESULT"
  FROM nation;

REGIONKEY NAME    LISTAGG( name ) RESULT    LISTAGG( name, ', ' ) RESULT
--------- ------- ------------------------- ----------------------------
        1 BRAZIL  BRAZILCANADAPERU          BRAZIL, CANADA, PERU        
        1 CANADA  BRAZILCANADAPERU          BRAZIL, CANADA, PERU        
        1 PERU    BRAZILCANADAPERU          BRAZIL, CANADA, PERU        
        1 null    BRAZILCANADAPERU          BRAZIL, CANADA, PERU        
        2 null    INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 INDIA   INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 null    INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 null    INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 JAPAN   INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 CHINA   INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 null    INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        2 VIETNAM INDIAJAPANCHINAVIETNAM    INDIA, JAPAN, CHINA, VIETNAM
        3 EGYPT   EGYPTIRANIRAQ             EGYPT, IRAN, IRAQ           
        3 IRAN    EGYPTIRANIRAQ             EGYPT, IRAN, IRAQ           
        3 IRAQ    EGYPTIRANIRAQ             EGYPT, IRAN, IRAQ           

15 rows selected.
```

<a id="1af3c5c68fbbc382"></a>
## LN

<a id="1208eb6b94d5870c"></a>
### 구문

```
LN( num )
```

<a id="bb6ee2b4e9e6c2ee"></a>
### 설명

LN 함수는 num의 자연 로그 값을 반환하는 함수이다.  

num은 0보다 큰 값이어야 한다.  
num이 NULL이면 NULL을 반환한다.

<a id="aa1f6cbdad829b14"></a>
### 사용 예

```
gSQL> SELECT LN( 2.71828182845905 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="1bc32b2291689342"></a>
## LNNVL

<a id="717cb3e464f6f111"></a>
### 구문

```
LNNVL( expr )
```

<a id="0796c4d8028f53c7"></a>
### 설명

Logical Not Null VaLue (LNNVL) 함수는 NOT logical operator와 유사하지만 다음 예제와 같이 입력값이 null일 경우 TRUE를 반환한다는 차이가 있다.

<a id="7152aed315db11fc"></a>
### 사용 예

```
gSQL> SELECT c1, c2, (c1 = c2), NOT(c1 = c2), LNNVL(c1 = c2) FROM t1;

C1   C2 (C1 = C2) NOT(C1 = C2) LNNVL(C1 = C2)
-- ---- --------- ------------ --------------
 1    1 TRUE      FALSE        FALSE         
 1    2 FALSE     TRUE         TRUE          
 1 null null      null         TRUE          

3 rows selected.
```

<a id="dc9d3b7e4ce6bf46"></a>
## LOCAL_GROUP_ID

<a id="9254517af3a3b779"></a>
### 구문

```
LOCAL_GROUP_ID()
```

<a id="a56c3338f9528987"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster group ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="05f5325943251ebb"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_GROUP_ID() FROM DUAL;

LOCAL_GROUP_ID()
----------------
               1

1 row selected.
```

<a id="2e4257c39f048c7e"></a>
## LOCAL_GROUP_NAME

<a id="3e935dfdc8b777a2"></a>
### 구문

```
LOCAL_GROUP_NAME()
```

<a id="f88d65ea78ed7c9f"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster group name을 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="854dfd906b0b899e"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_GROUP_NAME() FROM DUAL;

LOCAL_GROUP_NAME()
------------------
G1                

1 row selected.
```

<a id="2568235021ca182f"></a>
## LOCAL_MEMBER_ID

<a id="abe870ff12f6a271"></a>
### 구문

```
LOCAL_MEMBER_ID()
```

<a id="0abafc0c9cbeb5b3"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster member ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="6c1ef2214d4e0642"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_MEMBER_ID() FROM DUAL;

LOCAL_MEMBER_ID()
-----------------
                1

1 row selected.
```

<a id="f93a13cad5d7b9ce"></a>
## LOCAL_MEMBER_NAME

<a id="db1cf5e2dc3e0821"></a>
### 구문

```
LOCAL_MEMBER_NAME()
```

<a id="f43669396d1fe3bc"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster member name을 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="287f401f423b81cc"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_MEMBER_NAME() FROM DUAL;

LOCAL_MEMBER_NAME()
-------------------
G1N1               

1 row selected.
```

<a id="afd5f1462dcfbc60"></a>
## LOCAL_MEMBER_POSITION

<a id="95ec72465b5c7346"></a>
### 구문

```
LOCAL_MEMBER_POSITION()
```

<a id="431e0ca2a8741a24"></a>
### 설명

사용자 질의를 처리하는 server의 cluster member position을 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="23c025340487cb9c"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_MEMBER_POSITION() FROM DUAL;

LOCAL_MEMBER_POSITION()
-----------------------
                      0

1 row selected.
```

<a id="29a1e06e2f61c0cf"></a>
## LOCALTIME

<a id="0eb2ed7e58bdc6ac"></a>
### 구문

```
LOCALTIME [()]
STATEMENT_LOCALTIME()
```

<a id="27fb3496ceee6bc1"></a>
### 설명

Session 시간을 기준으로 현재 TIME WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• LOCALTIME, STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="0d7c964fff275914"></a>
### 사용 예

각 row의 시간값이 모두 같다.

```
gSQL>  SELECT LOCALTIME FROM t1;

LOCALTIME      
---------------
16:17:08.592459
16:17:08.592459
16:17:08.592459

3 rows selected.
```

<a id="b90cd72f5e69bd64"></a>
## LOCALTIMESTAMP

<a id="44f70a78265525f3"></a>
### 구문

```
LOCALTIMESTAMP [()]
STATEMENT_LOCALTIMESTAMP()
```

<a id="c21ce91b1ae4b269"></a>
### 설명

Session 시간을 기준으로 현재 TIMESTAMP WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• LOCALTIMESTAMP, STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="ca0aef2de2f0877a"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCALTIMESTAMP FROM t1;

LOCALTIMESTAMP            
--------------------------
2013-12-12 16:21:51.790614
2013-12-12 16:21:51.790614
2013-12-12 16:21:51.790614

3 rows selected.
```

<a id="ab56736fb79f42fc"></a>
## LOG

<a id="124cc0ad733d0ea3"></a>
### 구문

```
LOG( num2 )
LOG( num1, num2 )
```

<a id="142dc04ae2a6b641"></a>
### 설명

LOG 함수는 밑이 num1인 num2의 로그값을 반환한다.  
num1이 생략된 경우에는 밑이 10으로 계산된 값이 반환된다.

num1은 1과 0이 아닌 양수이어야 하고, num2는 양수이어야 한다.

num1 또는 num2가 NULL이면 NULL을 반환한다.

<a id="f73b3d2e8173f9f8"></a>
### 사용 예

```
gSQL> SELECT LOG( 100 ) AS RESULT1, LOG( 4, 16 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      2       2
1 row selected.
```

<a id="4b8d5f7b599da219"></a>
## LOGON_USER

<a id="8dce8c34801b4d66"></a>
### 구문

```
LOGON_USER()
```

<a id="63ef42605e0c7fc5"></a>
### 설명

로그인 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다.
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다.
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다.
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="4f805ce8f7a6683f"></a>
### 사용 예

```
% gsql test test

gSQL> SELECT LOGON_USER() AS result FROM DUAL;

RESULT
------
TEST  

1 row selected.
```

<a id="03c55163b33ff21c"></a>
## LOWER

<a id="8ac00afda797ecf7"></a>
### 구문

```
LOWER( str )
```

<a id="3f2964b5e3081542"></a>
### 설명

LOWER 함수는 str의 소문자를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.  
str이 NULL이면 결과값도 NULL이다.

인자 str과 동일한 타입이 반환된다.

<a id="a4639484fd484195"></a>
### 사용 예

```
gSQL> SELECT LOWER( 'SPRING' ) AS RESULT FROM DUAL;
RESULT
------
spring
1 row selected.
```

<a id="57c2aeb569da8a55"></a>
## LPAD

<a id="e7edbf03357e0dac"></a>
### 구문

```
LPAD( str, length, [, fill] )
```

<a id="f99e36ae1aeec666"></a>
### 설명

LPAD 함수는 string의 길이가 length가 될 때까지 str의 왼쪽에 문자열 fill을 추가한 값을 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

인자 length에는 숫자 타입이 올 수 있다.

length는 문자의 개수를 의미하며, 최대 범위는 결과 타입의 최대 PRECISION이다.  
fill이 생략된 경우, 공백 문자가 추가된다.  
str이 length보다 길이가 긴 경우에는 str을 length만큼 잘라서 반환한다.  
str, length, fill이 하나라도 NULL이면 결과값도 NULL이며, length가 0 또는 음수인 경우에도 결과값은 NULL이다.

결과 타입은 다음 표와 같다.

**LPAD의 결과 타입**

<a id="97f98d7eab7360fa"></a>
| 인자 str의 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="1db86ab9aec039c4"></a>
### 사용 예

```
gSQL> SELECT LPAD('AA', 5) AS RESULT1,
             LPAD('AA', 5, 'X' ) AS RESULT2,
             LPAD('AA', 1 ) AS RESULT3
      FROM DUAL;
RESULT1 RESULT2 RESULT3
------- ------- -------
   AA   XXXAA   A      
1 row selected.
```

<a id="c1673b54eb0d99bd"></a>
## LTRIM

<a id="ff9fba08820ba888"></a>
### 구문

```
LTRIM( trim_source [, trim_character ] )
```

<a id="55183c224ad03dd9"></a>
### 설명

LTRIM 함수는 trim_source에서 trim_character를 왼쪽 방향에서 비교하여 일치하는 문자가 없을 때까지 제거한 결과를 반환한다.

인자 trim_character와 trim_source에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

trim_character, trim_source 중 하나라도 NULL이면, 결과값은 NULL이다.  
trim_character가 생략된 경우에는 기본적으로 single blank space (' ')가 지정된다.

결과 타입은 다음과 같다.

**LTRIM의 결과 타입**

<a id="e1a4274861a05f82"></a>
| trim_source, trim_character 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="7be5083bf86254e3"></a>
### 사용 예

```
gSQL> SELECT LTRIM('      ltrim      ') AS RESULT1,
             LTRIM('______ltrim______','_') AS RESULT2
      FROM DUAL;
RESULT1     RESULT2    
----------- -----------
ltrim       ltrim______
1 row selected.
```

<a id="314460f16bf53fb9"></a>
## MAX

<a id="795b1b13a71cb7e9"></a>
### 구문

```
MAX( [ ALL | DISTINCT ] expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="9672a8404230fd7f"></a>
### 설명

Aggregation 함수로써 row들의 expr 중 최대값을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복을 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

MAX는 ALL과 DISTINCT에 영향을 받지 않고 동일한 결과를 낸다.

FILTER를 명시한 경우 condition을 만족하는 값들에 한하여 aggregation을 수행한다.

<a id="1445a28ab165f347"></a>
### 사용 예

```
gSQL> SELECT MAX( c1 ) FROM t1;

MAX(C1)
-------
      3

1 row selected.


gSQL> SELECT MAX( c1 ) FILTER( WHERE c1 < 3 ) FROM t1;

MAX(C1)
-------
      2

1 row selected.
```

<a id="f24a16652f711f98"></a>
## MAX() OVER

<a id="449aa9323df4ce9a"></a>
### 구문

```
MAX ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="8e8257d9fbad3a86"></a>
### 설명

Window function MAX은 expr 중 최대값을 구하는 함수이다.  
NULL 값은 연산에서 제외된다.

<a id="a7e7a6e2ef02a62a"></a>
### 사용 예

```
gSQL> SELECT product_id AS "PRODUCT_ID", min_price AS "MIN_PRICE"
             , MAX( min_price ) OVER ( ORDER BY product_id ) AS "MAX"
        FROM product_information
       WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE  MAX
---------- --------- ----
      1769      null null
      1770        73   73
      2378       247  247
      2382       731  731
      3355      null  731

5 rows selected.
```

<a id="6e2d4738fd4f25a5"></a>
## MEDIAN() OVER

<a id="b6190e5289b161ac"></a>
### 구문

```
MEDIAN ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="20d917c3a48d1710"></a>
### 설명

Window function MEDIAN은 중간에 위치한 row 값을 반환하는 함수이다.  
NULL은 연산에서 제외된다.

window 절 내에서 order by는 사용할 수 없다.  
window frame은 사용할 수 없다.

<a id="9e2a92ed50b00372"></a>
### 사용 예

```
gSQL> SELECT supplier_id, min_price
             , MEDIAN( min_price ) OVER ( PARTITION BY supplier_id ) AS "MEDIAN"
        FROM product_information
       WHERE supplier_id = 102050;

SUPPLIER_ID MIN_PRICE MEDIAN
----------- --------- ------
     102050        73    247
     102050       247    247
     102050       731    247
     102050      null    247
     102050      null    247

5 rows selected.
```

<a id="e9ae230f46525210"></a>
## MIN

<a id="c653466307b72798"></a>
### 구문

```
MIN( [ ALL | DISTINCT ] expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="c2f0b24e7c62a20c"></a>
### 설명

Aggregation 함수로써 row들의 expr 중 최소값을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

MIN은 ALL과 DISTINCT에 영향을 받지 않고 동일한 결과를 낸다.

FILTER를 명시한 경우 condition을 만족하는 값들에 한하여 aggregation을 수행한다.

<a id="daf8d26ae0afdaf7"></a>
### 사용 예

```
gSQL> SELECT MIN( c1 ) FROM t1;

MIN(C1)
-------
      1

1 row selected.


gSQL> SELECT MIN( c1 ) FILTER( WHERE c1 > 1 ) FROM t1;

MIN(C1)
-------
      2

1 row selected.
```

<a id="ba035b5b6ae776da"></a>
## MIN() OVER

<a id="6827782523626043"></a>
### 구문

```
MIN ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="92ba3e9026782935"></a>
### 설명

Window function MIN은 expr 중 최소값을 구하는 함수이다.  
NULL 값은 연산에서 제외된다.

<a id="4a51d22497c71108"></a>
### 사용 예

```
gSQL> SELECT product_id AS "PRODUCT_ID", min_price AS "MIN_PRICE"
             , MIN( min_price ) OVER ( ORDER BY product_id DESC ) AS "MIN"
        FROM product_information
       WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE  MIN
---------- --------- ----
      3355      null null
      2382       731  731
      2378       247  247
      1770        73   73
      1769      null   73

5 rows selected.
```

<a id="b6614f54ea98c663"></a>
## MOD

<a id="13d9158eebcd185c"></a>
### 구문

```
MOD( num1, num2 )
```

<a id="a46ba206c47a0fc8"></a>
### 설명

MOD는 num1을 num2로 나눈 나머지를 반환한다.  

인자 num1, num2에는 숫자타입이 올 수 있다.  
num2가 0이면 에러를 반환한다.  
인자 num1 또는 num2가 NULL이면 NULL을 반환한다.

<a id="d13f8dc0f0847e51"></a>
### 사용 예

```
gSQL> SELECT MOD(5, 4) AS RESULT1, MOD(-5, 4) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1      -1
1 row selected.
```

<a id="d1392f141e83ac3a"></a>
## MONTHS_BETWEEN

<a id="b558531a337e2c9c"></a>
### 구문

```
MONTHS_BETWEEN( date1, date2 )
```

<a id="2053f529c78e186e"></a>
### 설명

MONTHS_BETWEEN은 date2와 date1 사이의 일수를 31로 나눈 개월 수를 반환한다.

date1 또는 date2가 NULL이면 결과도 NULL이다.  
인자 date1, date2에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.

결과 타입은 NUMBER 이다.

> date1과 date2 모두에 동일한 날짜가 포함되어 있거나 (예: 2014-01-15 와 2014-02-15) 월의 마지막 날짜가 포함되어 있는 경우 (예: 2014-08-31와 2014-09-30), 타임스탬프 구간 (있는 경우)의 일치 여부와 상관없이 정수 결과를 반환한다.

<a id="9f264fa44e911034"></a>
### 사용 예

```
gSQL> SELECT
        MONTHS_BETWEEN('2018-01-18', '2018-01-17')
  FROM DUAL;

MONTHS_BETWEEN('2018-01-18', '2018-01-17')
------------------------------------------
                      3.225806451612903E-2
1 row selected.

gSQL> SELECT
        MONTHS_BETWEEN('2018-02-17', '2018-01-17')
  FROM DUAL;

MONTHS_BETWEEN('2018-02-17', '2018-01-17')
------------------------------------------
                                         1
1 row selected.

gSQL> SELECT
        MONTHS_BETWEEN('2018-02-28', '2018-01-31')
  FROM DUAL;

MONTHS_BETWEEN('2018-02-28', '2018-01-31')
------------------------------------------
                                         1
1 row selected.
```

<a id="8f75f4c5ce98d30f"></a>
## NEXT_DAY

<a id="9388feaa0858a94e"></a>
### 구문

```
NEXT_DAY( date, day )
```

<a id="17a11f7e0aa853f6"></a>
### 설명

인자로 주어진 date (날짜)를 지나 처음으로 도래하는 day (요일)의 날짜를 구한다.

두 번째 인자 day에는 day를 지칭하는 스트링 또는 숫자가 올 수 있다.  
• 스트링:  SUNDAY ~ SATURDAY  또는 SUN ~ SAT  
• 숫자:  1 (sunday) ~ 7 (saturday)  

입력 인자 중 하나라도 NULL이면 결과값도 NULL이다.

반환되는 타입은 date의 입력 타입에 상관없이 항상 DATE 타입이다.  
결과값의 시분초는 입력 인자 date의 시분초를 동일하게 반환한다.

<a id="a960102d9445243f"></a>
### 사용 예

- 2020-08-11은 화요일이다.

```
gSQL> SELECT NEXT_DAY( TO_DATE( '2020-08-11', 'YYYY-MM-DD'),
                       'SUNDAY' ) AS RESULT1
      FROM DUAL;
RESULT1   
----------
2020-08-16
1 row selected.

gSQL> SELECT NEXT_DAY( TO_DATE( '2020-08-11', 'YYYY-MM-DD' ),
                       'SUN' ) AS RESULT1
FROM DUAL;
RESULT1   
----------
2020-08-16
1 row selected.

gSQL> SELECT NEXT_DAY( TO_DATE( '2020-08-11', 'YYYY-MM-DD' ),
                       1 ) AS RESULT1
FROM DUAL;
RESULT1   
----------
2020-08-16
1 row selected.

gSQL> SELECT TO_CHAR( NEXT_DAY( TO_DATE( '2020-08-11', 'YYYY-MM-DD' ),
                                'SUNDAY' ),
                      'YYYY-MM-DD HH24:MI:SS' ) AS RESULT1
FROM DUAL;
RESULT1            
-------------------
2020-08-16 00:00:00
1 row selected.
```

<a id="608a9268f6f53c18"></a>
## NEXTVAL

<a id="1768416c0c0dcdae"></a>
### 구문

```
seq_name.NEXTVAL
NEXTVAL( seq_name )
NEXT VALUE FOR seq_name
```

<a id="9dc05ffdffbb39b8"></a>
### 설명

시퀀스 객체의 다음 값을 얻는다.

<a id="2c6e16f9dc6b8934"></a>
### 사용 예

```
gSQL> CREATE SEQUENCE seq;

Sequence created.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT seq.NEXTVAL FROM dual;

SEQ.NEXTVAL
-----------
          1

1 row selected.

gSQL> SELECT NEXTVAL( seq ) FROM dual;

NEXTVAL( SEQ )
--------------
             2

1 row selected.

gSQL> SELECT NEXT VALUE FOR seq FROM dual;

NEXT VALUE FOR SEQ
------------------
                 3

1 row selected.
```

<a id="97b8815e3ed2ffbc"></a>
## NTH_VALUE() OVER

<a id="99312a0cff916603"></a>
### 구문

```
NTH_VALUE ( expr, n ) [ FROM { FIRST | LAST } ][ { RESPECT | IGNORE } NULLS ] OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="309736f044d8b409"></a>
### 설명

Window function NTH_VALUE는 n 번째 row의 expr 값을 반환한다.  
window의 row 개수가 n 보다 적을 경우, NULL을 반환한다.

인자 n에는 숫자 타입 또는 숫자로 변환될 수 있는 타입이 올 수 있다.

FROM FIRST는 첫 번째 row 로부터 n 번째 row를 가리킨다.   
FROM LAST는 마지막 row 로부터 n 번째 row를 가리킨다.  
명시하지 않으면 기본값은 FROM FIRST 이다.

RESPECT NULLS는 NULL 값을 포함하여 n 번째 row의 값을 반환한다.  
IGNORE NULLS는 NULL이 아닌 row 중 n 번째 값을 반환한다.  
명시하지 않으면 기본값은 RESPECT NULLS 이다.

<a id="fdf2666bbc89caf3"></a>
### 사용 예

```
gSQL> SELECT product_id, min_price,
             NTH_VALUE( min_price, 2 ) OVER ( ORDER BY product_id ) AS nth_value
      FROM product_information
      WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE NTH_VALUE
---------- --------- ---------
      1769      null      null
      1770        73        73
      2378       247        73
      2382       731        73
      3355      null        73

5 rows selected.
```

다음은 FROM LAST를 명시했을 때의 예이다.

```
gSQL> SELECT product_id, min_price,
             NTH_VALUE( min_price, 2 ) FROM LAST OVER ( ORDER BY product_id ) AS nth_value
      FROM product_information
      WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE NTH_VALUE
---------- --------- ---------
      1769      null      null
      1770        73      null
      2378       247        73
      2382       731       247
      3355      null       731

5 rows selected.
```

다음은 IGNORE NULLS를 명시했을 때의 예이다.

```
gSQL> SELECT product_id, min_price,
             NTH_VALUE( min_price, 2 ) IGNORE NULLS OVER ( ORDER BY product_id ) AS nth_value
      FROM product_information
      WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE NTH_VALUE
---------- --------- ---------
      1769      null      null
      1770        73      null
      2378       247       247
      2382       731       247
      3355      null       247

5 rows selected.
```

<a id="f11c1348046c4464"></a>
## NTILE() OVER

<a id="20154af494a36f24"></a>
### 구문

```
NTILE( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="b26e99d6b8d8355e"></a>
### 설명

Window function NTILE은 각 row에 해당하는 버킷 번호를 반환한다.

버킷 번호는 1부터 시작하는 연속적인 정수이고, 버킷 개수는 expr 개수와 같다.  
버킷 개수가 row 개수보다 많은 경우, 각 row마다 버킷 한 개씩 나누어주고 나머지 버킷은 비워둔다.

expr은 양의 상수이어야 한다. expr이 고정된 숫자가 아닐 경우, expr은 window partition by 대상이어야 한다.

window frame은 사용할 수 없다.

<a id="38bb3cb708d797f0"></a>
### 사용 예

```
gSQL> SELECT department_id, salary,
             NTILE(3) OVER ( ORDER BY salary ) AS ntile
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY NTILE
------------- ------ -----
           60   4200     1
           60   4800     1
           60   4800     2
           60   6000     2
           60   9000     3

5 rows selected.
```

다음은 버킷 개수 (expr 개수)가 row 개수보다 큰 예이다.

```
gSQL> SELECT department_id, salary,
             NTILE(6) OVER ( ORDER BY salary ) AS ntile
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY NTILE
------------- ------ -----
           60   4200     1
           60   4800     2
           60   4800     3
           60   6000     4
           60   9000     5

5 rows selected.
```

<a id="5c39f8c5b46c9f0c"></a>
## NULLIF

<a id="91819f5d81936e75"></a>
### 구문

```
NULLIF( expr1, expr2 )
```

<a id="782ea43cb0da3127"></a>
### 설명

expr1과 expr2가 같으면 null을 반환하고, 같지 않으면 첫 번째 인자인 expr1을 반환한다.

expr1과 expr2의 타입이 서로 다를 경우, [결과 타입 조합 규칙](11-sql-elements.md#e881713e04641bea)에 따라 result type이 결정된다.

NULLIF는 CASE를 사용하여 동일하게 표현할 수 있다.

- NULLIF( expr1, expr2 )

```
CASE WHEN expr1 = expr2 THEN NULL 
       ELSE expr1 
  END
```

<a id="eecf2765629dc690"></a>
### 사용 예

```
gSQL> SELECT NULLIF( 'SUN', 'SUN' ) AS RESULT1, 
             NULLIF( 'SUN', 'MOON' ) AS RESULT2 
       FROM DUAL;
RESULT1 RESULT2
------- -------
null    SUN    
1 row selected.
```

<a id="ec0c8757a80dc2bb"></a>
## NUMTODSINTERVAL

<a id="d0c8fc02b12bc863"></a>
### 구문

```
NUMTODSINTERVAL( num, interval_indicator )
```

<a id="5eb25442e7eb8a19"></a>
### 설명

interval_indicator 단위인 number를 interval day to second 타입으로 변환하여 반환한다.

인자 number는 숫자 타입이다.

인자 interval_indicator는 CHAR, VARCHAR와 같은 문자 타입이며, 대소문자 구분없이 'DAY', 'HOUR', 'MINUTE', 'SECOND' 중 하나여야 한다.

인자 중 하나라도 NULL이면 결과로 NULL이 반환된다.

interval day(6) to second(6) 타입의 결과를 반환하며 precision은 사용자가 임의로 변경할 수 없다. 변환된 결과의 leading precision이 기본 precision을 초과하면 에러가 반환되며, fraction precision이 기본 precision을 초과하면 반올림한 결과를 반환한다.

<a id="b0cb3bc64e2a254e"></a>
### 사용 예

- 1 Day를 interval day to second 타입으로 변환한다.

```
gSQL> SELECT NUMTODSINTERVAL(1, 'DAY') FROM DUAL;

NUMTODSINTERVAL(1, 'DAY')
-------------------------
+000001 00:00:00.000000  

1 row selected.
```

- 36 Hour를 interval day to second 타입으로 변환한다.

```
gSQL> SELECT NUMTODSINTERVAL(36, 'HOUR') FROM DUAL;

NUMTODSINTERVAL(36, 'HOUR')
---------------------------
+000001 12:00:00.000000    

1 row selected.
```

- 1530 Minute를 interval day to second 타입으로 변환한다.

```
gSQL> SELECT NUMTODSINTERVAL(1530, 'MINUTE') FROM DUAL;

NUMTODSINTERVAL(1530, 'MINUTE')
-------------------------------
+000001 01:30:00.000000        

1 row selected.
```

- 90100.1234567 Second를 interval day to second로 변환한다.

```
gSQL> SELECT NUMTODSINTERVAL(90100.1234567, 'SECOND') FROM DUAL;

NUMTODSINTERVAL(90100.1234567, 'SECOND')
----------------------------------------
+000001 01:01:40.123457                 

1 row selected.
```

<a id="b5c581181c57d3ff"></a>
## NUMTOYMINTERVAL

<a id="a2ed13a0f092a4ec"></a>
### 구문

```
NUMTOYMINTERVAL( num, interval_indicator )
```

<a id="596c7c0f13432421"></a>
### 설명

interval_indicator 단위인 number를 interval year to month 타입으로 변환하여 반환한다.

인자 number는 숫자 타입이다.

인자 interval_indicator는 CHAR, VARCHAR와 같은 문자 타입이며, 대소문자 구분없이 'YEAR', 'MONTH' 중 하나여야 한다.

인자 중 하나라도 NULL이면 결과로 NULL이 반환된다.

interval year(6) to month 타입을 결과로 반환하며 precision은 사용자가 임의로 변경할 수 없다. 변환된 결과의 leading precision이 기본 precision을 초과하면 에러가 반환된다.

<a id="47413167806b7362"></a>
### 사용 예

- 1 Year를 interval year to month로 변환한다.

```
gSQL> SELECT NUMTOYMINTERVAL(1, 'YEAR') FROM DUAL;

NUMTOYMINTERVAL(1, 'YEAR')
--------------------------
+000001-00                

1 row selected.
```

- 13.5 Month를 interval year to month로 변환한다.

```
gSQL> SELECT NUMTOYMINTERVAL(13.5, 'MONTH') FROM DUAL;

NUMTOYMINTERVAL(13.5, 'MONTH')
------------------------------
+000001-02                    

1 row selected.
```

<a id="00a4fa9fc6ce087b"></a>
## NVL

<a id="5870c96af63fa379"></a>
### 구문

```
NVL( expr1, expr2 )
```

<a id="201112239d20e340"></a>
### 설명

expr1이 null이 아니면 expr1을 반환하고, expr1이 null이면 expr2를 반환한다.

결과 타입은 expr1의 데이터 타입에 따라 결정된다.  
expr1에 NULL이 기술된 경우에는 expr2의 타입에 따라 결과 타입이 결정된다.  
expr1의 데이터 타입이 숫자형 타입인 경우와 문자형 타입인 경우는 각각 expr1, expr2의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, expr2의 데이터 타입이 모두 CHAR 타입인 경우, 결과 타입은 VARCHAR로 결정된다.

<a id="94c769b4b46f0311"></a>
### 사용 예

```
gSQL> SELECT I1, NVL( I1, 0 ) FROM T1;
  I1 NVL( I1, 0 )
---- ------------
   1            1
null            0
2 rows selected.
```

<a id="efc7c9afd4e32b88"></a>
## NVL2

<a id="f24a98c1fb343922"></a>
### 구문

```
NVL2( expr1, expr2, expr3 )
```

<a id="e92df14f3449e99d"></a>
### 설명

expr1이 null이 아니면 expr2를 반환하고, expr1이 null이면 expr3을 반환한다.

결과 타입은 expr2의 데이터 타입에 따라 결정된다.  
expr2에 NULL이 기술된 경우에는 expr3의 타입에 따라 결과 타입이 결정된다.  
expr2의 데이터 타입이 숫자형인 경우와 문자형인 경우에는 각각 expr2, expr3의 범위를 포함할 수 있는 타입으로 결정된다.  
expr2, expr3의 데이터 타입이 모두 CHAR 타입인 경우, 결과 타입은 VARCHAR가 된다.

<a id="de47f99313fa6145"></a>
### 사용 예

```
gSQL> SELECT I1, NVL2( I1, I1 * 1000, 0 ) FROM T1;
  I1 NVL2( I1, I1 * 1000, 0 )
---- ------------------------
   1                     1000
null                        0
2 rows selected.
```

<a id="ebe17e037d8d8ea6"></a>
## OCTET_LENGTH

<a id="6e290778f46cd1aa"></a>
### 구문

```
OCTET_LENGTH( str )  

BYTE_LENGTH( str )     

LENGTHB( str )
```

<a id="f5907e3b3b8defe3"></a>
### 설명

OCTET_LENGTH는 str의 바이트 수를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

str의 타입이 CHARACTER면 공백문자도 계산에 포함된다.  
str이 NULL이면 결과값도 NULL이다.

OCTET_LENGTH의 alias로는 [BYTE_LENGTH](#2e9fab2319460d39)와 [LENGTHB](#601cb51b0994464d) 함수가 있다.

<a id="05bc016d2dcec92e"></a>
### 사용 예

- Multi byte character set (예: UTF8): 1 byte character

```
gSQL> SELECT OCTET_LENGTH( 'OCTET_LENGTH' ) AS RESULT_1BYTE_CHARACTERS 
        FROM DUAL;
RESULT_1BYTE_CHARACTERS
-----------------------
                     12
1 row selected.
```

- Multi byte character set (예: UTF8): 2 byte character

```
gSQL> SELECT OCTET_LENGTH( 'αβ' ) AS RESULT_2BYTE_CHARACTERS FROM DUAL;
RESULT_2BYTE_CHARACTERS
-----------------------
                      4
1 row selected.
```

<a id="f9762257927cdd90"></a>
## OVERLAY

<a id="3bdb9f8807392737"></a>
### 구문

```
OVERLAY( str1 PLACING str2 FROM start_position  [ FOR string_length ] )
```

<a id="3fe4a4876b54b610"></a>
### 설명

OVERLAY 함수는 str1의 start_position부터 string_length까지의 문자를 str2로 치환한 결과를 반환한다.

인자 str1과 str2에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARCATER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.  

인자 start_position과 string_length에는 숫자 타입이 올 수 있다.

- OVERLAY 결과는 다음과 같다.
+
    - FOR가 지정된 경우  
      SUBSTRING( str1 FROM 1 FOR (start_position - 1) )  
      || str2  
      || SUBSTRING( str1 FROM (start_position + string_length )
+
    - FOR가 생략된 경우  
      SUBSTRING( str1 FROM 1 FOR (start_position - 1) )  
      || str2  
      || SUBSTRING( str1 FROM (start_position + CHAR_LENGTH(str2))

자세한 내용은 [SUBSTRING](#6811306ff1562f60)을 참조한다.

결과 타입은 다음 표와 같다.

**OVERLAY의 결과 타입**

<a id="f3add52ac22e0053"></a>
| str1, str2 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="2437c07daa1911ee"></a>
### 사용 예

```
gSQL> SELECT
         OVERLAY( 'RESULT_OF_XXX_FUNC' PLACING 'OVERLAY' FROM 11 )
         AS RESULT1,
         OVERLAY( 'RESULT_OF_XXX_FUNC' PLACING 'OVERLAY' FROM 11 FOR 3 )
         AS RESULT2
      FROM DUAL;
RESULT1            RESULT2               
------------------ ----------------------
RESULT_OF_OVERLAYC RESULT_OF_OVERLAY_FUNC
1 row selected.
```

<a id="1da4d29d25993dd6"></a>
## PERCENT_RANK() OVER

<a id="47ac4a044c86a9c8"></a>
### 구문

```
PERCENT_RANK( ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="f591cc4f3ca32bbe"></a>
### 설명

Window function PERCENT_RANK는 전체 row 개수에 대해 각 row가 갖는 순위의 비율을 계산한다.

PERCENT_RANK 함수의 결과는 0부터 1 사이의 숫자이고, row 값이 같으면 비율 값도 같다.

window frame은 사용할 수 없다.

<a id="bd9b0885396c31a1"></a>
### 사용 예

```
gSQL> SELECT department_id, salary,
             PERCENT_RANK() OVER ( ORDER BY salary ) AS p_rank
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY P_RANK
------------- ------ ------
           60   4200      0
           60   4800    .25
           60   4800    .25
           60   6000    .75
           60   9000      1

5 rows selected.
```

<a id="f8428bd33ea54be9"></a>
## PERCENTILE_CONT() OVER

<a id="0f16041f36309303"></a>
### 구문

```
PERCENTILE_CONT( expr ) WITHIN GROUP ( ORDER BY <sort specification> ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="e2e5abec4c1a0d96"></a>
### 설명

Window function PERCENTILE_CONT는 연속된 분포 모델을 가정한 역 분포 함수 (inverse distribution function) 이다.

그룹 내에 정렬된 not null value 들에 대해 지정된 백분위수에 해당하는 값을 계산한다.   
계산된 값은 그룹 내에 정렬된 특정 값과 다를 수 있다.

expr은 백분위수로 0과 1 사이의 값이어야 한다.

OVER() 절에는 PARTITION BY 절만 기술할 수 있다.   
PARTITION BY 절을 사용하여 쿼리 결과 집합을 그룹으로 분할한다.

WITHIN GROUP ( ORDER BY &lt;sort specification&gt; )로 그룹 내 레코드를 정렬한다.   
ORDER BY에는 &lt;sort specification&gt;을 하나만 지정할 수 있다.

정렬된 value 중에 NULL은 제외된다.

계산식은 다음과 같다.

```
P : 백분위수 
N : 그룹 내에 정렬된 not null value의 레코드 수
RN = ( 1 + ( P * (N-1) ) )
CRN = CEILING( RN )
FRM = FLOOR( RN )

* if ( CRN = FRN = RN )
     RN의 sort expression value 
* else
     ( CRN - RN ) * FRN의 sort expression value + ( RN - FRN ) * CRN의 sort expression value
```

MEDIAN window 함수는 PERCENTILE_CONT window 함수 중에 특정한 케이스로써 백분위수 0.5를 기본값으로 가진다.

관련 내용은 다음을 참조한다.

- [MEDIAN() OVER](#6e2d4738fd4f25a5)
- [PERCENTILE_DISC() OVER](#52c5c48f4b031ee4)

<a id="b7aa2c33554739a4"></a>
### 사용 예

```
gSQL> 
SELECT item_no, 
       sales,
       PERCENTILE_CONT( 0.5 ) WITHIN GROUP ( ORDER BY sales ) 
                              OVER ( PARTITION BY item_no ) 
       AS PERCENTILE_CONT
  FROM store;

ITEM_NO SALES PERCENTILE_CONT
------- ----- ---------------
    100    50             125
    100    90             125
    100    90             125
    100   100             125
    100   120             125
    100   130             125
    100   150             125
    100   150             125
    100   170             125
    100   200             125
    235    50              90
    235    70              90
    235    90              90
    235   130              90
    235   190              90

15 rows selected.
```

<a id="52c5c48f4b031ee4"></a>
## PERCENTILE_DISC() OVER

<a id="9645e10e18b63f1b"></a>
### 구문

```
PERCENTILE_DISC( expr ) WITHIN GROUP ( ORDER BY <sort specification> ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="318f539c2e0dae1a"></a>
### 설명

Window function PERCENTILE_DISC는 이산 분포 모형을 가정하는 역 분포 함수 (inverse distribution function) 이다.

그룹 내에 정렬된 not null value에 대한 백분위수를 계산한다.   
계산된 백분위수 중 인자로 받은 백분위수보다 크거나 같은 값 중에 가장 작은 값을 결정한다.   
결정된 백분위수에 해당하는 값을 반환한다.

expr은 백분위수로 0과 1 사이의 값이어야 한다.

OVER() 절에는 PARTITION BY 절만 기술할 수 있다.   
PARTITION BY 절을 사용하여 쿼리 결과 집합을 그룹으로 분할한다.

WITHIN GROUP ( ORDER BY &lt;sort specification&gt; )로 그룹 내 레코드를 정렬한다.   
ORDER BY에는 &lt;sort specification&gt;을 하나만 지정할 수 있다.

정렬된 레코드로 sort expression value에 대한 CUME_DIST를 구한다.   
CUME_DIST를 계산할 때 NULL은 제외된다.

expr로 지정된 백분위수 보다 크거나 같은 CUME_DIST 중에 가장 작은 값을 결정한다.   
결정된 CUME_DIST에 해당하는 값을 반환한다.

결과 타입은 sort expression value 타입과 같다.

관련 내용은 [CUME_DIST() OVER](#46ea2ec9c3721407)를 참조한다.

<a id="9ab2126ae3e91f60"></a>
### 사용 예

```
gSQL> 
SELECT item_no, 
       sales,
       CUME_DIST() OVER ( PARTITION BY item_no ORDER BY sales ) 
       AS CUME_DIST,
       PERCENTILE_DISC( 0.5 ) WITHIN GROUP ( ORDER BY sales ) 
                              OVER ( PARTITION BY item_no ) 
       AS PERCENTILE_DISC
  FROM store;

ITEM_NO SALES CUME_DIST PERCENTILE_DISC
------- ----- --------- ---------------
    100    50        .1             120
    100    90        .3             120
    100    90        .3             120
    100   100        .4             120
    100   120        .5             120
    100   130        .6             120
    100   150        .8             120
    100   150        .8             120
    100   170        .9             120
    100   200         1             120
    235    50        .2              90
    235    70        .4              90
    235    90        .6              90
    235   130        .8              90
    235   190         1              90

15 rows selected.
```

<a id="b8d6532aec454831"></a>
## PHYSICAL_LENGTH

<a id="bc45f93c83d3ec3d"></a>
### 구문

```
PHYSICAL_LENGTH( expr )
```

<a id="4556670bcb72c795"></a>
### 설명

PHYSICAL_LENGTH 함수는 expr의 내부 표현 정보 byte 수를 반환한다.

인자 expr에는 모든 데이터 타입이 올 수 있다.

입력 인자가 NULL이면 결과는 0 이다.

<a id="dcb445f4ac1af79f"></a>
### 사용 예

- 입력 인자가 NULL인 경우

```
gSQL> SELECT PHYSICAL_LENGTH( NULL ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

- 다음은 1, 123, 12345의 NUMBER type byte 수를 보여주는 예이다.

```
gSQL> SELECT PHYSICAL_LENGTH( 1 ) AS RESULT FROM DUAL;
RESULT
------
     2
1 row selected.

gSQL> SELECT PHYSICAL_LENGTH( 123 ) AS RESULT FROM DUAL;
RESULT
------
     3
1 row selected.

gSQL> SELECT PHYSICAL_LENGTH( 12345 ) AS RESULT FROM DUAL;
RESULT
------
     4
1 row selected.
```

<a id="ef00931fa68bd858"></a>
## PI

<a id="68b9c6eca84a8b8f"></a>
### 구문

```
PI()
```

<a id="4a416512a97f47bb"></a>
### 설명

PI는 "π" constant를 반환한다.

<a id="571f5e4fe68587d8"></a>
### 사용 예

```
gSQL> SELECT PI() AS RESULT FROM DUAL;
              RESULT
--------------------
3.141592653589793E+0
1 row selected.
```

<a id="8ea4feaa9605d463"></a>
## POSITION

<a id="72e325c657aab229"></a>
### 구문

```
POSITION( str1 IN str2 )
```

<a id="c53421a77f7904f5"></a>
### 설명

POSITION 함수는 str2에서 첫 번째 str1을 찾아 그 위치를 반환하는 함수이다.

str1과 str2에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

str2에서 str1을 찾을 수 없는 경우, 리턴값 0이 반환된다.  
str2에서 str1을 찾은 경우, 1을 시작으로 그 찾은 위치를 반환한다.  
반환되는 위치값은 CHARACTER 단위로 계산된 값이다. (byte 단위가 아님)  
str1 또는 str2가 NULL이면, 반환되는 값도 NULL 이다.

<a id="0535a6ea9fdba025"></a>
### 사용 예

```
gSQL> SELECT POSITION( 'CHAR' IN 'LONG CHAR 2000' ) AS RESULT FROM DUAL;
RESULT
------
     6
1 row selected.
```

<a id="490f1f0ac5cc3ec9"></a>
## POWER

<a id="2ba747f0dca38a77"></a>
### 구문

```
POWER( num1, num2 )
```

<a id="645be6d26e340447"></a>
### 설명

POWER 함수는 num1에 num2를 제곱한 값을 반환한다.

인수 num1과 num2에는 숫자 타입이 올 수 있다.  

num1이 음수이면, num2는 정수여야 한다.  
num1 또는 num2의 값이 NULL이면, 결과값도 NULL이다.

<a id="65c55307799c609d"></a>
### 사용 예

```
gSQL> SELECT POWER( 2, 3 ) AS RESULT FROM DUAL;
RESULT
------
     8
1 row selected.
```

<a id="20f440225faf5f03"></a>
## RADIANS

<a id="b9a0909ef01b80d3"></a>
### 구문

```
RADIANS( degrees )
```

<a id="d9ed0650d05bcf7e"></a>
### 설명

RADIANS 함수는 degrees의 라디안을 반환한다.  

인자 degrees에는 숫자 타입이 올 수 있다.  
인자 degrees가 NULL이면 NULL을 반환한다.

<a id="abd186f301b69783"></a>
### 사용 예

```
gSQL> SELECT RADIANS( 180 ) AS RESULT FROM DUAL;
          RESULT
----------------
3.14159265358979
1 row selected.
```

<a id="ebddf91f17ff9c2d"></a>
## RANDOM

<a id="745518b5ad6cf9c0"></a>
### 구문

```
RANDOM( min, max )
```

<a id="d40b1cba3f8fc991"></a>
### 설명

RANDOM은 min 이상 max 이하의 random 값을 반환한다.  

인자 min, max에는 숫자 타입이 올 수 있다.  
인자 min 또는 max가 NULL이면 NULL을 반환한다.

<a id="e7f5cd8331367634"></a>
### 사용 예

```
gSQL> SELECT RANDOM( 1, 100 ) AS RESULT FROM DUAL;
          RESULT
----------------
34.1870528003201
1 row selected.
```

<a id="f22ac34b9aeabc5b"></a>
## RANK() OVER

<a id="b61aa9b88caac223"></a>
### 구문

```
RANK( ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="5fdaf3d67ad42acb"></a>
### 설명

Window function RANK는 순위를 계산하는 함수이다.

순위는 1부터 시작하는 정수이고, 값이 같은 row는 순위도 동일하다.

window frame은 사용할 수 없다.

<a id="f45e0070dc5b0471"></a>
### 사용 예

```
gSQL> SELECT department_id, salary,
             RANK() OVER ( ORDER BY salary ) AS rank
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY RANK
------------- ------ ----
           60   4200    1
           60   4800    2
           60   4800    2
           60   6000    4
           60   9000    5

5 rows selected.
```

<a id="8b7fe6b51af90fef"></a>
## RATIO_TO_REPORT() OVER

<a id="00b3e6e57b6f27d4"></a>
### 구문

```
RATIO_TO_REPORT ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="5992b784def6dbdb"></a>
### 설명

Window function RATIO_TO_REPORT는 expr 값의 합에서 각 row 값이 차지하는 비율을 계산한다.  
row 값이 NULL인 경우, 결과값으로 NULL을 반환한다.

window 절 내에서 order by는 사용할 수 없다.  
window frame은 사용할 수 없다.

<a id="eca3f4820e311448"></a>
### 사용 예

```
gSQL> SELECT supplier_id, min_price
             , RATIO_TO_REPORT( min_price ) OVER ( PARTITION BY supplier_id ) AS "RATIO"
        FROM product_information
       WHERE supplier_id = 102050;

SUPPLIER_ID MIN_PRICE             RATIO
----------- --------- -----------------
     102050       731  .695528068506185
     102050      null              null
     102050        73 .0694576593720266
     102050       247  .235014272121789
     102050      null              null

5 rows selected.
```

<a id="5a9c61acf90fd5c1"></a>
## REGEXP_COUNT

<a id="f0f18259cc3d3aed"></a>
### 구문

```
REGEXP_COUNT ( source_string, pattern [, position [, match_param ] ] )
```

<a id="1a914a576b50391c"></a>
### 설명

source_string 에서 pattern 이 match 된 횟수를 숫자로 반환한다.  
match 된 문자열이 없으면, 0 을 반환한다.

*source_string*  
검색 대상 문자 표현식으로, CHARACTER, CHARACTER VARING, CHARACTER LONG VARYING 과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있다.

*pattern*  
regular expression (정규 표현식)으로, CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있다.  
512 byte까지 기술할 수 있다.  
pattern 에서 지정할 수 있는 operator는 [Regular Expression Operators](11-sql-elements.md#9085d17c2eb9fcb1) 을 참조한다.

*position*  
source_string 에서 검색 시작 문자 위치를 나타내는 양의 정수이다.  
기본값은 1 이며, source_string 의 첫번째 문자부터 검색한다.

*match_param*  
function 의 기본 matching 수행동작을 변경할 수 있는 문자표현식으로, CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.

match_param 에는 'i', 'c', 'n', 'm', 'x' 를 지정할 수 있으며, 하나 이상 기술할 수 있다.

- **'i':**  대소문자를 구별하지 않는다. ( case-insensitive )
- **'c':**  대소문자를 구별한다. ( case-sensitive )
- **'n':**  Dot operator ( . ) 가 newline character 와의 match 를 허용한다.
- **'m':**  source_string 을 multiple line 으로 처리한다. 각각의 line 에 대해 ^ ( Beginning-of-Line Anchor ) 와 $ ( End-of-Line Anchor ) 를 해석한다.
- **'x':**  pattern 내의 whitespace 를 무시한다.

match_param 에 'i', 'c', 'n', 'm', 'x' 이외의 문자가 오는 경우 에러를 반환한다.  
match_param 에 'ic' 와 같이 모순되는 대소문자 매칭이 나열되었을 경우는 에러를 반환한다.

match_param 을 생략했을 경우,  
&nbsp;• 대소문자를 구별한다. ( case-sensitive )  
&nbsp;• Dot operator(.) 가 newline character 와의 match 를 허용하지 않는다.  
&nbsp;• source_string 을  single line 으로 처리한다.

<a id="d7f1eb14d803713f"></a>
### 사용 예

```
gSQL> 
SELECT reason_desc, REGEXP_COUNT( reason_desc, '\w+' ) AS word_cnt 
  FROM reason;
REASON_DESC                     WORD_CNT
------------------------------- --------
Wrong size                             2
Did not like the color                 5
No service location in my area         6
Found a better price in a store        7
4 rows selected.

### position
gSQL> 
SELECT start_date,
       REGEXP_COUNT( start_date, '-\d{2}', 3 ) AS RESULT
  FROM call_center;
START_DATE  RESULT
----------- ------
1998-01-01       2
1999-JAN-03      1
2000-02-21       2
2001-03-31       2
29-NOV-23        1
5 rows selected.
```

<a id="3a5d8345b833199f"></a>
## REGEXP_INSTR

<a id="4cab4d306d1a8aab"></a>
### 구문

```
REGEXP_INSTR ( source_string, pattern [, position [, occurrence [, return_opt [, match_param [, subexpr ] ] ] ] ] )
```

<a id="c657d13c187d08c9"></a>
### 설명

source_string 에서 pattern 이 match 된 문자열의 시작위치 또는 match 된 문자열의 다음 문자 위치를 숫자로 반환한다.   
match 된 문자열이 없을 경우, 0 을 반환한다.

*source_string*  
검색대상 문자 표현식으로, CHARACTER, CHARACTER VARING, CHARACTER LONG VARYING 과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있다.

*pattern*  
regular expression (정규 표현식)으로, CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있다.  
512 byte까지 기술할 수 있다.  
pattern 에서 지정할 수 있는 operator는 [Regular Expression Operators](11-sql-elements.md#9085d17c2eb9fcb1) 을 참조한다.

*position*  
source_string 에서 검색 시작 문자 위치를 나타내는 양의 정수이다.  
기본값은 1 이며, source_string 의 첫번째 문자부터 검색한다.

**occurrence**  
source_string 에서 pattern 으로 몇 번째 match 되는 것을 검색할지 지정하는 양의 정수이다.  
기본값은 1 이며, source_string 에서 첫번째로 match 되는 것을 검색한다는 의미이다.

**return_opt**  
source_string 에서 pattern 이 match 된 문자열에 관해 어떤 결과를 반환할지를 지정한다.

- return_opt 가 0 이면, 
    - 기본값이며, match 된 문자열의 첫 번째 문자위치를 반환한다.
- return_opt 가 1 이면,
    - 검색된 문자열 다음 문자위치를 반환한다.

*match_param*  
function 의 기본 matching 수행동작을 변경할 수 있는 문자표현식으로, CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.

match_param 에는 'i', 'c', 'n', 'm', 'x' 를 지정할 수 있으며, 하나 이상 기술할 수 있다.

- **'i':**  대소문자를 구별하지 않는다. ( case-insensitive )
- **'c':**  대소문자를 구별한다. ( case-sensitive )
- **'n':**  Dot operator ( . ) 가 newline character 와의 match 를 허용한다.
- **'m':**  source_string 을 multiple line 으로 처리한다. 각각의 line 에 대해 ^ ( Beginning-of-Line Anchor ) 와 $ ( End-of-Line Anchor ) 를 해석한다.
- **'x':**  pattern 내의 whitespace 를 무시한다.

match_param 에 'i', 'c', 'n', 'm', 'x' 이외의 문자가 오는 경우 에러를 반환한다.  
match_param 에 'ic' 와 같이 모순되는 대소문자 매칭이 나열되었을 경우는 에러를 반환한다.

match_param 을 생략했을 경우,  
&nbsp;• 대소문자를 구별한다. ( case-sensitive )  
&nbsp;• Dot operator(.) 가 newline character 와의 match 를 허용하지 않는다.  
&nbsp;• source_string 을  single line 으로 처리한다.

*subexpr*  
pattern 에 기술된 subexpression 을 지칭하는 0 부터 9 까지의 양의 숫자이다.  
subexpr 에 대한 자세한 내용은 [Regular Expression Operators](11-sql-elements.md#9085d17c2eb9fcb1) 에 기술된 내용을 참조한다.

<a id="60c4a502fe7fdc82"></a>
### 사용 예

```
gSQL> 
SELECT reason_desc, 
       REGEXP_INSTR( reason_desc, '[[:space:]]' ) AS RESULT
  FROM reason;
REASON_DESC                     RESULT
------------------------------- ------
Wrong size                           6
Did not like the color               4
No service location in my area       3
Found a better price in a store      6
4 rows selected.

### position, occurrence
gSQL> 
SELECT reason_desc, REGEXP_INSTR( reason_desc, '\w+', 1, 2 ) AS RESULT
  FROM reason;
REASON_DESC                     RESULT
------------------------------- ------
Wrong size                           7
Did not like the color               5
No service location in my area       4
Found a better price in a store      7
4 rows selected.

### return_opt
gSQL> 
SELECT reason_desc, 
       REGEXP_INSTR( reason_desc, '\w+', 1, 2, 0 ) AS RESULT_RETURN_OPT_0,
       REGEXP_INSTR( reason_desc, '\w+', 1, 2, 1 ) AS RESULT_RETURN_OPT_1
  FROM reason;
REASON_DESC                     RESULT_RETURN_OPT_0 RESULT_RETURN_OPT_1
------------------------------- ------------------- -------------------
Wrong size                                        7                  11
Did not like the color                            5                   8
No service location in my area                    4                  11
Found a better price in a store                   7                   8
4 rows selected.

### subexpr
gSQL> 
SELECT REGEXP_INSTR( '123456789', '(12)(3456(789))', 1, 1, 0, 'i', 3 ) 
       AS RESULT
  FROM dual;
RESULT
------
     7
1 row selected.
```

<a id="cbbf5abf3bd78123"></a>
## REGEXP_REPLACE

<a id="68f45922cd0feacb"></a>
### 구문

```
REGEXP_REPLACE ( source_string, pattern [, replace_string [, position [, occurrence [, match_param ] ] ] ]  )
```

<a id="ac1ce4df8859a1a4"></a>
### 설명

source_string 에서 pattern 에 match 되는 문자열을 replace_string 으로 대체한 문자열로 반환한다.

*source_string*  
검색 대상 문자 표현식으로, CHARACTER, CHARACTER VARING, CHARACTER LONG VARYING 과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있다.

*pattern*  
regular expression (정규 표현식)으로, CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있다.  
512 byte까지 기술할 수 있다.  
pattern 에서 지정할 수 있는 operator는 [Regular Expression Operators](11-sql-elements.md#9085d17c2eb9fcb1) 을 참조한다.

*replace_string*  
source_string 에서 pattern 에 match 되는 문자열을 대체할  문자 표현식으로, CHARACTER, CHARACTER VARING, CHARACTER LONG VARYING 과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있다.  
replace_string 에 \n 형식의 backrefercence 를 포함할 수 있으며,  n 은 1 ~ 9 까지의 정수이다.  
replace_string 에 backslash (\) 를 문자로 포함하고 싶다면, escape character backslash (\) 와 함께 기술해야 한다. ( '\\' )

*position*  
source_string 에서 검색 시작 문자 위치를 나타내는 양의 정수이다.  
기본값은 1 이며, source_string 의 첫번째 문자부터 검색한다.

*occurrence*  
source_string 에서 pattern 으로 몇 번째 match 되는 것을 검색할지 지정하는  양의 정수이다.  
0 인 경우, pattern 에 match 되는 모든 문자열을 replace_string 으로 대체한다.  
양의 정수인 n 인 경우, pattern 에 match 되는 n 번째 문자열을 replace_string 으로 대체한다.  
생략된 경우, 기본값은 0 이다.

*match_param*  
function 의 기본 matching 수행동작을 변경할 수 있는 문자표현식으로, CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.

match_param 에는 'i', 'c', 'n', 'm', 'x' 를 지정할 수 있으며, 하나 이상 기술할 수 있다.

- **'i':**  대소문자를 구별하지 않는다. ( case-insensitive )
- **'c':**  대소문자를 구별한다. ( case-sensitive )
- **'n':**  Dot operator ( . ) 가 newline character 와의 match 를 허용한다.
- **'m':**  source_string 을 multiple line 으로 처리한다. 각각의 line 에 대해 ^ ( Beginning-of-Line Anchor ) 와 $ ( End-of-Line Anchor ) 를 해석한다.
- **'x':**  pattern 내의 whitespace 를 무시한다.

match_param 에 'i', 'c', 'n', 'm', 'x' 이외의 문자가 오는 경우 에러를 반환한다.  
match_param 에 'ic' 와 같이 모순되는 대소문자 매칭이 나열되었을 경우는 에러를 반환한다.

match_param 을 생략했을 경우,  
&nbsp;• 대소문자를 구별한다. ( case-sensitive )  
&nbsp;• Dot operator (.) 가 newline character 와의 match 를 허용하지 않는다.  
&nbsp;• source_string 을  single line 으로 처리한다.

<a id="6839de18d215b2dc"></a>
### 사용 예

```
gSQL> 
SELECT reason_desc, 
       REGEXP_REPLACE( reason_desc, '\s', '[ ]' ) AS RESULT
  FROM reason;
REASON_DESC                     RESULT                                     
------------------------------- -------------------------------------------
Wrong size                      Wrong[ ]size                               
Did not like the color          Did[ ]not[ ]like[ ]the[ ]color             
No service location in my area  No[ ]service[ ]location[ ]in[ ]my[ ]area   
Found a better price in a store Found[ ]a[ ]better[ ]price[ ]in[ ]a[ ]store
4 rows selected.


### replace string 에 backreference 포함
gSQL> 
SELECT start_date,
       REGEXP_REPLACE( start_date, 
                       '([[:digit:]]{4})-([[:digit:]]{2})-([[:digit:]]{2})',
                       '\3/\2/\1' ) AS RESULT
  FROM call_center;
START_DATE RESULT    
---------- ----------
1998-01-01 01/01/1998
2000-02-21 21/02/2000
2001-03-31 31/03/2001
3 rows selected.
```

<a id="cefe81f21ed82b68"></a>
## REGEXP_SUBSTR

<a id="560e0e07e1b728d7"></a>
### 구문

```
REGEXP_SUBSTR ( source_string, pattern [, position [, occurrence [, match_param [, subexpr ] ] ] ] )
```

<a id="d81d08e773ae07ba"></a>
### 설명

source_string 에서 pattern 에 match 되는 문자열을 반환한다.

*source_string*  
검색대상 문자 표현식으로, CHARACTER, CHARACTER VARING, CHARACTER LONG VARYING 과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있다.

*pattern*  
regular expression (정규 표현식)으로, CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있다.  
512 byte까지 기술할 수 있다.  
pattern 에서 지정할 수 있는 operator는 [Regular Expression Operators](11-sql-elements.md#9085d17c2eb9fcb1) 을 참조한다.

*position*  
source_string 에서 검색 시작 문자 위치를 나타내는 양의 정수이다.  
기본값은 1 이며, source_string 의 첫번째 문자부터 검색한다.

**occurrence**  
source_string 에서 pattern 으로 몇 번째 match 되는 것을 검색할지 지정하는  양의 정수이다.  
기본값은 1 이며, source_string 에서 첫번째로 match 되는 것을 검색한다는 의미이다.

*match_param*  
function 의 기본 matching 수행동작을 변경할 수 있는 문자표현식으로, CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.

match_param 에는 'i', 'c', 'n', 'm', 'x' 를 지정할 수 있으며, 하나 이상 기술할 수 있다.

- **'i':**  대소문자를 구별하지 않는다. ( case-insensitive )
- **'c':**  대소문자를 구별한다. ( case-sensitive )
- **'n':**  Dot operator ( . ) 가 newline character 와의 match 를 허용한다.
- **'m':**  source_string 을 multiple line 으로 처리한다. 각각의 line 에 대해 ^ ( Beginning-of-Line Anchor ) 와 $ ( End-of-Line Anchor ) 를 해석한다.
- **'x':**  pattern 내의 whitespace 를 무시한다.

match_param 에 'i', 'c', 'n', 'm', 'x' 이외의 문자가 오는 경우 에러를 반환한다.  
match_param 에 'ic' 와 같이 모순되는 대소문자 매칭이 나열되었을 경우는 에러를 반환한다.

match_param 을 생략했을 경우,  
&nbsp;• 대소문자를 구별한다. ( case-sensitive )  
&nbsp;• Dot operator(.) 가 newline character 와의 match 를 허용하지 않는다.  
&nbsp;• source_string 을 single line 으로 처리한다.

*subexpr*  
pattern 에 기술된 subexpression 을 지칭하는 0 부터 9 까지의 양의 숫자이다.  
subexpression 은 ( ) 로 묶인 패턴의 일부이다.  
subexpression 에 대한 자세한 내용은 [Regular Expression Operators](11-sql-elements.md#9085d17c2eb9fcb1) 에 기술된 내용을 참조한다.

<a id="a4a2419aad14e3a1"></a>
### 사용 예

```
gSQL> 
SELECT reason_desc,
       REGEXP_SUBSTR( reason_desc, '[[:alpha:]]+' ) AS RESULT
  FROM reason;
REASON_DESC                     RESULT
------------------------------- ------
Wrong size                      Wrong 
Did not like the color          Did   
No service location in my area  No    
Found a better price in a store Found 
4 rows selected.


### position, occurrence
gSQL> 
SELECT start_date,
       REGEXP_SUBSTR( start_date, '[[:punct:]]\d+', 5, 2 ) AS RESULT
  FROM call_center;
START_DATE RESULT
---------- ------
1998-01-01 -01   
2000-02-21 -21   
2001-03-31 -31   
3 rows selected.

### subexpr
gSQL> 
SELECT start_date,
       REGEXP_SUBSTR( start_date, 
                      '([[:digit:]]{4})-([[:digit:]]{2})-([[:digit:]]{2})',
                      1,
                      1,
                      'i',
                      2 ) AS RESULT
  FROM call_center;
START_DATE RESULT
---------- ------
1998-01-01 01    
2000-02-21 02    
2001-03-31 03    
3 rows selected.
```

<a id="dc239c13bc818a97"></a>
## REGR_AVGX() OVER

<a id="217c6249034367d0"></a>
### 구문

```
REGR_AVGX( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="d8ad1c537b79c3da"></a>
### 설명

Window function REGR_AVGX는 선형회귀함수 (linear regression function) 이다.  
(X, Y) 집합의 least-squares-fit 선형 방정식의 독립변수 expr2의 평균값을 계산한다.

expr1과 expr2는 숫자형 타입을 인자로 받는다.

expr1은 종속변수 ( y ), expr2는 독립변수 ( x )에 해당한다.

expr1이 NULL이거나 expr2가 NULL인 경우에는 대상에서 제외된다.

계산식은 다음과 같다.

```
AVG( expr2 )
```

반환되는 타입은 숫자형 타입이다.

반환되는 값은 계산식에 의한 값이거나 NULL 일 수 있다.   
expr1 또는 expr2가 NULL 이어서 모든 레코드가 대상에서 제외되는 경우에는 NULL이 반환된다.

<a id="44cb97b477de9813"></a>
### 사용 예

```
gSQL> 
SELECT item_no,
       price,
       year,
       REGR_AVGX( price, year ) OVER ( PARTITION BY item_no )
       AS "REGR_AVGX(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_AVGX(price,year)
------- ----- ---- ---------------------
   3758 15000 2000                  2003
   3758 14700 2001                  2003
   3758 15300 2002                  2003
   3758 15200 2003                  2003
   3758 15100 2004                  2003
   3758 15300 2005                  2003
   3758 15350 2006                  2003

7 rows selected.
```

<a id="0dbeeb562321f811"></a>
## REGR_AVGY() OVER

<a id="ca9273c3b4411ab5"></a>
### 구문

```
REGR_AVGY( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="64728265fe60d116"></a>
### 설명

Window function REGR_AVGY는 선형회귀함수 (linear regression function) 이다.  
(X, Y) 집합의 least-squares-fit 선형 방정식의 종속변수 expr1의 평균값을 계산한다.

expr1과 expr2는 숫자형 타입을 인자로 받는다.

expr1은 종속변수 ( y ), expr2는 독립변수 ( x )에 해당한다.

expr1이 NULL이거나 expr2가 NULL인 경우에는 대상에서 제외된다.

계산식은 다음과 같다.

```
AVG( expr1 )
```

반환되는 타입은 숫자형 타입이다.

반환되는 값은 계산식에 의한 값이거나 NULL 일 수 있다.   
expr1 또는 expr2가 NULL 이어서 모든 레코드가 대상에서 제외되는 경우에는 NULL이 반환된다.

<a id="9b0301b047b0387b"></a>
### 사용 예

```
gSQL> 
SELECT item_no,
       price,
       year,
       round( REGR_AVGY( price, year ) OVER ( PARTITION BY item_no ), 5 )
       AS "REGR_AVGY(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_AVGY(price,year)
------- ----- ---- ---------------------
   3758 15000 2000           15135.71429
   3758 14700 2001           15135.71429
   3758 15300 2002           15135.71429
   3758 15200 2003           15135.71429
   3758 15100 2004           15135.71429
   3758 15300 2005           15135.71429
   3758 15350 2006           15135.71429

7 rows selected.
```

<a id="bc3457333732e609"></a>
## REGR_COUNT() OVER

<a id="ae6324e3da197905"></a>
### 구문

```
REGR_COUNT( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="8160dcc88233edaa"></a>
### 설명

Window function REGR_COUNT는 선형회귀함수 (linear regression function) 이다.   
(X, Y) 집합의 least-squares-fit 선형 방정식을 구하는 함수이다.

선형 방정식의 수행 대상이 되는 ( X, Y ) 모두가 not NULL인 쌍의 개수를 반환한다.

expr1과 expr2는 숫자형 타입을 인자로 받는다.

expr1은 종속변수 ( y ), expr2는 독립변수 ( x )에 해당한다.

expr1이 NULL이거나 expr2가 NULL인 경우에는 대상에서 제외된다.

반환되는 타입은 숫자형 타입이다.

expr1과 expr2가 모두 not NULL인 쌍의 수를 반환한다.   
expr1 또는 expr2가 NULL 이어서 모든 레코드가 대상에서 제외되는 경우에는 0을 반환한다.

<a id="8727c2dffd02548b"></a>
### 사용 예

```
gSQL> 
SELECT item_no,
       price,
       year,
       REGR_COUNT( price, year ) OVER ( PARTITION BY item_no )
       AS "REGR_COUNT(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_COUNT(price,year)
------- ----- ---- ----------------------
   3758 15000 2000                      7
   3758 14700 2001                      7
   3758 15300 2002                      7
   3758 15200 2003                      7
   3758 15100 2004                      7
   3758 15300 2005                      7
   3758 15350 2006                      7

7 rows selected.
```

<a id="af3a190d5ff8ba06"></a>
## REGR_INTERCEPT() OVER

<a id="885e0aad6479bfbe"></a>
### 구문

```
REGR_INTERCEPT( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="6130993454f6a81c"></a>
### 설명

Window function REGR_INTERCEPT는 선형회귀함수 (linear regression function) 이다.  
(X, Y) 집합의 least-squares-fit 선형 방정식의 y 절편을 계산한다.

expr1과 expr2는 숫자형 타입을 인자로 받는다.

expr1은 종속변수 ( y ), expr2는 독립변수 ( x )에 해당한다.

expr1이 NULL이거나 expr2가 NULL인 경우에는 대상에서 제외된다.

계산식은 다음과 같다.

```
AVG( expr1 ) - REGR_SLOPE( expr1, expr2 ) * AVG( expr2 )
```

반환되는 타입은 숫자형 타입이다.

반환되는 값은 계산식에 의한 값이거나 NULL 일 수 있다.

다음과 같은 경우에는 NULL이 반환된다.   
• expr1 또는 expr2가 NULL 이어서 모든 레코드가 대상에서 제외되는 경우  
• REGR_SLOPE의 결과가 null인 경우

<a id="ac0250243e2918b2"></a>
### 사용 예

```
gSQL> 
SELECT item_no,
       price,
       year,
       REGR_INTERCEPT( price, year ) OVER ( PARTITION BY item_no )
       AS "REGR_INTERCEPT(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_INTERCEPT(price,year)
------- ----- ---- --------------------------
   3758 15000 2000                  -131512.5
   3758 14700 2001                  -131512.5
   3758 15300 2002                  -131512.5
   3758 15200 2003                  -131512.5
   3758 15100 2004                  -131512.5
   3758 15300 2005                  -131512.5
   3758 15350 2006                  -131512.5

7 rows selected.
```

<a id="f2419709daefb084"></a>
## REGR_R2() OVER

<a id="c1b4550d6409f081"></a>
### 구문

```
REGR_R2( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="a72a4d36bffacdfc"></a>
### 설명

Window function REGR_R2는 선형회귀함수 (linear regression function) 이다.   
(X, Y) 집합의 least-squares-fit 선형 방정식의 결정계수 (R-squared 또는 적합도)를 계산한다.

expr1과 expr2는 숫자형 타입을 인자로 받는다.

expr1은 종속변수 ( y ), expr2는 독립변수 ( x )에 해당한다.

expr1이 NULL이거나 expr2가 NULL인 경우에는 대상에서 제외된다.

계산식은 다음과 같다.

```
VAR_POP( expr2 ) = 0 이면,  NULL 
VAR_POP( expr1 ) = 0  이고, VAR_POP( expr2 ) != 0  이면, 1
VAR_POP( expr1 ) > 0 이고, VAR_POP( expr2 ) != 0 이면, POWER( CORR( expr1, expr2), 2 )
```

반환되는 타입은 숫자형 타입이다.

반환되는 값은 계산식에 의한 값이거나 NULL 일 수 있다.

다음과 같은 경우에는 NULL이 반환된다.   
• expr1 또는 expr2가 NULL 이어서 모든 레코드가 대상에서 제외되는 경우  
• VAR_POP (expr2) 의 결과가 0 인 경우

<a id="4ca872e288ceae07"></a>
### 사용 예

```
gSQL> 
SELECT item_no,
       price,
       year,
       round( REGR_R2( price, year ) OVER ( PARTITION BY item_no ), 10 )
       AS "REGR_R2(price,year)"
  FROM store
 WHERE item_no = 3758;

ITEM_NO PRICE YEAR REGR_R2(price,year)
------- ----- ---- -------------------
   3758 15000 2000         .4786446469
   3758 14700 2001         .4786446469
   3758 15300 2002         .4786446469
   3758 15200 2003         .4786446469
   3758 15100 2004         .4786446469
   3758 15300 2005         .4786446469
   3758 15350 2006         .4786446469

7 rows selected.
```

<a id="55b6ea15f8a2d849"></a>
## REGR_SLOPE() OVER

<a id="ea666c46da173773"></a>
### 구문

```
REGR_SLOPE( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="6f22805233851c08"></a>
### 설명

Window function REGR_SLOPE는 선형회귀함수 (linear regression function) 이다.   
(X, Y) 집합의 least-squares-fit 선형 방정식의 기울기를 계산한다.

expr1과 expr2는 숫자형 타입을 인자로 받는다.

expr1은 종속변수 ( y ), expr2는 독립변수 ( x )에 해당한다.

expr1이 NULL이거나 expr2가 NULL인 경우에는 대상에서 제외된다.

계산식은 다음과 같다.

```
COVAR_POP(expr1, expr2) / VAR_POP(expr2)
```

반환되는 타입은 숫자형 타입이다.

반환되는 값은 계산식에 의한 값이거나 NULL 일 수 있다.

다음과 같은 경우에는 NULL이 반환된다.   
• expr1 또는 expr2가 NULL 이어서 모든 레코드가 대상에서 제외되는 경우   
• VAR_POP의 결과가 0 인 경우

<a id="63c619af7286f4f5"></a>
### 사용 예

```
gSQL> 
SELECT item_no,
       price,
       year,
       round( REGR_SLOPE( price, year ) OVER ( PARTITION BY item_no ), 10 )
       AS "REGR_SLOPE(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_SLOPE(price,year)
------- ----- ---- ----------------------
   3758 15000 2000          73.2142857143
   3758 14700 2001          73.2142857143
   3758 15300 2002          73.2142857143
   3758 15200 2003          73.2142857143
   3758 15100 2004          73.2142857143
   3758 15300 2005          73.2142857143
   3758 15350 2006          73.2142857143

7 rows selected.
```

<a id="0ed25bd5b207eb09"></a>
## REGR_SXX() OVER

<a id="2a7032d37a9b95f2"></a>
### 구문

```
REGR_SXX( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="eb160f5994068e4f"></a>
### 설명

Window function REGR_SXX는 선형회귀함수 (linear regression function) 이다.    
(X, Y) 집합의 least-squares-fit 선형 방정식의 진단 통계를 계산하는데 사용되는 보조 함수이다.

expr1과 expr2는 숫자형 타입을 인자로 받는다.

expr1은 종속변수 ( y ), expr2는 독립변수 ( x )에 해당한다.

expr1이 NULL이거나 expr2가 NULL인 경우에는 대상에서 제외된다.

계산식은 다음과 같다.

```
REGR_COUNT( expr1, expr2 ) * VAR_POP( expr2 )
```

반환되는 타입은 숫자형 타입이다.

반환되는 값은 계산식에 의한 값이거나 NULL 일 수 있다.   
expr1 또는 expr2가 NULL 이어서 모든 레코드가 대상에서 제외되는 경우에는 NULL이 반환된다.

<a id="7235ae7a686f4ffc"></a>
### 사용 예

```
gSQL> 
SELECT item_no,
       price,
       year,
       REGR_SXX( price, year ) OVER ( PARTITION BY item_no )
       AS "REGR_SXX(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_SXX(price,year)
------- ----- ---- --------------------
   3758 15000 2000                   28
   3758 14700 2001                   28
   3758 15300 2002                   28
   3758 15200 2003                   28
   3758 15100 2004                   28
   3758 15300 2005                   28
   3758 15350 2006                   28

7 rows selected.
```

<a id="467c0e80a94fbf4e"></a>
## REGR_SXY() OVER

<a id="2df06dccc44ecb30"></a>
### 구문

```
REGR_SXY( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="dd199b72bc7ab6f3"></a>
### 설명

Window function REGR_SXY는 선형회귀함수 (linear regression function) 이다.   
(X, Y) 집합의 least-squares-fit 선형 방정식의 진단 통계를 계산하는데 사용되는 보조 함수이다.

expr1과 expr2는 숫자형 타입을 인자로 받는다.

expr1은 종속변수 ( y ), expr2는 독립변수 ( x )에 해당한다.

expr1이 NULL이거나 expr2가 NULL인 경우에는 대상에서 제외된다.

계산식은 다음과 같다.

```
REGR_COUNT( expr1, expr2 ) * COVAR_POP( expr1, expr2 )
```

반환되는 타입은 숫자형 타입이다.

반환되는 값은 계산식에 의한 값이거나 NULL 일 수 있다.   
expr1 또는 expr2가 NULL 이어서 모든 레코드가 대상에서 제외되는 경우에는 NULL이 반환된다.

<a id="f9861de70d16cb51"></a>
### 사용 예

```
gSQL> 
SELECT item_no,
       price,
       year,
       REGR_SXY( price, year ) OVER ( PARTITION BY item_no )
       AS "REGR_SXY(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_SXY(price,year)
------- ----- ---- --------------------
   3758 15000 2000                 2050
   3758 14700 2001                 2050
   3758 15300 2002                 2050
   3758 15200 2003                 2050
   3758 15100 2004                 2050
   3758 15300 2005                 2050
   3758 15350 2006                 2050

7 rows selected.
```

<a id="ab7060c3d6b62f26"></a>
## REGR_SYY() OVER

<a id="69cbef4bfec71f3b"></a>
### 구문

```
REGR_SYY( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="e00de9a3778b5f24"></a>
### 설명

Window function REGR_SYY는 선형회귀함수 (linear regression function) 이다.   
(X, Y) 집합의 least-squares-fit 선형 방정식의 진단 통계를 계산하는데 사용되는 보조 함수이다.

expr1과 expr2는 숫자형 타입을 인자로 받는다.

expr1은 종속변수 ( y ), expr2는 독립변수 ( x )에 해당한다.

expr1이 NULL이거나 expr2가 NULL인 경우에는 대상에서 제외된다.

계산식은 다음과 같다.

```
REGR_COUNT( expr1, expr2 ) * VAR_POP( expr1 )
```

반환되는 타입은 숫자형 타입이다.

반환되는 값은 계산식에 의한 값이거나 NULL 일 수 있다.   
expr1 또는 expr2가 NULL 이어서 모든 레코드가 대상에서 제외되는 경우에는 NULL이 반환된다.

<a id="b0b19ef61cd16f41"></a>
### 사용 예

```
gSQL> 
SELECT item_no,
       price,
       year,
       round( REGR_SYY( price, year ) OVER ( PARTITION BY item_no ), 4 )
       AS "REGR_SYY(price,year)"
  FROM store;

ITEM_NO PRICE YEAR REGR_SYY(price,year)
------- ----- ---- --------------------
   3758 15000 2000          313571.4286
   3758 14700 2001          313571.4286
   3758 15300 2002          313571.4286
   3758 15200 2003          313571.4286
   3758 15100 2004          313571.4286
   3758 15300 2005          313571.4286
   3758 15350 2006          313571.4286

7 rows selected.
```

<a id="1f821bcbb4581842"></a>
## REPEAT

<a id="edbce982252084bb"></a>
### 구문

```
REPEAT( str, num )
```

<a id="4cad472daba39d6e"></a>
### 설명

REPEAT 함수는 num에 지정된 수만큼 str을 반복한 string을 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARCATER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

인자 num에는 숫자 타입이 올 수 있다.

str 또는 num 중의 하나라도 NULL이면, 결과값도 NULL이다.  
num의 값이 0 또는 음수인 경우에도 결과값은 NULL이다.

결과 타입은 다음 표와 같다.

**REPEAT의 결과 타입**

<a id="877887211fa665bb"></a>
| str 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="51c000d5b2ed87eb"></a>
### 사용 예

```
gSQL> SELECT REPEAT( 'ab', 3 ) AS RESULT FROM DUAL;
RESULT
------
ababab
1 row selected.
```

<a id="7cbb3ba7fc25e00f"></a>
## REPLACE

<a id="ba2d1861706674a2"></a>
### 구문

```
REPLACE( str, from, to )
```

<a id="765d1405a7e381df"></a>
### 설명

REPLACE는 str string 내의 모든 from string을 to string으로 치환하여 반환한다.

인자 str, from, to에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str 값이 NULL인 경우, 결과값은 NULL이다.  
from 값이 NULL인 경우, str 값을 변환하지 않고 반환한다.  
to 값이 생략되었거나 NULL인 경우, str에서 from을 제거한 값이 반환된다.

결과 타입은 다음 표와 같다.

**REPLACE의 결과 타입**

<a id="0e8ab250ffd7bfaa"></a>
| str 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="ec0489bd38fe5523"></a>
### 사용 예

```
gSQL> SELECT REPLACE( 'HI GLIESE', 'HI', 'HELLO' ) AS RESULT FROM DUAL;
RESULT      
------------
HELLO GLIESE
1 row selected.
```

<a id="c6f1ca3690636f48"></a>
## REVERSE

<a id="99404a1e85e2496d"></a>
### 구문

```
REVERSE( str )
```

<a id="691fb3fdd2e21749"></a>
### 설명

REVERSE는 str의 문자를 역순으로 반환한다.

인자로는 character string 타입 또는 binary string 타입으로 변환될 수 있는 타입이 올 수 있으며  
character string 타입은 해당 문자 단위로, binary string 타입은 byte 단위로 수행된다.

str이 NULL일 경우 NULL을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**REVERSE 인자와 결과 타입**

<a id="1f370df0ae304b7f"></a>
| str | 결과 타입 |
| --- | --- |
| CHAR | CHAR |
| VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY | BINARY |
| VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="366957f20ab75117"></a>
### 사용 예

```
gSQL> SELECT REVERSE( 'GOLDILOCKS' ) AS RESULT FROM DUAL;

RESULT      
----------
SKCOLIDLOG

1 row selected.

gSQL> SELECT REVERSE( '선재소프트 2018' ) AS RESULT FROM DUAL;

RESULT         
---------------
8102 트프소재선

1 row selected.
```

<a id="d84fc397d10c7016"></a>
## ROUND( number )

<a id="0146f23b93a0f9ae"></a>
### 구문

```
ROUND( num [, scale ] )
```

<a id="5bdcd45939bf70b9"></a>
### 설명

ROUND는 scale을 기준으로 num을 반올림한 값을 반환한다.

인자 num, scale에는 숫자 타입이 올 수 있다.

scale이 생략된 경우, scale은 0이 되어 ROUND( num, 0 )와 같이 수행된다.  
scale이 양수인 경우 소수점 오른쪽 자리수를 기준으로 반올림되고, scale이 음수인 경우 소수점 왼쪽 자리수를 기준으로 반올림된다.  

인자 num 또는 scale이 NULL이면 NULL을 반환한다.

<a id="0ef8c3fd6552c24c"></a>
### 사용 예

```
gSQL> SELECT ROUND( 152.4282, 2 ) AS RESULT FROM DUAL;
RESULT
------
152.43
1 row selected.

gSQL> SELECT ROUND( 152.4282, -2 ) AS RESULT FROM DUAL;
RESULT
------
   200
1 row selected.
```

<a id="21fbf0ba5ae52234"></a>
## ROUND( date )

<a id="18c01b4327fa1443"></a>
### 구문

```
ROUND( date [ , fmt ] )
```

<a id="e0d59efb2a7882e0"></a>
### 설명

ROUND( date ) 함수는 date를 지정된 fmt 단위로 반올림한 값을 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
인자 date 또는 fmt가 NULL이면 NULL을 반환한다.  

결과 타입은 인자로 받은 date 타입과 관계없이 항상 DATE 타입이다.

fmt가 생략되었을 경우의 기본값은 DAY 이며, 사용 가능한 형식문자열은 다음 표와 같다.

**fmt에 사용가능한 형식문자열**

<a id="0bd5b0aed1c88fdd"></a>
| 문자열 | 설명 |
| --- | --- |
| CC, SCC | 51년부터 반올림하여 네자리 연도로 표현한다. (예: XX01) |
| YYYY, YEAR, SYYYY, SYEAR, YYY, YY, Y | 7월 1일부터 반올림한다. |
| IYYY, IYY, IY, I | ISO 8601 표준에 정의된 calendar week를 수용하는 연도로써 7월 1일부터 반올림한다. |
| Q | 분기의 두 번째 달의 16일부터 반올림한다. |
| MONTH, MON, MM, RM | 16일부터 반올림한다. |
| WW | 연도의 1월 1일부터 한 주가 시작되며 해당 WEEK의 수요일 오후 12시부터 반올림한다. |
| IW | ISO 8601 표준에 정의된 calendar week (1 ~ 52주 또는 1 ~ 53주)로써 목요일 오후 12시부터 반올림한다. |
| W | 월의 1일을 한 주로 시작해서 해당 WEEK의 수요일 오후 12시부터 반올림한다. |
| DDD, DD, J | 오후 12시부터 반올림한다. |
| DAY, DY, D | WEEK의 수요일 오후 12시부터 반올림한다. |
| HH, HH12, HH24 | 30 분부터 반올림한다. |
| MI | 30 초부터 반올림한다. |

<a id="071959f05ec55e0e"></a>
### 사용 예

```
gSQL> SELECT 
      ROUND( TO_DATE( '2051-07-16', 'YYYY-MM-DD' ), 'CC' ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2101-01-01
1 row selected.

gSQL> SELECT 
      ROUND( TO_DATE( '2051-07-16', 'YYYY-MM-DD' ), 'YYYY' ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2052-01-01
1 row selected.

gSQL> SELECT 
      ROUND( TO_DATE( '2051-07-16', 'YYYY-MM-DD' ), 'MONTH' ) AS   RESULT 
      FROM DUAL;
RESULT    
----------
2051-08-01
1 row selected.

gSQL> SELECT 
      ROUND( TO_TIMESTAMP( '2001-05-05 15:22:33.999999', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ) ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2001-05-06
1 row selected.
```

<a id="09243273d0b502c2"></a>
## ROW_NUMBER() OVER

<a id="e5a92780d5662cd7"></a>
### 구문

```
ROW_NUMBER( ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="70299650f6e173f7"></a>
### 설명

Window function ROW_NUMBER는 각 row에 고유 번호를 할당한다.  
고유 번호는 1부터 시작하는 연속적인 정수이다.

window frame은 사용할 수 없다.

<a id="039befd31994a292"></a>
### 사용 예

```
gSQL> SELECT department_id, salary,
             ROW_NUMBER() OVER ( ORDER BY salary ) AS row_num
      FROM employees
      WHERE department_id = 60;

DEPARTMENT_ID SALARY ROW_NUM
------------- ------ -------
           60   4200       1
           60   4800       2
           60   4800       3
           60   6000       4
           60   9000       5

5 rows selected.
```

<a id="6bb3f3b9e9c6f50e"></a>
## ROWID_GRID_BLOCK_ID

<a id="bdb944005d6679e2"></a>
### 구문

```
ROWID_GRID_BLOCK_ID( rowid )
```

<a id="37acf17e17c69e23"></a>
### 설명

GRID block ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="310ffb3b3b932cee"></a>
### 사용 예

```
gSQL> SELECT C1, ROWID_GRID_BLOCK_ID( ROWID ) FROM T1;
C1 ROWID_GRID_BLOCK_ID( ROWID )
-- ----------------------------
 1                           52
 2                           52
 3                           52

3 rows selected.
```

<a id="cd8883c9cf87b7f3"></a>
## ROWID_GRID_BLOCK_SEQ

<a id="0be8c83ab01d25ae"></a>
### 구문

```
ROWID_GRID_BLOCK_SEQ( rowid )
```

<a id="5b7e199f58fd0a33"></a>
### 설명

GRID block sequence를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="2f66c2129b511cb8"></a>
### 사용 예

```
gSQL> SELECT C1, ROWID_GRID_BLOCK_SEQ( ROWID ) FROM T1;
C1 ROWID_GRID_BLOCK_SEQ( ROWID )
-- -----------------------------
 1                        747465
 2                        747466
 3                        747467

3 rows selected.
```

<a id="7acaab2066b99338"></a>
## ROWID_MEMBER_ID

<a id="49ab6c462e6f616b"></a>
### 구문

```
ROWID_MEMBER_ID( rowid )
```

<a id="bd849a5b5add46db"></a>
### 설명

Member ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="fa84b1ede7b7f8b3"></a>
### 사용 예

```
gSQL> SELECT C1, ROWID_MEMBER_ID( ROWID ) FROM T1;
C1 ROWID_MEMBER_ID( ROWID )
-- ------------------------
 1                        1
 2                        1
 3                        1

3 rows selected.
```

<a id="4ee48c1d18ede954"></a>
## ROWID_OBJECT_ID

<a id="fd79a82acfb202e5"></a>
### 구문

```
ROWID_OBJECT_ID( rowid )
```

<a id="93a2e5497d1e0f2f"></a>
### 설명

Object ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="5f2ded4f14c31dc1"></a>
### 사용 예

```
gSQL> SELECT ROWID_OBJECT_ID( t1.ROWID ) FROM t1;
ROWID_OBJECT_ID( T1.ROWID )
---------------------------
                      22012
                      22012
                      22012
                      22012
4 rows selected.
```

<a id="6cc0447e41b24c0b"></a>
## ROWID_PAGE_ID

<a id="b773b98e59870a94"></a>
### 구문

```
ROWID_PAGE_ID( rowid )
```

<a id="543df117756875fe"></a>
### 설명

Page ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="97731c065b4ce4cb"></a>
### 사용 예

```
gSQL> SELECT ROWID_PAGE_ID( t1.ROWID ) FROM t1;
ROWID_PAGE_ID( T1.ROWID )
-------------------------
                     8227
                     8227
                     8227
                     8227
4 rows selected.
```

<a id="5906bacda936fa19"></a>
## ROWID_ROW_NUMBER

<a id="b46583bdb4c6479e"></a>
### 구문

```
ROWID_ROW_NUMBER( rowid )
```

<a id="6db119712f5b0cd9"></a>
### 설명

Row number를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="26ef859ae2a1fe35"></a>
### 사용 예

```
gSQL> SELECT ROWID_ROW_NUMBER( t1.ROWID ) FROM t1;
ROWID_ROW_NUMBER( T1.ROWID )
----------------------------
                           0
                           1
                           2
                           3
4 rows selected.
```

<a id="140ec83744716830"></a>
## ROWID_SHARD_ID

<a id="700f8805ba63b3a6"></a>
### 구문

```
ROWID_SHARD_ID( rowid )
```

<a id="1b1aeb1cacc396ed"></a>
### 설명

Shard ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="e6cbfc5979384d94"></a>
### 사용 예

```
gSQL> SELECT C1, ROWID_SHARD_ID( ROWID ) FROM T1;
C1 ROWID_SHARD_ID( ROWID )
-- -----------------------
 1                       0
 2                       1
 3                       2

3 rows selected.
```

<a id="275b71b4fbb14ee1"></a>
## ROWID_TABLESPACE_ID

<a id="585e5f32c727006a"></a>
### 구문

```
ROWID_TABLESPACE_ID( rowid )
```

<a id="379db2b5faa1c7e6"></a>
### 설명

Tablespace ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="ce2122c1bf2aba45"></a>
### 사용 예

```
gSQL> SELECT ROWID_TABLESPACE_ID( t1.ROWID ) FROM t1;
ROWID_TABLESPACE_ID( T1.ROWID )
-------------------------------
                              2
                              2
                              2
                              2
4 rows selected.
```

<a id="3cb51993ddf55ab0"></a>
## ROWNUM

<a id="30c2ff1f1e7b4e39"></a>
### 구문

```
ROWNUM
```

<a id="230bd7e5a5251835"></a>
### 설명

WHERE 조건을 만족하는 row에 대하여 1부터 순차적으로 번호를 부여한다.

Oracle과의 호환성을 위해 WHERE 절에 ROWNUM 사용을 허용한다.

그러나 질의 결과의 개수를 제한하려면 다음과 같이 SQL 표준의 [offset limit clause](20-sql-references-h-z.md#4685bb3308f27adc)를 사용할 것을 권장한다.

- (비표준) ROWNUM을 이용하여 결과 개수 기술

```
gSQL> SELECT * FROM t1 WHERE ROWNUM <= 3;

C1
--
A 
B 
C 

3 rows selected.
```

- (SQL 표준) FETCH 구문을 이용하여 결과 개수 기술

```
gSQL> SELECT * FROM t1 FETCH 3;

C1
--
A 
B 
C 

3 rows selected.
```

질의 결과의 일부 범위를 제한하고자 할 때도 다음과 같이 OFFSET, FETCH 구문을 사용할 것을 권장한다.

- (비표준) ROWNUM을 이용하여 결과 개수의 범위 기술

```
gSQL> SELECT c1 
        FROM ( SELECT ROWNUM rn, c1 
                 FROM t1 )
        WHERE rn BETWEEN 2 AND 3;

C1
--
B 
C 

2 rows selected.
```

- (SQL 표준) OFFSET, FETCH 구문을 이용하여 결과 개수의 범위 기술

```
gSQL> SELECT c1 FROM t1 OFFSET 1 FETCH 2;

C1
--
B 
C 

2 rows selected.
```

결과 개수 제한 이외의 용도로 ROWNUM을 WHERE 절에 사용하는 것은 권장하지 않는다.

다음 예와 같이 모호한 조건 (WHERE c1 < ROWNUM + 3)을 사용할 경우, 실행 방법에 따라 동일한 질의에 대한 결과가 달라질 수 있다.

- 데이터 생성

```
CREATE TABLE t1 ( c1 INTEGER );
CREATE INDEX t1_idx ON t1(c1);
INSERT INTO t1 VALUES (1);
INSERT INTO t1 VALUES (2);
INSERT INTO t1 VALUES (3);
INSERT INTO t1 VALUES (4);
INSERT INTO t1 VALUES (5);
COMMIT;
```

- Oracle의 경우

```
SQL> SELECT ROWNUM, c1 FROM t1 WHERE c1 < ROWNUM + 3;

    ROWNUM	   C1
---------- ----------
	 1	    1
	 2	    2

SQL> DROP INDEX t1_idx;
```

    - 인덱스가 삭제되었다.

```
SQL> SELECT ROWNUM, c1 FROM t1 WHERE c1 < ROWNUM + 3;

    ROWNUM	   C1
---------- ----------
	 1	    1
	 2	    2
	 3	    3
	 4	    4
	 5	    5
```

- GOLDILOCKS의 경우

```
gSQL> SELECT ROWNUM, c1 FROM t1 WHERE c1 < ROWNUM + 3;

ROWNUM C1
------ --
     1  1
     2  2
     3  3
     4  4
     5  5

5 rows selected.

gSQL> DROP INDEX t1_idx;

Index dropped.

gSQL> SELECT ROWNUM, c1 FROM t1 WHERE c1 < ROWNUM + 3;

ROWNUM C1
------ --
     1  1
     2  2
     3  3
     4  4
     5  5

5 rows selected.
```

<a id="015aae951dbf8538"></a>
### 사용 예

```
gSQL> SELECT ROWNUM, c1 FROM t1;

ROWNUM C1
------ --
     1 A 
     2 B 
     3 C 
     4 D 
     5 E 

5 rows selected.
```

<a id="103a6121afa30d89"></a>
## RPAD

<a id="45c611522c1a9f8b"></a>
### 구문

```
RPAD( str, length, [, fill] )
```

<a id="dbdbe7e307aa96e8"></a>
### 설명

RPAD 함수는 string의 길이가 length가 될 때까지 str의 오른쪽에 문자열 fill을 추가한 값을 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

인자 length에는 숫자 타입이 올 수 있다.

length는 문자의 개수를 의미하며 최대 범위는 결과 타입의 최대 PRECISION이다.  
fill이 생략된 경우, 공백 문자가 추가된다.  
str이 length보다 길이가 긴 경우에는 str을 length만큼 잘라서 반환한다.  
str, length, fill 중 하나라도 NULL이면 결과값도 NULL이며, length가 0 또는 음수인 경우에도 결과값은 NULL이다.

결과 타입은 다음 표와 같다.

**RPAD의 결과 타입**

<a id="46c0805cac3e74cb"></a>
| 인자 str의 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="da083857bc44d4d9"></a>
### 사용 예

```
gSQL> SELECT RPAD('AA', 5) AS RESULT1,
             RPAD('AA', 5, 'X') AS RESULT2,
             RPAD('AA', 1) AS RESULT3
      FROM DUAL; 
RESULT1 RESULT2 RESULT3
------- ------- -------
AA      AAXXX   A      
1 row selected.
```

<a id="6209e4959fd4b648"></a>
## RTRIM

<a id="5dedbfd5f990f615"></a>
### 구문

```
RTRIM( trim_source [, trim_character ] )
```

<a id="29a18654621cf1d6"></a>
### 설명

RTRIM 함수는 trim_source에서 trim_character를 오른쪽 방향에서 비교하여 일치하는 문자가 없을 때까지 제거한 결과를 반환한다.

인자 trim_character와 trim_source에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

trim_character, trim_source 중 하나라도 NULL이면, 결과값은 NULL이다.  
trim_character가 생략된 경우에는 기본적으로 single blank space (' ')가 지정된다.

결과 타입은 다음과 같다.

**RTRIM의 결과 타입**

<a id="951b6fbc6e00af2f"></a>
| trim_source, trim_character 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="a95c4f84b5c02bff"></a>
### 사용 예

```
gSQL> SELECT RTRIM('      rtrim      ') AS RESULT1,
             RTRIM('______rtrim______','_') AS RESULT2
      FROM DUAL;
RESULT1     RESULT2    
----------- -----------
      rtrim ______rtrim
1 row selected.
```

<a id="f57af3ac6abb0112"></a>
## SESSION_ID

<a id="9a78a1848042f5f4"></a>
### 구문

```
SESSION_ID()
```

<a id="c23561729fb14a7b"></a>
### 설명

현재 session의 ID를 얻는다.

<a id="ce2d9fdf4ba11d22"></a>
### 사용 예

```
gSQL> SELECT SESSION_ID() FROM dual;

SESSION_ID()
------------
           4

1 row selected.
```

<a id="fe0cf26aca2f050a"></a>
## SESSION_SERIAL

<a id="8bac2684dab5131e"></a>
### 구문

```
SESSION_SERIAL()
```

<a id="fb0e2a529b230cc1"></a>
### 설명

현재 session의 serial 번호를 얻는다.

<a id="97ac87eeb087d574"></a>
### 사용 예

```
gSQL> SELECT SESSION_SERIAL() FROM dual;

SESSION_SERIAL()
----------------
              16

1 row selected.
```

<a id="e576d54163cde37e"></a>
## SESSION_USER

<a id="6740854903f59294"></a>
### 구문

```
SESSION_USER[()]
```

<a id="16ce0e3ac7c5fbe6"></a>
### 설명

세션 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다. 
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다. 
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다. 
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="03fda7d12f9ef20f"></a>
### 사용 예

```
% gsql sys gliese
gSQL>  SET SESSION AUTHORIZATION test;

Session set.

gSQL> SELECT LOGON_USER() AS result1, SESSION_USER() AS result2 FROM DUAL;

RESULT1 RESULT2
------- -------
SYS     TEST   

1 row selected.
```

<a id="3c731030f2080f50"></a>
## SESSIONTIMEZONE

<a id="2a4d97e6d0cf92d4"></a>
### 구문

```
SESSIONTIMEZONE()
```

<a id="f5e3be46620dd5fe"></a>
### 설명

SESSIONTIMEZONE은 현재 session의 time zone을 반환한다.  
반환되는 값은 '[+|-]TZH:TZM' format 형식의 문자이다.  
반환되는 타입은 varchar 이다.

<a id="84c6b4412840803b"></a>
### 사용 예

현재 session의 time zone을 확인한다.

```
gSQL> SELECT SESSIONTIMEZONE() FROM dual;

SESSIONTIMEZONE()
-----------------
+09:00           

1 row selected.
```

현재 session의 time zone을 변경하면 변경된 time zone 값을 반환한다.

```
gSQL> SET TIME ZONE '-05:00';

Session set.

gSQL> SELECT SESSIONTIMEZONE() FROM dual;

SESSIONTIMEZONE()
-----------------
-05:00           

1 row selected.
```

<a id="3c3d8eed1feaa1d9"></a>
## SHARD_GROUP_ID

<a id="0a8f37c6601d2afd"></a>
### 구문

```
SHARD_GROUP_ID( table_name, shard_key_value [, ... ] )
```

<a id="b7048162a9ebd56d"></a>
### 설명

SHARD_GROUP_ID 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard를 관리하는 group ID를 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 NATIVE_BIGINT이다.

> Cluster system에서 유효한 정보이다.

<a id="a5d18d6934a7673b"></a>
### 사용 예

```
gSQL> SELECT T1.C1, SHARD_GROUP_ID( T1, T1.C1 ) FROM T1;
C1 SHARD_GROUP_ID( T1, T1.C1 )
-- ---------------------------
A                            1
B                            2
C                            3

3 rows selected.


gSQL> SELECT SHARD_GROUP_ID( T1, 'B' ) FROM DUAL;
SHARD_GROUP_ID( T1, 'B' )
-------------------------
                        2

1 row selected.
```

<a id="44032d54399af461"></a>
## SHARD_GROUP_NAME

<a id="961e9b426d6f644a"></a>
### 구문

```
SHARD_GROUP_NAME( table_name, shard_key_value [, ... ] )
```

<a id="61a2787bbf4d36f7"></a>
### 설명

SHARD_GROUP_NAME 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard를 관리하는 group NAME을 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 VARCHAR이다.

> Cluster system에서 유효한 정보이다.

<a id="f7667b76200ae3c6"></a>
### 사용 예

```
gSQL> SELECT T1.C1, SHARD_GROUP_NAME( T1, T1.C1 ) FROM T1;

C1 SHARD_GROUP_NAME( T1, T1.C1 )
-- -----------------------------
A  G1                           
B  G2                           
C  G3                           

3 rows selected.

gSQL> SELECT SHARD_GROUP_NAME( T1, 'B' ) FROM DUAL;

SHARD_GROUP_NAME( T1, 'B' )
---------------------------
G2                         

1 row selected.
```

<a id="f9b439ced7819257"></a>
## SHARD_ID

<a id="dde99506457202a3"></a>
### 구문

```
SHARD_ID( table_name, shard_key_value [, ... ] )
```

<a id="b68614a925a40574"></a>
### 설명

SHARD_ID 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard에 대한 ID를 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 NATIVE_BIGINT이다.

> Cluster system에서 유효한 정보이다.

<a id="c312360d1d2171eb"></a>
### 사용 예

```
gSQL> SELECT T1.C1, SHARD_ID( T1, T1.C1 ) FROM T1;
C1 SHARD_ID( T1, T1.C1 )
-- ---------------------
A                      0
B                      1
C                      2

3 rows selected.


gSQL> SELECT SHARD_ID( T1, 'B' ) FROM DUAL;
SHARD_ID( T1, 'B' )
-------------------
                  1

1 row selected.
```

<a id="e30d0114d68cb106"></a>
## SHARD_NAME

<a id="888bfa0d8ff25b18"></a>
### 구문

```
SHARD_NAME( table_name, shard_key_value [, ... ] )
```

<a id="269bca3cb4276fbd"></a>
### 설명

SHARD_NAME 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard에 대한 NAME을 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 VARCHAR이다.

> Cluster system에서 유효한 정보이다.

<a id="29cbf333929ce0b2"></a>
### 사용 예

```
gSQL> SELECT T1.C1, SHARD_NAME( T1, T1.C1 ) FROM T1;

C1 SHARD_NAME( T1, T1.C1 )
-- -----------------------
A  S1                     
B  S2                     
C  S3                     

3 rows selected.

gSQL> SELECT SHARD_NAME( T1, 'B' ) FROM DUAL;

SHARD_NAME( T1, 'B' )
---------------------
S2                   

1 row selected.
```

<a id="2126c43ce8408f3a"></a>
## SHIFT_LEFT

<a id="d41b098e0431bf70"></a>
### 구문

```
SHIFT_LEFT( num, cnt )
```

<a id="8c391098aa825b3e"></a>
### 설명

SHIFT_LEFT 함수는 num을 cnt 비트만큼 왼쪽으로 이동시킨 값을 반환한다.

입력 인자 num, cnt에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환하면 소수점은 TRUNCATE 된다.

연산 시 cnt는 6 bit로 마스킹하여 6 bit 범위 내의 값으로 처리한다.

num 또는 cnt가 NULL이면 NULL을 반환한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="d907550409b6e424"></a>
### 사용 예

```
gSQL> SELECT SHIFT_LEFT(1, 3) FROM DUAL;
SHIFT_LEFT(1, 3)
----------------
               8
1 row selected.
```

<a id="c3159c8b187b7228"></a>
## SHIFT_RIGHT

<a id="17091a513fec74da"></a>
### 구문

```
SHIFT_RIGHT( num, cnt )
```

<a id="6e8147ec1a66bbab"></a>
### 설명

SHIFT_RIGHT 함수는 num을 cnt 비트만큼 오른쪽으로 이동시킨 값을 반환한다.

입력 인자 num, cnt에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환하면 소수점은 TRUNCATE 된다.

연산 시 cnt는 6 bit로 마스킹하여 6 bit 범위내의 값으로 처리한다.

num 또는 cnt가 NULL이면 NULL을 반환한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="b4cbcc5d2ddb8217"></a>
### 사용 예

```
gSQL> SELECT SHIFT_RIGHT(8, 3) FROM DUAL;
SHIFT_RIGHT(8, 3)
-----------------
                1
1 row selected.
```

<a id="4f30e22deda50e48"></a>
## SIGN

<a id="617d719009d06f50"></a>
### 구문

```
SIGN( num )
```

<a id="ac03f5bdb52732b9"></a>
### 설명

SIGN 함수는 num의 부호를 반환한다.

인자 num에는 숫자타입이 올 수 있다.

반환값은 다음과 같다.  
• num < 0 이면 -1  
• num = 0 이면 0  
• num > 0 이면 1

num이 NULL이면 NULL을 반환한다.

<a id="79e9e5fd6968b34e"></a>
### 사용 예

```
gSQL> SELECT SIGN(-10) AS RESULT1, 
             SIGN(0) AS RESULT2, 
             SIGN(10) AS RESULT3 FROM DUAL;
RESULT1 RESULT2 RESULT3
------- ------- -------
     -1       0       1
1 row selected.
```

<a id="347ea90359f89d0e"></a>
## SIN

<a id="fde488eb67ccf898"></a>
### 구문

```
SIN( num )
```

<a id="4f9971c08364f633"></a>
### 설명

SIN 함수는 num의 sine 값을 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="cf886c79c2b95450"></a>
### 사용 예

```
gSQL> SELECT SIN( 0 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="e5c09988e44a0ee4"></a>
## SPLIT_PART

<a id="1a51773a72a2d7e7"></a>
### 구문

```
SPLIT_PART( string, delimiter, field )
```

<a id="88613b40059d25bf"></a>
### 설명

SPLIT_PART 함수는 string 내에서 delimiter로 지정된 문자를 구분자로 하여 field의 문자열을 반환한다.

인자 string, delimiter에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

인자 field에는 숫자 타입이 올 수 있다.

string, delimiter, field 중에 하나라도 NULL인 경우에는 결과값도 NULL이다.  
field에는 1 이상의 숫자값만 올 수 있고, 0 또는 음수일 경우에는 에러를 반환한다.

결과 타입은 다음 표와 같다.

**SPLIT_PART의 결과 타입**

<a id="dbfddc518356abfe"></a>
| string 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="48dc2bdb0a6f056f"></a>
### 사용 예

```
gSQL> SELECT SPLIT_PART( 'AB;CD;EF;GH', ';', 3  ) AS RESULT FROM DUAL;
RESULT
------
EF    
1 row selected.
```

<a id="f0c1c8a3477d6d6f"></a>
## SQRT

<a id="5d373c1160358b94"></a>
### 구문

```
SQRT( num )
```

<a id="996c162ec4fb8df3"></a>
### 설명

SQRT 함수는 num의 제곱근을 반환한다.  

인자 num에는 숫자 타입이 올 수 있고, 음수가 아닌 0 이상의 값이어야 한다.  
인자 num이 NULL이면 NULL을 반환한다.

<a id="86143e74902eec64"></a>
### 사용 예

```
gSQL> SELECT SQRT( 9 ) AS RESULT FROM DUAL;
RESULT
------
     3
1 row selected.
```

<a id="bcca3fc8f6bc7136"></a>
## STATEMENT_DATE

<a id="5651cf2913d848fc"></a>
### 구문

```
STATEMENT_DATE()
CURRENT_DATE [()]
```

<a id="11866a11c7f4b271"></a>
### 설명

현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="b0a543f844f8ddcd"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_DATE() AS result FROM t1;

RESULT    
----------
2013-12-12
2013-12-12
2013-12-12

3 rows selected.
```

<a id="0494f700ca96575f"></a>
## STATEMENT_LOCALTIME

<a id="465de0840cd7b921"></a>
### 구문

```
STATEMENT_LOCALTIME()
LOCALTIME [()]
```

<a id="df07a32233e4fe06"></a>
### 설명

Session 시간을 기준으로 현재 TIME WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="3838d66ea587d9bb"></a>
### 사용 예

모든 row가 같은 시간값을 갖는다.

```
gSQL> SELECT STATEMENT_LOCALTIME() AS result FROM t1;

RESULT         
---------------
16:18:50.775870
16:18:50.775870
16:18:50.775870

3 rows selected.
```

<a id="65aa4ab1672611f0"></a>
## STATEMENT_LOCALTIMESTAMP

<a id="223ced8578cac62f"></a>
### 구문

```
STATEMENT_LOCALTIMESTAMP()
LOCALTIMESTAMP [()]
```

<a id="0be87a2a608bde9f"></a>
### 설명

Session 시간을 기준으로 현재 TIMESTAMP WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="e96bff6bd7765b85"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT STATEMENT_LOCALTIMESTAMP() FROM t1;

STATEMENT_LOCALTIMESTAMP()
--------------------------
2013-12-12 16:23:39.782187
2013-12-12 16:23:39.782187
2013-12-12 16:23:39.782187

3 rows selected.
```

<a id="4602661083943637"></a>
## STATEMENT_TIME

<a id="ef0187363dd0e63c"></a>
### 구문

```
STATEMENT_TIME()
CURRENT_TIME [()]
```

<a id="ae0c328af6b4bc3b"></a>
### 설명

TIME ZONE이 있는 현재 TIME (TIME WITH TIME ZONE type) 값을 얻는다.

CURRENT_TIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="05815370b6a78ad9"></a>
### 사용 예

모든 row가 같은 시간값을 갖는다.

```
gSQL> SELECT STATEMENT_TIME() AS result FROM t1;

RESULT                
----------------------
16:28:19.268513 +09:00
16:28:19.268513 +09:00
16:28:19.268513 +09:00

3 rows selected.
```

<a id="e4324e327ac60b19"></a>
## STATEMENT_TIMESTAMP

<a id="8e468eca833dbdb4"></a>
### 구문

```
STATEMENT_TIMESTAMP()
CURRENT_TIMESTAMP [()]
```

<a id="7bc865d641bd946c"></a>
### 설명

TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

CURRENT_TIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="1e54788244ab637a"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT STATEMENT_TIMESTAMP() AS result FROM t1;

RESULT                           
---------------------------------
2013-12-12 16:36:11.032957 +09:00
2013-12-12 16:36:11.032957 +09:00
2013-12-12 16:36:11.032957 +09:00

3 rows selected.
```

<a id="75d041f10dddde72"></a>
## STATEMENT_VIEW_SCN

<a id="568edf30a35b4693"></a>
### 구문

```
STATEMENT_VIEW_SCN()
```

<a id="bd98f1bcf585db1f"></a>
### 설명

현재 STATEMENT의 VIEW SCN을 얻는다.

<a id="0c1d98609b5e875a"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN() FROM dual;

STATEMENT_VIEW_SCN()
--------------------
17697.658.17880     

1 row selected.
```

<a id="252567f9d7e85bbd"></a>
## STATEMENT_VIEW_SCN_DCN

<a id="1aab19daac957598"></a>
### 구문

```
STATEMENT_VIEW_SCN_DCN()
```

<a id="ffdf1b2f6ac48780"></a>
### 설명

현재 STATEMENT의 VIEW SCN의 Domain Change Number (DCN) 값을 얻는다.

<a id="852e65b67fd20ac0"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_DCN() FROM dual;

STATEMENT_VIEW_SCN_DCN()
------------------------
                     658

1 row selected.
```

<a id="a149f2f013b01fe3"></a>
## STATEMENT_VIEW_SCN_GCN

<a id="300936c3329c9ab7"></a>
### 구문

```
STATEMENT_VIEW_SCN_GCN()
```

<a id="e0bff6d0d7a6a2e6"></a>
### 설명

현재 STATEMENT의 VIEW SCN의 Global Change Number (GCN) 값을 얻는다.

<a id="2679a52ce7004327"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_GCN() FROM dual;

STATEMENT_VIEW_SCN_GCN()
------------------------
                   17697

1 row selected.
```

<a id="302d97d24c71160c"></a>
## STATEMENT_VIEW_SCN_LCN

<a id="635f2fa1e270a030"></a>
### 구문

```
STATEMENT_VIEW_SCN_LCN()
```

<a id="e81bbc3fb5e39b29"></a>
### 설명

현재 STATEMENT의 VIEW SCN의 Local Change Number (LCN) 값을 얻는다.

<a id="045a56fefa8f8526"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_LCN() FROM dual;

STATEMENT_VIEW_SCN_LCN()
------------------------
                   17880

1 row selected.
```

<a id="f0420e3d95a59bdb"></a>
## STDDEV

<a id="f6caf9d150ff91d1"></a>
### 구문

```
STDDEV( [ ALL | DISTINCT ] expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="77bdc4092e5e8225"></a>
### 설명

Aggregation 함수로써 expr set의 표준편차 (standard deviation)를 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 수행하고, DISTINCT를 명시한 경우 중복을 제거한 값들에 대해 수행한다. 둘 다 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

FILTER를 명시한 경우 condition을 만족하는 값들에 한하여 aggregation을 수행한다.

NULL 값을 제외하고 DISTINCT로 중복을 제거한 후의 expr set의 개수가 한 개일 경우, [VARIANCE](#ab8b6a136b382960)와 같이 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV 인자와 결과 타입**

<a id="f41f79abc233fa9a"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

GOLDILOCKS는 다음과 같이 표준편차를 계산한다.  
　• expr set의 개수가 1이면 0을 반환한다.  
　• expr set의 개수가 1보다 크면 [STDDEV_SAMP( expr )](#76f1f4a01a39aaf0) 값을 반환한다.

> 표준편차는, 분산의 양의 제곱근으로써 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV 함수는 [VARIANCE](#ab8b6a136b382960) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV( [ ALL ] expr )  
>  = SQRT( VARIANCE( [ ALL ] expr ) )  
>   
> STDDEV( DISTINCT expr )  
>  = SQRT( VARIANCE( DISTINCT expr ) )

<a id="20220c4bfa9b2785"></a>
### 사용 예

```
gSQL> SELECT STDDEV(c1) FROM t1;

      STDDEV(C1)
----------------
11.4978258814438

1 row selected.


gSQL> SELECT STDDEV(ALL c1) FROM t1;

  STDDEV(ALL C1)
----------------
11.4978258814438

1 row selected.


gSQL> SELECT STDDEV(DISTINCT c1) FROM t1;

STDDEV(DISTINCT C1)
-------------------
   13.2759180473518

1 row selected.


gSQL> SELECT STDDEV(c1) FILTER( WHERE c1 > 0 ) FROM t1;

      STDDEV(C1)
----------------
11.4978258814438

1 row selected.
```

<a id="39c1758ce4105113"></a>
## STDDEV() OVER

<a id="40763deea2a278da"></a>
### 구문

```
STDDEV ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="fde768d9e5db3f73"></a>
### 설명

Window function STDDEV는 expr의 표준편차 (standard deviation)를 구하는 함수이다.  
NULL 값을 제외한 expr의 개수가 한 개일 경우, 결과로 0을 반환한다.

<a id="8ff6efbf3e19e64d"></a>
### 사용 예

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , STDDEV( min_price ) OVER ( ORDER BY min_price ) AS "STDDEV"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE           STDDEV
--------- ----------------
       73                0
      247 123.036579926459
      731 340.953564775811
     null 340.953564775811
     null 340.953564775811

5 rows selected.
```

<a id="0a4728846b8e14ba"></a>
## STDDEV_POP

<a id="e0c5a01c417c1d8e"></a>
### 구문

```
STDDEV_POP( expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="13ea41980a228ba2"></a>
### 설명

Aggregation 함수로써 expr set의 모 표준편차 (population standard deviation)를 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 0을 반환한다.

FILTER를 명시한 경우 condition을 만족하는 값들에 한하여 aggregation을 수행한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV_POP의 인자와 결과 타입**

<a id="7478f405599123a1"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 표준편차는 모 분산의 양의 제곱근으로써 모 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV_POP 함수는 [VAR_POP](#3c837bf115b1008a) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV_POP( expr )  
>  = SQRT( VAR_POP( expr ) )

<a id="50b6ea3c5c7de3b3"></a>
### 사용 예

```
gSQL> SELECT STDDEV_POP(c1) FROM t1;

 STDDEV_POP(C1)
---------------
10.283968105746

1 row selected.


gSQL> SELECT STDDEV_POP(c1) FILTER( WHERE c1 > 0 ) FROM t1;

 STDDEV_POP(C1)
---------------
10.283968105746

1 row selected.
```

<a id="01c0463a3aebd337"></a>
## STDDEV_POP() OVER

<a id="3af17941b3e37e90"></a>
### 구문

```
STDDEV_POP ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="e72419bb0c35e835"></a>
### 설명

Window function STDDEV_POP은 expr의 모 표준편차 (population standard deviation)를 구하는 함수이다.  
NULL 값을 제외한 expr의 개수가 한 개일 경우, 결과로 0을 반환한다.

<a id="bf9020e94d0666d6"></a>
### 사용 예

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , STDDEV_POP( min_price ) OVER ( ORDER BY min_price ) AS "STDDEV_POP"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE      STDDEV_POP
--------- ---------------
       73               0
      247              87
      731 278.38741989457
     null 278.38741989457
     null 278.38741989457

5 rows selected.
```

<a id="76f1f4a01a39aaf0"></a>
## STDDEV_SAMP

<a id="01d3bdc1fb1c7583"></a>
### 구문

```
STDDEV_SAMP( expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="24b3ed4aaef35526"></a>
### 설명

Aggregation 함수로써 expr set의 표본 표준편차 (sample standard deviation)를 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 NULL값을 반환한다.

FILTER를 명시한 경우 condition을 만족하는 값들에 한하여 aggregation을 수행한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV_SAMP의 인자와 결과 타입**

<a id="6355caa9e8627da4"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 표본 표준편차는 표본 분산의 양의 제곱근으로써 표본 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV_SAMP 함수 [VAR_SAMP](#dc962b0b48f04aed) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV_SAMP( expr )  
>  = SQRT( VAR_SAMP( expr ) )

<a id="b91c7bbab9acc3f6"></a>
### 사용 예

```
gSQL> SELECT STDDEV_SAMP(c1) FROM t1;

 STDDEV_SAMP(C1)
----------------
11.4978258814438

1 row selected.


gSQL> SELECT STDDEV_SAMP(c1) FILTER( WHERE c1 > 0 ) FROM t1;

 STDDEV_SAMP(C1)
----------------
11.4978258814438

1 row selected.
```

<a id="2438c9326be21907"></a>
## STDDEV_SAMP() OVER

<a id="93a6116bc01471b7"></a>
### 구문

```
STDDEV_SAMP ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="8e77bb1bb7291534"></a>
### 설명

Window function STDDEV_SAMP은 expr의 표본 표준편차 (sample standard deviation)를 구하는 함수이다.  
NULL 값을 제외한 expr의 개수가 한 개일 경우, 결과로 NULL을 반환한다.

<a id="1ee4da6a5e590d91"></a>
### 사용 예

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , STDDEV_SAMP( min_price ) OVER ( ORDER BY min_price ) AS "STDDEV_SAMP"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE      STDDEV_SAMP
--------- ----------------
       73             null
      247 123.036579926459
      731 340.953564775811
     null 340.953564775811
     null 340.953564775811

5 rows selected.
```

<a id="15ac63821b70703c"></a>
## STRING_AGG() OVER

<a id="a78d8cacec99fb08"></a>
### 구문

```
STRING_AGG( str [, delimiter] ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="252c9074b5ca4ee6"></a>
### 설명

Window function STRING_AGG는 OVER 절에 정의된 함수의 수행 범위에 따라 str을 연결하는 함수이다.

str이 NULL인 경우에는 제외된다.

delimiter는 str 연결 구분자이며, 생략할 경우 기본값은 NULL 이다.

str에는 character string 또는 binary string이 올 수 있다.  
str이 character string 이면, 결과타입은 varchar 이다.  
str이 binary string 이면, 결과타입은 varbinary 이다.

<a id="6ec0b7be79ae89e9"></a>
### 사용 예

```
gSQL> 
SELECT regionkey,
       name,
       STRING_AGG( name ) OVER ( PARTITION BY regionkey
                                 ORDER BY nationkey
                                 ROWS BETWEEN UNBOUNDED PRECEDING 
                                          AND CURRENT ROW ) 
       AS "STRING_AGG( name ) OVER",
       STRING_AGG( name, ', ' ) OVER ( PARTITION BY regionkey
                                       ORDER BY nationkey
                                       ROWS BETWEEN UNBOUNDED PRECEDING
                                                AND CURRENT ROW ) 
       AS "STRING_AGG( name, ', ' ) OVER"  
  FROM nation;

REGIONKEY NAME    STRING_AGG( name ) OVER STRING_AGG( name, ', ' ) OVER
--------- ------- ----------------------- -----------------------------
        1 BRAZIL  BRAZIL                  BRAZIL                       
        1 CANADA  BRAZILCANADA            BRAZIL, CANADA               
        1 PERU    BRAZILCANADAPERU        BRAZIL, CANADA, PERU         
        1 null    BRAZILCANADAPERU        BRAZIL, CANADA, PERU         
        2 null    null                    null                         
        2 INDIA   INDIA                   INDIA                        
        2 null    INDIA                   INDIA                        
        2 null    INDIA                   INDIA                        
        2 JAPAN   INDIAJAPAN              INDIA, JAPAN                 
        2 CHINA   INDIAJAPANCHINA         INDIA, JAPAN, CHINA          
        2 null    INDIAJAPANCHINA         INDIA, JAPAN, CHINA          
        2 VIETNAM INDIAJAPANCHINAVIETNAM  INDIA, JAPAN, CHINA, VIETNAM 
        3 EGYPT   EGYPT                   EGYPT                        
        3 IRAN    EGYPTIRAN               EGYPT, IRAN                  
        3 IRAQ    EGYPTIRANIRAQ           EGYPT, IRAN, IRAQ            

15 rows selected.
```

<a id="dd65acd21add6abf"></a>
## SUBSTR

<a id="8521b270211764ac"></a>
### 구문

```
SUBSTR( str FROM start_position [ FOR string_length ] )
SUBSTR( str, start_position [ , string_length ] )
```

<a id="c42eaf45f4fa1c43"></a>
### 설명

[SUBSTRING](#6811306ff1562f60)의 alias이다.

<a id="3321fccc8aae8492"></a>
### 사용 예

- Multi byte character set (예: UTF8): 1 byte character

```
gSQL> SELECT 
      SUBSTR( 'DATABASE MANAGEMENT SYSTEM', 10, 10 ) AS RESULT 
      FROM DUAL;
RESULT    
----------
MANAGEMENT
1 row selected.
```

- Multi byte character set (예: UTF8): 2 bytes or 3 bytes character

```
gSQL> SELECT SUBSTR( '“αβ≠ΑΒ”', 2, 5 ) AS RESULT FROM DUAL;
RESULT
------
αβ≠ΑΒ 
1 row selected.
```

<a id="1816902f3ae32864"></a>
## SUBSTRB

<a id="598fd537a4ca2fcb"></a>
### 구문

```
SUBSTRB( str, start_position [ , string_length ] )
```

<a id="e9706cfb63309303"></a>
### 설명

SUBSTRB 함수는 str에 대해 start_position으로부터 string_length 범위의 문자를 추출하여 반환한다.

SUBSTRB 함수는 start_position과 string_length가 byte 단위로 계산된다는 점 외에는 [SUBSTRING](#6811306ff1562f60) 함수와 동일하다.

<a id="a0a73e6b0614bc6c"></a>
### 사용 예

- Multi byte character set (예: UTF8): 1 byte character

```
gSQL> SELECT 
      SUBSTRB( 'DATABASE MANAGEMENT SYSTEM', 10, 10 ) AS RESULT 
      FROM DUAL;
RESULT    
----------
MANAGEMENT
1 row selected.
```

- Multi byte character set (예: UTF8): 2 bytes or 3 bytes character

```
gSQL> SELECT SUBSTRB( '“αβ≠ΑΒ”', 4, 11 ) AS RESULT FROM DUAL;
RESULT
------
αβ≠ΑΒ 
1 row selected.
```

<a id="6811306ff1562f60"></a>
## SUBSTRING

<a id="c6f5994be28a2f49"></a>
### 구문

```
SUBSTRING( str FROM start_position [ FOR string_length ] )  
SUBSTRING( str, start_position [ , string_length ] )
```

<a id="5b33d8e5cab5c8a9"></a>
### 설명

SUBSTRING 함수는 str에 대해 start_position으로부터 string_length 범위의 문자를 추출하여 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

인자 start_position과 string_length에는 숫자 타입이 올 수 있다.

str, start_position과 string_length 중의 하나라도 NULL인 경우, 결과값은 NULL이다.  
start_position과 string_length는 1부터 시작하며, character set에 따른 문자 단위로 계산된다. (byte 단위가 아님)

start_position이 0인 경우, 1로 처리된다.   
start_position이 양수인 경우, str의 앞부분에서부터 position의 위치를 찾는다.   
start_position이 음수인 경우, str의 뒷부분에서부터 position의 위치를 찾는다.   
string_length가 생략된 경우, start_position으로부터 str의 마지막 문자까지 반환한다.  
string_length에 0 또는 음수가 오는 경우, 결과값은 NULL이다.  
start_position > (str의 길이) 이면, 결과값은 NULL이다.   
(str의 길이 + start_position ) < 0 이면, 결과값은 NULL이다.

SUBSTR의 alias이다.  
자세한 내용은 [SUBSTR](#dd65acd21add6abf)과 [SUBSTRB](#1816902f3ae32864)를 참조한다.

결과 타입은 다음 표와 같다.

**SUBSTRING의 결과 타입**

<a id="9cc443065c5a6c72"></a>
| str | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="fe507d1d5fbc6332"></a>
### 사용 예

- Multi byte character set (예: UTF8): 1 byte character

```
gSQL> SELECT 
      SUBSTRING( 'DATABASE MANAGEMENT SYSTEM' FROM 10 FOR 10 ) AS RESULT 
      FROM DUAL;
RESULT    
----------
MANAGEMENT
1 row selected.
```

- Multi byte character set (예: UTF8): 2 bytes or 3 bytes character

```
gSQL> SELECT SUBSTRING( '“αβ≠ΑΒ”' FROM 2 FOR 5 ) AS RESULT FROM DUAL;
RESULT
------
αβ≠ΑΒ 
1 row selected.
```

<a id="ec30d624521e1798"></a>
## SUM

<a id="d0e57117a484d850"></a>
### 구문

```
SUM( [ ALL | DISTINCT ] expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="dc49058c10b5dce0"></a>
### 설명

Aggregation 함수로써 expr 값들의 합을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복을 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.  

FILTER를 명시한 경우 condition을 만족하는 값들에 한하여 aggregation을 수행한다.

<a id="9f099f806e4ca4c4"></a>
### 사용 예

```
gSQL> SELECT SUM( c1 ) FROM t1;

SUM(C1)
-------
      6

1 row selected.


gSQL> SELECT SUM( c1 ) FILTER( WHERE c1 > 1 ) FROM t1;

SUM(C1)
-------
      5

1 row selected.
```

<a id="1a83ad57ee5a8705"></a>
## SUM() OVER

<a id="3f0d1235322444cc"></a>
### 구문

```
SUM ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="a71f8b6c494a1e02"></a>
### 설명

Window function SUM은 expr 값의 합을 구하는 함수이다.  
NULL 값은 연산에서 제외된다.

<a id="6f000a111670d4af"></a>
### 사용 예

```
gSQL> SELECT min_price AS "MIN_PRICE"
             , SUM( min_price ) OVER ( ORDER BY min_price ) AS "SUM"
        FROM product_information
       WHERE supplier_id = 102050;

MIN_PRICE  SUM
--------- ----
       73   73
      247  320
      731 1051
     null 1051
     null 1051

5 rows selected.
```

<a id="082d06d73d6c99a7"></a>
## SYSDATE

<a id="db9fe92b36981a34"></a>
### 구문

```
SYSDATE
```

<a id="581a576e2978a794"></a>
### 설명

Database server가 위치하는 OS 시간을 기준으로 현재의 DATE type 값을 얻는다.

<a id="25a0868cabb5c0eb"></a>
### 사용 예

```
gSQL> SELECT SYSDATE FROM t1;

SYSDATE   
----------
2013-12-12
2013-12-12
2013-12-12

3 rows selected.
```

<a id="40bdc17e19662a82"></a>
## SYS_EXTRACT_UTC

<a id="db40c52599e3c93b"></a>
### 구문

```
SYS_EXTRACT_UTC( datetime_with_timezone )
```

<a id="6f74136376317cc7"></a>
### 설명

SYS_EXTRACT_UTC 는  UTC (Coordinated Universal Time—formerly Greenwich Mean Time) 값을 반환한다.  
timezone이 명시되지 않은 경우, session time zone으로 계산된다.

입력 인자에는 TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
결과 타입은 TIME 또는 TIMESTAMP 타입이다.

<a id="8acfb8d7ce55107d"></a>
### 사용 예

```
gSQL> SELECT
      SYS_EXTRACT_UTC( 
          TO_TIMESTAMP_TZ( '2017-05-25 00:00:00.000000 +09:00',
                           'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM' ) 
          ) AS RESULT
      FROM DUAL; 
RESULT                    
--------------------------
2017-05-24 15:00:00.000000
1 row selected.
```

<a id="2fe60c11f4576cb8"></a>
## SYSTIME

<a id="daa0517914c2e856"></a>
### 구문

```
SYSTIME
```

<a id="1e14535dd3169fe2"></a>
### 설명

Database server가 위치하는 OS 시간을 기준으로 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

<a id="dda852af888bc0d1"></a>
### 사용 예

```
gSQL> SELECT SYSTIME FROM t1;

SYSTIME               
----------------------
16:30:46.954941 +09:00
16:30:46.954941 +09:00
16:30:46.954941 +09:00

3 rows selected.
```

<a id="85bb49d3d48c5c50"></a>
## SYSTIMESTAMP

<a id="800c4ee39964210d"></a>
### 구문

```
SYSTIMESTAMP
```

<a id="4d347663d20aad62"></a>
### 설명

Database server가 위치하는 OS 시간을 기준으로 TIME ZONE이 있는 현재 TIMESTAMP WITH TIME ZONE type 값을 얻는다.

<a id="f8195797eeba75c2"></a>
### 사용 예

```
gSQL> SELECT SYSTIMESTAMP FROM t1;

SYSTIMESTAMP                     
---------------------------------
2013-12-12 16:37:34.432241 +09:00
2013-12-12 16:37:34.432241 +09:00
2013-12-12 16:37:34.432241 +09:00

3 rows selected.
```

<a id="b6629b53c0b75cd5"></a>
## TABLE_PHYSICAL_STATS

<a id="2f7306921e362943"></a>
### 구문

```
TABLE_PHYSICAL_STATS( [schema_name.]table_name [,sampling_ratio_value] )
```

<a id="a11e2834eaee9bc7"></a>
### 설명

TABLE_PHYSICAL_STATS 는 테이블에 할당된 페이지의 단편화 (fragmentation) 정보를 반환하는 함수이다.

입력 인자 table_name은 identifier로 지정해야 하며, 해당 객체가 일반 테이블이 아닌 경우, 에러가 발생한다.

입력 인자 sampling_ratio_value는 객체가 보유한 전체 페이지 중 분석 대상으로 접근할 페이지의 비율 (%) 을 의미한다. 전체 페이지를 모두 처리하지 않고 일부 페이지만 무작위로 샘플링하여 분석함으로써, 작업을 더욱 빠르고 효율적으로 수행할 수 있다. 결과로 출력되는 Used 및 Fragmented는 할당된 전체 페이지가 아니라, 샘플링된 페이지를 기준으로 분석된 크기이다. 이 인자를 생략하면 기본적으로 100%가 적용되어 전체 페이지를 분석한다. 값의 범위는 1~100이며, 범위를 벗어나면 오류가 반환된다.

결과 타입은 VARCHAR 이며, Page, Used, Fragmented 정보를 반환한다.  
• Page: 테이블에 할당된 전체 페이지 수이다.  
• Used: 사용된 공간의 크기로서 페이지의 헤더 크기와 저장된 데이터 크기의 합이며, 단위는 byte이다.  
• Fragmented: 단편화 된 공간의 크기로서 단위는 byte 이다.

> 클러스터의 모든 노드에서 확인하고자 할 때에는 GLOBAL_DUAL 을 사용할 수 있다.

<a id="98b343b35952857e"></a>
### 사용 예

- DUAL 사용 시
    - 접속한 노드의 객체 정보를 반환한다.
    - 클러스터 환경에서는 클러스터 도메인을 기술할 수 있다.

```
gSQL> SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(T1) FROM DUAL;
CLUSTER_MEMBER_NAME TABLE_PHYSICAL_STATS(T1)                     
------------------- ---------------------------------------------
G1N1                Page: 992, Used: 4935498, Fragmented: 2133312
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(PUBLIC.T1) FROM DUAL;
CLUSTER_MEMBER_NAME TABLE_PHYSICAL_STATS(PUBLIC.T1)              
------------------- ---------------------------------------------
G1N1                Page: 992, Used: 4935498, Fragmented: 2133312
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(PUBLIC.T1, 50) FROM DUAL;
CLUSTER_MEMBER_NAME TABLE_PHYSICAL_STATS(PUBLIC.T1, 50)          
------------------- ---------------------------------------------
G1N1                Page: 992, Used: 2497724, Fragmented: 1079680
1 row selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(T1) FROM DUAL@G1N1
      UNION ALL
      SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(T1) FROM DUAL@G2N1
      UNION ALL
      SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(T1) FROM DUAL@G3N1;
CLUSTER_MEMBER_NAME TABLE_PHYSICAL_STATS(T1)                        
------------------- ------------------------------------------------
G1N1                Page: 992, Used: 4935498, Fragmented: 2133312   
G2N1                Page: 2912, Used: 14806136, Fragmented: 6400000 
G3N1                Page: 5760, Used: 29611846, Fragmented: 12800000
3 rows selected.
```

- GLOBAL_DUAL 사용 시
    - 클러스터 환경에서 모든 노드의 객체 정보를 반환한다.
    - 클러스터 도메인을 기술할 수 있다.

```
gSQL> SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(PUBLIC.T1, 50)
        FROM GLOBAL_DUAL
      ORDER BY CLUSTER_MEMBER_NAME;
CLUSTER_MEMBER_NAME TABLE_PHYSICAL_STATS(PUBLIC.T1, 50)            
------------------- -----------------------------------------------
G1N1                Page: 992, Used: 2591000, Fragmented: 1120000  
G1N2                Page: 992, Used: 2290444, Fragmented: 990080   
G2N1                Page: 2912, Used: 7120068, Fragmented: 3077760 
G2N2                Page: 2912, Used: 7405078, Fragmented: 3200960 
G3N1                Page: 5760, Used: 15095166, Fragmented: 6525120
G3N2                Page: 5760, Used: 14494054, Fragmented: 6265280
6 rows selected.

gSQL> SELECT CLUSTER_MEMBER_NAME, TABLE_PHYSICAL_STATS(PUBLIC.T1, 50)
        FROM GLOBAL_DUAL@G1N1|G2N1|G3N1
      ORDER BY CLUSTER_MEMBER_NAME;
CLUSTER_MEMBER_NAME TABLE_PHYSICAL_STATS(PUBLIC.T1, 50)            
------------------- -----------------------------------------------
G1N1                Page: 992, Used: 2399266, Fragmented: 1037120  
G2N1                Page: 2912, Used: 7353258, Fragmented: 3178560 
G3N1                Page: 5760, Used: 14633968, Fragmented: 6325760
3 rows selected.
```

<a id="b8421f4ba9b9b484"></a>
## TAN

<a id="b063e70c35e4df5b"></a>
### 구문

```
TAN( num )
```

<a id="0582bf0f78c7669e"></a>
### 설명

TAN 함수는 num의 tangent 값을 라디안 단위로 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="229b47e51a7d9d78"></a>
### 사용 예

```
gSQL> SELECT TAN( 1 ) AS RESULT FROM DUAL;
         RESULT
---------------
1.5574077246549
1 row selected.
```

<a id="a81b5df21d4b3b16"></a>
## TO_BASE64

<a id="dca6552e861ff0b7"></a>
### 구문

```
TO_BASE64( str )
```

<a id="3f1ec300019cc10a"></a>
### 설명

TO_BASE64는 str을 base64 인코딩으로 변환한 문자를 반환한다.  
인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입 또는 문자 타입으로 변환될 수 있는 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.  
결과 타입은 CHARACTER VARYING 또는 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.

Base64 인코딩은 8 비트 바이너리 데이터를 ascii 영역으로 구성된 64개의 문자로 표현한다.  
64개의 문자는 A~Z, a~z, 0~9, +, / 로 구성된다.

6 bit를 하나의 문자로 표현하며, 세 개의 문자 (24 bit)를 하나의 단위로 네 개의 문자로 표현한다.  
인코딩 된 문자가 네 개의 문자를 채우지 못하면 나머지는 '=' 로 채운다.  
인코딩 된 문자가 76개를 넘으면 newline이 추가되어 여러 라인으로 나누어진다.

Base64 인코딩 된 문자의 디코딩은 FROM_BASE64() 함수를 이용한다.  
Base64를 디코딩 할 때는 newline, carriage return, tab, space가 무시된다.

자세한 내용은 [FROM_BASE64](#a5fd965acdfbf4d5)를 참조한다.

<a id="d3e3c4169950ebc0"></a>
### 사용 예

```
gSQL> SELECT TO_BASE64( 'abc' ), TO_BASE64( 'abcd' ) FROM DUAL;

TO_BASE64( 'abc' ) TO_BASE64( 'abcd' )
------------------ -------------------
YWJj               YWJjZA==           
1 row selected.
```

<a id="49e380b1da61d32b"></a>
## TO_CHAR( datetime )

<a id="e0d061aae228ef56"></a>
### 구문

```
TO_CHAR( datetime [, fmt ] )
```

<a id="cdfbe4829569cbf2"></a>
### 설명

TO_CHAR( datetime ) 함수는 datetime을 명시된 fmt 형식의 문자열로 변환하여 반환한다.

인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  

입력 인자의 값이 하나라도 NULL이면 NULL을 반환한다.

fmt가 생략된 경우, default format 형식을 따른다.  
• DATE: [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#09118aefc816172d)  
• TIMESTAMP: [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#b83b0daa42003bc4)  
• TIMESTAMP WITH TIME ZONE: [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#8cf319a54a7fec34)  
• TIME: [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#d78680ceba6107a9)  
• TIME WITH TIME ZONE: [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#d8ed241efdbfc8ee)

인자 datetime이 INTERVAL 타입인 경우, fmt와 무관하게 string으로 변환하여 반환한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#95e37f19cf8bd6a2)을 참조한다.

결과 타입은 CHARACTER VARYING 이다.

<a id="08a17fba04f3dad1"></a>
### 사용 예

다음은 fmt가 생략되고, NLS_DATE_FORMAT = 'YYYY-MM-DD' 인 경우의 예이다.

```
gSQL> SELECT 
      TO_CHAR( TO_DATE( '2012-03-15','YYYY-MM-DD' ) ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2012-03-15
1 row selected.
```

다음은 fmt가 지정된 경우의 예이다.

```
gSQL> SELECT 
      TO_CHAR( TO_DATE('2012-03-15','YYYY-MM-DD'), 'DD-MON-YY' ) AS RESULT
      FROM DUAL;
RESULT   
---------
15-MAR-12
1 row selected.
```

<a id="69fde4657a756aff"></a>
## TO_CHAR( number )

<a id="19284ed8ca8771a6"></a>
### 구문

```
TO_CHAR( number [, fmt ] )
```

<a id="a6d71a9f459aa3cd"></a>
### 설명

TO_CHAR( number ) 함수는 number를 명시된 fmt 형식의 문자열로 변환하여 반환한다.

인자 number에는 숫자 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, 모든 유효 숫자를 문자열로 변환하여 반환한다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#36aa4bb1bae7fc27)을 참조한다.  
입력 인자의 값이 하나라도 NULL이면 NULL을 반환한다.

결과 타입은 CHARACTER VARYING 이다.

<a id="222aff3bc82f2280"></a>
### 사용 예

```
gSQL> SELECT TO_CHAR( 12500000 ) AS RESULT FROM DUAL;
RESULT  
--------
12500000
1 row selected.

gSQL> SELECT TO_CHAR( 12500000, 'S999,999,999' ) AS RESULT FROM DUAL;
RESULT      
------------
 +12,500,000
1 row selected.
```

<a id="e1ae1f9cb408151d"></a>
## TO_DATE

<a id="2cd1154a6e93dcb6"></a>
### 구문

```
TO_DATE( str [, fmt ] )
```

<a id="77d8001398194c2b"></a>
### 설명

TO_DATE 함수는 명시된 fmt 형식의 문자열 str을 DATE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_DATE_FORMAT은 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#95e37f19cf8bd6a2)을 참조한다.  
자세한 내용은 [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#09118aefc816172d)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

결과 타입은 DATE 이다.

<a id="ea0a61fd7daa7a50"></a>
### 사용 예

다음은 fmt가 생략되었고, NLS_DATE_FORMAT = 'YYYY-MM-DD' 인 경우의 예이다.

```
gSQL> SELECT TO_DATE( '2009-07-29' ) AS RESULT FROM DUAL;
RESULT    
----------
2009-07-29
1 row selected.
```

다음은 fmt가 지정된 경우의 예이다.

```
gSQL> SELECT TO_DATE( '29-JUL-09', 'DD-MON-YY' ) AS RESULT FROM DUAL;
RESULT    
----------
2009-07-29
1 row selected.
```

<a id="860aa4f498a985ca"></a>
## TO_NATIVE_BIGINT

<a id="c34f9fd99e788ef5"></a>
### 구문

```
TO_NATIVE_BIGINT( str [, fmt ] )
```

<a id="82ee99ef1b241d2c"></a>
### 설명

TO_NATIVE_BIGINT 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_BIGINT 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#36aa4bb1bae7fc27)을 참조한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="fa838d3d8bc4b881"></a>
### 사용 예

```
gSQL> SELECT TO_NATIVE_BIGINT( '123.45' ) AS RESULT1,
             TO_NATIVE_BIGINT( '+123.45', 'S999.99' ) AS RESULT2
        FROM DUAL;
RESULT1 RESULT2
------- -------
    123     123
1 row selected.
```

<a id="b6f99a7754f9a09a"></a>
## TO_NATIVE_DOUBLE

<a id="5e6de1703852f741"></a>
### 구문

```
TO_NATIVE_DOUBLE( str [, fmt ] )
```

<a id="22f2733dc3901f12"></a>
### 설명

TO_NATIVE_DOUBLE 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_DOUBLE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#36aa4bb1bae7fc27)을 참조한다.

결과 타입은 NATIVE_DOUBLE이다.

<a id="fd8493234d4b79dc"></a>
### 사용 예

```
gSQL> SELECT TO_NATIVE_DOUBLE( '123.45' ) AS RESULT1, 
             TO_NATIVE_DOUBLE( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
1 row selected.
```

<a id="f4ea0087d7690777"></a>
## TO_NATIVE_INTEGER

<a id="44742bad2b07e271"></a>
### 구문

```
TO_NATIVE_INTEGER( str [, fmt ] )
```

<a id="c42ed8a757ff7766"></a>
### 설명

TO_NATIVE_INTEGER 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_INTEGER 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#36aa4bb1bae7fc27)을 참조한다.

결과 타입은 NATIVE_INTEGER이다.

<a id="02561757c34a9bf2"></a>
### 사용 예

```
gSQL> SELECT TO_NATIVE_INTEGER( '123.45' ) AS RESULT1,
             TO_NATIVE_INTEGER( '+123.45', 'S999.99' ) AS RESULT2
        FROM DUAL;
RESULT1 RESULT2
------- -------
    123     123
1 row selected.
```

<a id="9c39d911dce66749"></a>
## TO_NATIVE_REAL

<a id="978dc2a564e2b905"></a>
### 구문

```
TO_NATIVE_REAL( str [, fmt ] )
```

<a id="782a8ca5d8f68689"></a>
### 설명

TO_NATIVE_REAL 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_REAL 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#36aa4bb1bae7fc27)을 참조한다.

결과 타입은 NATIVE_REAL이다.

<a id="8d3c62450af469da"></a>
### 사용 예

```
gSQL> SELECT TO_NATIVE_REAL( '123.45' ) AS RESULT1, 
             TO_NATIVE_REAL( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
```

<a id="802fe8044515d1c9"></a>
## TO_NATIVE_SMALLINT

<a id="f3e05b7b3e1566a8"></a>
### 구문

```
TO_NATIVE_SMALLINT( str [, fmt ] )
```

<a id="7f6c0e59253a9ff5"></a>
### 설명

TO_NATIVE_SMALLINT 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_SMALLINT 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYIN과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#36aa4bb1bae7fc27)을 참조한다.

결과 타입은 NATIVE_SMALLINT이다.

<a id="03e4b8b906d04096"></a>
### 사용 예

```
gSQL> SELECT TO_NATIVE_SMALLINT( '123.45' ) AS RESULT1,
             TO_NATIVE_SMALLINT( '+123.45', 'S999.99' ) AS RESULT2
        FROM DUAL;
RESULT1 RESULT2
------- -------
    123     123
1 row selected.
```

<a id="5b93653f4677d64c"></a>
## TO_NUMBER

<a id="ee6b99151705ee3d"></a>
### 구문

```
TO_NUMBER( str [, fmt] )
```

<a id="5903ae1a8727099a"></a>
### 설명

TO_NUMBER 함수는 명시된 fmt 형식의 문자열 str을 NUMBER 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#36aa4bb1bae7fc27)을 참조한다.

결과 타입은 NUMBER이다.

<a id="179ffdbc564b5ae8"></a>
### 사용 예

```
gSQL> SELECT TO_NUMBER( '123.45' ) AS RESULT1, 
             TO_NUMBER( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
1 row selected.
```

<a id="91b2febb7ce81d9c"></a>
## TO_TIME

<a id="5ec230a383967207"></a>
### 구문

```
TO_TIME( str [, fmt ] )
```

<a id="cea35138023601bc"></a>
### 설명

TO_TIME 함수는 명시된 fmt 형식의 문자열 str을 TIME 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIME_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#95e37f19cf8bd6a2)을 참조한다.  
자세한 내용은 [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#d78680ceba6107a9)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

결과 타입은 TIME 이다.

<a id="6dcbb941ae586d16"></a>
### 사용 예

다음은 fmt가 생략되었고, NLS_TIME_FORMAT = 'HH24:MI:SS.FF6' 인 경우의 예이다.

```
gSQL> SELECT TO_TIME( '11:22:33.999999' ) AS RESULT FROM DUAL;
RESULT         
---------------
11:22:33.999999
1 row selected.
```

다음은 fmt가 지정된 경우의 예이다.

```
gSQL> SELECT 
      TO_TIME( '112233.999999/P.M.', 'HH12MISS.FF6/P.M.' ) AS RESULT 
      FROM DUAL;
RESULT         
---------------
23:22:33.999999
1 row selected.
```

<a id="09815ff744a36043"></a>
## TO_TIME_TZ

<a id="ef8df9e8ae5f1c9d"></a>
### 구문

```
TO_TIME_TZ( str [, fmt ] )
```

<a id="8c8a7043cadf3f89"></a>
### 설명

TO_TIME_WITH_TIME_ZONE의 alias이다.  
자세한 내용은 [TO_TIME_WITH_TIME_ZONE](#a9f9c02ecbf276e7)과 [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#d8ed241efdbfc8ee)을 참조한다.

<a id="04e40d342abeb57b"></a>
### 사용 예

다음은 fmt가 생략되었고, NLS_TIME_WITH_TIME_ZONE_FORMAT = 'HH24:MI:SS.FF6 TZH:TZM' 인 경우의 예이다.

```
gSQL> SELECT TO_TIME_TZ( '11:22:33.999999 +09:00' ) AS RESULT FROM DUAL;
RESULT                
----------------------
11:22:33.999999 +09:00
1 row selected.
```

다음은 fmt가 지정된 경우의 예이다.

```
gSQL> SELECT TO_TIME_TZ( '11:22:33.999999 +09:00 PM', 
                         'HH12:MI:SS.FF6 TZH:TZM PM' ) AS RESULT 
      FROM DUAL;
RESULT                
----------------------
23:22:33.999999 +09:00
1 row selected.
```

<a id="a9f9c02ecbf276e7"></a>
## TO_TIME_WITH_TIME_ZONE

<a id="1f3a240f2df25fca"></a>
### 구문

```
TO_TIME_WITH_TIME_ZONE( str [, fmt ] )
TO_TIME_TZ( str [, fmt ] )
```

<a id="243590ac10831383"></a>
### 설명

TO_TIME_WITH_TIME_ZONE 함수는 명시된 fmt 형식의 문자열 str을 TIME WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIME_WITH_TIME_ZONE_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#95e37f19cf8bd6a2)을 참조한다.  
자세한 내용은 [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#d8ed241efdbfc8ee)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

TO_TIME_WITH_TIME_ZONE의 alias로는 [TO_TIME_TZ](#09815ff744a36043) 함수가 있다.

결과 타입은 TIME WITH TIME ZONE 이다.

<a id="2c18535889eedaf0"></a>
### 사용 예

다음은 fmt가 생략되었고, NLS_TIME_WITH_TIME_ZONE_FORMAT = 'HH24:MI:SS.FF6 TZH:TZM' 인 경우의 예이다.

```
gSQL> SELECT 
      TO_TIME_WITH_TIME_ZONE( '11:22:33.999999 +09:00' ) AS RESULT 
      FROM DUAL;
RESULT                
----------------------
11:22:33.999999 +09:00
1 row selected.
```

다음은 fmt가 지정된 경우의 예이다.

```
gSQL> SELECT 
      TO_TIME_WITH_TIME_ZONE( '11:22:33.999999 +09:00 PM', 
                              'HH12:MI:SS.FF6 TZH:TZM PM' ) 
      AS RESULT 
      FROM DUAL;
RESULT                
----------------------
23:22:33.999999 +09:00
1 row selected.
```

<a id="48f2f9c2be120650"></a>
## TO_TIMESTAMP

<a id="d18bb6eeac7db550"></a>
### 구문

```
TO_TIMESTAMP( str [, fmt ] )
```

<a id="adc2be78989e627f"></a>
### 설명

TO_TIMESTAMP 함수는 명시된 fmt 형식의 문자열 str을 TIMESTAMP 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIMESTAMP_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#95e37f19cf8bd6a2)을 참조한다.  
자세한 내용은 [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#b83b0daa42003bc4)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

결과 타입은 TIMESTAMP 이다.

<a id="c928d384a01ed8ca"></a>
### 사용 예

다음은 fmt가 생략되었고, NLS_TIMESTAMP_FORMAT = 'YYYY-MM-DD HH24:MI:SS.FF6'' 인 경우의 예이다.

```
gSQL> SELECT 
      TO_TIMESTAMP( '2009-07-29 11:22:33.999999' ) AS RESULT 
      FROM DUAL;
RESULT                    
--------------------------
2009-07-29 11:22:33.999999
1 row selected.
```

다음은 fmt가 지정된 경우의 예이다.

```
gSQL> SELECT 
      TO_TIMESTAMP( '090729 112233999999 PM', 'YYMMDD HH12MISSFF6 PM' ) 
      AS RESULT 
      FROM DUAL;

RESULT                    
--------------------------
2009-07-29 23:22:33.999999
1 row selected.
```

<a id="06416af7336d7daf"></a>
## TO_TIMESTAMP_TZ

<a id="ef52658c353751fc"></a>
### 구문

```
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="0d7c107a1248253f"></a>
### 설명

TO_TIMESTAMP_WITH_TIME_ZONE의 alias 이다.  
자세한 내용은 [TO_TIMESTAMP_WITH_TIME_ZONE](#667ef9b2a77a0436)과 [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#8cf319a54a7fec34)을 참조한다.

<a id="1fefef6e5cb71be5"></a>
### 사용 예

다음은 fmt가 생략되었고, NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT = 'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM' 인 경우의 예이다.

```
gSQL> SELECT 
      TO_TIMESTAMP_TZ( '2009-07-29 11:22:33.999999 +09:00' ) AS RESULT 
      FROM DUAL;
RESULT                           
---------------------------------
2009-07-29 11:22:33.999999 +09:00
1 row selected.
```

다음은 fmt가 지정된 경우의 예이다.

```
gSQL> SELECT 
      TO_TIMESTAMP_TZ( '29-JUL-09 11:22:33.999999 +09:00',
                       'DD-MON-RR HH12:MI:SS.FF6 TZH:TZM' ) AS RESULT 
      FROM DUAL;
RESULT                           
---------------------------------
2009-07-29 11:22:33.999999 +09:00
1 row selected.
```

<a id="667ef9b2a77a0436"></a>
## TO_TIMESTAMP_WITH_TIME_ZONE

<a id="b345f11ea7c3bec2"></a>
### 구문

```
TO_TIMESTAMP_WITH_TIME_ZONE( str [, fmt ] )
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="b52e573bdb991f11"></a>
### 설명

TO_TIMESTAMP_WITH_TIME_ZONE 함수는 명시된 fmt 형식의 문자열 str을 TIMESTAMP WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#95e37f19cf8bd6a2)을 참조한다.  
자세한 내용은 [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#8cf319a54a7fec34)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

TO_TIMESTAMP_WITH_TIME_ZONE의 alias로는 [TO_TIMESTAMP_TZ](#06416af7336d7daf) 함수가 있다.

결과 타입은 TIMESTAMP WITH TIME ZONE 이다.

<a id="e38deb2ec5fbebad"></a>
### 사용 예

다음은 fmt가 생략되었고, NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT = 'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM' 인 경우의 예이다.

```
gSQL> SELECT 
      TO_TIMESTAMP_WITH_TIME_ZONE( '2009-07-29 11:22:33.999999 +09:00' ) 
      AS RESULT 
      FROM DUAL;
RESULT                           
---------------------------------
2009-07-29 11:22:33.999999 +09:00
1 row selected.
```

다음은 fmt가 지정된 경우의 예이다.

```
gSQL> SELECT 
      TO_TIMESTAMP_WITH_TIME_ZONE( '29-JUL-09 11:22:33.999999 +09:00',
                                   'DD-MON-RR HH12:MI:SS.FF6 TZH:TZM' ) 
      AS RESULT 
      FROM DUAL;
RESULT                           
---------------------------------
2009-07-29 11:22:33.999999 +09:00
1 row selected.
```

<a id="9b10ec80b2a03980"></a>
## TRANSACTION_DATE

<a id="cbc1996d81f6b16f"></a>
### 구문

```
TRANSACTION_DATE()
```

<a id="27193e355ab81477"></a>
### 설명

Session 시간을 기준으로 현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="989ed33a35384fb1"></a>
### 사용 예

동일한 transaction 내에서는 날짜 값이 항상 같다.

```
gSQL> SELECT TRANSACTION_DATE() FROM dual;

TRANSACTION_DATE()
------------------
2013-12-12        

1 row selected.

gSQL> SELECT TRANSACTION_DATE() FROM dual;

TRANSACTION_DATE()
------------------
2013-12-12        

1 row selected.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT TRANSACTION_DATE() FROM dual;

TRANSACTION_DATE()
------------------
2013-12-13        

1 row selected.
```

<a id="4a034746c1090f4f"></a>
## TRANSACTION_LOCALTIME

<a id="35ec3483fafa94c9"></a>
### 구문

```
TRANSACTION_LOCALTIME()
```

<a id="0eb8d80797f352a8"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 없는 현재 시간 (TIME WITHOUT TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="98a6e6721d2f0dbd"></a>
### 사용 예

동일한 transaction 내에서는 시간값이 항상 같다.

```
gSQL> SELECT TRANSACTION_LOCALTIME() FROM dual;

TRANSACTION_LOCALTIME()
-----------------------
16:43:24.391834        

1 row selected.

gSQL> SELECT TRANSACTION_LOCALTIME() FROM dual;

TRANSACTION_LOCALTIME()
-----------------------
16:43:24.391834        

1 row selected.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT TRANSACTION_LOCALTIME() FROM dual;

TRANSACTION_LOCALTIME()
-----------------------
16:43:32.651833        

1 row selected.
```

<a id="ff99817aedcfa218"></a>
## TRANSACTION_LOCALTIMESTAMP

<a id="d338cba51cca4d9a"></a>
### 구문

```
TRANSACTION_LOCALTIMESTAMP()
```

<a id="f56976e409d0eacf"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 없는 현재 TIMESTAMP (TIMESTAMP WITHOUT TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="f65bf4dc3c28b810"></a>
### 사용 예

동일한 transaction 내에서는 TIMESTAMP 값이 항상 같다.

```
gSQL> SELECT TRANSACTION_LOCALTIMESTAMP() FROM dual;

TRANSACTION_LOCALTIMESTAMP()
----------------------------
2013-12-12 16:43:32.651833  

1 row selected.

gSQL> SELECT TRANSACTION_LOCALTIMESTAMP() FROM dual;

TRANSACTION_LOCALTIMESTAMP()
----------------------------
2013-12-12 16:43:32.651833  

1 row selected.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT TRANSACTION_LOCALTIMESTAMP() FROM dual;

TRANSACTION_LOCALTIMESTAMP()
----------------------------
2013-12-12 16:46:07.831834  

1 row selected.
```

<a id="9ca27a5be131a69d"></a>
## TRANSACTION_TIME

<a id="5346975cd6d5ba19"></a>
### 구문

```
TRANSACTION_TIME()
```

<a id="dfa64fbb091815c4"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="64f5a8a7938befc0"></a>
### 사용 예

동일한 transaction 내에서는 시간값이 항상 같다.

```
gSQL> SELECT TRANSACTION_TIME() FROM dual;

TRANSACTION_TIME()    
----------------------
16:46:07.831834 +09:00

1 row selected.

gSQL> SELECT TRANSACTION_TIME() FROM dual;

TRANSACTION_TIME()    
----------------------
16:46:07.831834 +09:00

1 row selected.

gSQL> COMMIT;

Commit complete.

gSQL> SELECT TRANSACTION_TIME() FROM dual;

TRANSACTION_TIME()    
----------------------
16:48:00.691827 +09:00

1 row selected.
```

<a id="3b4cff9a30424ac1"></a>
## TRANSACTION_TIMESTAMP

<a id="3ca73131dffcf2dd"></a>
### 구문

```
TRANSACTION_TIMESTAMP()
```

<a id="88ad7e243d6d2881"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="f1b022f183c67147"></a>
### 사용 예

동일한 transaction 내에서는 TIMESTAMP 값이 항상 같다.

```
gSQL> SELECT TRANSACTION_TIMESTAMP() FROM dual;

TRANSACTION_TIMESTAMP()          
---------------------------------
2013-12-12 16:48:00.691827 +09:00

1 row selected.

gSQL> SELECT TRANSACTION_TIMESTAMP() FROM dual;

TRANSACTION_TIMESTAMP()          
---------------------------------
2013-12-12 16:48:00.691827 +09:00

1 row selected.

gSQL> COMMIT;

Commit complete.

gSQL>  SELECT TRANSACTION_TIMESTAMP() FROM dual;

TRANSACTION_TIMESTAMP()          
---------------------------------
2013-12-12 16:49:26.291827 +09:00

1 row selected.
```

<a id="2cfe96c173495d9a"></a>
## TRANSLATE

<a id="9202bc3f9976928e"></a>
### 구문

```
TRANSLATE( string, from, to )
```

<a id="653232d00597988c"></a>
### 설명

TRANSLATE는 문자를 치환하는 함수로써 from의 문자와 일치하는 string의 문자를 from의 문자와 같은 위치에 있는 to의 문자로 치환하여 반환한다.

인자 string, from, to에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

string, from, to 중의 하나라도 NULL이면 결과값도 NULL이다.

- from의 문자와 일치하는 string 문자가 있을 경우
    - from의 길이와 to의 길이가 같으면 from의 문자와 같은 위치에 있는 to의 문자로 치환한다.
    - from의 길이가 to의 길이보다 길면 to의 문자 길이 이후의 위치에 있는 from의 문자는 string에서 제거된다.
    - from의 문자가 중복된 문자로 이뤄져 있으면 from의 중복되는 문자의 첫 위치와 동일한 위치에 있는 to의 문자로 치환된다.
- from의 문자와 일치하는 string 문자가 없을 경우, string은 치환되지 않는다.

결과 타입은 다음 표와 같다.

**TRANSLATE의 결과 타입**

<a id="c1e8636c4528f792"></a>
| string 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="0ece10f3c851534b"></a>
### 사용 예

- from의 문자와 일치하는 string 문자가 있으면 같은 위치에 있는 to의 문자로 치환된다.
    - A → Z, C → Y, E → X, G → W

```
gSQL> SELECT TRANSLATE('ABCDEFG', 'ACEG', 'ZYXW') AS RESULT
FROM DUAL;
RESULT 
-------
ZBYDXFW
1 row selected.
```

- from의 문자열 길이가 to의 문자열 길이보다 길면, to의 문자열 길이 이후에 위치한 from의 문자는 string에서 제거되고 치환된다.
    - A → Z, C → Y, E 제거, G 제거

```
gSQL> SELECT TRANSLATE('ABCDEFG', 'ACEG', 'ZY') AS RESULT
      FROM DUAL;
RESULT
------
ZBYDF 
1 row selected.
```

<a id="06cfed983d14eaf0"></a>
## TRIM

<a id="e026cb40fb065c8d"></a>
### 구문

```
TRIM([ [ LEADING | TRAILING | BOTH ]  [trim_character] FROM ] trim_source)
```

<a id="e4d995dc91bcf2fb"></a>
### 설명

TRIM 함수는 trim_source에서 trim_character를 LEADING, TRAILING, BOTH 방향에서 비교하여 일치되는 문자가 없을 때까지 제거한 결과를 반환한다.

인자 trim_character와 trim_source에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

trim_character, trim_source 중 하나라도 NULL이면 결과값은 NULL이다.

- [ LEADING | TRAILING | BOTH ]
    - LEADING: trim_source의 앞부분부터 trim_character를 제거한다.
    - TRAILING: trim_source의 뒷부분부터 trim_character를 제거한다.
    - BOTH: trim_source의 앞뒤 양방향에서 trim_character를 제거한다.
- trim_character는 한 개의 문자만 허용된다.
- trim_character가 생략된 경우에는 single blank space (' ')가 기본적으로 지정된다.
- FROM이 지정된 경우
    - [ LEADING | TRAILING | BOTH ] 또는 trim_character 또는 [ LEADING | TRAILING | BOTH ] trim_character가 지정되어야 한다.
        - 예: TRIM( LEADING FROM ' abc' ) , TRIM( 'x' FROM 'xabc' ) , TRIM( LEADING 'x' FROM 'xabc' )
    - [ LEADING | TRAILING | BOTH ]이 생략된 경우에는 BOTH가 기본적으로 지정된다.
- FROM이 생략된 경우
    - TRIM( trim_source )인 경우이며 TRIM( BOTH ' ' FROM trim_source )과 동일하게 수행된다.

결과 타입은 다음 표와 같다.

**TRIM의 결과 타입**

<a id="b2aa94aa0fdb03df"></a>
| trim_character, trim_source 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="a45c58970766424c"></a>
### 사용 예

```
gSQL> SELECT TRIM( LEADING '_' FROM '___TRIM FUNCTION___' ) AS RESULT 
      FROM DUAL;
RESULT          
----------------
TRIM FUNCTION___
1 row selected.

gSQL> SELECT TRIM( TRAILING '_' FROM '___TRIM FUNCTION___' ) AS RESULT 
      FROM DUAL;
RESULT          
----------------
___TRIM FUNCTION
1 row selected.

gSQL> SELECT TRIM( BOTH '_' FROM '___TRIM FUNCTION___' ) AS RESULT 
      FROM DUAL;
RESULT       
-------------
TRIM FUNCTION
1 row selected.
```

<a id="c9dc8637f4717039"></a>
## TRUNC( number )

<a id="ffc101e771d52b84"></a>
### 구문

```
TRUNC( num [ , scale ] )
```

<a id="de49fa49899835a6"></a>
### 설명

TRUNC( number ) 함수는 scale 기준으로 num을 버림한 값을 반환한다.

인자 num과 scale에는 숫자 타입이 올 수 있다.  
인자 num 또는 scale이 NULL이면 NULL을 반환한다.

scale이 생략된 경우, scale은 0이 되어 TRUNC( num, 0 )일 때와 같이 실행된다.  
scale이 양수인 경우, 소수점 오른쪽 자리수를 기준으로 버림한다.  
scale이 음수인 경우, 소수점 왼쪽 자리수를 기준으로 버림한다.

<a id="735a61a7050df8a7"></a>
### 사용 예

```
gSQL> SELECT TRUNC( 142.4282, 2 ) AS RESULT FROM DUAL;
RESULT
------
142.42
1 row selected.

gSQL> SELECT TRUNC( 142.4282, -2 ) AS RESULT FROM DUAL;
RESULT
------
   100
1 row selected.
```

<a id="254ca85fec0f9d40"></a>
## TRUNC( date )

<a id="7aaad1894123dd2c"></a>
### 구문

```
TRUNC( date [ , fmt ] )
```

<a id="1f7ad7ef1f8d7b6c"></a>
### 설명

TRUNC( date ) 함수는 date를 지정된 fmt 단위로 버림한 값을 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
인자 date 또는 fmt이 NULL이면 NULL을 반환한다.

결과 타입은 인자로 받은 date 타입과 관계없이 항상 DATE 타입이다.

fmt가 생략되었을 경우의 기본값은 DAY이며, 사용 가능한 형식문자열은 다음 표와 같다.

**fmt에 사용가능한 형식문자열**

<a id="163e5b02958c23a9"></a>
| 형식문자열 | 설명 |
| --- | --- |
| CC, SCC | 세기 |
| YYYY, YEAR, SYYYY, SYEAR, YYY, YY, Y | 년 |
| IYYY, IYY, IY, I | ISO 8601 표준에 정의된 calendar week를 수용하는 연도 |
| Q | 분기 |
| MONTH, MON, MM, RM | 월 |
| WW | 연도의 1월 1일을 한 주로 시작하는 주 |
| IW | ISO 8601 표준에 정의된 calendar week (1~52주 또는 1~53주)로 지정된 연도의 첫 번째 목요일이 있는 주가 첫 번째 주 |
| W | 월의 1일을 한 주로 시작하는 주 |
| DDD, DD, J | 일 |
| DAY, DY, D | 요일 |
| HH, HH12, HH24 | 시 |
| MI | 분 |

<a id="ef49cf48b6a614f4"></a>
### 사용 예

```
gSQL> SELECT 
      TRUNC( TO_DATE( '2051-07-16', 'YYYY-MM-DD' ), 'CC' ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2001-01-01
1 row selected.

gSQL> SELECT 
      TRUNC( TO_DATE( '2051-07-16', 'YYYY-MM-DD' ), 'YYYY' ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2051-01-01
1 row selected.

gSQL> SELECT 
      TRUNC( TO_DATE( '2051-07-16', 'YYYY-MM-DD' ), 'MONTH' ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2051-07-01
1 row selected.

gSQL> SELECT 
      TRUNC( TO_TIMESTAMP( '2001-05-05 11:22:33.999999',         
             'YYYY-MM-DD HH24:MI:SS.FF6' ) ) AS RESULT 
      FROM DUAL;
RESULT    
----------
2001-05-05
1 row selected.
```

<a id="f76fb8f8d18ecc4d"></a>
## UPPER

<a id="e92cda3d33798bf3"></a>
### 구문

```
UPPER( str )
```

<a id="9463c9345682096a"></a>
### 설명

UPPER 함수는 str의 대문자를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.  
str이 NULL이면 결과값도 NULL이다.

반환되는 타입은 인자 str과 동일한 타입이다.

<a id="c3396f6f40dc3a21"></a>
### 사용 예

```
gSQL> SELECT UPPER( 'spring' ) AS RESULT FROM DUAL;
RESULT
------
SPRING
1 row selected.
```

<a id="7f7d06540fb972c9"></a>
## UNHEX

<a id="4120549ff8558e3d"></a>
### 구문

```
UNHEX( str )
```

<a id="0f3b4910fd537f6d"></a>
### 설명

인자 str은 16진수 문자이며, 이를 각 byte로 표현하여 binary string으로 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 BINARY VARYING이나 BINARY LONG VARYING과 같은 BINARY 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 16진수 범위에 속하지 않는 문자가 포함되면 에러를 반환한다.

자세한 내용은 [HEX](#de12493c5a02b161)를 참조한다.

<a id="11257eedac013b33"></a>
### 사용 예

```
gSQL> SELECT UNHEX( HEX( 'abc' ) ) FROM DUAL;
UNHEX( HEX( 'abc' ) )
---------------------
616263               
1 row selected.
```

<a id="fbccba95d47850a1"></a>
## UNHEX_TO_CHARSTR

<a id="935e8e2037d6d481"></a>
### 구문

```
UNHEX_TO_CHARSTR( str )
```

<a id="8c90ca202601b79b"></a>
### 설명

인자 str은 16진수 문자이며 이를 각 byte로 표현하여 character string으로 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 CHARACTER VARYING이나 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 16진수 범위에 속하지 않는 문자가 포함되면 에러를 반환한다.

자세한 내용은 [HEX](#de12493c5a02b161)와 [UNHEX](#7f7d06540fb972c9)를 참조한다.

<a id="7f4e4c1d29c41178"></a>
### 사용 예

```
gSQL> SELECT UNHEX_TO_CHARSTR( '616263' ) FROM DUAL;
UNHEX_TO_CHARSTR( '616263' )
----------------------------
abc                         
1 row selected.

gSQL> SELECT UNHEX_TO_CHARSTR( HEX( 'abc' ) ) FROM DUAL;
UNHEX_TO_CHARSTR( HEX( 'abc' ) )
--------------------------------
abc                             
1 row selected.
```

<a id="1021d52d545afbb0"></a>
## USER_ID

<a id="2d92634879c66573"></a>
### 구문

```
USER_ID ()
```

<a id="4894e672dc9cc5be"></a>
### 설명

현재 사용자의 number ID를 얻는다.

> Cluster system에서는 접속한 server에 따라 다른 값을 가질 수 있다.  
> 현재 사용자의 이름을 얻는 [CURRENT_USER](#b74ed317d4b03cd1) 함수 사용을 권장한다.

<a id="c45bee25c76efa0e"></a>
### 사용 예

```
% gsql test test

gSQL> SELECT USER_ID() FROM dual;

USER_ID()
---------
        6

1 row selected.
```

<a id="90a906b332bd5922"></a>
## UUID

<a id="226a5d19a7ad42a2"></a>
### 구문

```
UUID()
```

<a id="6ef31d6931acfcc3"></a>
### 설명

UUID 함수는 전역고유식별자 (Universal Unique Identifier) 를 생성하여 반환한다.  
반환되는 타입은 VARBINARY 이며 내부적으로 16 바이트로 구성된다.

<a id="57dd038d4e4bd47b"></a>
### 사용 예

```
gSQL> SELECT HEX( UUID() ) FROM DUAL;
HEX( UUID() )                   
--------------------------------
E6F0A5C2387511E8B95259E479C2FD50
1 row selected.
```

<a id="3c837bf115b1008a"></a>
## VAR_POP

<a id="17c198ced45435e9"></a>
### 구문

```
VAR_POP( expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="26c5f9cb82e48695"></a>
### 설명

Aggregation 함수로써 expr set의 모 분산 (population variance)을 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 0을 반환한다.

FILTER를 명시한 경우 condition을 만족하는 값들에 한하여 aggregation을 수행한다.

인자와 결과 타입은 다음 표와 같다.

**VAR_POP 인자와 결과 타입**

<a id="565d5cc9901dcccd"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 분산은 모 집단 (전체)의 분산이며 분산은 편차 제곱의 평균이다. 즉, 데이터의 각 값에서 모 평균 (전체의 평균)을 빼고 제곱해서 모두 더한 뒤 모 집단의 데이터 개수로 나눈다.  
> 이는 각 관찰값들이 평균으로부터 얼마나 많이 퍼져있는지 파악하는데 사용된다.

자세한 내용은 [STDDEV_POP](#0a4728846b8e14ba)을 참조한다.

<a id="ffea443a6cf0569f"></a>
### 사용 예

```
gSQL> SELECT VAR_POP(c1) FROM t1;

VAR_POP(C1)
-----------
     105.76

1 row selected.


gSQL> SELECT VAR_POP(c1) FILTER( WHERE c1 > 0 ) FROM t1;

VAR_POP(C1)
-----------
     105.76

1 row selected.
```

<a id="99f8aaa14ba889ca"></a>
## VAR_POP() OVER

<a id="59a26e532282a3d8"></a>
### 구문

```
VAR_POP ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="c945a6a267c37442"></a>
### 설명

Window function VAR_POP은 expr의 모 분산 (population variance)을 구하는 함수이다.  
NULL 값을 제외한 expr이 한 개일 경우, 결과로 0을 반환한다.

<a id="a0c7334ee38b0369"></a>
### 사용 예

```
gSQL> SELECT product_id, min_price
             , VAR_POP( min_price ) OVER ( ORDER BY product_id ) AS "VAR_POP"
        FROM product_information
       WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE          VAR_POP
---------- --------- ----------------
      1769      null             null
      1770        73                0
      2378       247             7569
      2382       731 77499.5555555556
      3355      null 77499.5555555556

5 rows selected.
```

<a id="dc962b0b48f04aed"></a>
## VAR_SAMP

<a id="cdf1b34fef18f083"></a>
### 구문

```
VAR_SAMP( expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="95d6e20e1ff73314"></a>
### 설명

Aggregation 함수로써 expr set의 표본 분산 (sample variance)을 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 NULL값을 반환한다.

FILTER를 명시한 경우 condition을 만족하는 값들에 한하여 aggregation을 수행한다.

인자와 결과 타입은 다음 표와 같다.

**VAR_SAMP 인자와 결과 타입**

<a id="18674e0a18351abd"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 집단 (전체)을 다루는 모 분산과 달리, 표본 분산은 추출한 표본으로 평균과 편차를 다룬다. 즉, 데이터의 각 값에서 표본의 평균을 빼고 제곱해서 모두 더한 뒤, 표본 집단의 데이터 개수 - 1로 나눈다.  
> 이는 모 집단의 분산을 추정하는 데 사용된다.

자세한 내용은 [STDDEV_SAMP](#76f1f4a01a39aaf0)을 참조한다.

<a id="9229e79b8d569515"></a>
### 사용 예

```
gSQL> SELECT VAR_SAMP(c1) FROM t1;

VAR_SAMP(C1)
------------
       132.2

1 row selected.


gSQL> SELECT VAR_SAMP(c1) FILTER( WHERE c1 > 0 ) FROM t1;

VAR_SAMP(C1)
------------
       132.2

1 row selected.
```

<a id="c444a0ff2efb2aae"></a>
## VAR_SAMP() OVER

<a id="f3e0cbacd79ee11f"></a>
### 구문

```
VAR_SAMP ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="3bfb4ea452d0389f"></a>
### 설명

Window function VAR_SAMP는 expr의 표본 분산 (sample variance)을 구하는 함수이다.  
NULL 값을 제외한 expr이 한 개일 경우, 결과로 NULL을 반환한다.

<a id="f3b41652c6d08cc4"></a>
### 사용 예

```
gSQL> SELECT product_id, min_price
             , VAR_SAMP( min_price ) OVER ( ORDER BY product_id ) AS "VAR_SAMP"
        FROM product_information
       WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE         VAR_SAMP
---------- --------- ----------------
      1769      null             null
      1770        73             null
      2378       247            15138
      2382       731 116249.333333333
      3355      null 116249.333333333

5 rows selected.
```

<a id="ab8b6a136b382960"></a>
## VARIANCE

<a id="00a520b008be1159"></a>
### 구문

```
VARIANCE( [ ALL | DISTINCT ] expr ) [ FILTER ( [ WHERE ] condition ) ]
```

<a id="35ae36583f3989fd"></a>
### 설명

Aggregation 함수로써 expr set의 분산 (variance)을 얻는다.

ALL을 명시한 경우 모든 값들에 대해 수행하고, DISTINCT를 명시한 경우 중복을 제거한 값들에 대해 수행한다. 둘 다 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

NULL 값을 제외하고 DISTINCT로 중복을 제거한 후의 expr set의 개수가 한 개일 경우, 0을 반환한다.

FILTER를 명시한 경우 condition을 만족하는 값들에 한하여 aggregation을 수행한다.

인자와 결과 타입은 다음 표와 같다.

**VARIANCE 인자와 결과 타입**

<a id="367b7d7077344ae6"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> GOLDILOCKS는 분산을 다음과 같이 계산한다.  
> 　• expr set의 개수가 1이면 0을 반환한다.  
> 　• expr set의 개수가 1보다 크면 [VAR_SAMP( exp )](#dc962b0b48f04aed) 값을 반환한다.

<a id="381e21c7ce254b82"></a>
### 사용 예

```
gSQL> SELECT VARIANCE(c1) FROM t1;

VARIANCE(C1)
------------
       132.2

1 row selected.


gSQL> SELECT VARIANCE(ALL c1) FROM t1;

VARIANCE(ALL C1)
----------------
           132.2

1 row selected.


gSQL> SELECT VARIANCE(DISTINCT c1) FROM t1;

VARIANCE(DISTINCT C1)
---------------------
               176.25

1 row selected.


gSQL> SELECT VARIANCE(c1) FILTER( WHERE c1 > 0 ) FROM t1;

VARIANCE(C1)
------------
       132.2

1 row selected.
```

<a id="75eb00197e439b14"></a>
## VARIANCE() OVER

<a id="339e229389f1a661"></a>
### 구문

```
VARIANCE ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

<a id="d818fac9adedab26"></a>
### 설명

Window function VARIANCE는 expr의 분산 (variance)을 구하는 함수이다.  
NULL 값을 제외한 expr이 한 개일 경우, 결과로 0을 반환한다.

<a id="7ca36cc632613b66"></a>
### 사용 예

```
gSQL> SELECT product_id, min_price
             , VARIANCE( min_price ) OVER ( ORDER BY product_id ) AS "VARIANCE"
        FROM product_information
       WHERE supplier_id = 102050;

PRODUCT_ID MIN_PRICE         VARIANCE
---------- --------- ----------------
      1769      null             null
      1770        73                0
      2378       247            15138
      2382       731 116249.333333333
      3355      null 116249.333333333

5 rows selected.
```

<a id="de255a4e725990b5"></a>
## VERSION

<a id="53e2fa208edccc8f"></a>
### 구문

```
VERSION()
```

<a id="a3368a830373ce4b"></a>
### 설명

제품의 version string을 얻는다.

<a id="74d0f149449490c9"></a>
### 사용 예

```
gSQL> SELECT VERSION() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="3ca6f7a7fdf7ba43"></a>
## WIDTH_BUCKET

<a id="59b160b9811201b2"></a>
### 구문

```
WIDTH_BUCKET( num, min, max, cnt )
```

<a id="409d3885d3d6186d"></a>
### 설명

WIDTH_BUCKET 함수는 명시된 min, max 범위에서 cnt와 동일한 넓이를 갖는 구간을 생성하고, num이 속하는 구간의 위치를 반환한다.

인자 num, min, max, cnt에는 숫자 타입이 올 수 있다.

min, max는 구간에 대한 범위를 의미하며, min, max 값이 같은 경우에는 에러를 반환한다.  
cnt는 구간 개수를 의미하고 양의 정수이어야 하며 0 이거나 음수인 경우에는 에러를 반환한다.  
구간의 위치에는 1부터 시작하는 번호가 부여된다.

num, min, max, cnt 중 하나라도 NULL인 경우, 결과값도 NULL이다.

<a id="64d45c5efbb77c52"></a>
### 사용 예

```
gSQL> SELECT WIDTH_BUCKET( 5, 1, 20, 5 ) AS RESULT FROM DUAL;
RESULT
------
     2
1 row selected.
```

---

[← 16. Built-in Data Type References](16-built-in-data-type-references.md) · [전체 목차](../README.md) · [18. SQL References (A~B) →](18-sql-references-a-b.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
