<a id="822295347c70e20d"></a>

# 17. Built-in Function References

> 원본: [GOLDILOCKS 21c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/21c_1/manual/ko/822295347c70e20d)  
> 태그: `21c.1_35_tag`

[← 16. Built-in Data Type References](16-built-in-data-type-references.md) · [전체 목차](../README.md) · [18. SQL References (A~B) →](18-sql-references-a-b.md)

<a id="af997730fa70be3b"></a>
## * (MULTIPLICATION)

<a id="036bbbb03bbce6ff"></a>
### 구문

```
expr1 * expr2
```

<a id="393859214f2f42fe"></a>
### 설명

expr1과 expr2의 곱하기 연산 결과를 반환한다.

곱하기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#989fb42b7e593473)을 참조한다.

**숫자형 * 연산**

<a id="767666ee25f43c32"></a>
| expr1 (expr2) | expr2 (expr1) | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="d7cdf9ce849d8a98"></a>
<table class="table column_count_3"><caption>INTERVAL * 연산 </caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>숫자형 타입</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>숫자형 타입</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_left" colspan="3"><div>자세한 내용은 <a class="reference text" href="#81d43d118f6fb7f8">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

**표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입**

<a id="81d43d118f6fb7f8"></a>
<table><thead><tr><th align="center">INTERVAL YEAR TO MONTH</th><th align="center">INTERVAL DAY TO SECOND</th></tr></thead><tbody><tr><td valign="middle"><ul><li>INTERVAL YEAR</li><li>INTERVAL MONTH</li><li>INTERVAL YEAR TO MONTH</li></ul></td><td valign="middle"><ul><li>INTERVAL DAY</li><li>INTERVAL HOUR</li><li>INTERVAL MINUTE</li><li>INTERVAL SECOND</li><li>INTERVAL DAY TO HOUR</li><li>INTERVAL DAY TO MINUTE</li><li>INTERVAL DAY TO SECOND</li><li>INTERVAL HOUR TO MINUTE</li><li>INTERVAL HOUR TO SECOND</li><li>INTERVAL MINUTE TO SECOND</li></ul></td></tr></tbody></table>

<a id="150d4386ccbf6ad2"></a>
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

<a id="db13b63b957824aa"></a>
## + (ADDITION)

<a id="3f1f75a3cabf9958"></a>
### 구문

```
expr1 + expr2
```

<a id="0c8c2d002f70a0db"></a>
### 설명

expr1과 expr2의 더하기 연산 결과를 반환한다.

더하기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#989fb42b7e593473)을 참조한다.

**숫자형 + 연산**

<a id="171f5dd508e1f0ff"></a>
| expr1 (expr2) | expr2 (expr1) | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="05a59fb0fe50dbae"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) + 연산</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#81d43d118f6fb7f8">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="510525c85aa94263"></a>
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

<a id="13a37274c0deceb9"></a>
## + (POSITIVE)

<a id="bb30fe8f4dd3e040"></a>
### 구문

```
+ expr
```

<a id="fb800197bd784a72"></a>
### 설명

expr에 + 부호를 표시한다.

<a id="bb313f92658417fb"></a>
### 사용 예

```
gSQL> SELECT +3 AS RESULT1, +(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      3      -3
1 row selected.
```

<a id="64ea5f260518054b"></a>
## - (NEGATIVE)

<a id="02923ef9413fa962"></a>
### 구문

```
- expr
```

<a id="8585972144a3f5e4"></a>
### 설명

expr에 - 부호를 표시한다.

<a id="da3b23a636891138"></a>
### 사용 예

```
gSQL> SELECT -3 AS RESULT1, -(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     -3       3
1 row selected.
```

<a id="70163cb329be5f55"></a>
## - (SUBTRACTION)

<a id="a9b13f14ef30fdc1"></a>
### 구문

```
expr1 - expr2
```

<a id="fe7bf449a0aa743d"></a>
### 설명

expr1과 expr2의 뺄셈 연산 결과를 반환한다.

뺄셈 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#989fb42b7e593473)을 참조한다.

**숫자형 - 연산**

<a id="d34abbd845a55b0c"></a>
| expr1 | expr2 | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="fa79742da0f3bdd2"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) - 연산</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMBER</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#81d43d118f6fb7f8">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="fff6411d9b2735b4"></a>
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

<a id="9c2f18800d554e32"></a>
## / (DIVISION)

<a id="d7f92967707be179"></a>
### 구문

```
expr1 / expr2
```

<a id="bcee9310089dd22a"></a>
### 설명

expr1과 expr2의 나누기 연산 결과를 반환한다.

나누기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#989fb42b7e593473)을 참조한다.

**숫자형/ 연산**

<a id="d997dc214435c8b0"></a>
| expr1 | expr2 | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER | NUMBER |
| NATIVE_DOUBLE | NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="d066c120224128d1"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL)/ 연산</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(결과 타입은 interval type 이다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#81d43d118f6fb7f8">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="79c42a1af6e858a6"></a>
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

<a id="eb1de4ad06cd1eb0"></a>
## || (CONCATENATE)

<a id="dd4ecd2d62eef771"></a>
### 구문

```
str1 || str2
```

<a id="9e1e23bec17845c9"></a>
### 설명

CONCATENATE는 str1과 str2를 연결한 문자열을 반환한다.

str1과 str2 중 하나가 null인 경우 null이 아닌 나머지 str이 반환되고, str1과 str2가 모두 null인 경우 NULL이 반환된다.

인자로는 character string 타입 또는 binary string 타입으로 변환될 수 있는 타입이 올 수 있다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#989fb42b7e593473)을 참조한다.

[CONCAT](#8e412ddd8eee59b0), [CONCATENATE](#5abbc874e791d306)의 alias 이다.

결과 타입은 다음 표와 같다.

**|| (CONCATENATE)의 결과 타입**

<a id="875dc6f2ca899064"></a>
| Data type | CHAR | VARCHAR | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR | CHAR | VARCHAR | LONG VARCHAR |
| VARCHAR | VARCHAR | VARCHAR | LONG VARCHAR |
| LONG VARCHAR | LONG VARCHAR | LONG VARCHAR | LONG VARCHAR |
| Data type | BINARY | VARBINARY | LONG VARBINARY |
| BINARY | BINARY | VARBINARY | LONG VARBINARY |
| VARBINARY | VARBINARY | VARBINARY | LONG VARBINARY |
| LONG VARBINARY | LONG VARBINARY | LONG VARBINARY | LONG VARBINARY |

<a id="3492dbe6064dc976"></a>
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

<a id="029105ad43ff6473"></a>
## ABS

<a id="3f98e42479342a42"></a>
### 구문

```
ABS( num )
```

<a id="711a7094bf60451f"></a>
### 설명

ABS는 num의 절대값을 반환한다.  

인자 num에는 숫자 타입 또는 숫자로 변환될 수 있는 타입이 올 수 있다.  
num이 NULL이면 NULL을 반환한다.

<a id="017d22b3f2e50f30"></a>
### 사용 예

```
gSQL> SELECT ABS(-1) AS RESULT1, ABS(1) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1       1
1 row selected.
```

<a id="d50090dcf05a544b"></a>
## ACOS

<a id="565bb0ca16d7f3d7"></a>
### 구문

```
ACOS( num )
```

<a id="27d4bc53f56ff626"></a>
### 설명

ACOS 함수는 num의 arc cosine 값을 반환한다.  

인자 num은 -1 이상 1 이하의 값이어야 한다.  
num이 NULL이면 NULL을 반환한다.  

0 ~ pi 사이의 라디안 값을 반환한다.

<a id="2e7505fc55685297"></a>
### 사용 예

```
gSQL> SELECT ACOS( 1 ) FROM DUAL;
ACOS( 1 )
---------
        0
1 row selected.
```

<a id="8155528e40a56dc6"></a>
## ADDDATE

<a id="da92d409323a7848"></a>
### 구문

```
ADDDATE( date, INTERVAL expr unit  )
ADDDATE( expr, days )
```

<a id="9655b06f864016f1"></a>
### 설명

ADDDATE는 입력받은 첫 번째 인자에 두 번째 인자를 더하기 연산하여 그 결과를 반환한다.  

첫 번째 인자에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있고, 두 번째 인자에는 INTERVAL 또는 숫자 타입이 올 수 있다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.

결과 타입은 [(DATETIME/INTERVAL) + 연산](#05a59fb0fe50dbae)과 동일하다.

<a id="e1e370114500c587"></a>
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

<a id="b020b78089e822e1"></a>
## ADDTIME

<a id="b71b5a46dad9a6f5"></a>
### 구문

```
ADDTIME( expr1, expr2 )
```

<a id="06b7dac7e053a79a"></a>
### 설명

ADDTIME은 입력받은 expr2를 expr1에 더하여 그 결과를 반환한다.

expr1에는 TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE TYPE이 올 수 있고, expr2에는 INTERVAL DAY TO SECOND TYPE이 올 수 있다.  

expr1이나 expr2가 NULL이면 결과값은 NULL이다.

결과 타입은 [(DATETIME/INTERVAL) + 연산](#05a59fb0fe50dbae)과 동일하다.

<a id="d680c6039348fdc9"></a>
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

<a id="19eaaefc29187c9a"></a>
## ADD_MONTHS

<a id="a401f83376d93f7a"></a>
### 구문

```
ADD_MONTHS( date, number )
```

<a id="39c0a632807b58be"></a>
### 설명

ADD_MONTHS는 date에 number 숫자만큼의 달을 더한 값을 반환한다.  
만약 ADD_MONTHS 연산 후에 날짜가 그 달의 마지막 날보다 큰 경우에는 마지막 날짜로 조정한다.  

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있으며 인자 number에는 숫자타입이 올 수 있다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.

결과 타입은 입력 인자 date 타입과 관계없이 항상 DATE 타입이다.

<a id="6fee51738697931b"></a>
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

<a id="7046f0f931aee593"></a>
## ASCII

<a id="75f3c70b2aa15cd7"></a>
### 구문

```
ASCII( char )
```

<a id="fca60d5c92027db8"></a>
### 설명

char의 첫 번째 문자에 대한 database character set code를 십진수로 반환한다.

char에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있고, 반환되는 타입은 NUMBER 이다.  
char가 NULL이면 NULL을 반환한다.

<a id="49e18afaf49c6c80"></a>
### 사용 예

```
gSQL> SELECT ASCII( 'G' ) AS RESULT FROM DUAL;
RESULT
------
    71
1 row selected.
```

<a id="412e44507672db47"></a>
## ASIN

<a id="44248fd40af49ad2"></a>
### 구문

```
ASIN( num )
```

<a id="890f181d59dad32b"></a>
### 설명

ASIN 함수는 num의 arc sin 값을 반환한다.

인자 num은 -1 이상 1 이하의 값이어야 한다.  
num이 NULL이면 NULL을 반환한다.

-pi/2 ~ pi/2 사이의 라디안 값을 반환한다.

<a id="5fba7e4583fda14e"></a>
### 사용 예

```
gSQL> SELECT ASIN( 0 ) FROM DUAL;
ASIN( 0 )
---------
        0
1 row selected.
```

<a id="1f037917d8d2fa63"></a>
## ATAN

<a id="5f7e83aa8f5ff9d0"></a>
### 구문

```
ATAN( num )
```

<a id="5c6998119f455b78"></a>
### 설명

ATAN 함수는 num의 arc tangent 값을 반환한다.

num 값 범위의 제한은 없으며, -pi/2 ~ pi/2 사이의 라디안 값을 반환한다.   
num이 NULL이면 NULL을 반환한다.

<a id="708bfdfe21e5c3bf"></a>
### 사용 예

```
gSQL> SELECT ATAN(0.5) FROM DUAL;
       ATAN(0.5)
----------------
.463647609000806
1 row selected.
```

<a id="b9490de1ccd6ba74"></a>
## ATAN2

<a id="82706e9ba686171f"></a>
### 구문

```
ATAN2( num1, num2 )
```

<a id="7ce2b2573dedfd19"></a>
### 설명

ATAN2 함수는 num1과 num2의 arc tangent 값을 반환한다.

인자 num1 값 범위의 제한은 없으며 -pi ~ pi 사이의 라디안 값을 반환한다.   
num1 또는 num2 중 하나라도 NULL이면 NULL을 반환한다.

<a id="df858a8943c6d014"></a>
### 사용 예

```
gSQL> SELECT ATAN2(1,2) FROM DUAL; 
      ATAN2(1,2)
----------------
.463647609000806
1 row selected.
```

<a id="038e004a4c8081ac"></a>
## AVG

<a id="955206e736c63082"></a>
### 구문

```
AVG( [ ALL | DISTINCT ] num )
```

<a id="4eebe7d22d0319d8"></a>
### 설명

Aggregation 함수로써 expr 들의 평균값을 얻는데 사용된다.

ALL을 명시한 경우, 모든 값들에 대한 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복 제거한 값들에 대한 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

<a id="9bb3df1e44ff9488"></a>
### 사용 예

```
gSQL> SELECT AVG(c1) FROM t1;

AVG(C1)
-------
      2

1 row selected.
```

<a id="60566ba476b28747"></a>
## BITAND

<a id="812648c5030b3ce8"></a>
### 구문

```
BITAND( num1, num2 )
```

<a id="e233e86b69d9e518"></a>
### 설명

num1과 num2의 비트에 대한 AND 연산 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.

결과 타입은 NATIVE_BIGINT이다.

<a id="fdc93fdcca447bec"></a>
### 사용 예

```
gSQL> SELECT BITAND(2, 4) FROM DUAL;
BITAND(2, 4)
------------
           0
1 row selected.
```

<a id="0026cac7fa48b3ca"></a>
## BITNOT

<a id="bc298f2ed2f7960e"></a>
### 구문

```
BITNOT( num )
```

<a id="93af6bb216762ee7"></a>
### 설명

num의 비트에 대해 NOT 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자가 NULL이면 결과값도 NULL이다.

결과 타입은 다음과 같다.  
• 입력 인자가 NATIVE_SMALLINT인 경우, NATIVE_SMALLINT  
• 입력 인자가 NATIVE_INTEGER인 경우, NATIVE_INTEGER  
• 입력 인자가 NATIVE_BIGINT인 경우, NATIVE_BIGINT

<a id="f9d64190b61bd08f"></a>
### 사용 예

```
gSQL> SELECT BITNOT( 5 ) AS RESULT FROM DUAL;
RESULT
------
    -6
1 row selected.
```

<a id="adaf07a2bfb70dd6"></a>
## BITOR

<a id="7d48aba773e2f0c0"></a>
### 구문

```
BITOR( num1, num2 )
```

<a id="e00ab2b176ed389d"></a>
### 설명

num1과 num2의 비트에 대해 OR 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자의 값이 하나라도 NULL이면 결과는 NULL이다.

결과 타입은 NATIVE_BIGINT이다.

<a id="18056c41e69cb8b9"></a>
### 사용 예

```
gSQL> SELECT BITOR( 2, 4 ) FROM DUAL;
BITOR( 2, 4 )
-------------
            6
1 row selected.
```

<a id="72fdc6b7372f55e3"></a>
## BITXOR

<a id="4938d41570037e4c"></a>
### 구문

```
BITXOR( num1, num2 )
```

<a id="9c54f3e585a246bc"></a>
### 설명

num1과 num2의 비트에 대해 XOR 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자의 값이 하나라도 NULL이면 결과는 NULL이다.

결과 타입은 NATIVE_BIGINT이다.

<a id="64c224580d788d45"></a>
### 사용 예

```
gSQL> SELECT BITXOR( 5, 3 ) FROM DUAL;
BITXOR( 5, 3 )
-------------
            6
1 row selected.
```

<a id="c5dabaf7c7fc95da"></a>
## BIT_LENGTH

<a id="04d95bca00881ae8"></a>
### 구문

```
BIT_LENGTH( str )
```

<a id="150b019f36ddd019"></a>
### 설명

BIT_LENGTH는 str의 비트 수를 반환한다.  
str이 NULL이면 NULL을 반환한다.

<a id="a3517da01e63a8b0"></a>
### 사용 예

```
gSQL> SELECT BIT_LENGTH( 'LIKE' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
             32
    1 row selected.
```

<a id="25e0a6a386a0a2d3"></a>
## BYTE_LENGTH

<a id="8d0f6e21aae08779"></a>
### 구문

```
BYTE_LENGTH( str )
```

<a id="2cf63359e8a5a3ca"></a>
### 설명

OCTET_LENGTH의 alias이다.  
자세한 내용은 [OCTET_LENGTH](#35d190ce222da53e), [LENGTHB](#e79ab79dbaf95eb5)를 참조한다.

<a id="c6d3d1033642c2c4"></a>
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

<a id="df2d1b3270188299"></a>
## CASE2

<a id="8e97f0194a0f47c9"></a>
### 구문

```
CASE2( condition1, result1
      [, condition2, result2
       , ...
       , conditionN, resultN ]
      [, default ] )
```

<a id="2af85f20205fd325"></a>
### 설명

CASE2는 기술된 순서대로 condition을 평가한다.  
비교 결과가 FALSE이면 TRUE가 나올 때까지 평가한다.  
비교 결과가 TRUE이면 대응되는 result를 반환하고, 이후는 평가하지 않는다.  
비교 결과가 모두 FALSE인 경우에는 default를 반환하고, default가 생략된 경우에는 NULL을 반환한다.

result에 여러 type이 오는 경우, [결과 타입 조합 규칙](11-sql-elements.md#6c6b5ffe8b689af0)에 따라 result type이 결정된다.

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

<a id="d61afb47fae0e194"></a>
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

<a id="192a2bfde9804073"></a>
## CBRT

<a id="0943e1dec0d873b6"></a>
### 구문

```
CBRT( num )
```

<a id="2e25e82b2de576b5"></a>
### 설명

num의 세제곱근을 반환한다.  
num이 NULL이면 결과값도 NULL이 반환된다.

<a id="0e8136fef692d694"></a>
### 사용 예

```
gSQL> SELECT CBRT( 27 ) FROM DUAL;
CBRT( 27 )
----------
         3
1 row selected.
```

<a id="94f8b4f19b45fa6a"></a>
## CEIL

<a id="7c2860833df64921"></a>
### 구문

```
CEIL( num )
CEILING( num )
```

<a id="9db98c5a73f17518"></a>
### 설명

CEIL 함수는 num 보다 크거나 같은 가장 작은 정수를 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="9bd6143d94913834"></a>
### 사용 예

```
gSQL> SELECT CEIL( 3.5 ) AS RESULT1, CEIL( -3.5 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      4      -3
1 row selected.
```

<a id="9ae0e8baccb95b89"></a>
## CHAR_LENGTH

<a id="045b53130fe6ad1f"></a>
### 구문

```
CHAR_LENGTH( str )            
CHARACTER_LENGTH( str )
```

<a id="dcfdf5d6e2d74493"></a>
### 설명

CHAR_LENGTH는 str에 대해 character set에 따른 문자수를 반환한다.

str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있고, 반환되는 타입은 NATIVE_BIGINT 이다.

str의 타입이 CHARACTER 타입이면 공백문자 (trailing blank)를 포함하여 계산한다.  
str이 NULL이면 NULL이 반환된다.

[LENGTH](#e6e7e718d44b4153)의 alias이다.

<a id="df3844bdcfc9e764"></a>
### 사용 예

Multi byte character set: (예:UTF8)

```
gSQL> SELECT CHAR_LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="8bec9eb5c5a928fc"></a>
## CHR

<a id="566a96c33dd07bab"></a>
### 구문

```
CHR( num )
```

<a id="426edf1ead991105"></a>
### 설명

num에 대응하는 database character set code 내의 charater를 반환한다.

num은 숫자 타입이다.  
num이 NULL이면 NULL을 반환한다.  

결과 타입은 VARCHAR 이다.

<a id="7082caacfc455fca"></a>
### 사용 예

```
gSQL> SELECT CHR(71) FROM DUAL;
CHR(71)
-------
G      
1 row selected.
```

<a id="2e1917090958b23d"></a>
## CLOCK_DATE

<a id="c8fc028b052f19ce"></a>
### 구문

```
CLOCK_DATE()
```

<a id="932834706a0e1b5c"></a>
### 설명

함수가 호출될 때마다 현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="126c44cb85a298eb"></a>
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

<a id="931c185df04c8ec4"></a>
## CLOCK_LOCALTIME

<a id="2cd1e4c9d612eab3"></a>
### 구문

```
CLOCK_LOCALTIME()
```

<a id="ac99e4c513c6fb0b"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 없는 현재 시간 (TIME WITHOUT TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="dc0c2093894ba8a3"></a>
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

<a id="a7b2d06a17a4ec23"></a>
## CLOCK_LOCALTIMESTAMP

<a id="39bbc8d1838e48a6"></a>
### 구문

```
CLOCK_LOCALTIMESTAMP()
```

<a id="62b3e29d3cf4ec76"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 없는 현재 TIMESTAMP (TIMESTAMP WITHOUT TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="676955ec35ae0d0e"></a>
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

<a id="61c7b84fe6cb3c2d"></a>
## CLOCK_TIME

<a id="034de717da676911"></a>
### 구문

```
CLOCK_TIME()
```

<a id="5f63fc618289d17e"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="9ac67e2b95566ebd"></a>
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

<a id="904b7618db274017"></a>
## CLOCK_TIMESTAMP

<a id="f2c5fbe41951c1b2"></a>
### 구문

```
CLOCK_TIMESTAMP()
```

<a id="6d7e70fc69c82bec"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="20898d998913d839"></a>
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

<a id="c5ca4dde81d1b8aa"></a>
## COALESCE

<a id="83a173a282b28f8f"></a>
### 구문

```
COALESCE( expr1, ..., exprN )
```

<a id="33c254f73837b71b"></a>
### 설명

expr list들 중에 null이 아닌 첫 번째 expr을 반환한다.  
expr list들이 모두 null인 경우에는 null을 반환한다.  
expr은 두 개 이상이어야 한다.

expr list에 여러 type들이 오는 경우에는 [결과 타입 조합 규칙](11-sql-elements.md#6c6b5ffe8b689af0)에 따라 result type이 결정된다.

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

<a id="8227cea413b44ad1"></a>
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

<a id="8e412ddd8eee59b0"></a>
## CONCAT

<a id="f9b6033413792ca5"></a>
### 구문

```
CONCAT( str1, str2, ... )
```

<a id="8b7f50f7a6ef59eb"></a>
### 설명

\|| ( CONCATENATE )의 alias 이다.  
CONCAT 함수의 argument로써 2 ~ 254 개까지 설정할 수 있다.  
자세한 내용은 [|| (CONCATENATE)](#eb1de4ad06cd1eb0), [CONCATENATE](#5abbc874e791d306)를 참조한다.

<a id="3c8a59f1382d2a10"></a>
### 사용 예

```
gSQL> SELECT CONCAT( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="5abbc874e791d306"></a>
## CONCATENATE

<a id="513a7c8923aa5118"></a>
### 구문

```
CONCATENATE( str1, str2, ... )
```

<a id="17f2c404682acf39"></a>
### 설명

\|| ( CONCATENATE ) 의 alias 이다.  
CONCATENATE 함수의 argument로 2 ~ 254 개까지 설정할 수 있다.  
자세한 내용은 [CONCAT](#8e412ddd8eee59b0), [|| (CONCATENATE)](#eb1de4ad06cd1eb0)를 참조한다.

<a id="382749c6c6de12de"></a>
### 사용 예

```
gSQL> SELECT CONCATENATE( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="10c8c79caaf09e32"></a>
## COS

<a id="e12bde57f487e632"></a>
### 구문

```
COS(num)
```

<a id="f9681a8f1c4d4fae"></a>
### 설명

num의 COSINE 값을 반환한다.  
인자값 num이 NULL이면 결과값도 NULL이다.

<a id="5e3be98b4dbbd222"></a>
### 사용 예

```
gSQL> SELECT COS( 0 ) FROM DUAL;
COS( 0 )
--------
       1
1 row selected.
```

<a id="c55eca582abab1f7"></a>
## COT

<a id="194f3d08ed0fe88d"></a>
### 구문

```
COT(num)
```

<a id="65a7b1fc5460cd94"></a>
### 설명

num의 COTANGENT 값을 반환한다.  
인자값 num이 NULL이면 결과값도 NULL이다.

<a id="dc96bf217dcf6b3b"></a>
### 사용 예

```
gSQL> SELECT COT( 1 ) FROM DUAL;
        COT( 1 )
----------------
.642092615934331
1 row selected.
```

<a id="6dae358719e753b9"></a>
## COUNT

<a id="65d5780e3aec25d9"></a>
### 구문

```
COUNT( [ ALL | DISTINCT ] expr )
```

<a id="19a0d5d8dd26349f"></a>
### 설명

Aggregation 함수로써 expr이 NULL 값이 아닌 row의 개수를 얻는다.

ALL을 명시한 경우, 모든 값들에 대한 aggregation을 수행한다.  
DISTINCT을 명시한 경우, 중복 제거한 값들에 대한 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

<a id="d31091f84bedb6e7"></a>
### 사용 예

```
gSQL> SELECT COUNT(c1) FROM t1;

COUNT(C1)
---------
        3

1 row selected.
```

<a id="974eea80802f256d"></a>
## COUNT(*)

<a id="040c42c5d8cf3cac"></a>
### 구문

```
COUNT(*)
```

<a id="26a113d796389bb3"></a>
### 설명

Aggregation 함수로써 row의 개수를 얻는다.   
별도의 expression을 지정하지 않으므로 값의 NULL 여부와 무관하다.

<a id="117d20013caf05f1"></a>
### 사용 예

```
gSQL> SELECT COUNT(*) FROM t1;

COUNT(*)
--------
       4

1 row selected.
```

<a id="1c3594571c058054"></a>
## CURRENT_CATALOG

<a id="8a4d39c910dab6ce"></a>
### 구문

```
CURRENT_CATALOG [()]
```

<a id="ad2d2d3eb53b5676"></a>
### 설명

catalog name (database 이름)을 얻는다.

<a id="86092afb27cbf726"></a>
### 사용 예

```
gSQL> SELECT CURRENT_CATALOG FROM dual;

CURRENT_CATALOG
---------------
TEST_DB        

1 row selected.
```

<a id="b3e140ddcf9d499a"></a>
## CURRENT_DATE

<a id="ad61670e2076ca84"></a>
### 구문

```
CURRENT_DATE [()]
STATEMENT_DATE()
```

<a id="6fc6333b0b22cf49"></a>
### 설명

현재 날짜 (DATE type) 값을 얻는다.

CURRENT_DATE는 SQL 표준 함수이다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• CURRENT_DATE, STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="9fabfede61cc4c90"></a>
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

<a id="77732dd3353e6821"></a>
## CURRENT_SCHEMA

<a id="bf5a6a6b1d5efb24"></a>
### 구문

```
CURRENT_SCHEMA [()]
```

<a id="6457e28ef15b3539"></a>
### 설명

사용자의 현재 SCHEMA를 얻는다.

<a id="fdbd41e3e967b64f"></a>
### 사용 예

```
gSQL> SELECT CURRENT_SCHEMA FROM dual;

CURRENT_SCHEMA
--------------
PUBLIC        

1 row selected.
```

<a id="3469686fb426b33d"></a>
## CURRENT_TIME

<a id="6d821cad1e60ef94"></a>
### 구문

```
CURRENT_TIME [()]
STATEMENT_TIME()
```

<a id="79427f6484a9b80a"></a>
### 설명

Session 시간을 기준으로 현재 TIME WITH TIME ZONE type 값을 얻는다.

CURRENT_TIME은 SQL 표준 함수이다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• CURRENT_TIME, STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="eb6b39d7e979b99b"></a>
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

<a id="cd6d299d197b8fdc"></a>
## CURRENT_TIMESTAMP

<a id="63abff93673f4790"></a>
### 구문

```
CURRENT_TIMESTAMP [()]
STATEMENT_TIMESTAMP()
```

<a id="75de4fa73e15ef78"></a>
### 설명

Session 시간을 기준으로 TIMESTAMP WITH TIME ZONE type 값을 얻는다.

CURRENT_TIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• CURRENT_TIMESTAMP, STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="022bdc30d788d132"></a>
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

<a id="1b9a25dc057af2e2"></a>
## CURRENT_USER

<a id="4734425f1f8f3af0"></a>
### 구문

```
CURRENT_USER [()]
```

<a id="5728ce22c307d67c"></a>
### 설명

현재 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다.
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다.
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다.
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="c8fb4e08b9bf13e1"></a>
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

<a id="aec74f0a0f494b5c"></a>
## CURRVAL

<a id="9535bb120b7b052e"></a>
### 구문

```
seq_name.CURRVAL
CURRVAL(seq_name)
```

<a id="420cb87315b371de"></a>
### 설명

시퀀스 객체의 현재 값을 얻는다.

최소 한 번은 NEXTVAL(seq_name) 등으로 시퀀스 값을 설정해야 한다.

<a id="73b7a16a0589139d"></a>
### 사용 예

```
gSQL> SELECT seq.CURRVAL FROM dual;

SEQ.CURRVAL
-----------
          1

1 row selected.
```

<a id="00edc6f6ee526056"></a>
## DATEADD

<a id="3ecabcc9a52cd644"></a>
### 구문

```
DATEADD( datepart, number, date )
```

<a id="488fee0c9ac669b6"></a>
### 설명

date의 지정된 datepart에 number를 더한 값을 반환한다.

number가 소수점인 경우 반올림되지 않는다.  
date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE 타입이 올 수 있다.  
number 또는 date가 NULL인 경우에는 결과값도 NULL이다.

인자로 받은 date의 타입과 동일한 결과 타입이 반환된다.

**datepart에 사용 가능한 형식문자열**

<a id="a0d397b1848d128f"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">설명</th></tr><tr><td>YEAR</td><td>년</td></tr><tr><td>QUARTER</td><td>분기</td></tr><tr><td>MONTH</td><td>월</td></tr><tr><td>DAYOFYEAR</td><td>일</td></tr><tr><td>DAY</td><td>요일</td></tr><tr><td>WEEK</td><td>주</td></tr><tr><td>WEEKDAY</td><td>평일</td></tr><tr><td>HOUR</td><td>시</td></tr><tr><td>MINUTE</td><td>분</td></tr><tr><td>SECOND</td><td>초</td></tr><tr><td>MILLISECOND</td><td>밀리세컨드</td></tr><tr><td>MICROSECOND</td><td>마이크로세컨드</td></tr></tbody></table>

<a id="0d6d1daf251b6169"></a>
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

<a id="232dcf9a5fceba80"></a>
## DATEDIFF

<a id="612c4f64b1f8e35b"></a>
### 구문

```
DATEDIFF( datepart, startdate, enddate )
```

<a id="7f07b824118752ad"></a>
### 설명

enddate에서 startdate를 뺀 값을 지정된 datepart로 반환한다.

startdate와 enddate에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME TYPE이 올 수 있다.  
startdate 또는 enddate가 NULL이면 결과값도 NULL이다.

결과 타입은 NUMBER이다.

**datepart에 사용 가능한 형식문자열**

<a id="852d03b39a9a3edf"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">설명</th></tr><tr><td>YEAR</td><td>년</td></tr><tr><td>QUARTER</td><td>분기</td></tr><tr><td>MONTH</td><td>월</td></tr><tr><td>DAYOFYEAR</td><td>일</td></tr><tr><td>DAY</td><td>요일</td></tr><tr><td>HOUR</td><td>시</td></tr><tr><td>MINUTE</td><td>분</td></tr><tr><td>SECOND</td><td>초</td></tr><tr><td>MILLISECOND</td><td>밀리세컨트</td></tr><tr><td>MICROSECOND</td><td>마이크로세컨드</td></tr></tbody></table>

<a id="509c02c71c1a33d9"></a>
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

<a id="4ab8da44ea09379c"></a>
## DATE_ADD

<a id="817f2d7edf2c15b2"></a>
### 구문

```
DATE_ADD( date, INTERVAL expr unit  )
```

<a id="7006a7ca2a2602b5"></a>
### 설명

[ADDDATE](#8155528e40a56dc6) ( date, INTERVAL expr unit )와 동일한 함수이다.

<a id="456e6974419eaeb8"></a>
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

<a id="06fb17e12584a19d"></a>
## DATE_PART

<a id="9ba6b2c2b1031173"></a>
### 구문

```
DATE_PART( field, datetime )
```

<a id="d82c1cfd9a7a226b"></a>
### 설명

DATE_PART는 EXTRACT 함수와 결과값이 같은 함수로써 입력한 datetime 타입에서 지정된 field를 찾아 반환한다.

인자 field에는 문자 literal만 올 수 있으며, YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, TIMEZONE_HOUR, TIMEZONE_MINUTE를 문자 literal로 지정할 수 있다.  
인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.

field가 datetime의 범위에 있지 않는 경우 에러를 반환한다.  
또한, DATE 타입인 경우에는 field에 YEAR, MONTH, DAY 만 올 수 있고, 그 외에는 에러를 반환한다.  
datatime이 NULL이면 NULL을 반환한다.  

반환되는 타입은 NUMBER이다.

자세한 내용은 [EXTRACT](#eaf8c9856f496517)를 참조한다.

<a id="7b23944155043f31"></a>
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

<a id="7f32d27119030479"></a>
## DECODE

<a id="aa4ef9d19228f7cf"></a>
### 구문

```
DECODE( expr, comparison_expr1, result1
           [, comparison_expr2, result2
            , ...
            , comparison_exprN, resultN ]
           [, default ] )
```

<a id="bf2929dfcd4082fb"></a>
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

<a id="8ef8573603e1095e"></a>
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

<a id="2e1bb3386a11a4a5"></a>
## DEGREES

<a id="23c47ff21ab01743"></a>
### 구문

```
DEGREES( radians )
```

<a id="22f8191792076c46"></a>
### 설명

라디안 단위로 표시된 각도 radians를 도 단위로 변환한 값을 반환한다.  
radians가 NULL이면 NULL이 반환된다.

<a id="2fd8890bc13aff55"></a>
### 사용 예

```
gSQL> SELECT DEGREES( PI() ) AS RESULT FROM DUAL;
RESULT
------
   180
1 row selected.
```

<a id="80b22b5947a8bb93"></a>
## DIGEST

<a id="c56b46fdfc71bf25"></a>
### 구문

```
DIGEST( data, type )
```

<a id="604153c93025295c"></a>
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

<a id="4d5b2d27e0aab5b6"></a>
### 사용 예

```
gSQL> SELECT HEX( DIGEST( 'my password', 'SHA256' ) ) AS RESULT FROM DUAL;

RESULT                                                          
----------------------------------------------------------------
BB14292D91C6D0920A5536BB41F3A50F66351B7B9D94C804DFCE8A96CA1051F2

1 row selected.
```

<a id="73fa81e0cd63ccdd"></a>
## DUMP

<a id="16f37b7c39f2d580"></a>
### 구문

```
DUMP( expr )
```

<a id="3660d7c02fc54062"></a>
### 설명

DUMP 함수는 expr의 내부 표현정보를 반환한다.  
내부 표현정보는 데이터 타입, 길이 (byte length), 데이터 정보로 보여준다.

expr에는 모든 타입이 가능하다.  
expr이 NULL이면 NULL을 반환한다.  

반환되는 타입은 CHARACTER VARYING이다.

<a id="456b03b872a41b08"></a>
### 사용 예

```
gSQL> SELECT DUMP( 'DUMP' ) AS RESULT FROM DUAL;
RESULT                           
---------------------------------
Type=CHAR Len=4 : Str=68,85,77,80
1 row selected.
```

<a id="8fb56f36ae981831"></a>
## EXP

<a id="ddab3f1fb05d8753"></a>
### 구문

```
EXP( num )
```

<a id="f818469c4b5c026f"></a>
### 설명

EXP 함수는 e (자연로그 베이스)의 num의 제곱값을 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="d4162a11fb1a043e"></a>
### 사용 예

```
gSQL> SELECT EXP( 1 ) AS RESULT FROM DUAL;
          RESULT
----------------
2.71828182845905
1 row selected.
```

<a id="eaf8c9856f496517"></a>
## EXTRACT

<a id="eaccfff1babc4d4f"></a>
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

<a id="275ab78c1a41fb8a"></a>
### 설명

EXTRACT는 입력한 datetime 타입에서 지정된 field를 찾아 반환한다.

인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.

field가 datetime의 범위에 있지 않는 경우에는 에러를 반환한다.  
또, DATE 타입인 경우에는 field에 YEAR, MONTH, DAY만 올 수 있고, 그 외의 경우에는 에러를 반환한다.  
반환되는 타입은 NUMBER이다.

EXTRACT 함수의 결과는 [DATE_PART](#06fb17e12584a19d)와 동일하다.

<a id="0cb58dce2a65a8b8"></a>
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

<a id="78b7d775ef70bbb6"></a>
## FACTORIAL

<a id="8e8a023a07956a94"></a>
### 구문

```
FACTORIAL( num )
```

<a id="8e088df17171c0ea"></a>
### 설명

FACTORIAL 함수는 1 ~ num 까지의 연속된 자연수를 차례로 곱한 값을 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="387c396fa3285571"></a>
### 사용 예

```
gSQL> SELECT FACTORIAL( 5 ) AS RESULT FROM DUAL;
RESULT
------
   120
1 row selected.
```

<a id="517d80f8a80d0ee2"></a>
## FLOOR

<a id="579fd39e4feacf8e"></a>
### 구문

```
FLOOR( num )
```

<a id="b42efc6bda106800"></a>
### 설명

FLOOR 함수는 num 보다 크지 않은 가장 큰 정수를 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="ff1953b9605173a3"></a>
### 사용 예

```
gSQL> SELECT FLOOR(42.8) AS RESULT1, FLOOR(-42.8) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     42     -43
1 row selected.
```

<a id="81bb5bf2cda8e6cc"></a>
## FROM_BASE64

<a id="822c879fd11f08fa"></a>
### 구문

```
FROM_BASE64( str )
```

<a id="a2b9bd86ed702e12"></a>
### 설명

FROM_BASE64는 base64 인코딩으로 변환된 문자를 입력 받아 디코딩된 binary string을 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 BINARY VARYING 또는 BINARY LONG VARYING과 같은 BINARY 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 base64 문자 범위에 속하지 않는 문자가 포함되면, 에러를 반환한다.  
디코딩 할 때 str의 newline, carriage return, tab, space는 무시된다.

자세한 내용은 [TO_BASE64](#d9af2a22021e0c5a)를 참조한다.

<a id="dfba5309785cd9f7"></a>
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

<a id="5afecf371a5e4324"></a>
## FROM_TZ

<a id="d0349f1f2aa00472"></a>
### 구문

```
FROM_TZ( timestamp, timezone )
```

<a id="0ce0b36cf00cb578"></a>
### 설명

FROM_TZ 함수는 timestamp와 정해진 format의 timezone을 TIMESTAMP WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 timestamp는 TIMESTAMP 타입이거나 TIMESTAMP 타입으로 변환이 가능해야 한다.   
인자 timestamp가 NULL이면 결과는 NULL이다.

인자 timezone은 CHARACTER, CHARACTER VARYING와 같은 CHARACTER 문자 타입이어야 하며, format은 'TZH:TZM'이다.   
인자 timezone이 NULL이면 결과는 NULL이다.

결과 타입은 TIMESTAMP(6) WITH TIME ZONE 이다.

<a id="be36e6ad1febdd9f"></a>
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

<a id="78766de31e1413c9"></a>
## GREATEST

<a id="e10f01d2bab99fdc"></a>
### 구문

```
GREATEST( expr1 [, expr2, ... exprn ] )
```

<a id="5b257a7f3525f5d7"></a>
### 설명

GREATEST 함수는 인자로 받은 expr들 중에 가장 큰 값을 반환한다.

인자로 받은 expr들 중 하나라도 NULL인 경우, 결과값은 NULL이다.

결과 타입은 expr1 (첫 번째 expr)의 데이터 타입이다.  
expr1 (첫 번째 expr)의 데이터 타입이 숫자형인 경우와 문자형인 경우는 각각 expr1, ..., exprN의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, ..., exprN에 모두 CHAR 타입이 기술된 경우, 모든 expr은 VARCHAR 타입으로 비교되고, 결과 타입은 VARCHAR 타입으로 결정된다.

<a id="565a27da8f6fd3a7"></a>
### 사용 예

```
gSQL> SELECT GREATEST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
   200
1 row selected.
```

<a id="ee0de90d79a88820"></a>
## HASH32

<a id="0efa520b9ff610b2"></a>
### 구문

```
HASH32( expr [, expr]... )
```

<a id="288bfad181cd5922"></a>
### 설명

HASH32 함수는 인자로 받은 expr들의 해시값을 계산하여 반환한다.

인자는 최소 1개부터 최대 32개까지 기술할 수 있다.  
입력 인자에 하나라도 NULL이 포함되어 있으면 결과값은 NULL이다.

결과 타입은 NATIVE_INTEGER 타입이다.

<a id="ff3a4106c22650cf"></a>
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

<a id="74db15c6a19d6e5e"></a>
## HEX

<a id="d50ad9533d59a8f2"></a>
### 구문

```
HEX( str )
```

<a id="becfa78ab48e1b31"></a>
### 설명

인자 str을 16진수 문자로 반환한다.  
인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입 또는 문자 타입으로 변환될 수 있는 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.  
결과 타입은 CHARACTER VARYING 또는 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.

HEX 함수의 인자로 숫자타입이 오는 경우에는 에러를 반환한다.  
10진수 숫자를 16진수로 변환하고자 하는 경우에는  'X' number format을 이용한 TO_CHAR() 함수를 사용할 수 있다.  
예: TO_CHAR( 255, 'XX' )

자세한 내용은 [UNHEX](#ad3481b3c1a32b46)를 참조한다.

<a id="471a63e0b3b08e14"></a>
### 사용 예

```
gSQL> SELECT HEX( 'abc' ) FROM DUAL;
HEX( 'abc' )
------------
616263      
1 row selected.
```

<a id="efe01af27e53ba4b"></a>
## INITCAP

<a id="0bf1d88247418088"></a>
### 구문

```
INITCAP( str )
```

<a id="4c2b479d0fb0cc49"></a>
### 설명

INITCAP 함수는 주어진 문자열 str의 각 단어들의 첫 번째 문자를 대문자로 변환하고 첫 번째 문자 이후의 문자를 소문자로 변환하여 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.

문자열의 각 단어는 white space, 알파벳 또는 숫자가 아닌 문자로 구분한다.  
str이 NULL이면 결과값도 NULL이다.

인자로 받는 str의 타입과 동일한 타입이 반환된다.

<a id="f47f2d23848d7b28"></a>
### 사용 예

```
gSQL> SELECT INITCAP( 'hi GLIESE' ) AS RESULT FROM DUAL;
RESULT   
---------
Hi Gliese
1 row selected.
```

<a id="20fcf46e73b8c05f"></a>
## INSTR

<a id="fac61f23f2c78e08"></a>
### 구문

```
INSTR( str, substr [, position [, occurrence ] ] )
```

<a id="f97a054860308810"></a>
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

<a id="858934ba27a9c6c3"></a>
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

<a id="0d7ebddf7dc8cec0"></a>
## LAST_DAY

<a id="2fe6580104b638da"></a>
### 구문

```
LAST_DAY( date )
```

<a id="189f3581de8217e3"></a>
### 설명

LAST_DAY 함수는 date에 포함된 월의 마지막 날짜를 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
반환되는 타입은 인자 date의 타입에 상관없이 항상 DATE이다.  

date가 NULL이면 NULL을 반환한다.

<a id="898119a7a68c196f"></a>
### 사용 예

```
gSQL> SELECT 
      LAST_DAY( TO_DATE( '2012-07-10', 'YYYY-MM-DD' ) ) AS RESULT FROM DUAL;
RESULT    
----------
2012-07-31
1 row selected.
```

<a id="fa116f65a7a51b74"></a>
## LAST_IDENTITY_VALUE

<a id="a64bd42c5dc4cb4e"></a>
### 구문

```
LAST_IDENTITY_VALUE()
```

<a id="9460e000c1b149b3"></a>
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

INSERT 할 때 생성된 identity column의 값을 얻으려면 다음과 같이 [INSERT INTO name RETURNING .. INTO](20-sql-references-h-z.md#4973f950df1e0e03) 구문을 사용한다.

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

<a id="519286e227b0eb3e"></a>
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

<a id="2c20856ed4ab8e73"></a>
## LEAST

<a id="89f37d3c562a70a1"></a>
### 구문

```
LEAST( expr1 [, expr2, ... exprn ] )
```

<a id="c8317280717cdf21"></a>
### 설명

LEAST 함수는 인자로 받은 expr들 중에 가장 작은 값을 반환한다.

인자로 받은 expr들 중 하나라도 NULL인 경우, 결과값은 NULL이다.

결과 타입은 expr1 (첫 번째 expr)의 데이터 타입에 따라 결정된다.  
expr1 (첫 번째 expr)의 데이터 타입이 숫자형인 경우와 문자형인 경우에는 각각 expr1, ..., exprN의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, ..., exprN에 모두 CHAR 타입이 기술된 경우, 모든 expr은 VARCHAR 타입으로 비교되고, 결과 타입은 VARCHAR 타입이 된다.

<a id="379617e640d39095"></a>
### 사용 예

```
gSQL> SELECT LEAST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="e6e7e718d44b4153"></a>
## LENGTH

<a id="e9d01bfd437e8cf1"></a>
### 구문

```
LENGTH( str )
```

<a id="d65458ece1004d7d"></a>
### 설명

[CHAR_LENGTH](#9ae0e8baccb95b89)의 alias 이다.

<a id="cd76ac726ceb4355"></a>
### 사용 예

Multi byte character set: (예: UTF8)

```
gSQL> SELECT LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="e79ab79dbaf95eb5"></a>
## LENGTHB

<a id="129d1d930b362b6f"></a>
### 구문

```
LENGTHB( str )
```

<a id="0313e4f7962f1940"></a>
### 설명

OCTET_LENGTH의 alias이다.  
자세한 내용은 [OCTET_LENGTH](#35d190ce222da53e), [BYTE_LENGTH](#25e0a6a386a0a2d3)를 참조한다.

<a id="f723e0d1c3e7b995"></a>
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

<a id="9f4abcff31a6c8d7"></a>
## LN

<a id="a44398c4a43fafc0"></a>
### 구문

```
LN( num )
```

<a id="7f2c7b916a3dcc08"></a>
### 설명

LN 함수는 num의 자연 로그 값을 반환하는 함수이다.  

num은 0보다 큰 값이어야 한다.  
num이 NULL이면 NULL을 반환한다.

<a id="9669b9a2676fc383"></a>
### 사용 예

```
gSQL> SELECT LN( 2.71828182845905 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="6aa3540ccb96f3e5"></a>
## LNNVL

<a id="dca7c28e31e46131"></a>
### 구문

```
LNNVL( expr )
```

<a id="f8ed9766630c5fd1"></a>
### 설명

Logical Not Null VaLue (LNNVL) 함수는 NOT logical operator와 유사하지만 다음 예제와 같이 입력값이 null일 경우 TRUE를 반환한다는 차이가 있다.

<a id="6802d70c3ee18365"></a>
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

<a id="2d359318c4254077"></a>
## LOCALTIME

<a id="944adfab04e1765c"></a>
### 구문

```
LOCALTIME [()]
STATEMENT_LOCALTIME()
```

<a id="b2d14b43a5fb4a16"></a>
### 설명

Session 시간을 기준으로 현재 TIME WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• LOCALTIME, STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="445107be56e1ea1b"></a>
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

<a id="a5096307b8fa5bfc"></a>
## LOCALTIMESTAMP

<a id="2f8884aa3cc117ca"></a>
### 구문

```
LOCALTIMESTAMP [()]
STATEMENT_LOCALTIMESTAMP()
```

<a id="7999526d07dddda6"></a>
### 설명

Session 시간을 기준으로 현재 TIMESTAMP WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• LOCALTIMESTAMP, STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="e0afb24236c0c454"></a>
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

<a id="6ec5e646352c3f3e"></a>
## LOCAL_GROUP_ID

<a id="4f15d65b50e0a97d"></a>
### 구문

```
LOCAL_GROUP_ID()
```

<a id="79d7ef61fdbe1423"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster group ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="5f646dd6d49b6e84"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_GROUP_ID() FROM DUAL;

LOCAL_GROUP_ID()
----------------
               1

1 row selected.
```

<a id="551cfdccc39fc5f3"></a>
## LOCAL_GROUP_NAME

<a id="80b1d0b1af768f65"></a>
### 구문

```
LOCAL_GROUP_NAME()
```

<a id="db5cb1c2d5200edd"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster group name을 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="14f51744f43e2480"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_GROUP_NAME() FROM DUAL;

LOCAL_GROUP_NAME()
------------------
G1                

1 row selected.
```

<a id="6bd794742f5341d9"></a>
## LOCAL_MEMBER_ID

<a id="61f192061c17b62d"></a>
### 구문

```
LOCAL_MEMBER_ID()
```

<a id="8fa5d64fb7d04564"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster member ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="ebbe0371ea138077"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_MEMBER_ID() FROM DUAL;

LOCAL_MEMBER_ID()
-----------------
                1

1 row selected.
```

<a id="5598ac912dba365f"></a>
## LOCAL_MEMBER_NAME

<a id="3071221fe950d939"></a>
### 구문

```
LOCAL_MEMBER_NAME()
```

<a id="382335e76e64573f"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster member name을 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="d354c3d63bc5c4de"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_MEMBER_NAME() FROM DUAL;

LOCAL_MEMBER_NAME()
-------------------
G1N1               

1 row selected.
```

<a id="6b06a31a803355ab"></a>
## LOG

<a id="6d4cd2abf8ce9af0"></a>
### 구문

```
LOG( num2 )
LOG( num1, num2 )
```

<a id="3e9f5953fb75446d"></a>
### 설명

LOG 함수는 밑이 num1인 num2의 로그값을 반환한다.  
num1이 생략된 경우에는 밑이 10으로 계산된 값이 반환된다.

num1은 1과 0이 아닌 양수이어야 하고, num2는 양수이어야 한다.

num1 또는 num2가 NULL이면 NULL을 반환한다.

<a id="7cd405e043796924"></a>
### 사용 예

```
gSQL> SELECT LOG( 100 ) AS RESULT1, LOG( 4, 16 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      2       2
1 row selected.
```

<a id="3dc1aaa26b309756"></a>
## LOGON_USER

<a id="cda6b5557c1b9c2a"></a>
### 구문

```
LOGON_USER()
```

<a id="50a13c1b31116338"></a>
### 설명

로그인 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다.
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다.
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다.
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="3b6770aebc48e4ff"></a>
### 사용 예

```
% gsql test test

gSQL> SELECT LOGON_USER() AS result FROM DUAL;

RESULT
------
TEST  

1 row selected.
```

<a id="342a3fe68604f849"></a>
## LOWER

<a id="c05e9372130c4a5d"></a>
### 구문

```
LOWER( str )
```

<a id="24174121e341dfad"></a>
### 설명

LOWER 함수는 str의 소문자를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.  
str이 NULL이면 결과값도 NULL이다.

인자 str과 동일한 타입이 반환된다.

<a id="04610e13975ef690"></a>
### 사용 예

```
gSQL> SELECT LOWER( 'SPRING' ) AS RESULT FROM DUAL;
RESULT
------
spring
1 row selected.
```

<a id="dbaee6114a8fa843"></a>
## LPAD

<a id="87071fd5d95a390c"></a>
### 구문

```
LPAD( str, length, [, fill] )
```

<a id="a037b9ec6f2fdbd0"></a>
### 설명

LPAD 함수는 string의 길이가 length가 될 때까지 str의 왼쪽에 문자열 fill을 추가한 값을 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER  문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

인자 length에는 숫자 타입이 올 수 있다.

length는 문자의 개수를 의미하며, 최대 범위는 결과 타입의 최대 PRECISION이다.  
fill이 생략된 경우, 공백 문자가 추가된다.  
str이 length보다 길이가 긴 경우에는 str을 length만큼 잘라서 반환한다.  
str, length, fill이 하나라도 NULL이면 결과값도 NULL이며, length가 0 또는 음수인 경우에도 결과값은 NULL이다.

결과 타입은 다음 표와 같다.

**LPAD의 결과 타입**

<a id="3053c54921ec4e51"></a>
| 인자 str의 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="952d5fe5506b5ec8"></a>
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

<a id="e829e58666056b81"></a>
## LTRIM

<a id="88948d4899e2085f"></a>
### 구문

```
LTRIM( trim_source [, trim_character ] )
```

<a id="507a999c23b7cfd9"></a>
### 설명

LTRIM 함수는 trim_source에서 trim_character를 왼쪽 방향에서 비교하여 일치하는 문자가 없을 때까지 제거한 결과를 반환한다.

인자 trim_character와 trim_source에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

trim_character, trim_source 중 하나라도 NULL이면, 결과값은 NULL이다.  
trim_character가 생략된 경우에는 기본적으로 single blank space (' ')가 지정된다.

결과 타입은 다음과 같다.

**LTRIM의 결과 타입**

<a id="b662324e8e84ae67"></a>
| trim_source, trim_character 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="7c66bbf6f36a16ba"></a>
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

<a id="800d2fb1c54a4734"></a>
## MAX

<a id="39776c4fd54941e8"></a>
### 구문

```
MAX( [ ALL | DISTINCT ] expr )
```

<a id="e0a5cc1a11efa079"></a>
### 설명

Aggregation 함수로써 row들의 expr 중 최대값을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복을 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

MAX는 ALL과 DISTINCT에 영향을 받지 않고 동일한 결과를 낸다.

<a id="a6f5a43d97e88922"></a>
### 사용 예

```
gSQL> SELECT MAX(c1) FROM t1;

MAX(C1)
-------
      3

1 row selected.
```

<a id="646bfb8179bb295e"></a>
## MIN

<a id="29634cf593f1ee95"></a>
### 구문

```
MIN( [ ALL | DISTINCT ] expr )
```

<a id="2510008fd7c4fa9c"></a>
### 설명

Aggregation 함수로써 row들의 expr 중 최소값을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

MIN은 ALL과 DISTINCT에 영향을 받지 않고 동일한 결과를 낸다.

<a id="9da05606802eb700"></a>
### 사용 예

```
gSQL> SELECT MIN(c1) FROM t1;

MIN(C1)
-------
      1

1 row selected.
```

<a id="fa5068891222a0a6"></a>
## MOD

<a id="004fedd59655c3db"></a>
### 구문

```
MOD( num1, num2 )
```

<a id="3d4aa111def68540"></a>
### 설명

MOD는 num1을 num2로 나눈 나머지를 반환한다.  

인자 num1, num2에는 숫자타입이 올 수 있다.  
num2가 0이면 에러를 반환한다.  
인자 num1 또는 num2가 NULL이면 NULL을 반환한다.

<a id="da63ae1cd1edf2b9"></a>
### 사용 예

```
gSQL> SELECT MOD(5, 4) AS RESULT1, MOD(-5, 4) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1      -1
1 row selected.
```

<a id="fd33291a939c4da2"></a>
## MONTHS_BETWEEN

<a id="4c9c7196c0a68c43"></a>
### 구문

```
MONTHS_BETWEEN( date1, date2 )
```

<a id="4d191181e01d8613"></a>
### 설명

MONTHS_BETWEEN은 date2와 date1 사이의 일수를 31로 나눈 개월 수를 반환한다.

date1 또는 date2가 NULL이면 결과도 NULL이다.  
인자 date1, date2에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.

결과 타입은 NUMBER 이다.

> date1과 date2 모두에 동일한 날짜가 포함되어 있거나 (예: 2014-01-15 와 2014-02-15) 월의 마지막 날짜가 포함되어 있는 경우 (예: 2014-08-31와 2014-09-30), 타임스탬프 구간 (있는 경우)의 일치 여부와 상관없이 정수 결과를 반환한다.

<a id="9c360610e5456eaa"></a>
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

<a id="db3dd9eac6a042b0"></a>
## NEXT_DAY

<a id="37691af3e4418ea5"></a>
### 구문

```
NEXT_DAY( date, day )
```

<a id="3e910409257ba2bf"></a>
### 설명

인자로 주어진 date (날짜)를 지나 처음으로 도래하는 day (요일)의 날짜를 구한다.

두 번째 인자 day에는 day를 지칭하는 스트링 또는 숫자가 올 수 있다.  
• 스트링:  SUNDAY ~ SATURDAY  또는 SUN ~ SAT  
• 숫자:  1 (sunday) ~ 7 (saturday)  

입력 인자 중 하나라도 NULL이면 결과값도 NULL이다.

반환되는 타입은 date의 입력 타입에 상관없이 항상 DATE 타입이다.  
결과값의 시분초는 입력 인자 date의 시분초를 동일하게 반환한다.

<a id="a3da325c401df088"></a>
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

<a id="d36ad8ad2fda2581"></a>
## NEXTVAL

<a id="942830e80f8e6732"></a>
### 구문

```
seq_name.NEXTVAL
NEXTVAL( seq_name )
NEXT VALUE FOR seq_name
```

<a id="ea3475d97f00a4f6"></a>
### 설명

시퀀스 객체의 다음 값을 얻는다.

<a id="dd0739d85e33a882"></a>
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

<a id="8244c8ae106a4b4a"></a>
## NULLIF

<a id="f69a1b2d42e16ae4"></a>
### 구문

```
NULLIF( expr1, expr2 )
```

<a id="db1e834402cc2ed6"></a>
### 설명

expr1과 expr2가 같으면 null을 반환하고, 같지 않으면 첫 번째 인자인 expr1을 반환한다.

expr1과 expr2의 타입이 서로 다를 경우, [결과 타입 조합 규칙](11-sql-elements.md#6c6b5ffe8b689af0)에 따라 result type이 결정된다.

NULLIF는 CASE를 사용하여 동일하게 표현할 수 있다.

- NULLIF( expr1, expr2 )

```
CASE WHEN expr1 = expr2 THEN NULL 
       ELSE expr1 
  END
```

<a id="c7f513e29b494ed4"></a>
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

<a id="0798c8b515a1a2d9"></a>
## NUMTODSINTERVAL

<a id="3c873eb393715b64"></a>
### 구문

```
NUMTODSINTERVAL( num, interval_indicator )
```

<a id="0b990e0f1791d1f4"></a>
### 설명

interval_indicator 단위인 number를 interval day to second 타입으로 변환하여 반환한다.

인자 number는 숫자 타입이다.

인자 interval_indicator는 CHAR, VARCHAR와 같은 문자 타입이며, 대소문자 구분없이 'DAY', 'HOUR', 'MINUTE', 'SECOND' 중 하나여야 한다.

인자 중 하나라도 NULL이면 결과로 NULL이 반환된다.

interval day(6) to second(6) 타입의 결과를 반환하며 precision은 사용자가 임의로 변경할 수 없다. 변환된 결과의 leading precision이 기본 precision을 초과하면 에러가 반환되며, fraction precision이 기본 precision을 초과하면 반올림한 결과를 반환한다.

<a id="ff62b317cb88f50f"></a>
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

<a id="b81b07ac22696e8f"></a>
## NUMTOYMINTERVAL

<a id="8bbc45670fcc9bf4"></a>
### 구문

```
NUMTOYMINTERVAL( num, interval_indicator )
```

<a id="2d4f212bf82f84ea"></a>
### 설명

interval_indicator 단위인 number를 interval year to month 타입으로 변환하여 반환한다.

인자 number는 숫자 타입이다.

인자 interval_indicator는 CHAR, VARCHAR와 같은 문자 타입이며, 대소문자 구분없이 'YEAR', 'MONTH' 중 하나여야 한다.

인자 중 하나라도 NULL이면 결과로 NULL이 반환된다.

interval year(6) to month 타입을 결과로 반환하며 precision은 사용자가 임의로 변경할 수 없다. 변환된 결과의 leading precision이 기본 precision을 초과하면 에러가 반환된다.

<a id="652b62a6541659c2"></a>
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

<a id="5943d38974268654"></a>
## NVL

<a id="44169b0316d7bab6"></a>
### 구문

```
NVL( expr1, expr2 )
```

<a id="59b1e202a202845c"></a>
### 설명

expr1이 null이 아니면 expr1을 반환하고, expr1이 null이면 expr2를 반환한다.

결과 타입은 expr1의 데이터 타입에 따라 결정된다.  
expr1에 NULL이 기술된 경우에는 expr2의 타입에 따라 결과 타입이 결정된다.  
expr1의 데이터 타입이 숫자형 타입인 경우와 문자형 타입인 경우는 각각 expr1, expr2의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, expr2의 데이터 타입이 모두 CHAR 타입인 경우, 결과 타입은 VARCHAR로 결정된다.

<a id="6db0183b452a2180"></a>
### 사용 예

```
gSQL> SELECT I1, NVL( I1, 0 ) FROM T1;
  I1 NVL( I1, 0 )
---- ------------
   1            1
null            0
2 rows selected.
```

<a id="8592e7c074fc51b7"></a>
## NVL2

<a id="e5e7dd65367d169a"></a>
### 구문

```
NVL2( expr1, expr2, expr3 )
```

<a id="8d2c90cc6fb0fdc9"></a>
### 설명

expr1이 null이 아니면 expr2를 반환하고, expr1이 null이면 expr3을 반환한다.

결과 타입은 expr2의 데이터 타입에 따라 결정된다.  
expr2에 NULL이 기술된 경우에는 expr3의 타입에 따라 결과 타입이 결정된다.  
expr2의 데이터 타입이 숫자형인 경우와 문자형인 경우에는 각각 expr2, expr3의 범위를 포함할 수 있는 타입으로 결정된다.  
expr2, expr3의 데이터 타입이 모두 CHAR 타입인 경우, 결과 타입은 VARCHAR가 된다.

<a id="263030bae01383a7"></a>
### 사용 예

```
gSQL> SELECT I1, NVL2( I1, I1 * 1000, 0 ) FROM T1;
  I1 NVL2( I1, I1 * 1000, 0 )
---- ------------------------
   1                     1000
null                        0
2 rows selected.
```

<a id="35d190ce222da53e"></a>
## OCTET_LENGTH

<a id="2598de6002562406"></a>
### 구문

```
OCTET_LENGTH( str )  

BYTE_LENGTH( str )     

LENGTHB( str )
```

<a id="42fede7bcd622504"></a>
### 설명

OCTET_LENGTH는 str의 바이트 수를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

str의 타입이 CHARACTER면 공백문자도 계산에 포함된다.  
str이 NULL이면 결과값도 NULL이다.

OCTET_LENGTH의 alias로는 [BYTE_LENGTH](#25e0a6a386a0a2d3)와 [LENGTHB](#e79ab79dbaf95eb5) 함수가 있다.

<a id="f860f08c4db46eb8"></a>
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

<a id="6ea53c8d491266fa"></a>
## OVERLAY

<a id="9175f34e136d051e"></a>
### 구문

```
OVERLAY( str1 PLACING str2 FROM start_position  [ FOR string_length ] )
```

<a id="08cc991359852360"></a>
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

자세한 내용은 [SUBSTRING](#665bcb4395b5720c)을 참조한다.

결과 타입은 다음 표와 같다.

**OVERLAY의 결과 타입**

<a id="fa7008acfe9ae63e"></a>
| str1, str2 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="57f336bdeecb1b8e"></a>
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

<a id="5c3d68470f87e67b"></a>
## PHYSICAL_LENGTH

<a id="94546230eb353b0e"></a>
### 구문

```
PHYSICAL_LENGTH( expr )
```

<a id="332f3fcef0799712"></a>
### 설명

PHYSICAL_LENGTH 함수는 expr의 내부 표현 정보 byte 수를 반환한다.

인자 expr에는 모든 데이터 타입이 올 수 있다.

입력 인자가 NULL이면 결과는 0 이다.

<a id="d75ff9d5cb694c4b"></a>
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

<a id="52db833face01cd1"></a>
## PI

<a id="1fd7c8bf2cef022d"></a>
### 구문

```
PI()
```

<a id="2ad00be56cac4c10"></a>
### 설명

PI는 "π" constant를 반환한다.

<a id="b5b1c4d205053b2d"></a>
### 사용 예

```
gSQL> SELECT PI() AS RESULT FROM DUAL;
              RESULT
--------------------
3.141592653589793E+0
1 row selected.
```

<a id="001b6c3fa907abf4"></a>
## POSITION

<a id="fcccaf1cb5b74557"></a>
### 구문

```
POSITION( str1 IN str2 )
```

<a id="417b64017d254d6a"></a>
### 설명

POSITION 함수는 str2에서 첫 번째 str1을 찾아 그 위치를 반환하는 함수이다.

str1과 str2에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

str2에서 str1을 찾을 수 없는 경우, 리턴값 0이 반환된다.  
str2에서 str1을 찾은 경우, 1을 시작으로 그 찾은 위치를 반환한다.  
반환되는 위치값은 CHARACTER 단위로 계산된 값이다. (byte 단위가 아님)  
str1 또는 str2가 NULL이면, 반환되는 값도 NULL 이다.

<a id="e91bcaa702ec0f53"></a>
### 사용 예

```
gSQL> SELECT POSITION( 'CHAR' IN 'LONG CHAR 2000' ) AS RESULT FROM DUAL;
RESULT
------
     6
1 row selected.
```

<a id="edfcdf4cc4aae780"></a>
## POWER

<a id="9575c8e7fdd011be"></a>
### 구문

```
POWER( num1, num2 )
```

<a id="e9fc98e7a58fd173"></a>
### 설명

POWER 함수는 num1에 num2를 제곱한 값을 반환한다.

인수 num1과 num2에는 숫자 타입이 올 수 있다.  

num1이 음수이면, num2는 정수여야 한다.  
num1 또는 num2의 값이 NULL이면, 결과값도 NULL이다.

<a id="1d753fe11226b596"></a>
### 사용 예

```
gSQL> SELECT POWER( 2, 3 ) AS RESULT FROM DUAL;
RESULT
------
     8
1 row selected.
```

<a id="056d329722dc4537"></a>
## RADIANS

<a id="8bfdaff82c08b6ce"></a>
### 구문

```
RADIANS( degrees )
```

<a id="e58f3856017ca9da"></a>
### 설명

RADIANS 함수는 degrees의 라디안을 반환한다.  

인자 degrees에는 숫자 타입이 올 수 있다.  
인자 degrees가 NULL이면 NULL을 반환한다.

<a id="3c971984d1d1bc0b"></a>
### 사용 예

```
gSQL> SELECT RADIANS( 180 ) AS RESULT FROM DUAL;
          RESULT
----------------
3.14159265358979
1 row selected.
```

<a id="297facfedf722390"></a>
## RANDOM

<a id="088472b8a15e78c5"></a>
### 구문

```
RANDOM( min, max )
```

<a id="b92b6a9d0a338bfe"></a>
### 설명

RANDOM은 min 이상 max 이하의 random 값을 반환한다.  

인자 min, max에는 숫자 타입이 올 수 있다.  
인자 min 또는 max가 NULL이면 NULL을 반환한다.

<a id="368adc8f89079d0a"></a>
### 사용 예

```
gSQL> SELECT RANDOM( 1, 100 ) AS RESULT FROM DUAL;
          RESULT
----------------
34.1870528003201
1 row selected.
```

<a id="5b3be95b4b5c3f72"></a>
## REPEAT

<a id="ef9bd16d9d8cd99f"></a>
### 구문

```
REPEAT( str, num )
```

<a id="e304600cf1d20e79"></a>
### 설명

REPEAT 함수는 num에 지정된 수만큼 str을 반복한 string을 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARCATER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

인자 num에는 숫자 타입이 올 수 있다.

str 또는 num 중의 하나라도 NULL이면, 결과값도 NULL이다.  
num의 값이 0 또는 음수인 경우에도 결과값은 NULL이다.

결과 타입은 다음 표와 같다.

**REPEAT의 결과 타입**

<a id="f0724ad8a95f7c96"></a>
| str 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="460baa5c5bd9cb7f"></a>
### 사용 예

```
gSQL> SELECT REPEAT( 'ab', 3 ) AS RESULT FROM DUAL;
RESULT
------
ababab
1 row selected.
```

<a id="c5dc37bd228c6cbd"></a>
## REPLACE

<a id="734116ab224e3ccd"></a>
### 구문

```
REPLACE( str, from, to )
```

<a id="4f9fea50cfc93f3e"></a>
### 설명

REPLACE는 str string 내의 모든 from string을 to string으로 치환하여 반환한다.

인자 str, from, to에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str 값이 NULL인 경우, 결과값은 NULL이다.  
from 값이 NULL인 경우, str 값을 변환하지 않고 반환한다.  
to 값이 생략되었거나 NULL인 경우, str에서 from을 제거한 값이 반환된다.

결과 타입은 다음 표와 같다.

**REPLACE의 결과 타입**

<a id="66d1304e7d292f7b"></a>
| str 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="1526ff24b4670135"></a>
### 사용 예

```
gSQL> SELECT REPLACE( 'HI GLIESE', 'HI', 'HELLO' ) AS RESULT FROM DUAL;
RESULT      
------------
HELLO GLIESE
1 row selected.
```

<a id="76d50a65126c479d"></a>
## REVERSE

<a id="7d5f68ceb9886f81"></a>
### 구문

```
REVERSE( str )
```

<a id="f4b3c260761a1f7a"></a>
### 설명

REVERSE는 str의 문자를 역순으로 반환한다.

인자로는 character string 타입 또는 binary string 타입으로 변환될 수 있는 타입이 올 수 있으며  
character string 타입은 해당 문자 단위로, binary string 타입은 byte 단위로 수행된다.

str이 NULL일 경우 NULL을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**REVERSE 인자와 결과 타입**

<a id="f6e435e7079e2d5d"></a>
| str | 결과 타입 |
| --- | --- |
| CHAR | CHAR |
| VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY | BINARY |
| VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="27b49e9f954a3c4e"></a>
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

<a id="b76bd26c7e0f9c8b"></a>
## ROUND( number )

<a id="4e592d7a9539c3f8"></a>
### 구문

```
ROUND( num [, scale ] )
```

<a id="61c16318a6ee150e"></a>
### 설명

ROUND는 scale을 기준으로 num을 반올림한 값을 반환한다.

인자 num, scale에는 숫자 타입이 올 수 있다.

scale이 생략된 경우, scale은 0이 되어 ROUND( num, 0 )와 같이 수행된다.  
scale이 양수인 경우 소수점 오른쪽 자리수를 기준으로 반올림되고, scale이 음수인 경우 소수점 왼쪽 자리수를 기준으로 반올림된다.  

인자 num 또는 scale이 NULL이면 NULL을 반환한다.

<a id="a4a4a4326ca48401"></a>
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

<a id="60b049eb771af7dd"></a>
## ROUND( date )

<a id="49dc8189fb26058d"></a>
### 구문

```
ROUND( date [ , fmt ] )
```

<a id="12605f6e54bc58c8"></a>
### 설명

ROUND( date ) 함수는 date를 지정된 fmt 단위로 반올림한 값을 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
인자 date 또는 fmt가 NULL이면 NULL을 반환한다.  

결과 타입은 인자로 받은 date 타입과 관계없이 항상 DATE 타입이다.

fmt가 생략되었을 경우의 기본값은 DAY 이며, 사용 가능한 형식문자열은 다음 표와 같다.

**fmt에 사용가능한 형식문자열**

<a id="d516a326daa756d4"></a>
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

<a id="3d396326076204f2"></a>
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

<a id="832d6cefe0c56168"></a>
## ROWID_GRID_BLOCK_ID

<a id="706c00de4f037fd6"></a>
### 구문

```
ROWID_GRID_BLOCK_ID( rowid )
```

<a id="5e7cb4e027f07d47"></a>
### 설명

GRID block ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="e0dbaebe2c76c7af"></a>
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

<a id="d41efdb4843b4416"></a>
## ROWID_GRID_BLOCK_SEQ

<a id="127becb969e74ed7"></a>
### 구문

```
ROWID_GRID_BLOCK_SEQ( rowid )
```

<a id="800fb63babc32ba3"></a>
### 설명

GRID block sequence를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="33711d22ba79d31f"></a>
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

<a id="e5e83e0f6c37102c"></a>
## ROWID_MEMBER_ID

<a id="6cb697e3188fa14d"></a>
### 구문

```
ROWID_MEMBER_ID( rowid )
```

<a id="371e97f5ff86bee9"></a>
### 설명

Member ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="2d4873491a2e051f"></a>
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

<a id="446b3b0c3c09bd94"></a>
## ROWID_OBJECT_ID

<a id="d028398bb8bea483"></a>
### 구문

```
ROWID_OBJECT_ID( rowid )
```

<a id="57f6151f206f694f"></a>
### 설명

Object ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="d6977f7e128a7a8c"></a>
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

<a id="ac684ad4ba380e22"></a>
## ROWID_PAGE_ID

<a id="55039e522a7bbfbf"></a>
### 구문

```
ROWID_PAGE_ID( rowid )
```

<a id="d1453e667626965c"></a>
### 설명

Page ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="1c5d5f3bef03e9ba"></a>
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

<a id="d237d52ed0369a2f"></a>
## ROWID_ROW_NUMBER

<a id="1cdeeaa8bd54ab77"></a>
### 구문

```
ROWID_ROW_NUMBER( rowid )
```

<a id="70319d8afef988c3"></a>
### 설명

Row number를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="5654293d517cdc11"></a>
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

<a id="aecbacb2e1cfe297"></a>
## ROWID_SHARD_ID

<a id="fa441d9b70c75cf6"></a>
### 구문

```
ROWID_SHARD_ID( rowid )
```

<a id="3595a5e602770e45"></a>
### 설명

Shard ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="2a28fb250e97ec05"></a>
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

<a id="89f4640bade213c1"></a>
## ROWID_TABLESPACE_ID

<a id="07c7b8c6863c7f7b"></a>
### 구문

```
ROWID_TABLESPACE_ID( rowid )
```

<a id="df525f9722178e78"></a>
### 설명

Tablespace ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="3f26cd08502272f6"></a>
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

<a id="cef5408f85f7df02"></a>
## ROWNUM

<a id="0b8ba21d6863957b"></a>
### 구문

```
ROWNUM
```

<a id="b33b654801db14cd"></a>
### 설명

WHERE 조건을 만족하는 row에 대하여 1부터 순차적으로 번호를 부여한다.

Oracle과의 호환성을 위해 WHERE 절에 ROWNUM 사용을 허용한다.

그러나 질의 결과의 개수를 제한하려면 다음과 같이 SQL 표준의 [offset limit clause](20-sql-references-h-z.md#d71e29f430201f4a)를 사용할 것을 권장한다.

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

<a id="d879d5e5c6718945"></a>
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

<a id="0cece345b548c125"></a>
## RPAD

<a id="11661c382b6d1746"></a>
### 구문

```
RPAD( str, length, [, fill] )
```

<a id="b6a42613f726fbad"></a>
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

<a id="97a30dc691e8bfd5"></a>
| 인자 str의 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="a7d863ef20a1b146"></a>
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

<a id="cc28bf3a9eecbb99"></a>
## RTRIM

<a id="bbdc90a261d72034"></a>
### 구문

```
RTRIM( trim_source [, trim_character ] )
```

<a id="6213a6017c63b00c"></a>
### 설명

RTRIM 함수는 trim_source에서 trim_character를 오른쪽 방향에서 비교하여 일치하는 문자가 없을 때까지 제거한 결과를 반환한다.

인자 trim_character와 trim_source에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

trim_character, trim_source 중 하나라도 NULL이면, 결과값은 NULL이다.  
trim_character가 생략된 경우에는 기본적으로 single blank space (' ')가 지정된다.

결과 타입은 다음과 같다.

**RTRIM의 결과 타입**

<a id="31582fdfb15f1ec2"></a>
| trim_source, trim_character 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="3e523b73a9d1d52c"></a>
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

<a id="162818d37467114e"></a>
## SESSION_ID

<a id="7a4319279807e59a"></a>
### 구문

```
SESSION_ID()
```

<a id="67cda9949d29d32d"></a>
### 설명

현재 session의 ID를 얻는다.

<a id="9103d05f9330ed47"></a>
### 사용 예

```
gSQL> SELECT SESSION_ID() FROM dual;

SESSION_ID()
------------
           4

1 row selected.
```

<a id="77f6c9921955465f"></a>
## SESSION_SERIAL

<a id="2993cba03e5ddd95"></a>
### 구문

```
SESSION_SERIAL()
```

<a id="ad619b29ed6f03b2"></a>
### 설명

현재 session의 serial 번호를 얻는다.

<a id="976f4e40ffd2203c"></a>
### 사용 예

```
gSQL> SELECT SESSION_SERIAL() FROM dual;

SESSION_SERIAL()
----------------
              16

1 row selected.
```

<a id="b659d72f01caff99"></a>
## SESSION_USER

<a id="3cb4ef683c09c14a"></a>
### 구문

```
SESSION_USER[()]
```

<a id="1414bc10836bc63e"></a>
### 설명

세션 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다. 
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다. 
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다. 
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="c482e4d17b955e8c"></a>
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

<a id="e3ba6091448062c6"></a>
## SHARD_GROUP_ID

<a id="a52bd2e19b7437e4"></a>
### 구문

```
SHARD_GROUP_ID( table_name, shard_key_value [, ... ] )
```

<a id="7853be85ba1adcc8"></a>
### 설명

SHARD_GROUP_ID 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard를 관리하는 group ID를 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 NATIVE_BIGINT이다.

> Cluster system에서 유효한 정보이다.

<a id="c3d3806290ca25f7"></a>
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

<a id="1fbd9cda6d636188"></a>
## SHARD_GROUP_NAME

<a id="ad7cc3afbb728bb9"></a>
### 구문

```
SHARD_GROUP_NAME( table_name, shard_key_value [, ... ] )
```

<a id="68deadb7f4c7419b"></a>
### 설명

SHARD_GROUP_NAME 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard를 관리하는 group NAME을 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 VARCHAR이다.

> Cluster system에서 유효한 정보이다.

<a id="6b93d2eb18fa3193"></a>
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

<a id="fe550fb4ac11caf7"></a>
## SHARD_ID

<a id="fede30b3ad58e65d"></a>
### 구문

```
SHARD_ID( table_name, shard_key_value [, ... ] )
```

<a id="d7433b755cfd6cb5"></a>
### 설명

SHARD_ID 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard에 대한 ID를 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 NATIVE_BIGINT이다.

> Cluster system에서 유효한 정보이다.

<a id="0136289715596c9b"></a>
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

<a id="34cd6fbc99750ddd"></a>
## SHARD_NAME

<a id="ac05f223e5226027"></a>
### 구문

```
SHARD_NAME( table_name, shard_key_value [, ... ] )
```

<a id="a0e5db1427c6b257"></a>
### 설명

SHARD_NAME 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard에 대한 NAME을 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 VARCHAR이다.

> Cluster system에서 유효한 정보이다.

<a id="caec773698a517a7"></a>
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

<a id="76781ce47783c254"></a>
## SHIFT_LEFT

<a id="acc0c87058040229"></a>
### 구문

```
SHIFT_LEFT( num, cnt )
```

<a id="8efe7a8068bda192"></a>
### 설명

SHIFT_LEFT 함수는 num을 cnt 비트만큼 왼쪽으로 이동시킨 값을 반환한다.

입력 인자 num, cnt에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환하면 소수점은 TRUNCATE 된다.

연산 시 cnt는 6 bit로 마스킹하여 6 bit 범위 내의 값으로 처리한다.

num 또는 cnt가 NULL이면 NULL을 반환한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="297da4aaa8c43e28"></a>
### 사용 예

```
gSQL> SELECT SHIFT_LEFT(1, 3) FROM DUAL;
SHIFT_LEFT(1, 3)
----------------
               8
1 row selected.
```

<a id="f118c8dc69ece3ec"></a>
## SHIFT_RIGHT

<a id="e4b81393d9896b81"></a>
### 구문

```
SHIFT_RIGHT( num, cnt )
```

<a id="1c41c98086520cd0"></a>
### 설명

SHIFT_RIGHT 함수는 num을 cnt 비트만큼 오른쪽으로 이동시킨 값을 반환한다.

입력 인자 num, cnt에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환하면 소수점은 TRUNCATE 된다.

연산 시 cnt는 6 bit로 마스킹하여 6 bit 범위내의 값으로 처리한다.

num 또는 cnt가 NULL이면 NULL을 반환한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="997f5a0ac30e08cb"></a>
### 사용 예

```
gSQL> SELECT SHIFT_RIGHT(8, 3) FROM DUAL;
SHIFT_RIGHT(8, 3)
-----------------
                1
1 row selected.
```

<a id="4af70086918fb37c"></a>
## SIGN

<a id="75cb419ef75c32f0"></a>
### 구문

```
SIGN( num )
```

<a id="19c30ec4e33cde49"></a>
### 설명

SIGN 함수는 num의 부호를 반환한다.

인자 num에는 숫자타입이 올 수 있다.

반환값은 다음과 같다.  
• num < 0 이면 -1  
• num = 0 이면 0  
• num > 0 이면 1

num이 NULL이면 NULL을 반환한다.

<a id="b16a99a5dd300f7d"></a>
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

<a id="2a88ebf25d9ad0f3"></a>
## SIN

<a id="51b6b40e325f8e0c"></a>
### 구문

```
SIN( num )
```

<a id="316791dc06cc24ec"></a>
### 설명

SIN 함수는 num의 sine 값을 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="f62ff3f1f0049d32"></a>
### 사용 예

```
gSQL> SELECT SIN( 0 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="6da1ee8b633a2f5b"></a>
## SPLIT_PART

<a id="b530d125c3213efc"></a>
### 구문

```
SPLIT_PART( string, delimiter, field )
```

<a id="78ee1683567afc04"></a>
### 설명

SPLIT_PART 함수는 string 내에서 delimiter로 지정된 문자를 구분자로 하여 field의 문자열을 반환한다.

인자 string, delimiter에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

인자 field에는 숫자 타입이 올 수 있다.

string, delimiter, field 중에 하나라도 NULL인 경우에는 결과값도 NULL이다.  
field에는 1 이상의 숫자값만 올 수 있고, 0 또는 음수일 경우에는 에러를 반환한다.

결과 타입은 다음 표와 같다.

**SPLIT_PART의 결과 타입**

<a id="221f7284964cdabb"></a>
| string 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="4f9cf844c46247be"></a>
### 사용 예

```
gSQL> SELECT SPLIT_PART( 'AB;CD;EF;GH', ';', 3  ) AS RESULT FROM DUAL;
RESULT
------
EF    
1 row selected.
```

<a id="5abfe5134cc90d11"></a>
## SQRT

<a id="9d38e46bf6cd21e1"></a>
### 구문

```
SQRT( num )
```

<a id="40a8d077b85df506"></a>
### 설명

SQRT 함수는 num의 제곱근을 반환한다.  

인자 num에는 숫자 타입이 올 수 있고, 음수가 아닌 0 이상의 값이어야 한다.  
인자 num이 NULL이면 NULL을 반환한다.

<a id="e3d320e13374457c"></a>
### 사용 예

```
gSQL> SELECT SQRT( 9 ) AS RESULT FROM DUAL;
RESULT
------
     3
1 row selected.
```

<a id="3e267036bee6c7f2"></a>
## STATEMENT_DATE

<a id="94dd5977b63526e4"></a>
### 구문

```
STATEMENT_DATE()
CURRENT_DATE [()]
```

<a id="80ff67680f395883"></a>
### 설명

현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="147d631240b45ea9"></a>
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

<a id="e9bfb87d489352c3"></a>
## STATEMENT_LOCALTIME

<a id="098c765bc759ec08"></a>
### 구문

```
STATEMENT_LOCALTIME()
LOCALTIME [()]
```

<a id="eb9ad411e2de6a59"></a>
### 설명

Session 시간을 기준으로 현재 TIME WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="ccfb36b25087a891"></a>
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

<a id="1ec091cca8f15c96"></a>
## STATEMENT_LOCALTIMESTAMP

<a id="58b0436dc0cbdda5"></a>
### 구문

```
STATEMENT_LOCALTIMESTAMP()
LOCALTIMESTAMP [()]
```

<a id="298e01ccd74ec370"></a>
### 설명

Session 시간을 기준으로 현재 TIMESTAMP WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="09fa4f9f7cad34b7"></a>
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

<a id="6dbf5bf6478be35e"></a>
## STATEMENT_TIME

<a id="6d20c078fa182e2e"></a>
### 구문

```
STATEMENT_TIME()
CURRENT_TIME [()]
```

<a id="90de958c1ae3e133"></a>
### 설명

TIME ZONE이 있는 현재 TIME (TIME WITH TIME ZONE type) 값을 얻는다.

CURRENT_TIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="5ad60ba8ac04eb11"></a>
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

<a id="d6b34aa7b3769030"></a>
## STATEMENT_TIMESTAMP

<a id="e96a30731d780146"></a>
### 구문

```
STATEMENT_TIMESTAMP()
CURRENT_TIMESTAMP [()]
```

<a id="09b974a931558e84"></a>
### 설명

TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

CURRENT_TIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="3e4b4cf58c9e31ff"></a>
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

<a id="2140466b3c549c55"></a>
## STATEMENT_VIEW_SCN

<a id="2e2fcf96d3abdbd4"></a>
### 구문

```
STATEMENT_VIEW_SCN()
```

<a id="96bc3c04b8396ce5"></a>
### 설명

현재 STATEMENT의 VIEW SCN을 얻는다.

<a id="96846aa7a447e602"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN() FROM dual;

STATEMENT_VIEW_SCN()
--------------------
17697.658.17880     

1 row selected.
```

<a id="750856ee51e8b5f3"></a>
## STATEMENT_VIEW_SCN_DCN

<a id="a334f816b0c881c0"></a>
### 구문

```
STATEMENT_VIEW_SCN_DCN()
```

<a id="634af190c5c40e85"></a>
### 설명

현재 STATEMENT의 VIEW SCN의 Domain Change Number (DCN) 값을 얻는다.

<a id="13420e82174d7398"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_DCN() FROM dual;

STATEMENT_VIEW_SCN_DCN()
------------------------
                     658

1 row selected.
```

<a id="44b4e2b9bd1c1e95"></a>
## STATEMENT_VIEW_SCN_GCN

<a id="444d7490e9f6f67a"></a>
### 구문

```
STATEMENT_VIEW_SCN_GCN()
```

<a id="5cc3f83a941bb428"></a>
### 설명

현재 STATEMENT의 VIEW SCN의 Global Change Number (GCN) 값을 얻는다.

<a id="367c26f2e7b68f8f"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_GCN() FROM dual;

STATEMENT_VIEW_SCN_GCN()
------------------------
                   17697

1 row selected.
```

<a id="5fb491817ce46e27"></a>
## STATEMENT_VIEW_SCN_LCN

<a id="ffa0d9e51a8a52f7"></a>
### 구문

```
STATEMENT_VIEW_SCN_LCN()
```

<a id="9b6e374c50558462"></a>
### 설명

현재 STATEMENT의 VIEW SCN의 Local Change Number (LCN) 값을 얻는다.

<a id="ad513656f258b7db"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_LCN() FROM dual;

STATEMENT_VIEW_SCN_LCN()
------------------------
                   17880

1 row selected.
```

<a id="ef48d7168e3cbd63"></a>
## STDDEV

<a id="7007f7d2da220960"></a>
### 구문

```
STDDEV( [ ALL | DISTINCT ] expr )
```

<a id="d939aac362524002"></a>
### 설명

Aggregation 함수로써 expr set의 표준편차 (standard deviation)를 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 수행하고, DISTINCT를 명시한 경우 중복을 제거한 값들에 대해 수행한다. 둘 다 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

NULL 값을 제외하고 DISTINCT로 중복을 제거한 후의 expr set의 개수가 한 개일 경우, [VARIANCE](#1606402ae153f86e)와 같이 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV 인자와 결과 타입**

<a id="8b880513f382c340"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

GOLDILOCKS는 다음과 같이 표준편차를 계산한다.  
　• expr set의 개수가 1이면 0을 반환한다.  
　• expr set의 개수가 1보다 크면 [STDDEV_SAMP( expr )](#a1c9763e7cd69449) 값을 반환한다.

> 표준편차는, 분산의 양의 제곱근으로써 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV 함수는 [VARIANCE](#1606402ae153f86e) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV( [ ALL ] expr )  
>  = SQRT( VARIANCE( [ ALL ] expr ) )  
>   
> STDDEV( DISTINCT expr )  
>  = SQRT( VARIANCE( DISTINCT expr ) )

<a id="c8f8458fc71e51a1"></a>
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
```

<a id="691944807590830f"></a>
## STDDEV_POP

<a id="42a8458530d6700b"></a>
### 구문

```
STDDEV_POP( expr )
```

<a id="81db208f8fe7c421"></a>
### 설명

Aggregation 함수로써 expr set의 모 표준편차 (population standard deviation)를 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV_POP의 인자와 결과 타입**

<a id="496396ddc4596242"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 표준편차는 모 분산의 양의 제곱근으로써 모 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV_POP 함수는 [VAR_POP](#2a39166cd54fb778) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV_POP( expr )  
>  = SQRT( VAR_POP( expr ) )

<a id="12c26f636a2d4a5e"></a>
### 사용 예

```
gSQL> SELECT STDDEV_POP(c1) FROM t1;

 STDDEV_POP(C1)
---------------
10.283968105746

1 row selected.
```

<a id="a1c9763e7cd69449"></a>
## STDDEV_SAMP

<a id="9d33d8443cdc12a9"></a>
### 구문

```
STDDEV_SAMP( expr )
```

<a id="307f50d816c0db4b"></a>
### 설명

Aggregation 함수로써 expr set의 표본 표준편차 (sample standard deviation)를 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 NULL값을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV_SAMP의 인자와 결과 타입**

<a id="86ce68ada5aea04c"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 표본 표준편차는 표본 분산의 양의 제곱근으로써 표본 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV_SAMP 함수는 [VAR_SAMP](#70d7f8d062fdcab6) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV_SAMP( expr )  
>  = SQRT( VAR_SAMP( expr ) )

<a id="756a3a8c273ca1f5"></a>
### 사용 예

```
gSQL> SELECT STDDEV_SAMP(c1) FROM t1;

 STDDEV_SAMP(C1)
----------------
11.4978258814438

1 row selected.
```

<a id="78e8f4bf2d4e5fa0"></a>
## SUBSTR

<a id="041093f476bcd1f5"></a>
### 구문

```
SUBSTR( str FROM start_position [ FOR string_length ] )
SUBSTR( str, start_position [ , string_length ] )
```

<a id="f392efdd88fdea2f"></a>
### 설명

[SUBSTRING](#665bcb4395b5720c)의 alias이다.

<a id="82cf6886ff00fc94"></a>
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

<a id="653bde41d8ebfba1"></a>
## SUBSTRB

<a id="43f35c95a325b086"></a>
### 구문

```
SUBSTRB( str, start_position [ , string_length ] )
```

<a id="dd2cd982cb119c0c"></a>
### 설명

SUBSTRB 함수는 str에 대해 start_position으로부터 string_length 범위의 문자를 추출하여 반환한다.

SUBSTRB 함수는 start_position과 string_length가 byte 단위로 계산된다는 점 외에는 [SUBSTRING](#665bcb4395b5720c) 함수와 동일하다.

<a id="30c3db7d135efe67"></a>
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

<a id="665bcb4395b5720c"></a>
## SUBSTRING

<a id="31e6cd7e8ee36fe7"></a>
### 구문

```
SUBSTRING( str FROM start_position [ FOR string_length ] )  
SUBSTRING( str, start_position [ , string_length ] )
```

<a id="925c8a17ae1bada9"></a>
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
자세한 내용은 [SUBSTR](#78e8f4bf2d4e5fa0)과 [SUBSTRB](#653bde41d8ebfba1)를 참조한다.

결과 타입은 다음 표와 같다.

**SUBSTRING의 결과 타입**

<a id="58eaa6474a845717"></a>
| str | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="edddff449c338c6c"></a>
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

<a id="cad509b70c5fc67f"></a>
## SUM

<a id="7303e6cad4a56c9e"></a>
### 구문

```
SUM( [ ALL | DISTINCT ] expr )
```

<a id="6c7bcbadc11e57d7"></a>
### 설명

Aggregation 함수로써 expr 값들의 합을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복을 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

<a id="0e362047f6948a27"></a>
### 사용 예

```
gSQL> SELECT SUM(c1) FROM t1;

SUM(C1)
-------
      6

1 row selected.
```

<a id="9122a929ceda22e6"></a>
## SYSDATE

<a id="ae533131e9d28372"></a>
### 구문

```
SYSDATE
```

<a id="80d1662fe05e7b1f"></a>
### 설명

Database server가 위치하는 OS 시간을 기준으로 현재의 DATE type 값을 얻는다.

<a id="e6f062fe25358e7c"></a>
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

<a id="b0212c486e67fb50"></a>
## SYS_EXTRACT_UTC

<a id="5ca94b318bd26aab"></a>
### 구문

```
SYS_EXTRACT_UTC( datetime_with_timezone )
```

<a id="8e3eeebe12de0a78"></a>
### 설명

SYS_EXTRACT_UTC 는  UTC (Coordinated Universal Time—formerly Greenwich Mean Time) 값을 반환한다.  
timezone이 명시되지 않은 경우, session time zone으로 계산된다.

입력 인자에는 time, time with time zone, timestamp, timestamp with time zone 타입이 올 수 있다.  
결과 타입은 time 또는 timestamp 타입이다.

<a id="675c615c9c2e022c"></a>
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

<a id="ee6c6896466ed396"></a>
## SYSTIME

<a id="0f9cf80758dcfbc1"></a>
### 구문

```
SYSTIME
```

<a id="96336eda985b844c"></a>
### 설명

Database server가 위치하는 OS 시간을 기준으로 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

<a id="09e2beddf0740915"></a>
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

<a id="fc86096ea251b499"></a>
## SYSTIMESTAMP

<a id="67496e88d3a8bd8e"></a>
### 구문

```
SYSTIMESTAMP
```

<a id="7a7e28d82468e817"></a>
### 설명

Database server가 위치하는 OS 시간을 기준으로 TIME ZONE이 있는 현재 TIMESTAMP WITH TIME ZONE type 값을 얻는다.

<a id="7844d4baf6499caf"></a>
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

<a id="a36f51ad4be8f61d"></a>
## TAN

<a id="e84fe0cf38597e8c"></a>
### 구문

```
TAN( num )
```

<a id="cddbfa52645141ad"></a>
### 설명

TAN 함수는 num의 tangent 값을 라디안 단위로 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="ea767423472c6165"></a>
### 사용 예

```
gSQL> SELECT TAN( 1 ) AS RESULT FROM DUAL;
         RESULT
---------------
1.5574077246549
1 row selected.
```

<a id="d9af2a22021e0c5a"></a>
## TO_BASE64

<a id="f7cbf9e2a608856b"></a>
### 구문

```
TO_BASE64( str )
```

<a id="c941e29668fd0792"></a>
### 설명

TO_BASE64는 str을 base64 인코딩으로 변환한 문자를 반환한다.  
인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입 또는 문자 타입으로 변환될 수 있는 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.  
결과 타입은 CHARACTER VARYING 또는 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.

Base64 인코딩은 8 비트  바이너리 데이터를 ascii 영역으로 구성된 64개의 문자로 표현한다.  
64개의 문자는 A~Z, a~z, 0~9, +, / 로 구성된다.

6 bit를 하나의 문자로 표현하며, 세 개의 문자 (24 bit)를 하나의 단위로 네 개의 문자로 표현한다.  
인코딩 된 문자가 네 개의 문자를 채우지 못하면 나머지는 '=' 로 채운다.  
인코딩 된 문자가 76개를 넘으면 newline이 추가되어 여러 라인으로 나누어진다.

Base64 인코딩 된 문자의 디코딩은 FROM_BASE64() 함수를 이용한다.  
Base64를 디코딩 할 때는 newline, carriage return, tab, space가 무시된다.

자세한 내용은 [FROM_BASE64](#81bb5bf2cda8e6cc)를 참조한다.

<a id="64b1141df45a033b"></a>
### 사용 예

```
gSQL> SELECT TO_BASE64( 'abc' ), TO_BASE64( 'abcd' ) FROM DUAL;

TO_BASE64( 'abc' ) TO_BASE64( 'abcd' )
------------------ -------------------
YWJj               YWJjZA==           
1 row selected.
```

<a id="dd1c3bac182981a9"></a>
## TO_CHAR( datetime )

<a id="91b9eb63c5c426e5"></a>
### 구문

```
TO_CHAR( datetime [, fmt ] )
```

<a id="480c741c68789eb3"></a>
### 설명

TO_CHAR( datetime ) 함수는 datetime을 명시된 fmt 형식의 문자열로 변환하여 반환한다.

인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  

입력 인자의 값이 하나라도 NULL이면 NULL을 반환한다.

fmt가 생략된 경우, default format 형식을 따른다.  
• DATE: [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#3743e60c126ee1e1)  
• TIMESTAMP: [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#02892516d7d97f96)  
• TIMESTAMP WITH TIME ZONE: [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#0cecf8f45a110468)  
• TIME: [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#94b62e1d8e627da5)  
• TIME WITH TIME ZONE: [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#4446f2d6ee237e50)

인자 datetime이 INTERVAL 타입인 경우, fmt와 무관하게 string으로 변환하여 반환한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#eed3005eda2495e4)을 참조한다.

결과 타입은 CHARACTER VARYING 이다.

<a id="3d6daefa81f8ed12"></a>
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

<a id="de3c8115ff06677b"></a>
## TO_CHAR( number )

<a id="3d0fd1796d44e8d4"></a>
### 구문

```
TO_CHAR( number [, fmt ] )
```

<a id="1d895cc711d0e5cb"></a>
### 설명

TO_CHAR( number ) 함수는 number를 명시된 fmt 형식의 문자열로 변환하여 반환한다.

인자 number에는 숫자 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, 모든 유효 숫자를 문자열로 변환하여 반환한다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#4b3cf819ff97fe13)을 참조한다.  
입력 인자의 값이 하나라도 NULL이면 NULL을 반환한다.

결과 타입은 CHARACTER VARYING 이다.

<a id="bb42f6c7d7bd760e"></a>
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

<a id="6e2b1adfe49416aa"></a>
## TO_DATE

<a id="414441de204d3332"></a>
### 구문

```
TO_DATE( str [, fmt ] )
```

<a id="5b8152bfb512021c"></a>
### 설명

TO_DATE 함수는 명시된 fmt 형식의 문자열 str을 DATE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_DATE_FORMAT은 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#eed3005eda2495e4)을 참조한다.  
자세한 내용은 [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#3743e60c126ee1e1)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

결과 타입은 DATE 이다.

<a id="a91a27c85e385995"></a>
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

<a id="8dd1638a1aa797ea"></a>
## TO_NATIVE_BIGINT

<a id="012aac8b07bf675d"></a>
### 구문

```
TO_NATIVE_BIGINT( str [, fmt ] )
```

<a id="d5f79781e344defb"></a>
### 설명

TO_NATIVE_BIGINT 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_BIGINT 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#4b3cf819ff97fe13)을 참조한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="5b24138366e36e3e"></a>
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

<a id="84b3c63569781301"></a>
## TO_NATIVE_DOUBLE

<a id="a657da2bf65e68cf"></a>
### 구문

```
TO_NATIVE_DOUBLE( str [, fmt ] )
```

<a id="41205862e5d1dfa0"></a>
### 설명

TO_NATIVE_DOUBLE 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_DOUBLE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#4b3cf819ff97fe13)을 참조한다.

결과 타입은 NATIVE_DOUBLE이다.

<a id="d9d0eb142815616e"></a>
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

<a id="45faeaf6d6a5842d"></a>
## TO_NATIVE_INTEGER

<a id="08340f80c5e53504"></a>
### 구문

```
TO_NATIVE_INTEGER( str [, fmt ] )
```

<a id="edb268d4410ce379"></a>
### 설명

TO_NATIVE_INTEGER 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_INTEGER 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#4b3cf819ff97fe13)을 참조한다.

결과 타입은 NATIVE_INTEGER이다.

<a id="5ae5bec8159660e4"></a>
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

<a id="3d1db5cc109c387a"></a>
## TO_NATIVE_REAL

<a id="b709ca755d5f1cad"></a>
### 구문

```
TO_NATIVE_REAL( str [, fmt ] )
```

<a id="376c280e953d7435"></a>
### 설명

TO_NATIVE_REAL 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_REAL 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#4b3cf819ff97fe13)을 참조한다.

결과 타입은 NATIVE_REAL이다.

<a id="39041e1588d0da86"></a>
### 사용 예

```
gSQL> SELECT TO_NATIVE_REAL( '123.45' ) AS RESULT1, 
             TO_NATIVE_REAL( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
```

<a id="f850b5d15547e490"></a>
## TO_NATIVE_SMALLINT

<a id="17353af9a774a24a"></a>
### 구문

```
TO_NATIVE_SMALLINT( str [, fmt ] )
```

<a id="329d04af8f480739"></a>
### 설명

TO_NATIVE_SMALLINT 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_SMALLINT 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYIN과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#4b3cf819ff97fe13)을 참조한다.

결과 타입은 NATIVE_SMALLINT이다.

<a id="38ea02c4fc4501e0"></a>
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

<a id="b09d69a11c48fa7f"></a>
## TO_NUMBER

<a id="33eb7ffe79a28ad0"></a>
### 구문

```
TO_NUMBER( str [, fmt] )
```

<a id="05b60d96fa384c0b"></a>
### 설명

TO_NUMBER 함수는 명시된 fmt 형식의 문자열 str을 NUMBER 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#4b3cf819ff97fe13)을 참조한다.

결과 타입은 NUMBER이다.

<a id="2c247c116f8726d2"></a>
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

<a id="902e283826bfefaa"></a>
## TO_TIME

<a id="066db71acd51071b"></a>
### 구문

```
TO_TIME( str [, fmt ] )
```

<a id="034d709d6906b9af"></a>
### 설명

TO_TIME 함수는 명시된 fmt 형식의 문자열 str을 TIME 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIME_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#eed3005eda2495e4)을 참조한다.  
자세한 내용은 [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#94b62e1d8e627da5)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

결과 타입은 TIME 이다.

<a id="8879feebb8a07cb3"></a>
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

<a id="744bf83cdfd44b1c"></a>
## TO_TIME_TZ

<a id="23756b2d8920b162"></a>
### 구문

```
TO_TIME_TZ( str [, fmt ] )
```

<a id="f035ff14ad6fd339"></a>
### 설명

TO_TIME_WITH_TIME_ZONE의 alias이다.  
자세한 내용은 [TO_TIME_WITH_TIME_ZONE](#9876b9f39430073d)과 [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#4446f2d6ee237e50)을 참조한다.

<a id="b0a34d691a1bae4e"></a>
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

<a id="9876b9f39430073d"></a>
## TO_TIME_WITH_TIME_ZONE

<a id="498287deef8bae97"></a>
### 구문

```
TO_TIME_WITH_TIME_ZONE( str [, fmt ] )
TO_TIME_TZ( str [, fmt ] )
```

<a id="6141812ae1531617"></a>
### 설명

TO_TIME_WITH_TIME_ZONE 함수는 명시된 fmt 형식의 문자열 str을 TIME WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIME_WITH_TIME_ZONE_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#eed3005eda2495e4)을 참조한다.  
자세한 내용은 [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#4446f2d6ee237e50)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

TO_TIME_WITH_TIME_ZONE의 alias로는 [TO_TIME_TZ](#744bf83cdfd44b1c) 함수가 있다.

결과 타입은 TIME WITH TIME ZONE 이다.

<a id="efadb32c427d8a7d"></a>
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

<a id="2a4e6f6e440db4e0"></a>
## TO_TIMESTAMP

<a id="85f9c42cf12e0d95"></a>
### 구문

```
TO_TIMESTAMP( str [, fmt ] )
```

<a id="af16d59ec37d86c2"></a>
### 설명

TO_TIMESTAMP 함수는 명시된 fmt 형식의 문자열 str을 TIMESTAMP 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIMESTAMP_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#eed3005eda2495e4)을 참조한다.  
자세한 내용은 [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#02892516d7d97f96)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

결과 타입은 TIMESTAMP 이다.

<a id="1f76292593c6041d"></a>
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

<a id="6d8a2769b5bafd2d"></a>
## TO_TIMESTAMP_TZ

<a id="da50738be4f4387a"></a>
### 구문

```
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="e7dcbe9e91a323a2"></a>
### 설명

TO_TIMESTAMP_WITH_TIME_ZONE의 alias 이다.  
자세한 내용은 [TO_TIMESTAMP_WITH_TIME_ZONE](#d15ebb2b4d41176d)과 [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#0cecf8f45a110468)을 참조한다.

<a id="3d5b3bc1c4285385"></a>
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

<a id="d15ebb2b4d41176d"></a>
## TO_TIMESTAMP_WITH_TIME_ZONE

<a id="7a5a7097de87bf65"></a>
### 구문

```
TO_TIMESTAMP_WITH_TIME_ZONE( str [, fmt ] )
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="79845d3c9a61dcab"></a>
### 설명

TO_TIMESTAMP_WITH_TIME_ZONE 함수는 명시된 fmt 형식의 문자열 str을 TIMESTAMP WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#eed3005eda2495e4)을 참조한다.  
자세한 내용은 [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#0cecf8f45a110468)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

TO_TIMESTAMP_WITH_TIME_ZONE의 alias로는 [TO_TIMESTAMP_TZ](#6d8a2769b5bafd2d) 함수가 있다.

결과 타입은 TIMESTAMP WITH TIME ZONE 이다.

<a id="cc2f271788aac263"></a>
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

<a id="b9b375d76d45710d"></a>
## TRANSACTION_DATE

<a id="d34c3bc73e057f06"></a>
### 구문

```
TRANSACTION_DATE()
```

<a id="307b63b9caf81937"></a>
### 설명

Session 시간을 기준으로 현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="9dcb9ab339c2d2cf"></a>
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

<a id="a3bbfb702261dcee"></a>
## TRANSACTION_LOCALTIME

<a id="ec46ee22519dc841"></a>
### 구문

```
TRANSACTION_LOCALTIME()
```

<a id="4e4557e5be15b670"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 없는 현재 시간 (TIME WITHOUT TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="72a49a89cbf2907f"></a>
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

<a id="e58488664e5177f8"></a>
## TRANSACTION_LOCALTIMESTAMP

<a id="058f6fc97c4e217c"></a>
### 구문

```
TRANSACTION_LOCALTIMESTAMP()
```

<a id="921e4e474252c770"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 없는 현재 TIMESTAMP (TIMESTAMP WITHOUT TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="6653c9daa44a93db"></a>
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

<a id="eedb68811986416b"></a>
## TRANSACTION_TIME

<a id="7d62e5d00120cdb8"></a>
### 구문

```
TRANSACTION_TIME()
```

<a id="9f8007a129b1b2a6"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="06852a47bf2bf99b"></a>
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

<a id="ee59134da308f231"></a>
## TRANSACTION_TIMESTAMP

<a id="b30412aa973433fc"></a>
### 구문

```
TRANSACTION_TIMESTAMP()
```

<a id="8fb47911725048b5"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="dd19c9940fa1e6e8"></a>
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

<a id="c3600e332f7ea901"></a>
## TRANSLATE

<a id="ed3711e3aae02b88"></a>
### 구문

```
TRANSLATE( string, from, to )
```

<a id="a8fa5b2772e59b5b"></a>
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

<a id="c01d6fa71c897348"></a>
| string 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="9fa887ccb8c2ea8e"></a>
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

<a id="133fb72e441bff70"></a>
## TRIM

<a id="5f761ed9c2749174"></a>
### 구문

```
TRIM([ [ LEADING | TRAILING | BOTH ]  [trim_character] FROM ] trim_source)
```

<a id="30105c23358a7fb1"></a>
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
    - [ LEADING | TRAILING | BOTH ] 이 생략된 경우에는 BOTH가 기본적으로 지정된다.
- FROM이 생략된 경우
    - TRIM( trim_source ) 인 경우이며 TRIM( BOTH ' ' FROM trim_source )과 동일하게 수행된다.

결과 타입은 다음 표와 같다.

**TRIM의 결과 타입**

<a id="3278665e1cfb070f"></a>
| trim_character, trim_source 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="bd1ba3f84397716c"></a>
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

<a id="3f2126d1f78e754c"></a>
## TRUNC( number )

<a id="296adcdbf5712269"></a>
### 구문

```
TRUNC( num [ , scale ] )
```

<a id="4f8a0a4910424169"></a>
### 설명

TRUNC( number ) 함수는 scale 기준으로 num을 버림한 값을 반환한다.

인자 num과 scale에는 숫자 타입이 올 수 있다.  
인자 num 또는 scale이 NULL이면 NULL을 반환한다.

scale이 생략된 경우, scale은 0이 되어 TRUNC( num, 0 )일 때와 같이 실행된다.  
scale이 양수인 경우, 소수점 오른쪽 자리수를 기준으로 버림한다.  
scale이 음수인 경우, 소수점 왼쪽 자리수를 기준으로 버림한다.

<a id="8115bda08b6d4175"></a>
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

<a id="8e5f5fcbd196c008"></a>
## TRUNC( date )

<a id="e781129f8c9b4021"></a>
### 구문

```
TRUNC( date [ , fmt ] )
```

<a id="9be28bf424b7490f"></a>
### 설명

TRUNC( date ) 함수는 date를 지정된 fmt 단위로 버림한 값을 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
인자 date 또는 fmt이 NULL이면 NULL을 반환한다.

결과 타입은 인자로 받은 date 타입과 관계없이 항상 DATE 타입이다.

fmt가 생략되었을 경우의 기본값은 DAY이며, 사용 가능한 형식문자열은 다음 표와 같다.

**fmt에 사용가능한 형식문자열**

<a id="a09ca622a05e37f1"></a>
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

<a id="ccff74c0afbe96d6"></a>
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

<a id="6d635c45e1d6eb9c"></a>
## UPPER

<a id="45325a90ef4de9c9"></a>
### 구문

```
UPPER( str )
```

<a id="0f6624ac57360537"></a>
### 설명

UPPER 함수는 str의 대문자를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.  
str이 NULL이면 결과값도 NULL이다.

반환되는 타입은 인자 str과 동일한 타입이다.

<a id="f4634c7bca72c388"></a>
### 사용 예

```
gSQL> SELECT UPPER( 'spring' ) AS RESULT FROM DUAL;
RESULT
------
SPRING
1 row selected.
```

<a id="ad3481b3c1a32b46"></a>
## UNHEX

<a id="4ff9ca9b441bc628"></a>
### 구문

```
UNHEX( str )
```

<a id="ee6335073fbb5bfd"></a>
### 설명

인자 str은 16진수 문자이며, 이를 각 byte로 표현하여 binary string으로 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 BINARY VARYING이나 BINARY LONG VARYING과 같은 BINARY 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 16진수 범위에 속하지 않는 문자가 포함되면 에러를 반환한다.

자세한 내용은 [HEX](#74db15c6a19d6e5e)를 참조한다.

<a id="0182c429395a51ad"></a>
### 사용 예

```
gSQL> SELECT UNHEX( HEX( 'abc' ) ) FROM DUAL;
UNHEX( HEX( 'abc' ) )
---------------------
616263               
1 row selected.
```

<a id="6a348bc934a84ac1"></a>
## UNHEX_TO_CHARSTR

<a id="246ac50f99d0b651"></a>
### 구문

```
UNHEX_TO_CHARSTR( str )
```

<a id="e1811f8881618d90"></a>
### 설명

인자 str은 16진수 문자이며 이를 각 byte로 표현하여 character string으로 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 CHARACTER VARYING이나 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 16진수 범위에 속하지 않는 문자가 포함되면 에러를 반환한다.

자세한 내용은 [HEX](#74db15c6a19d6e5e)와 [UNHEX](#ad3481b3c1a32b46)를 참조한다.

<a id="4793b385e805ba78"></a>
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

<a id="8cca28ecf2cfc2f1"></a>
## USER_ID

<a id="1e74fc049d758fe2"></a>
### 구문

```
USER_ID ()
```

<a id="3875bc7a77b28ebe"></a>
### 설명

현재 사용자의 number ID를 얻는다.

> Cluster system에서는 접속한 server에 따라 다른 값을 가질 수 있다.  
> 현재 사용자의 이름을 얻는 [CURRENT_USER](#1b9a25dc057af2e2) 함수 사용을 권장한다.

<a id="f4154010b3aa6dd6"></a>
### 사용 예

```
% gsql test test

gSQL> SELECT USER_ID() FROM dual;

USER_ID()
---------
        6

1 row selected.
```

<a id="75131efeef783c56"></a>
## UUID

<a id="388e4fe6c2e8c016"></a>
### 구문

```
UUID()
```

<a id="17c8e538725b886a"></a>
### 설명

UUID 함수는 전역고유식별자 (Universal Unique Identifier) 를 생성하여 반환한다.  
반환되는 타입은 VARBINARY 이며 내부적으로 16 바이트로 구성된다.

<a id="e63d92e82136c3e0"></a>
### 사용 예

```
gSQL> SELECT HEX( UUID() ) FROM DUAL;
HEX( UUID() )                   
--------------------------------
E6F0A5C2387511E8B95259E479C2FD50
1 row selected.
```

<a id="2a39166cd54fb778"></a>
## VAR_POP

<a id="20194f06051054c6"></a>
### 구문

```
VAR_POP( expr )
```

<a id="de2a5957d6660455"></a>
### 설명

Aggregation 함수로써 expr set의 모 분산 (population variance)을 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**VAR_POP 인자와 결과 타입**

<a id="8e431d407a7c0ae2"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 분산은 모 집단 (전체)의 분산이며 분산은 편차 제곱의 평균이다. 즉, 데이터의 각 값에서 모 평균 (전체의 평균)을 빼고 제곱해서 모두 더한 뒤 모 집단의 데이터 개수로 나눈다.  
> 이는 각 관찰값들이 평균으로부터 얼마나 많이 퍼져있는지 파악하는데 사용된다.

자세한 내용은 [STDDEV_POP](#691944807590830f) 을 참조한다.

<a id="cb118438713a0033"></a>
### 사용 예

```
gSQL> SELECT VAR_POP(c1) FROM t1;

VAR_POP(C1)
-----------
     105.76

1 row selected.
```

<a id="70d7f8d062fdcab6"></a>
## VAR_SAMP

<a id="bee5506775f1fbe1"></a>
### 구문

```
VAR_SAMP( expr )
```

<a id="ce0fc4d473b5737e"></a>
### 설명

Aggregation 함수로써 expr set의 표본 분산 (sample variance)을 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 NULL값을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**VAR_SAMP 인자와 결과 타입**

<a id="de31a14e7537426d"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 집단 (전체)을 다루는 모 분산과 달리, 표본 분산은 추출한 표본으로 평균과 편차를 다룬다. 즉, 데이터의 각 값에서 표본의 평균을 빼고 제곱해서 모두 더한 뒤, 표본 집단의 데이터 개수 - 1로 나눈다.  
> 이는 모 집단의 분산을 추정하는 데 사용된다.

자세한 내용은 [STDDEV_SAMP](#a1c9763e7cd69449)을 참조한다.

<a id="9f88e1983479839e"></a>
### 사용 예

```
gSQL> SELECT VAR_SAMP(c1) FROM t1;

VAR_SAMP(C1)
------------
       132.2

1 row selected.
```

<a id="1606402ae153f86e"></a>
## VARIANCE

<a id="c74117c472d8b26b"></a>
### 구문

```
VARIANCE( [ ALL | DISTINCT ] expr )
```

<a id="413064f1e5374e34"></a>
### 설명

Aggregation 함수로써 expr set의 분산 (variance)을 얻는다.

ALL을 명시한 경우 모든 값들에 대해 수행하고, DISTINCT를 명시한 경우 중복을 제거한 값들에 대해 수행한다. 둘 다 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

NULL 값을 제외하고 DISTINCT로 중복을 제거한 후의 expr set의 개수가 한 개일 경우, 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**VARIANCE 인자와 결과 타입**

<a id="5034d19572131c98"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> GOLDILOCKS는 분산을 다음과 같이 계산한다.  
> 　• expr set의 개수가 1이면 0을 반환한다.  
> 　• expr set의 개수가 1보다 크면, [VAR_SAMP( expr )](#70d7f8d062fdcab6) 값을 반환한다.

자세한 내용은 [STDDEV](#ef48d7168e3cbd63)를 참조한다.

<a id="9d07c8693235fac8"></a>
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
```

<a id="82119327fc309997"></a>
## VERSION

<a id="619673c1c6d19b85"></a>
### 구문

```
VERSION()
```

<a id="2e1c0674a26fe95b"></a>
### 설명

제품의 version string을 얻는다.

<a id="fc0e9d6671b29af4"></a>
### 사용 예

```
gSQL> SELECT VERSION() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="38f3d78c2ef2508d"></a>
## WIDTH_BUCKET

<a id="709253f9bac54e6d"></a>
### 구문

```
WIDTH_BUCKET( num, min, max, cnt )
```

<a id="8686db2f7db0b9ca"></a>
### 설명

WIDTH_BUCKET 함수는 명시된 min, max 범위에서 cnt와 동일한 넓이를 갖는 구간을 생성하고, num이 속하는 구간의 위치를 반환한다.

인자 num, min, max, cnt에는 숫자 타입이 올 수 있다.

min, max는 구간에 대한 범위를 의미하며, min, max 값이 같은 경우에는 에러를 반환한다.  
cnt는 구간 개수를 의미하고 양의 정수이어야 하며 0 이거나 음수인 경우에는 에러를 반환한다.  
구간의 위치에는 1부터 시작하는 번호가 부여된다.

num, min, max, cnt 중 하나라도 NULL인 경우, 결과값도 NULL이다.

<a id="e523b7cbf0211302"></a>
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
