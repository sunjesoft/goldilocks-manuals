<a id="720e951636c144f4"></a>

# 17. Built-in Function References

> 원본: [GOLDILOCKS 22c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/ko/720e951636c144f4)  
> 태그: `22c.1_10_tag`

[← 16. Built-in Data Type References](16-built-in-data-type-references.md) · [전체 목차](../README.md) · [18. SQL References (A~B) →](18-sql-references-a-b.md)

<a id="a842749e8da6524b"></a>
## * (MULTIPLICATION)

<a id="c93cb5d8e8676c39"></a>
### 구문

```
expr1 * expr2
```

<a id="5a872844e2afd249"></a>
### 설명

expr1과 expr2의 곱하기 연산 결과를 반환한다.

곱하기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#13f721d87552f184)을 참조한다.

**숫자형 * 연산**

<a id="1ab109418a882903"></a>
| expr1 (expr2) | expr2 (expr1) | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="353d1c3ed7505386"></a>
<table class="table column_count_3"><caption>INTERVAL * 연산 </caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>숫자형 타입</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>숫자형 타입</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_left" colspan="3"><div>자세한 내용은 <a class="reference text" href="#ced66a5fbf5b2d18">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

**표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입**

<a id="ced66a5fbf5b2d18"></a>
<table><thead><tr><th align="center">INTERVAL YEAR TO MONTH</th><th align="center">INTERVAL DAY TO SECOND</th></tr></thead><tbody><tr><td valign="middle"><ul><li>INTERVAL YEAR</li><li>INTERVAL MONTH</li><li>INTERVAL YEAR TO MONTH</li></ul></td><td valign="middle"><ul><li>INTERVAL DAY</li><li>INTERVAL HOUR</li><li>INTERVAL MINUTE</li><li>INTERVAL SECOND</li><li>INTERVAL DAY TO HOUR</li><li>INTERVAL DAY TO MINUTE</li><li>INTERVAL DAY TO SECOND</li><li>INTERVAL HOUR TO MINUTE</li><li>INTERVAL HOUR TO SECOND</li><li>INTERVAL MINUTE TO SECOND</li></ul></td></tr></tbody></table>

<a id="df0b524e8769f589"></a>
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

<a id="9c6d59e57297e8d6"></a>
## + (ADDITION)

<a id="dd9e006c9bf316ae"></a>
### 구문

```
expr1 + expr2
```

<a id="fc630d190d55f490"></a>
### 설명

expr1과 expr2의 더하기 연산 결과를 반환한다.

더하기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#13f721d87552f184)을 참조한다.

**숫자형 + 연산**

<a id="e4eca7bab6deaaf0"></a>
| expr1 (expr2) | expr2 (expr1) | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="1daf6f0e545b5943"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) + 연산</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#ced66a5fbf5b2d18">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="659dface1d859949"></a>
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

<a id="90a545af325b31a6"></a>
## + (POSITIVE)

<a id="2b38686dad1ec145"></a>
### 구문

```
+ expr
```

<a id="a48d9e416268e27a"></a>
### 설명

expr에 + 부호를 표시한다.

<a id="9ea56c82c1eacb84"></a>
### 사용 예

```
gSQL> SELECT +3 AS RESULT1, +(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      3      -3
1 row selected.
```

<a id="04d3079c3c0cce94"></a>
## - (NEGATIVE)

<a id="3b4f083e1e90ce53"></a>
### 구문

```
- expr
```

<a id="7b017a9010d658c7"></a>
### 설명

expr에 - 부호를 표시한다.

<a id="bd69937fb2d56f0f"></a>
### 사용 예

```
gSQL> SELECT -3 AS RESULT1, -(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     -3       3
1 row selected.
```

<a id="e52b1a1f7ed28013"></a>
## - (SUBTRACTION)

<a id="977d155d1665958b"></a>
### 구문

```
expr1 - expr2
```

<a id="cc067acdf75bd122"></a>
### 설명

expr1과 expr2의 뺄셈 연산 결과를 반환한다.

뺄셈 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#13f721d87552f184)을 참조한다.

**숫자형 - 연산**

<a id="7fa8e303349b7df6"></a>
| expr1 | expr2 | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="de14e9cf53e6ac6a"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) - 연산</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMBER</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#ced66a5fbf5b2d18">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="76b3765ac112ff78"></a>
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

<a id="540345df2d77ac37"></a>
## / (DIVISION)

<a id="83ee42edda68f9c5"></a>
### 구문

```
expr1 / expr2
```

<a id="a591fcbcf4ed79a6"></a>
### 설명

expr1과 expr2의 나누기 연산 결과를 반환한다.

나누기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#13f721d87552f184)을 참조한다.

**숫자형/ 연산**

<a id="cd479b4941e2be7f"></a>
| expr1 | expr2 | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER | NUMBER |
| NATIVE_DOUBLE | NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="0912e15dcc64dab0"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL)/ 연산</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(결과 타입은 interval type 이다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#ced66a5fbf5b2d18">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="6eda967a1efbeb18"></a>
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

<a id="94d05d46527b1454"></a>
## || (CONCATENATE)

<a id="ac099de94f3324b4"></a>
### 구문

```
str1 || str2
```

<a id="2576e6a076fa7c30"></a>
### 설명

CONCATENATE는 str1과 str2를 연결한 문자열을 반환한다.

str1과 str2 중 하나가 null인 경우 null이 아닌 나머지 str이 반환되고, str1과 str2가 모두 null인 경우 NULL이 반환된다.

인자로는 character string 타입 또는 binary string 타입으로 변환될 수 있는 타입이 올 수 있다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#13f721d87552f184)을 참조한다.

[CONCAT](#21898ed289b71e9e), [CONCATENATE](#e1ffa015dcc39973)의 alias 이다.

결과 타입은 다음 표와 같다.

**|| (CONCATENATE)의 결과 타입**

<a id="23844ddbc147f366"></a>
| Data type | CHAR | VARCHAR | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR | CHAR | VARCHAR | LONG VARCHAR |
| VARCHAR | VARCHAR | VARCHAR | LONG VARCHAR |
| LONG VARCHAR | LONG VARCHAR | LONG VARCHAR | LONG VARCHAR |
| Data type | BINARY | VARBINARY | LONG VARBINARY |
| BINARY | BINARY | VARBINARY | LONG VARBINARY |
| VARBINARY | VARBINARY | VARBINARY | LONG VARBINARY |
| LONG VARBINARY | LONG VARBINARY | LONG VARBINARY | LONG VARBINARY |

<a id="9ec031a7bb7b5595"></a>
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

<a id="1f4f39b5fe45d62e"></a>
## ABS

<a id="d4c6bf00d6528b4f"></a>
### 구문

```
ABS( num )
```

<a id="99052b75f3cc869a"></a>
### 설명

ABS는 num의 절대값을 반환한다.  

인자 num에는 숫자 타입 또는 숫자로 변환될 수 있는 타입이 올 수 있다.  
num이 NULL이면 NULL을 반환한다.

<a id="a8e169bc788e4cd4"></a>
### 사용 예

```
gSQL> SELECT ABS(-1) AS RESULT1, ABS(1) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1       1
1 row selected.
```

<a id="42c59ba3e29a5923"></a>
## ACOS

<a id="93272146a07f5e00"></a>
### 구문

```
ACOS( num )
```

<a id="9ad2807b26ec3b92"></a>
### 설명

ACOS 함수는 num의 arc cosine 값을 반환한다.  

인자 num은 -1 이상 1 이하의 값이어야 한다.  
num이 NULL이면 NULL을 반환한다.  

0 ~ pi 사이의 라디안 값을 반환한다.

<a id="60dbd2e3fc12f046"></a>
### 사용 예

```
gSQL> SELECT ACOS( 1 ) FROM DUAL;
ACOS( 1 )
---------
        0
1 row selected.
```

<a id="c2a5181352d3260a"></a>
## ADDDATE

<a id="7062e4ffc44b56ed"></a>
### 구문

```
ADDDATE( date, INTERVAL expr unit  )
ADDDATE( expr, days )
```

<a id="c4a889d26bcef011"></a>
### 설명

ADDDATE는 입력받은 첫 번째 인자에 두 번째 인자를 더하기 연산하여 그 결과를 반환한다.  

첫 번째 인자에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있고, 두 번째 인자에는 INTERVAL 또는 숫자 타입이 올 수 있다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.

결과 타입은 [(DATETIME/INTERVAL) + 연산](#1daf6f0e545b5943)과 동일하다.

<a id="3637db5e61471c59"></a>
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

<a id="432fcc73655612f3"></a>
## ADDTIME

<a id="0317b840158cb2c2"></a>
### 구문

```
ADDTIME( expr1, expr2 )
```

<a id="f20724a41fe02be7"></a>
### 설명

ADDTIME은 입력받은 expr2를 expr1에 더하여 그 결과를 반환한다.

expr1에는 TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE TYPE이 올 수 있고, expr2에는 INTERVAL DAY TO SECOND TYPE이 올 수 있다.  

expr1이나 expr2가 NULL이면 결과값은 NULL이다.

결과 타입은 [(DATETIME/INTERVAL) + 연산](#1daf6f0e545b5943)과 동일하다.

<a id="f2818ea41a6799bf"></a>
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

<a id="5d547893c3f897b6"></a>
## ADD_MONTHS

<a id="1db8121b6ac01b7a"></a>
### 구문

```
ADD_MONTHS( date, number )
```

<a id="68d67fda7110b892"></a>
### 설명

ADD_MONTHS는 date에 number 숫자만큼의 달을 더한 값을 반환한다.  
만약 ADD_MONTHS 연산 후에 날짜가 그 달의 마지막 날보다 큰 경우에는 마지막 날짜로 조정한다.  

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있으며 인자 number에는 숫자타입이 올 수 있다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.

결과 타입은 입력 인자 date 타입과 관계없이 항상 DATE 타입이다.

<a id="1b5fcc27d66b7666"></a>
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

<a id="410ae77fae8283c1"></a>
## ASCII

<a id="a6e34e932697e931"></a>
### 구문

```
ASCII( char )
```

<a id="bd43c1f55967d11d"></a>
### 설명

char의 첫 번째 문자에 대한 database character set code를 십진수로 반환한다.

char에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있고, 반환되는 타입은 NUMBER 이다.  
char가 NULL이면 NULL을 반환한다.

<a id="d8dc2a7620b40335"></a>
### 사용 예

```
gSQL> SELECT ASCII( 'G' ) AS RESULT FROM DUAL;
RESULT
------
    71
1 row selected.
```

<a id="79b351cfec571851"></a>
## ASIN

<a id="1a808f6384e60770"></a>
### 구문

```
ASIN( num )
```

<a id="ff6712726a54caa8"></a>
### 설명

ASIN 함수는 num의 arc sin 값을 반환한다.

인자 num은 -1 이상 1 이하의 값이어야 한다.  
num이 NULL이면 NULL을 반환한다.

-pi/2 ~ pi/2 사이의 라디안 값을 반환한다.

<a id="dffeb4dc4caa9c2c"></a>
### 사용 예

```
gSQL> SELECT ASIN( 0 ) FROM DUAL;
ASIN( 0 )
---------
        0
1 row selected.
```

<a id="d1d7d36726d869ed"></a>
## ATAN

<a id="0d0327d41d07c959"></a>
### 구문

```
ATAN( num )
```

<a id="7c158438d9082307"></a>
### 설명

ATAN 함수는 num의 arc tangent 값을 반환한다.

num 값 범위의 제한은 없으며, -pi/2 ~ pi/2 사이의 라디안 값을 반환한다.   
num이 NULL이면 NULL을 반환한다.

<a id="9e09f591e0174565"></a>
### 사용 예

```
gSQL> SELECT ATAN(0.5) FROM DUAL;
       ATAN(0.5)
----------------
.463647609000806
1 row selected.
```

<a id="bce06904c92ef5b0"></a>
## ATAN2

<a id="6b828e692f7021a2"></a>
### 구문

```
ATAN2( num1, num2 )
```

<a id="40c1f339fe13514f"></a>
### 설명

ATAN2 함수는 num1과 num2의 arc tangent 값을 반환한다.

인자 num1 값 범위의 제한은 없으며 -pi ~ pi 사이의 라디안 값을 반환한다.   
num1 또는 num2 중 하나라도 NULL이면 NULL을 반환한다.

<a id="359d82ac3b7e9588"></a>
### 사용 예

```
gSQL> SELECT ATAN2(1,2) FROM DUAL; 
      ATAN2(1,2)
----------------
.463647609000806
1 row selected.
```

<a id="83c5f3d87d8165b5"></a>
## AVG

<a id="9807e646e4d91094"></a>
### 구문

```
AVG( [ ALL | DISTINCT ] num )
```

<a id="fb9143e33b72bf44"></a>
### 설명

Aggregation 함수로써 expr 들의 평균값을 얻는데 사용된다.

ALL을 명시한 경우, 모든 값들에 대한 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복 제거한 값들에 대한 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

<a id="56faf6d7e5c313ae"></a>
### 사용 예

```
gSQL> SELECT AVG(c1) FROM t1;

AVG(C1)
-------
      2

1 row selected.
```

<a id="835b15256b40d117"></a>
## AVG() OVER

<a id="d63fdcdc3d50eb6a"></a>
### 구문

```
AVG ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="dc445a0cbb133b51"></a>
### 설명

Window function AVG는 expr의 평균값을 구하는 함수이다.  
NULL 값은 연산에서 제외된다.

<a id="5016fd885f77158d"></a>
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

<a id="c7c27fffddd355a9"></a>
## BITAND

<a id="d8aabf5aed17868f"></a>
### 구문

```
BITAND( num1, num2 )
```

<a id="cd945f8b5d60db88"></a>
### 설명

num1과 num2의 비트에 대한 AND 연산 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.

결과 타입은 NATIVE_BIGINT이다.

<a id="c732f01985e9de8c"></a>
### 사용 예

```
gSQL> SELECT BITAND(2, 4) FROM DUAL;
BITAND(2, 4)
------------
           0
1 row selected.
```

<a id="c65bd08f03b880a1"></a>
## BITNOT

<a id="55be9dfa6b6547b5"></a>
### 구문

```
BITNOT( num )
```

<a id="e07a09b776d032f6"></a>
### 설명

num의 비트에 대해 NOT 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자가 NULL이면 결과값도 NULL이다.

결과 타입은 다음과 같다.  
• 입력 인자가 NATIVE_SMALLINT인 경우, NATIVE_SMALLINT  
• 입력 인자가 NATIVE_INTEGER인 경우, NATIVE_INTEGER  
• 입력 인자가 NATIVE_BIGINT인 경우, NATIVE_BIGINT

<a id="e9ad7e930a4b763f"></a>
### 사용 예

```
gSQL> SELECT BITNOT( 5 ) AS RESULT FROM DUAL;
RESULT
------
    -6
1 row selected.
```

<a id="58dc5eeae984843f"></a>
## BITOR

<a id="c53759a600c98a2e"></a>
### 구문

```
BITOR( num1, num2 )
```

<a id="d755d5ff65abe90e"></a>
### 설명

num1과 num2의 비트에 대해 OR 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자의 값이 하나라도 NULL이면 결과는 NULL이다.

결과 타입은 NATIVE_BIGINT이다.

<a id="297f21a51e3924a3"></a>
### 사용 예

```
gSQL> SELECT BITOR( 2, 4 ) FROM DUAL;
BITOR( 2, 4 )
-------------
            6
1 row selected.
```

<a id="0e23bc40878f5030"></a>
## BITXOR

<a id="9657283c5f46b621"></a>
### 구문

```
BITXOR( num1, num2 )
```

<a id="4861af6dff0669c1"></a>
### 설명

num1과 num2의 비트에 대해 XOR 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자의 값이 하나라도 NULL이면 결과는 NULL이다.

결과 타입은 NATIVE_BIGINT이다.

<a id="c3b3ae2b46482985"></a>
### 사용 예

```
gSQL> SELECT BITXOR( 5, 3 ) FROM DUAL;
BITXOR( 5, 3 )
-------------
            6
1 row selected.
```

<a id="ace36ceae7d6f8bf"></a>
## BIT_LENGTH

<a id="cd40a84419175998"></a>
### 구문

```
BIT_LENGTH( str )
```

<a id="dfdbfd5fe26d0641"></a>
### 설명

BIT_LENGTH는 str의 비트 수를 반환한다.  
str이 NULL이면 NULL을 반환한다.

<a id="302d9ddacc3823eb"></a>
### 사용 예

```
gSQL> SELECT BIT_LENGTH( 'LIKE' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
             32
    1 row selected.
```

<a id="6df1a08d7fc63870"></a>
## BYTE_LENGTH

<a id="f406472235b545d2"></a>
### 구문

```
BYTE_LENGTH( str )
```

<a id="24cab1de5f96cfca"></a>
### 설명

OCTET_LENGTH의 alias이다.  
자세한 내용은 [OCTET_LENGTH](#a18ea2fd60d92536), [LENGTHB](#ab2de866cc92bd9f)를 참조한다.

<a id="1dc044e430736a1d"></a>
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

<a id="682868a8233ab008"></a>
## CASE2

<a id="07c16a25c0e48734"></a>
### 구문

```
CASE2( condition1, result1
      [, condition2, result2
       , ...
       , conditionN, resultN ]
      [, default ] )
```

<a id="b3c025a8a7650935"></a>
### 설명

CASE2는 기술된 순서대로 condition을 평가한다.  
비교 결과가 FALSE이면 TRUE가 나올 때까지 평가한다.  
비교 결과가 TRUE이면 대응되는 result를 반환하고, 이후는 평가하지 않는다.  
비교 결과가 모두 FALSE인 경우에는 default를 반환하고, default가 생략된 경우에는 NULL을 반환한다.

result에 여러 type이 오는 경우, [결과 타입 조합 규칙](11-sql-elements.md#1f2159979be55fba)에 따라 result type이 결정된다.

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

<a id="4f3b5dd966bae76b"></a>
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

<a id="91d8799032c0d362"></a>
## CBRT

<a id="ae3774708c6f8bdd"></a>
### 구문

```
CBRT( num )
```

<a id="8d8cf99e8e31ae5c"></a>
### 설명

num의 세제곱근을 반환한다.  
num이 NULL이면 결과값도 NULL이 반환된다.

<a id="3fd4e52787729d94"></a>
### 사용 예

```
gSQL> SELECT CBRT( 27 ) FROM DUAL;
CBRT( 27 )
----------
         3
1 row selected.
```

<a id="a1a2d68e02c98341"></a>
## CEIL

<a id="8acbdbc8677e1404"></a>
### 구문

```
CEIL( num )
CEILING( num )
```

<a id="fe56376a17ea0f1e"></a>
### 설명

CEIL 함수는 num 보다 크거나 같은 가장 작은 정수를 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="820053b9450b0c81"></a>
### 사용 예

```
gSQL> SELECT CEIL( 3.5 ) AS RESULT1, CEIL( -3.5 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      4      -3
1 row selected.
```

<a id="b519d2a71da13c53"></a>
## CHAR_LENGTH

<a id="7bbc1bec5fd3592d"></a>
### 구문

```
CHAR_LENGTH( str )            
CHARACTER_LENGTH( str )
```

<a id="c648b3c8800f9adc"></a>
### 설명

CHAR_LENGTH는 str에 대해 character set에 따른 문자수를 반환한다.

str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있고, 반환되는 타입은 NATIVE_BIGINT 이다.

str의 타입이 CHARACTER 타입이면 공백문자 (trailing blank)를 포함하여 계산한다.  
str이 NULL이면 NULL이 반환된다.

[LENGTH](#8e1ef05fbd729197)의 alias이다.

<a id="8ebea78498dea164"></a>
### 사용 예

Multi byte character set: (예:UTF8)

```
gSQL> SELECT CHAR_LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="f77af64b0edbf108"></a>
## CHR

<a id="2e25ce17b4f02d03"></a>
### 구문

```
CHR( num )
```

<a id="3eb43ffbc7ad3073"></a>
### 설명

num에 대응하는 database character set code 내의 charater를 반환한다.

num은 숫자 타입이다.  
num이 NULL이면 NULL을 반환한다.  

결과 타입은 VARCHAR 이다.

<a id="4bbb8abb511b1422"></a>
### 사용 예

```
gSQL> SELECT CHR(71) FROM DUAL;
CHR(71)
-------
G      
1 row selected.
```

<a id="04bcbdc9ceffb73e"></a>
## CLOCK_DATE

<a id="b8038f9f9a3837d5"></a>
### 구문

```
CLOCK_DATE()
```

<a id="113e412d1adacba8"></a>
### 설명

함수가 호출될 때마다 현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="2544491013c9c55a"></a>
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

<a id="86d4c2de879cba29"></a>
## CLOCK_LOCALTIME

<a id="2475e7532c71830e"></a>
### 구문

```
CLOCK_LOCALTIME()
```

<a id="f022fe0425b3f6e7"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 없는 현재 시간 (TIME WITHOUT TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="edf386ce2b29e2ba"></a>
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

<a id="2791e46bc688a1d5"></a>
## CLOCK_LOCALTIMESTAMP

<a id="fae93e6286b8e867"></a>
### 구문

```
CLOCK_LOCALTIMESTAMP()
```

<a id="28b805c1c60c5705"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 없는 현재 TIMESTAMP (TIMESTAMP WITHOUT TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="8f445d9ff49f184e"></a>
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

<a id="f158497fd0a1fb54"></a>
## CLOCK_TIME

<a id="be044a1893f01fba"></a>
### 구문

```
CLOCK_TIME()
```

<a id="3265a5aea6e56e60"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="8fb90887e8d790ce"></a>
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

<a id="1f2ff85c6ba57bd4"></a>
## CLOCK_TIMESTAMP

<a id="2348933f359456bb"></a>
### 구문

```
CLOCK_TIMESTAMP()
```

<a id="2d25e51fad667386"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="0c00b6557497b6bc"></a>
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

<a id="e259af4354869c93"></a>
## COALESCE

<a id="484cbc6b903f6fb9"></a>
### 구문

```
COALESCE( expr1, ..., exprN )
```

<a id="1156f03134d85bef"></a>
### 설명

expr list들 중에 null이 아닌 첫 번째 expr을 반환한다.  
expr list들이 모두 null인 경우에는 null을 반환한다.  
expr은 두 개 이상이어야 한다.

expr list에 여러 type들이 오는 경우에는 [결과 타입 조합 규칙](11-sql-elements.md#1f2159979be55fba)에 따라 result type이 결정된다.

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

<a id="1c3692cca64ceaf8"></a>
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

<a id="21898ed289b71e9e"></a>
## CONCAT

<a id="5acc077f3949bf17"></a>
### 구문

```
CONCAT( str1, str2, ... )
```

<a id="2442b11625fad04b"></a>
### 설명

\|| ( CONCATENATE )의 alias 이다.  
CONCAT 함수의 argument로써 2 ~ 254 개까지 설정할 수 있다.  
자세한 내용은 [|| (CONCATENATE)](#94d05d46527b1454), [CONCATENATE](#e1ffa015dcc39973)를 참조한다.

<a id="162524928a144bdd"></a>
### 사용 예

```
gSQL> SELECT CONCAT( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="e1ffa015dcc39973"></a>
## CONCATENATE

<a id="a7260f65941e9d5f"></a>
### 구문

```
CONCATENATE( str1, str2, ... )
```

<a id="690910282a68504e"></a>
### 설명

\|| ( CONCATENATE ) 의 alias 이다.  
CONCATENATE 함수의 argument로 2 ~ 254 개까지 설정할 수 있다.  
자세한 내용은 [CONCAT](#21898ed289b71e9e), [|| (CONCATENATE)](#94d05d46527b1454)를 참조한다.

<a id="c4614e5cc67716a7"></a>
### 사용 예

```
gSQL> SELECT CONCATENATE( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="d9632d2ba01ca2d7"></a>
## CORR() OVER

<a id="54967768e4e9fabf"></a>
### 구문

```
CORR( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="3222b8b9f9b34b20"></a>
### 설명

Window function CORR는 expr 쌍의 상관계수 (coefficient of correlation)를 구하는 함수이다.

expr1 또는 expr2가 NULL일 경우, 계산에서 제외된다.  
expr 쌍의 row 개수가 한 개 이하일 경우, 결과로 NULL을 반환한다.

<a id="7dfb7a0095257d53"></a>
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

<a id="97e86e962965cea7"></a>
## COS

<a id="9ca4584dbbf2b04c"></a>
### 구문

```
COS(num)
```

<a id="94f53e12533ccb26"></a>
### 설명

num의 COSINE 값을 반환한다.  
인자값 num이 NULL이면 결과값도 NULL이다.

<a id="9a0867cf61f34c90"></a>
### 사용 예

```
gSQL> SELECT COS( 0 ) FROM DUAL;
COS( 0 )
--------
       1
1 row selected.
```

<a id="a275aa46b32ad0ac"></a>
## COT

<a id="75f25f7744a85d00"></a>
### 구문

```
COT(num)
```

<a id="79f7d4e44bbf1053"></a>
### 설명

num의 COTANGENT 값을 반환한다.  
인자값 num이 NULL이면 결과값도 NULL이다.

<a id="b69eb85aa011db3b"></a>
### 사용 예

```
gSQL> SELECT COT( 1 ) FROM DUAL;
        COT( 1 )
----------------
.642092615934331
1 row selected.
```

<a id="58e206fbb98f3db9"></a>
## COUNT

<a id="43a9a122a53e73ef"></a>
### 구문

```
COUNT( [ ALL | DISTINCT ] expr )
```

<a id="2a280b5d92bf094e"></a>
### 설명

Aggregation 함수로써 expr이 NULL 값이 아닌 row의 개수를 얻는다.

ALL을 명시한 경우, 모든 값들에 대한 aggregation을 수행한다.  
DISTINCT을 명시한 경우, 중복 제거한 값들에 대한 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

<a id="b6764b4ddf6c7110"></a>
### 사용 예

```
gSQL> SELECT COUNT(c1) FROM t1;

COUNT(C1)
---------
        3

1 row selected.
```

<a id="6b3846c0e98dfbb0"></a>
## COUNT() OVER

<a id="e86e37a0ed6e4cfa"></a>
### 구문

```
COUNT ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="da9862b71dde573b"></a>
### 설명

Window function COUNT는 row의 개수를 세는 함수이다.  
NULL 값은 연산에서 제외된다.

<a id="807a2059c616f439"></a>
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

<a id="1a7a24f23c859a1c"></a>
## COUNT(*)

<a id="3832c4129f401482"></a>
### 구문

```
COUNT(*)
```

<a id="346a4a5b82bc7dc1"></a>
### 설명

Aggregation 함수로써 row의 개수를 얻는다.   
별도의 expression을 지정하지 않으므로 값의 NULL 여부와 무관하다.

<a id="96e58517fb60da2d"></a>
### 사용 예

```
gSQL> SELECT COUNT(*) FROM t1;

COUNT(*)
--------
       4

1 row selected.
```

<a id="f18cfec75b1aca69"></a>
## COUNT(*) OVER

<a id="44d28a3afe9e585d"></a>
### 구문

```
COUNT(*) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="406d907d635decf7"></a>
### 설명

Window function COUNT(*)는 row의 개수를 세는 함수이다.  
별도로 expression을 지정하지 않으므로 값의 NULL 여부와는 무관하다.

<a id="fcbf72f589f57b3c"></a>
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

<a id="943b1f26a1391c68"></a>
## COVAR_POP() OVER

<a id="ee9502d31f546ad1"></a>
### 구문

```
COVAR_POP( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="322ae43b8ab07bc2"></a>
### 설명

Window function COVAR_POP은 expr 쌍의 모집단 공분산 (population covariance)을 구하는 함수이다.

expr1 또는 expr2가 NULL일 경우, 계산에서 제외된다.   
expr 쌍의 row 개수가 한 개 이하일 경우, 결과로 0을 반환한다.

<a id="a7aa5e64622868ce"></a>
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

<a id="ec44fe8e0d27217a"></a>
## COVAR_SAMP() OVER

<a id="a20de7e55f1f81fc"></a>
### 구문

```
COVAR_SAMP( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="265975b058736ad8"></a>
### 설명

Window function COVAR_SAMP는 expr 쌍의 표본 공분산 (sample covariance)을 구하는 함수이다.

expr1 또는 expr2가 NULL일 경우, 계산에서 제외된다.  
expr 쌍의 row 개수가 한 개 이하일 경우, 결과로 NULL을 반환한다.

<a id="79b6498ba1984cc6"></a>
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

<a id="086281afc9e11656"></a>
## CUME_DIST() OVER

<a id="4cb46231dcbf63a7"></a>
### 구문

```
CUME_DIST( ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="50ce1e7fc5938fd1"></a>
### 설명

Window function CUME_DIST는 현재 row 값의 상대적 위치에 따른 누적 분포도를 계산한다.

CUME_DIST 함수의 결과는 0부터 1 사이의 숫자이다.  
Row들의 값이 같을 경우 그 중에 가장 큰 누적 분포 값으로 동일한 결과를 반환한다.

window frame은 사용할 수 없다.

<a id="cc2f472c1182109a"></a>
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

<a id="9907b96078077446"></a>
## CURRENT_CATALOG

<a id="b7f27796fb4425a1"></a>
### 구문

```
CURRENT_CATALOG [()]
```

<a id="f2fe73baad421026"></a>
### 설명

catalog name (database 이름)을 얻는다.

<a id="6bd7b0813e0bde46"></a>
### 사용 예

```
gSQL> SELECT CURRENT_CATALOG FROM dual;

CURRENT_CATALOG
---------------
TEST_DB        

1 row selected.
```

<a id="cc3c5c6e1a4a1ab3"></a>
## CURRENT_DATE

<a id="f9afe99f33f2a664"></a>
### 구문

```
CURRENT_DATE [()]
STATEMENT_DATE()
```

<a id="d680bf05509b9e86"></a>
### 설명

현재 날짜 (DATE type) 값을 얻는다.

CURRENT_DATE는 SQL 표준 함수이다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• CURRENT_DATE, STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="9770b5a708d2a00c"></a>
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

<a id="c7072a3ca3b390cd"></a>
## CURRENT_SCHEMA

<a id="821aac9586cee8c3"></a>
### 구문

```
CURRENT_SCHEMA [()]
```

<a id="55c0b4ac5423d376"></a>
### 설명

사용자의 현재 SCHEMA를 얻는다.

<a id="fd945c854a5e7716"></a>
### 사용 예

```
gSQL> SELECT CURRENT_SCHEMA FROM dual;

CURRENT_SCHEMA
--------------
PUBLIC        

1 row selected.
```

<a id="4d2334f9a506a5d6"></a>
## CURRENT_TIME

<a id="471bf90a2ad05954"></a>
### 구문

```
CURRENT_TIME [()]
STATEMENT_TIME()
```

<a id="780d40f635775fae"></a>
### 설명

Session 시간을 기준으로 현재 TIME WITH TIME ZONE type 값을 얻는다.

CURRENT_TIME은 SQL 표준 함수이다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• CURRENT_TIME, STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="19f89a4d1d6ece6a"></a>
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

<a id="54b2bf8ace65caa9"></a>
## CURRENT_TIMESTAMP

<a id="103ed62f8dadd39d"></a>
### 구문

```
CURRENT_TIMESTAMP [()]
STATEMENT_TIMESTAMP()
```

<a id="1153238968a1fc31"></a>
### 설명

Session 시간을 기준으로 TIMESTAMP WITH TIME ZONE type 값을 얻는다.

CURRENT_TIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• CURRENT_TIMESTAMP, STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="139dcdfbc3bc4cd2"></a>
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

<a id="4075373efcce5443"></a>
## CURRENT_USER

<a id="ad6f8b96fc8154be"></a>
### 구문

```
CURRENT_USER [()]
```

<a id="eb2c03cd3ee26bea"></a>
### 설명

현재 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다.
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다.
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다.
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="ba73138531d0f0b3"></a>
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

<a id="c26d63f93f4c6a17"></a>
## CURRVAL

<a id="f019c485f016dce5"></a>
### 구문

```
seq_name.CURRVAL
CURRVAL(seq_name)
```

<a id="8a2dd0eace8dd319"></a>
### 설명

시퀀스 객체의 현재 값을 얻는다.

최소 한 번은 NEXTVAL(seq_name) 등으로 시퀀스 값을 설정해야 한다.

<a id="21c6b8b8fa4832ca"></a>
### 사용 예

```
gSQL> SELECT seq.CURRVAL FROM dual;

SEQ.CURRVAL
-----------
          1

1 row selected.
```

<a id="d91b0bdad431e179"></a>
## DATEADD

<a id="292005116b9ac5e0"></a>
### 구문

```
DATEADD( datepart, number, date )
```

<a id="2202501ba5e54b10"></a>
### 설명

date의 지정된 datepart에 number를 더한 값을 반환한다.

number가 소수점인 경우 반올림되지 않는다.  
date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE 타입이 올 수 있다.  
number 또는 date가 NULL인 경우에는 결과값도 NULL이다.

인자로 받은 date의 타입과 동일한 결과 타입이 반환된다.

**datepart에 사용 가능한 형식문자열**

<a id="1f19a3a84447c9d7"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">설명</th></tr><tr><td>YEAR</td><td>년</td></tr><tr><td>QUARTER</td><td>분기</td></tr><tr><td>MONTH</td><td>월</td></tr><tr><td>DAYOFYEAR</td><td>일</td></tr><tr><td>DAY</td><td>요일</td></tr><tr><td>WEEK</td><td>주</td></tr><tr><td>WEEKDAY</td><td>평일</td></tr><tr><td>HOUR</td><td>시</td></tr><tr><td>MINUTE</td><td>분</td></tr><tr><td>SECOND</td><td>초</td></tr><tr><td>MILLISECOND</td><td>밀리세컨드</td></tr><tr><td>MICROSECOND</td><td>마이크로세컨드</td></tr></tbody></table>

<a id="e47236312ea5b6ed"></a>
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

<a id="1aaaa78d6b01287e"></a>
## DATEDIFF

<a id="d61129e16ae37bc3"></a>
### 구문

```
DATEDIFF( datepart, startdate, enddate )
```

<a id="a09a7f3eb20140da"></a>
### 설명

enddate에서 startdate를 뺀 값을 지정된 datepart로 반환한다.

startdate와 enddate에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME TYPE이 올 수 있다.  
startdate 또는 enddate가 NULL이면 결과값도 NULL이다.

결과 타입은 NUMBER이다.

**datepart에 사용 가능한 형식문자열**

<a id="5e302c2a5589b325"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">설명</th></tr><tr><td>YEAR</td><td>년</td></tr><tr><td>QUARTER</td><td>분기</td></tr><tr><td>MONTH</td><td>월</td></tr><tr><td>DAYOFYEAR</td><td>일</td></tr><tr><td>DAY</td><td>요일</td></tr><tr><td>HOUR</td><td>시</td></tr><tr><td>MINUTE</td><td>분</td></tr><tr><td>SECOND</td><td>초</td></tr><tr><td>MILLISECOND</td><td>밀리세컨트</td></tr><tr><td>MICROSECOND</td><td>마이크로세컨드</td></tr></tbody></table>

<a id="389d2f52386f0126"></a>
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

<a id="5ab01cb4a29d4853"></a>
## DATE_ADD

<a id="7c065c6c098f823d"></a>
### 구문

```
DATE_ADD( date, INTERVAL expr unit  )
```

<a id="d4f0c966a274a304"></a>
### 설명

[ADDDATE](#c2a5181352d3260a) ( date, INTERVAL expr unit )와 동일한 함수이다.

<a id="e3145ea233211ca4"></a>
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

<a id="112a5cc6e562361e"></a>
## DATE_PART

<a id="6ca4b2c89b00a27f"></a>
### 구문

```
DATE_PART( field, datetime )
```

<a id="4ca0b2f3be777f78"></a>
### 설명

DATE_PART는 EXTRACT 함수와 결과값이 같은 함수로써 입력한 datetime 타입에서 지정된 field를 찾아 반환한다.

인자 field에는 문자 literal만 올 수 있으며, YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, TIMEZONE_HOUR, TIMEZONE_MINUTE를 문자 literal로 지정할 수 있다.  
인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.

field가 datetime의 범위에 있지 않는 경우 에러를 반환한다.  
또한, DATE 타입인 경우에는 field에 YEAR, MONTH, DAY 만 올 수 있고, 그 외에는 에러를 반환한다.  
datatime이 NULL이면 NULL을 반환한다.  

반환되는 타입은 NUMBER이다.

자세한 내용은 [EXTRACT](#0175a57e731e4b60)를 참조한다.

<a id="d019614790a371a8"></a>
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

<a id="905d19774e15a365"></a>
## DECODE

<a id="dc003bce32778f19"></a>
### 구문

```
DECODE( expr, comparison_expr1, result1
           [, comparison_expr2, result2
            , ...
            , comparison_exprN, resultN ]
           [, default ] )
```

<a id="aec8e3ba87f15c64"></a>
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

<a id="9ffc5706b9877713"></a>
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

<a id="f5f62649420167d6"></a>
## DEGREES

<a id="6b5fbb9f30e05deb"></a>
### 구문

```
DEGREES( radians )
```

<a id="3e37da256177af8e"></a>
### 설명

라디안 단위로 표시된 각도 radians를 도 단위로 변환한 값을 반환한다.  
radians가 NULL이면 NULL이 반환된다.

<a id="e9638ff338525e83"></a>
### 사용 예

```
gSQL> SELECT DEGREES( PI() ) AS RESULT FROM DUAL;
RESULT
------
   180
1 row selected.
```

<a id="bad7f99d700c87c5"></a>
## DENSE_RANK() OVER

<a id="29f513c07faa2be6"></a>
### 구문

```
DENSE_RANK( ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="ed0dbd64473ed448"></a>
### 설명

Window function DENSE_RANK는 순위를 계산하는 함수이다.

순위는 1부터 시작하는 연속적인 정수이고, 값이 같은 row는 순위도 동일하다.  
그러나 RANK와는 다르게 값이 같은 row들이 나와도 순위를 건너뛰지 않는다.

window frame은 사용할 수 없다.

<a id="246ef13be26cc4e1"></a>
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

<a id="3347f8813d778ce7"></a>
## DIGEST

<a id="107296bd787add4e"></a>
### 구문

```
DIGEST( data, type )
```

<a id="d341fa2dbc4ea34e"></a>
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

<a id="e7cbbb14b4031087"></a>
### 사용 예

```
gSQL> SELECT HEX( DIGEST( 'my password', 'SHA256' ) ) AS RESULT FROM DUAL;

RESULT                                                          
----------------------------------------------------------------
BB14292D91C6D0920A5536BB41F3A50F66351B7B9D94C804DFCE8A96CA1051F2

1 row selected.
```

<a id="3258901c48487311"></a>
## DUMP

<a id="5670c1071f331e6f"></a>
### 구문

```
DUMP( expr )
```

<a id="46364bb4e383fd22"></a>
### 설명

DUMP 함수는 expr의 내부 표현정보를 반환한다.  
내부 표현정보는 데이터 타입, 길이 (byte length), 데이터 정보로 보여준다.

expr에는 모든 타입이 가능하다.  
expr이 NULL이면 NULL을 반환한다.  

반환되는 타입은 CHARACTER VARYING이다.

<a id="3bcf9009d56f315c"></a>
### 사용 예

```
gSQL> SELECT DUMP( 'DUMP' ) AS RESULT FROM DUAL;
RESULT                           
---------------------------------
Type=CHAR Len=4 : Str=68,85,77,80
1 row selected.
```

<a id="4ed33f779675d012"></a>
## EXP

<a id="d9722718a3c4076c"></a>
### 구문

```
EXP( num )
```

<a id="1edf468d6d501564"></a>
### 설명

EXP 함수는 e (자연로그 베이스)의 num의 제곱값을 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="b9a8fafa4f5cc3a1"></a>
### 사용 예

```
gSQL> SELECT EXP( 1 ) AS RESULT FROM DUAL;
          RESULT
----------------
2.71828182845905
1 row selected.
```

<a id="0175a57e731e4b60"></a>
## EXTRACT

<a id="f6f0966d2bcacbf3"></a>
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

<a id="94b06522b7472e1f"></a>
### 설명

EXTRACT는 입력한 datetime 타입에서 지정된 field를 찾아 반환한다.

인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.

field가 datetime의 범위에 있지 않는 경우에는 에러를 반환한다.  
또, DATE 타입인 경우에는 field에 YEAR, MONTH, DAY만 올 수 있고, 그 외의 경우에는 에러를 반환한다.  
반환되는 타입은 NUMBER이다.

EXTRACT 함수의 결과는 [DATE_PART](#112a5cc6e562361e)와 동일하다.

<a id="a4b2187ed68b5cab"></a>
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

<a id="1501f0eb209f71bb"></a>
## FACTORIAL

<a id="2860d810ab93e3a1"></a>
### 구문

```
FACTORIAL( num )
```

<a id="e2ec4e6ea34faafd"></a>
### 설명

FACTORIAL 함수는 1 ~ num 까지의 연속된 자연수를 차례로 곱한 값을 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="c27c79c42b1a532c"></a>
### 사용 예

```
gSQL> SELECT FACTORIAL( 5 ) AS RESULT FROM DUAL;
RESULT
------
   120
1 row selected.
```

<a id="52cb50b571038ebf"></a>
## FIRST() OVER

<a id="c1967d83e7fc698d"></a>
### 구문

```
aggregation_function KEEP ( DENSE_RANK FIRST ORDER BY <sort specification list> ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="4104310512c9cf7a"></a>
### 설명

Window function FIRST 함수는 KEEP 절 내 order by에 쓰인 sort specification list를 정렬한 후, DENSE_RANK 순위가 1인 row들의 aggregation function 값을 반환한다.

aggregation_function에 해당하는 함수는 AVG, COUNT, COUNT(*), SUM, MAX, MIN, STDDEV, VARIANCE 이다.

window 절 내에서 order by는 사용할 수 없다.  
window frame은 사용할 수 없다.

<a id="14db6611c511d400"></a>
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

<a id="0e013a10bffcc0b1"></a>
## FIRST_VALUE() OVER

<a id="c2f23935a184dcfd"></a>
### 구문

```
FIRST_VALUE ( expr ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

FIRST_VALUE ( expr [ RESPECT NULLS | IGNORE NULLS ] ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="665c37ea8e0c56c1"></a>
### 설명

Window function FIRST_VALUE는 expr의 첫 번째 값을 반환한다.

RESPECT NULLS는 NULL 값을 포함하여 row 중에 가장 첫 번째 값을 반환한다.  
IGNORE NULLS는 NULL이 아닌 row 중에 가장 첫 번째 값을 반환한다.  
명시하지 않으면 기본값은 RESPECT NULLS 이다.

window 절 내에서 order by는 사용할 수 없다.  
window frame은 사용할 수 없다.

<a id="ced06f849752c6a5"></a>
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

<a id="444bf2ec527abba9"></a>
## FLOOR

<a id="3f3b2a91efcd4cc2"></a>
### 구문

```
FLOOR( num )
```

<a id="2668e4190028a034"></a>
### 설명

FLOOR 함수는 num 보다 크지 않은 가장 큰 정수를 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="aee99559d1a9dbfa"></a>
### 사용 예

```
gSQL> SELECT FLOOR(42.8) AS RESULT1, FLOOR(-42.8) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     42     -43
1 row selected.
```

<a id="c27d56064ad6329e"></a>
## FROM_BASE64

<a id="ef1299c1ec8ddace"></a>
### 구문

```
FROM_BASE64( str )
```

<a id="0c342e7a30731d8e"></a>
### 설명

FROM_BASE64는 base64 인코딩으로 변환된 문자를 입력 받아 디코딩된 binary string을 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 BINARY VARYING 또는 BINARY LONG VARYING과 같은 BINARY 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 base64 문자 범위에 속하지 않는 문자가 포함되면, 에러를 반환한다.  
디코딩 할 때 str의 newline, carriage return, tab, space는 무시된다.

자세한 내용은 [TO_BASE64](#0be5effb386e026c)를 참조한다.

<a id="7a4254f4c962be61"></a>
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

<a id="a29c27126b850dbe"></a>
## FROM_TZ

<a id="ae9d829d8069af2e"></a>
### 구문

```
FROM_TZ( timestamp, timezone )
```

<a id="b8e1b5e0e79560b0"></a>
### 설명

FROM_TZ 함수는 timestamp와 정해진 format의 timezone을 TIMESTAMP WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 timestamp는 TIMESTAMP 타입이거나 TIMESTAMP 타입으로 변환이 가능해야 한다.   
인자 timestamp가 NULL이면 결과는 NULL이다.

인자 timezone은 CHARACTER, CHARACTER VARYING와 같은 CHARACTER 문자 타입이어야 하며, format은 'TZH:TZM'이다.   
인자 timezone이 NULL이면 결과는 NULL이다.

결과 타입은 TIMESTAMP(6) WITH TIME ZONE 이다.

<a id="b438acaa3f3d7707"></a>
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

<a id="7391c4b9201fd9c4"></a>
## GREATEST

<a id="edcddd8fca0e362e"></a>
### 구문

```
GREATEST( expr1 [, expr2, ... exprn ] )
```

<a id="cba1bb821891a675"></a>
### 설명

GREATEST 함수는 인자로 받은 expr들 중에 가장 큰 값을 반환한다.

인자로 받은 expr들 중 하나라도 NULL인 경우, 결과값은 NULL이다.

결과 타입은 expr1 (첫 번째 expr)의 데이터 타입이다.  
expr1 (첫 번째 expr)의 데이터 타입이 숫자형인 경우와 문자형인 경우는 각각 expr1, ..., exprN의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, ..., exprN에 모두 CHAR 타입이 기술된 경우, 모든 expr은 VARCHAR 타입으로 비교되고, 결과 타입은 VARCHAR 타입으로 결정된다.

<a id="471212b7d9cb8c8d"></a>
### 사용 예

```
gSQL> SELECT GREATEST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
   200
1 row selected.
```

<a id="8342c475ec896fe9"></a>
## HASH32

<a id="f9ef04ece4bd40ca"></a>
### 구문

```
HASH32( expr [, expr]... )
```

<a id="cd1be48e780d6bd7"></a>
### 설명

HASH32 함수는 인자로 받은 expr들의 해시값을 계산하여 반환한다.

인자는 최소 1개부터 최대 32개까지 기술할 수 있다.  
입력 인자에 하나라도 NULL이 포함되어 있으면 결과값은 NULL이다.

결과 타입은 NATIVE_INTEGER 타입이다.

<a id="184ae830f32fc4ab"></a>
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

<a id="52d5e89a219d4ad8"></a>
## HEX

<a id="238c31e94e26f263"></a>
### 구문

```
HEX( str )
```

<a id="274bb09aeb62dfd5"></a>
### 설명

인자 str을 16진수 문자로 반환한다.  
인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입 또는 문자 타입으로 변환될 수 있는 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.  
결과 타입은 CHARACTER VARYING 또는 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.

HEX 함수의 인자로 숫자타입이 오는 경우에는 에러를 반환한다.  
10진수 숫자를 16진수로 변환하고자 하는 경우에는  'X' number format을 이용한 TO_CHAR() 함수를 사용할 수 있다.  
예: TO_CHAR( 255, 'XX' )

자세한 내용은 [UNHEX](#2f7997bd53d13aae)를 참조한다.

<a id="90b235fd4a26288d"></a>
### 사용 예

```
gSQL> SELECT HEX( 'abc' ) FROM DUAL;
HEX( 'abc' )
------------
616263      
1 row selected.
```

<a id="7a1f67e4185b474c"></a>
## INITCAP

<a id="5da3a06d09760238"></a>
### 구문

```
INITCAP( str )
```

<a id="bf9aa48b188425a2"></a>
### 설명

INITCAP 함수는 주어진 문자열 str의 각 단어들의 첫 번째 문자를 대문자로 변환하고 첫 번째 문자 이후의 문자를 소문자로 변환하여 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.

문자열의 각 단어는 white space, 알파벳 또는 숫자가 아닌 문자로 구분한다.  
str이 NULL이면 결과값도 NULL이다.

인자로 받는 str의 타입과 동일한 타입이 반환된다.

<a id="0c022f4fbe5c872c"></a>
### 사용 예

```
gSQL> SELECT INITCAP( 'hi GLIESE' ) AS RESULT FROM DUAL;
RESULT   
---------
Hi Gliese
1 row selected.
```

<a id="5570dbb806e3f64b"></a>
## INSTR

<a id="3a40118cf2ab46d7"></a>
### 구문

```
INSTR( str, substr [, position [, occurrence ] ] )
```

<a id="e8b4113f721fabbc"></a>
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

<a id="0243aa74ed55cd7e"></a>
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

<a id="b61dd6a49c780b6c"></a>
## JSON_ARRAY

<a id="a03d7cc5294c5587"></a>
### 구문

```
JSON_ARRAY( [ value_expression [, ...] ]
            [<JSON constructor null clause>]
            [<JSON output clause>]
          )
```

&lt; JSON constructor null clause &gt;에 대한 자세한 내용은 [JSON Constructor Null Clause](11-sql-elements.md#1b21a71bc53a0bdb)를 참조한다.

&lt; JSON output clause &gt;에 대한 자세한 내용은 [JSON Output Clause](11-sql-elements.md#9111e5ebb45ba887)를 참조한다.

<a id="4947b61e34ee512f"></a>
### 설명

JSON_ARRAY는 0개 이상의 expr을 JSON ARRAY 문자열로 반환한다.

JSON constructor null clause는 SQL null 값을 어떻게 처리할지 지정하는 옵션이다.  
명시하지 않으면 기본값은 ABSENT ON NULL이다.

JSON output clause는 함수 결과의 데이터 타입을 지정하는 옵션이다.  
명시하지 않으면 기본값은 VARCHAR(4000)이다.

<a id="ee08029b33d7faf2"></a>
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

<a id="f83ff049ae9a4dca"></a>
## JSON_ARRAYAGG

<a id="cefc02079f94d2ac"></a>
### 구문

```
JSON_ARRAYAGG( value_expression
               [<JSON constructor null clause>]
               [<JSON output clause>]
             )
```

&lt; JSON constructor null clause &gt;에 대한 자세한 내용은 [JSON Constructor Null Clause](11-sql-elements.md#1b21a71bc53a0bdb)를 참조한다.

&lt; JSON output clause &gt;에 대한 자세한 내용은 [JSON Output Clause](11-sql-elements.md#9111e5ebb45ba887)를 참조한다.

<a id="aae4899411320e7a"></a>
### 설명

JSON_ARRAYAGG는 aggregation 함수로서 value expression을 연결하여 한 개의 JSON array string row를 반환한다.

JSON constructor null clause는 SQL null 값을 어떻게 처리할지 지정하는 옵션이다.  
명시하지 않으면 기본값은 ABSENT ON NULL이다.

JSON output clause는 함수 결과의 데이터 타입을 지정하는 옵션이다.  
명시하지 않으면 기본값은 VARCHAR(4000)이다.

<a id="0c5ab82530305dc2"></a>
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
```

<a id="b4e9b27c653ad930"></a>
## JSON_ARRAYAGG() OVER

<a id="b393107fa5db9e56"></a>
### 구문

```
JSON_ARRAYAGG( value_expression
               [<JSON constructor null clause>]
               [<JSON output clause>]
             ) OVER < window name or specification >
```

&lt; JSON constructor null clause &gt;에 대한 자세한 내용은 [JSON Constructor Null Clause](11-sql-elements.md#1b21a71bc53a0bdb)를 참조한다.

&lt; JSON output clause &gt;에 대한 자세한 내용은 [JSON Output Clause](11-sql-elements.md#9111e5ebb45ba887)를 참조한다.

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="bd6ddb7bf969793f"></a>
### 설명

Window function JSON_ARRAYAGG는 window 범위 내의 value expression을 연결하여 JSON array 문자열을 생성하는 함수이다.

JSON constructor null clause는 SQL null 값을 어떻게 처리할지 지정하는 옵션이다.  
명시하지 않으면 기본값은 ABSENT ON NULL이다.

JSON output clause는 함수 결과의 데이터 타입을 지정하는 옵션이다.  
명시하지 않으면 VARCHAR(4000)이다.

<a id="39df14627dba2a96"></a>
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

<a id="4bd256362ba916f7"></a>
## JSON_OBJECT

<a id="1f4285137bf5c503"></a>
### 구문

```
JSON_OBJECT( [ <JSON name and value> [, ...] ]
             [ <JSON constuctor null clause> ]
             [ <JSON output clause> ]
           )

<JSON name and value> ::=
    [KEY] <JSON name> VALUE <value_expression>
  | <JSON name> : <value_expression>
```

&lt; JSON constructor null clause &gt;에 대한 자세한 내용은 [JSON Constructor Null Clause](11-sql-elements.md#1b21a71bc53a0bdb)를 참조한다.

&lt; JSON output clause &gt;에 대한 자세한 내용은 [JSON Output Clause](11-sql-elements.md#9111e5ebb45ba887)를 참조한다.

<a id="6ee4c10592c770d9"></a>
### 설명

JSON_OBJECT는 0개 이상의 JSON name and value를 JSON object 문자열로 반환한다.  
JSON name은 character string으로 표현 가능한 expresssion이어야 한다.

JSON constructor null clause는 SQL null 값을 어떻게 처리할지 지정하는 옵션이다.  
명시하지 않으면 기본값은 NULL ON NULL이다.

JSON output clause는 함수 결과의 데이터 타입을 지정하는 옵션이다.  
명시하지 않으면 기본값은 VARCHAR(4000)이다.

<a id="3499b3e2ab57e12f"></a>
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

<a id="0f4b8dc36d92141a"></a>
## JSON_OBJECTAGG

<a id="5bbf29f9e2fbf2ff"></a>
### 구문

```
JSON_OBJECTAGG( <JSON name and value>
                [ <JSON constructor null clause> ]
                [ <JSON output clause> ]
              )

<JSON name and value> ::=
    [KEY] <JSON name> VALUE <value_expression>
  | <JSON name> : <value_expression>
```

&lt; JSON constructor null clause &gt;에 대한 자세한 내용은 [JSON Constructor Null Clause](11-sql-elements.md#1b21a71bc53a0bdb)를 참조한다.

&lt; JSON output clause &gt;에 대한 자세한 내용은 [JSON Output Clause](11-sql-elements.md#9111e5ebb45ba887)를 참조한다.

<a id="9fb322e7676ee849"></a>
### 설명

JSON_OBJECTAGG는 aggregation 함수로서 JSON name and value 쌍을 연결하여 한 개의 JSON object string row를 반환한다.   
JSON name은 character string으로 표현할 수 있는 expresssion이어야 한다.

JSON constructor null clause는 SQL null 값을 어떻게 처리할지 지정하는 옵션이다.  
명시하지 않으면 기본값은 NULL ON NULL이다.

JSON output clause는 함수 결과의 데이터 타입을 지정하는 옵션이다.  
명시하지 않으면 기본값은 VARCHAR(4000)이다.

<a id="9fd4da8d82cc988e"></a>
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
```

<a id="84fd623d2f683372"></a>
## JSON_OBJECTAGG() OVER

<a id="1c14729ab93fa12c"></a>
### 구문

```
JSON_OBJECTAGG( <JSON name and value>
                [ <JSON constructor null clause> ]
                [ <JSON output clause> ]
              ) OVER < window name or specification >

<JSON name and value> ::=
    [KEY] <JSON name> VALUE <value_expression>
  | <JSON name> : <value_expression>
```

&lt; JSON constructor null clause &gt;에 대한 자세한 내용은 [JSON Constructor Null Clause](11-sql-elements.md#1b21a71bc53a0bdb)를 참조한다.

&lt; JSON output clause &gt;에 대한 자세한 내용은 [JSON Output Clause](11-sql-elements.md#9111e5ebb45ba887)를 참조한다.

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="8685ecafa9b3855e"></a>
### 설명

Window function JSON_OBJECTAGG는 window 범위 내의 JSON name and value 쌍을 연결하여 JSON object 문자열을 생성하는 함수이다.   
JSON name은 character string으로 표현할 수 있는 expresssion이어야 한다.

JSON constructor null clause는 SQL null 값을 어떻게 처리할지 지정하는 옵션이다.  
명시하지 않으면 기본값은 NULL ON NULL이다.

JSON output clause는 함수 결과의 데이터 타입을 지정하는 옵션이다.  
명시하지 않으면 기본값은 VARCHAR(4000)이다.

<a id="162865cc0c1f633d"></a>
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

<a id="05e585e418d8c23d"></a>
## LAG() OVER

<a id="ed28aac94df54f5d"></a>
### 구문

```
LAG ( expr [, offset [, default ] ] ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

LAG ( expr [ RESPECT NULLS | IGNORE NULLS ] [, offset [, default ] ] ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="bd182b2c142088bc"></a>
### 설명

Window function LAG는 현재 row에서 offset 만큼 이전의 row 값을 반환한다.  
Offset이 window 범위를 벗어나면 default 값을 반환한다.

Offset, default 값을 명시하지 않으면 기본값으로 설정된다.  
Offset 기본값은 1이고, default 기본값은 NULL 이다.

RESPECT NULLS는 NULL 값을 포함하여 offset 만큼 이전의 row 값을 반환한다.  
IGNORE NULLS는 NULL이 아닌 row 중 offset 만큼 이전의 row 값을 반환한다.  
명시하지 않으면 기본값은 RESPECT NULLS이다.

window frame은 사용할 수 없다.

<a id="60db54f48db6a9d3"></a>
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

<a id="bae7034c41dc0736"></a>
## LAST() OVER

<a id="d965eadd72ea06c1"></a>
### 구문

```
aggregation_function KEEP ( DENSE_RANK LAST ORDER BY <sort specification list> ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="2f5b502bbdda94be"></a>
### 설명

Window function LAST 함수는 KEEP 절 내 order by에 쓰인 sort specification list를 정렬한 후, DENSE_RANK 순위가 마지막인 row들의 aggregation function 값을 반환한다.

aggregation_function에 해당하는 함수는 AVG, COUNT, COUNT(*), SUM, MAX, MIN, STDDEV, VARIANCE 이다.

window 절 내에서 order by는 사용할 수 없다.  
window frame은 사용할 수 없다.

<a id="12dbb6f695e23fdb"></a>
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

<a id="b9cb7ddff037c07a"></a>
## LAST_DAY

<a id="5967ac2c93fa7524"></a>
### 구문

```
LAST_DAY( date )
```

<a id="658cc1a2079cd31d"></a>
### 설명

LAST_DAY 함수는 date에 포함된 월의 마지막 날짜를 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
반환되는 타입은 인자 date의 타입에 상관없이 항상 DATE이다.  

date가 NULL이면 NULL을 반환한다.

<a id="06113906ed16c9dc"></a>
### 사용 예

```
gSQL> SELECT 
      LAST_DAY( TO_DATE( '2012-07-10', 'YYYY-MM-DD' ) ) AS RESULT FROM DUAL;
RESULT    
----------
2012-07-31
1 row selected.
```

<a id="65d110850ea8f107"></a>
## LAST_IDENTITY_VALUE

<a id="60c1d74acc6bfa39"></a>
### 구문

```
LAST_IDENTITY_VALUE()
```

<a id="7b38c08a3c8cf99e"></a>
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

INSERT 할 때 생성된 identity column의 값을 얻으려면 다음과 같이 [INSERT INTO name RETURNING .. INTO](20-sql-references-h-z.md#1aa03bfe5a515887) 구문을 사용한다.

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

<a id="3f31e2aa0f3b5e33"></a>
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

<a id="3d4c94647b08fc86"></a>
## LAST_VALUE() OVER

<a id="12ed2daf404c94d2"></a>
### 구문

```
LAST_VALUE ( expr ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

LAST_VALUE ( expr [ RESPECT NULLS | IGNORE NULLS ] ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="fc18a2c0fdb367df"></a>
### 설명

Window function LAST_VALUE는 expr의 마지막 값을 반환한다.

RESPECT NULLS는 NULL 값을 포함하여 row 중 마지막 값을 반환한다.  
IGNORE NULLS는 NULL이 아닌 row 중 마지막 값을 반환한다.  
명시하지 않으면 기본값은 RESPECT NULLS이다.

window 절 내 order by는 사용할 수 없다.  
window frame은 사용할 수 없다.

<a id="7fef2da53382a744"></a>
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

<a id="070eaeb9bbf94ced"></a>
## LEAD() OVER

<a id="af20d9ed943e726f"></a>
### 구문

```
LEAD ( expr [, offset [, default ] ] ) [ RESPECT NULLS | IGNORE NULLS ] OVER < window name or specification >

LEAD ( expr [ RESPECT NULLS | IGNORE NULLS ] [, offset [, default ] ] ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="6db5082ebb38b0f4"></a>
### 설명

Window function LEAD는 현재 row에서 offset 만큼 이후의 row 값을 반환한다.  
offset이 window 범위를 벗어났을 경우 default 값을 반환한다.

offset, default 값을 명시하지 않으면 기본값으로 설정된다.  
offset의 기본값은 1이고, default의 기본값은 NULL 이다.

RESPECT NULLS는 NULL 값을 포함하여 row 중 offset 만큼 이후의 row 값을 반환한다.  
IGNORE NULLS는 NULL이 아닌 row 중 offset 만큼 이후의 row 값을 반환한다.  
명시하지 않으면 기본값은 RESPECT NULLS이다.

window frame은 사용할 수 없다.

<a id="0d9d1fdc80ad7343"></a>
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

<a id="d6520bef7b3f9f99"></a>
## LEAST

<a id="e2b4e0d86da92cfd"></a>
### 구문

```
LEAST( expr1 [, expr2, ... exprn ] )
```

<a id="14cda1fa59b27dd7"></a>
### 설명

LEAST 함수는 인자로 받은 expr들 중에 가장 작은 값을 반환한다.

인자로 받은 expr들 중 하나라도 NULL인 경우, 결과값은 NULL이다.

결과 타입은 expr1 (첫 번째 expr)의 데이터 타입에 따라 결정된다.  
expr1 (첫 번째 expr)의 데이터 타입이 숫자형인 경우와 문자형인 경우에는 각각 expr1, ..., exprN의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, ..., exprN에 모두 CHAR 타입이 기술된 경우, 모든 expr은 VARCHAR 타입으로 비교되고, 결과 타입은 VARCHAR 타입이 된다.

<a id="6a8aec35c4eed104"></a>
### 사용 예

```
gSQL> SELECT LEAST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="8e1ef05fbd729197"></a>
## LENGTH

<a id="fee814f7930a2144"></a>
### 구문

```
LENGTH( str )
```

<a id="b816e5fd2f696b62"></a>
### 설명

[CHAR_LENGTH](#b519d2a71da13c53)의 alias 이다.

<a id="88449fbfbed3f809"></a>
### 사용 예

Multi byte character set: (예: UTF8)

```
gSQL> SELECT LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="ab2de866cc92bd9f"></a>
## LENGTHB

<a id="cb5931cfd8249c18"></a>
### 구문

```
LENGTHB( str )
```

<a id="b7bc594c0e7b7750"></a>
### 설명

OCTET_LENGTH의 alias이다.  
자세한 내용은 [OCTET_LENGTH](#a18ea2fd60d92536), [BYTE_LENGTH](#6df1a08d7fc63870)를 참조한다.

<a id="2861980471cc1d52"></a>
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

<a id="6ea28efce28dc2ac"></a>
## LISTAGG() OVER

<a id="aa06efa1c48da613"></a>
### 구문

```
LISTAGG( str [, delimiter] ) WITHIN GROUP ( ORDER BY <sort specification list> ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="1680c0ae0fb25f2c"></a>
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

<a id="323f959c6847eceb"></a>
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

<a id="432c18b51b430d3b"></a>
## LN

<a id="a62057069ddbbee8"></a>
### 구문

```
LN( num )
```

<a id="2ac45a0592bc82c4"></a>
### 설명

LN 함수는 num의 자연 로그 값을 반환하는 함수이다.  

num은 0보다 큰 값이어야 한다.  
num이 NULL이면 NULL을 반환한다.

<a id="5f4d784268aca42e"></a>
### 사용 예

```
gSQL> SELECT LN( 2.71828182845905 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="532aa900227892f2"></a>
## LNNVL

<a id="d91904e79d27eb1c"></a>
### 구문

```
LNNVL( expr )
```

<a id="7e171720e75d7767"></a>
### 설명

Logical Not Null VaLue (LNNVL) 함수는 NOT logical operator와 유사하지만 다음 예제와 같이 입력값이 null일 경우 TRUE를 반환한다는 차이가 있다.

<a id="af756bafd3e0497a"></a>
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

<a id="6d5473801bbf93c7"></a>
## LOCALTIME

<a id="68816cfd1fb0900b"></a>
### 구문

```
LOCALTIME [()]
STATEMENT_LOCALTIME()
```

<a id="3203a931b9b0b7a0"></a>
### 설명

Session 시간을 기준으로 현재 TIME WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• LOCALTIME, STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="c5c3b0339e1f36e7"></a>
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

<a id="a21be090210e5344"></a>
## LOCALTIMESTAMP

<a id="5bfd4cf651229d65"></a>
### 구문

```
LOCALTIMESTAMP [()]
STATEMENT_LOCALTIMESTAMP()
```

<a id="321af116f8ab0c9a"></a>
### 설명

Session 시간을 기준으로 현재 TIMESTAMP WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• LOCALTIMESTAMP, STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="df62d0547b4cf4cf"></a>
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

<a id="cc0c11b36d334cef"></a>
## LOCAL_GROUP_ID

<a id="37b01ebe0c734c02"></a>
### 구문

```
LOCAL_GROUP_ID()
```

<a id="12a0e90eedd141a3"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster group ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="772ac9eec8265e12"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_GROUP_ID() FROM DUAL;

LOCAL_GROUP_ID()
----------------
               1

1 row selected.
```

<a id="6395804d6e8aba4d"></a>
## LOCAL_GROUP_NAME

<a id="fc171a86061acbdb"></a>
### 구문

```
LOCAL_GROUP_NAME()
```

<a id="56b248a03289dcb8"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster group name을 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="c7b7ee436cee8ff6"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_GROUP_NAME() FROM DUAL;

LOCAL_GROUP_NAME()
------------------
G1                

1 row selected.
```

<a id="53e42feb12081a17"></a>
## LOCAL_MEMBER_ID

<a id="df3a035ae92f79da"></a>
### 구문

```
LOCAL_MEMBER_ID()
```

<a id="c1491e3a16f831eb"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster member ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="5c6447723a9320ab"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_MEMBER_ID() FROM DUAL;

LOCAL_MEMBER_ID()
-----------------
                1

1 row selected.
```

<a id="d7a6a73216643aff"></a>
## LOCAL_MEMBER_NAME

<a id="70887e7c7fb5f6cb"></a>
### 구문

```
LOCAL_MEMBER_NAME()
```

<a id="0dc05d441d45368d"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster member name을 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="9630186d01601196"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_MEMBER_NAME() FROM DUAL;

LOCAL_MEMBER_NAME()
-------------------
G1N1               

1 row selected.
```

<a id="78bba66616ead26c"></a>
## LOG

<a id="73f9f183bb571228"></a>
### 구문

```
LOG( num2 )
LOG( num1, num2 )
```

<a id="a422a87f00f6a039"></a>
### 설명

LOG 함수는 밑이 num1인 num2의 로그값을 반환한다.  
num1이 생략된 경우에는 밑이 10으로 계산된 값이 반환된다.

num1은 1과 0이 아닌 양수이어야 하고, num2는 양수이어야 한다.

num1 또는 num2가 NULL이면 NULL을 반환한다.

<a id="15d8933f7f226fda"></a>
### 사용 예

```
gSQL> SELECT LOG( 100 ) AS RESULT1, LOG( 4, 16 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      2       2
1 row selected.
```

<a id="3498773bf8e8b611"></a>
## LOGON_USER

<a id="9ef816f65b08c1b7"></a>
### 구문

```
LOGON_USER()
```

<a id="cca980c2fc2911b9"></a>
### 설명

로그인 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다.
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다.
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다.
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="2c2ef647f46d1f29"></a>
### 사용 예

```
% gsql test test

gSQL> SELECT LOGON_USER() AS result FROM DUAL;

RESULT
------
TEST  

1 row selected.
```

<a id="fbaa49b0c8c3e278"></a>
## LOWER

<a id="ef890c74a23fc613"></a>
### 구문

```
LOWER( str )
```

<a id="fb8ede2d2770c579"></a>
### 설명

LOWER 함수는 str의 소문자를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.  
str이 NULL이면 결과값도 NULL이다.

인자 str과 동일한 타입이 반환된다.

<a id="190033cbf6a8926f"></a>
### 사용 예

```
gSQL> SELECT LOWER( 'SPRING' ) AS RESULT FROM DUAL;
RESULT
------
spring
1 row selected.
```

<a id="8b9286fa3caf6f95"></a>
## LPAD

<a id="e07cd513f0b93412"></a>
### 구문

```
LPAD( str, length, [, fill] )
```

<a id="77c224934a4a8210"></a>
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

<a id="3d3b3c04b350e2a8"></a>
| 인자 str의 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="8b8e6e66fc2e93e4"></a>
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

<a id="5fe2c15537e257b6"></a>
## LTRIM

<a id="111343fb57bd0895"></a>
### 구문

```
LTRIM( trim_source [, trim_character ] )
```

<a id="bfbe33e8bba30230"></a>
### 설명

LTRIM 함수는 trim_source에서 trim_character를 왼쪽 방향에서 비교하여 일치하는 문자가 없을 때까지 제거한 결과를 반환한다.

인자 trim_character와 trim_source에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

trim_character, trim_source 중 하나라도 NULL이면, 결과값은 NULL이다.  
trim_character가 생략된 경우에는 기본적으로 single blank space (' ')가 지정된다.

결과 타입은 다음과 같다.

**LTRIM의 결과 타입**

<a id="5cf9609b3293944a"></a>
| trim_source, trim_character 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="baf96acc6a1664eb"></a>
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

<a id="c464d0fb3e0d21cb"></a>
## MAX

<a id="314bb5171dbf1c23"></a>
### 구문

```
MAX( [ ALL | DISTINCT ] expr )
```

<a id="da39f4d0460e8c69"></a>
### 설명

Aggregation 함수로써 row들의 expr 중 최대값을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복을 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

MAX는 ALL과 DISTINCT에 영향을 받지 않고 동일한 결과를 낸다.

<a id="f6d2bd28a0cc9443"></a>
### 사용 예

```
gSQL> SELECT MAX(c1) FROM t1;

MAX(C1)
-------
      3

1 row selected.
```

<a id="aa0b8c59f7333575"></a>
## MAX() OVER

<a id="eff3f9b45691bd50"></a>
### 구문

```
MAX ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="c232a594fc9195fa"></a>
### 설명

Window function MAX은 expr 중 최대값을 구하는 함수이다.  
NULL 값은 연산에서 제외된다.

<a id="bff36d0dded0a85b"></a>
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

<a id="0fe2e3d98c843ed2"></a>
## MEDIAN() OVER

<a id="aad6660eecbf3c4b"></a>
### 구문

```
MEDIAN ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="5d59b18fe55402e7"></a>
### 설명

Window function MEDIAN은 중간에 위치한 row 값을 반환하는 함수이다.  
NULL은 연산에서 제외된다.

window 절 내에서 order by는 사용할 수 없다.  
window frame은 사용할 수 없다.

<a id="a0b90c2ef42cdbc0"></a>
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

<a id="e6e8cb4b62354647"></a>
## MIN

<a id="8a71479a909bbb27"></a>
### 구문

```
MIN( [ ALL | DISTINCT ] expr )
```

<a id="21fda213df70e1a1"></a>
### 설명

Aggregation 함수로써 row들의 expr 중 최소값을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

MIN은 ALL과 DISTINCT에 영향을 받지 않고 동일한 결과를 낸다.

<a id="7832e2ad2f78dd3e"></a>
### 사용 예

```
gSQL> SELECT MIN(c1) FROM t1;

MIN(C1)
-------
      1

1 row selected.
```

<a id="96afb30d699d16ac"></a>
## MIN() OVER

<a id="15411ecd8f6f15c5"></a>
### 구문

```
MIN ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="515f64fd3a3c0abd"></a>
### 설명

Window function MIN은 expr 중 최소값을 구하는 함수이다.  
NULL 값은 연산에서 제외된다.

<a id="00ebb691de2944ad"></a>
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

<a id="02d82f627fbe56c6"></a>
## MOD

<a id="f31977382eddbc30"></a>
### 구문

```
MOD( num1, num2 )
```

<a id="a8ca2e08e8b63091"></a>
### 설명

MOD는 num1을 num2로 나눈 나머지를 반환한다.  

인자 num1, num2에는 숫자타입이 올 수 있다.  
num2가 0이면 에러를 반환한다.  
인자 num1 또는 num2가 NULL이면 NULL을 반환한다.

<a id="8e7eb545e157b409"></a>
### 사용 예

```
gSQL> SELECT MOD(5, 4) AS RESULT1, MOD(-5, 4) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1      -1
1 row selected.
```

<a id="7c1feecffb8e852a"></a>
## MONTHS_BETWEEN

<a id="df46bb4e4936b842"></a>
### 구문

```
MONTHS_BETWEEN( date1, date2 )
```

<a id="20356bbba84d864a"></a>
### 설명

MONTHS_BETWEEN은 date2와 date1 사이의 일수를 31로 나눈 개월 수를 반환한다.

date1 또는 date2가 NULL이면 결과도 NULL이다.  
인자 date1, date2에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.

결과 타입은 NUMBER 이다.

> date1과 date2 모두에 동일한 날짜가 포함되어 있거나 (예: 2014-01-15 와 2014-02-15) 월의 마지막 날짜가 포함되어 있는 경우 (예: 2014-08-31와 2014-09-30), 타임스탬프 구간 (있는 경우)의 일치 여부와 상관없이 정수 결과를 반환한다.

<a id="17b9ebe85364edd8"></a>
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

<a id="7d6a6731e477d031"></a>
## NEXT_DAY

<a id="ed5544f4b5827337"></a>
### 구문

```
NEXT_DAY( date, day )
```

<a id="7779569b95880e3b"></a>
### 설명

인자로 주어진 date (날짜)를 지나 처음으로 도래하는 day (요일)의 날짜를 구한다.

두 번째 인자 day에는 day를 지칭하는 스트링 또는 숫자가 올 수 있다.  
• 스트링:  SUNDAY ~ SATURDAY  또는 SUN ~ SAT  
• 숫자:  1 (sunday) ~ 7 (saturday)  

입력 인자 중 하나라도 NULL이면 결과값도 NULL이다.

반환되는 타입은 date의 입력 타입에 상관없이 항상 DATE 타입이다.  
결과값의 시분초는 입력 인자 date의 시분초를 동일하게 반환한다.

<a id="23f3663173629438"></a>
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

<a id="2c7bda07cb754833"></a>
## NEXTVAL

<a id="f98abd43747ec30b"></a>
### 구문

```
seq_name.NEXTVAL
NEXTVAL( seq_name )
NEXT VALUE FOR seq_name
```

<a id="191a5d4f0ce79da9"></a>
### 설명

시퀀스 객체의 다음 값을 얻는다.

<a id="e5a24938f894e71e"></a>
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

<a id="4aa994adaaeccda6"></a>
## NTH_VALUE() OVER

<a id="76fb94574445bebb"></a>
### 구문

```
NTH_VALUE ( expr, n ) [ FROM { FIRST | LAST } ][ { RESPECT | IGNORE } NULLS ] OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="7ef07eb203a33929"></a>
### 설명

Window function NTH_VALUE는 n 번째 row의 expr 값을 반환한다.  
window의 row 갯수가 n 보다 적을 경우, NULL을 반환한다.

인자 n에는 숫자 타입 또는 숫자로 변환될 수 있는 타입이 올 수 있다.

FROM FIRST는 첫 번째 row 로부터 n 번째 row를 가리킨다.   
FROM LAST는 마지막 row 로부터 n 번째 row를 가리킨다.  
명시하지 않으면 기본값은 FROM FIRST 이다.

RESPECT NULLS는 NULL 값을 포함하여 n 번째 row의 값을 반환한다.  
IGNORE NULLS는 NULL이 아닌 row 중 n 번째 값을 반환한다.  
명시하지 않으면 기본값은 RESPECT NULLS 이다.

<a id="234c5c610d6574ff"></a>
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

<a id="25be3cced6bb359e"></a>
## NTILE() OVER

<a id="d276500cef452615"></a>
### 구문

```
NTILE( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="4ed7d8a9534aba4e"></a>
### 설명

Window function NTILE은 각 row에 해당하는 버킷 번호를 반환한다.

버킷 번호는 1부터 시작하는 연속적인 정수이고, 버킷 개수는 expr 개수와 같다.  
버킷 개수가 row 개수보다 많은 경우, 각 row마다 버킷 한 개씩 나누어주고 나머지 버킷은 비워둔다.

expr은 양의 상수이어야 한다. expr이 고정된 숫자가 아닐 경우, expr은 window partition by 대상이어야 한다.

window frame은 사용할 수 없다.

<a id="f5f1adef5ffe7ace"></a>
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

<a id="e6667aff3c67db52"></a>
## NULLIF

<a id="2ee09df9fefdc047"></a>
### 구문

```
NULLIF( expr1, expr2 )
```

<a id="a9d97272047f6079"></a>
### 설명

expr1과 expr2가 같으면 null을 반환하고, 같지 않으면 첫 번째 인자인 expr1을 반환한다.

expr1과 expr2의 타입이 서로 다를 경우, [결과 타입 조합 규칙](11-sql-elements.md#1f2159979be55fba)에 따라 result type이 결정된다.

NULLIF는 CASE를 사용하여 동일하게 표현할 수 있다.

- NULLIF( expr1, expr2 )

```
CASE WHEN expr1 = expr2 THEN NULL 
       ELSE expr1 
  END
```

<a id="4deb142b66774069"></a>
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

<a id="8d2d1b12e6b735b3"></a>
## NUMTODSINTERVAL

<a id="d42865d97b920748"></a>
### 구문

```
NUMTODSINTERVAL( num, interval_indicator )
```

<a id="f0f99954cd3f6560"></a>
### 설명

interval_indicator 단위인 number를 interval day to second 타입으로 변환하여 반환한다.

인자 number는 숫자 타입이다.

인자 interval_indicator는 CHAR, VARCHAR와 같은 문자 타입이며, 대소문자 구분없이 'DAY', 'HOUR', 'MINUTE', 'SECOND' 중 하나여야 한다.

인자 중 하나라도 NULL이면 결과로 NULL이 반환된다.

interval day(6) to second(6) 타입의 결과를 반환하며 precision은 사용자가 임의로 변경할 수 없다. 변환된 결과의 leading precision이 기본 precision을 초과하면 에러가 반환되며, fraction precision이 기본 precision을 초과하면 반올림한 결과를 반환한다.

<a id="2595ac5d1c8010af"></a>
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

<a id="8c462e51ea16a194"></a>
## NUMTOYMINTERVAL

<a id="61af3463a98f9a50"></a>
### 구문

```
NUMTOYMINTERVAL( num, interval_indicator )
```

<a id="a011600a809dfa9e"></a>
### 설명

interval_indicator 단위인 number를 interval year to month 타입으로 변환하여 반환한다.

인자 number는 숫자 타입이다.

인자 interval_indicator는 CHAR, VARCHAR와 같은 문자 타입이며, 대소문자 구분없이 'YEAR', 'MONTH' 중 하나여야 한다.

인자 중 하나라도 NULL이면 결과로 NULL이 반환된다.

interval year(6) to month 타입을 결과로 반환하며 precision은 사용자가 임의로 변경할 수 없다. 변환된 결과의 leading precision이 기본 precision을 초과하면 에러가 반환된다.

<a id="ca38b474631b941c"></a>
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

<a id="6364c9a8359687ee"></a>
## NVL

<a id="7bf721285d401f3d"></a>
### 구문

```
NVL( expr1, expr2 )
```

<a id="394986abde5ad598"></a>
### 설명

expr1이 null이 아니면 expr1을 반환하고, expr1이 null이면 expr2를 반환한다.

결과 타입은 expr1의 데이터 타입에 따라 결정된다.  
expr1에 NULL이 기술된 경우에는 expr2의 타입에 따라 결과 타입이 결정된다.  
expr1의 데이터 타입이 숫자형 타입인 경우와 문자형 타입인 경우는 각각 expr1, expr2의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, expr2의 데이터 타입이 모두 CHAR 타입인 경우, 결과 타입은 VARCHAR로 결정된다.

<a id="fde74dd7c90496d8"></a>
### 사용 예

```
gSQL> SELECT I1, NVL( I1, 0 ) FROM T1;
  I1 NVL( I1, 0 )
---- ------------
   1            1
null            0
2 rows selected.
```

<a id="68ca3ce707e7d42a"></a>
## NVL2

<a id="ccc7ebab981ae33c"></a>
### 구문

```
NVL2( expr1, expr2, expr3 )
```

<a id="8feb17277dad6417"></a>
### 설명

expr1이 null이 아니면 expr2를 반환하고, expr1이 null이면 expr3을 반환한다.

결과 타입은 expr2의 데이터 타입에 따라 결정된다.  
expr2에 NULL이 기술된 경우에는 expr3의 타입에 따라 결과 타입이 결정된다.  
expr2의 데이터 타입이 숫자형인 경우와 문자형인 경우에는 각각 expr2, expr3의 범위를 포함할 수 있는 타입으로 결정된다.  
expr2, expr3의 데이터 타입이 모두 CHAR 타입인 경우, 결과 타입은 VARCHAR가 된다.

<a id="bdd77705480aac63"></a>
### 사용 예

```
gSQL> SELECT I1, NVL2( I1, I1 * 1000, 0 ) FROM T1;
  I1 NVL2( I1, I1 * 1000, 0 )
---- ------------------------
   1                     1000
null                        0
2 rows selected.
```

<a id="a18ea2fd60d92536"></a>
## OCTET_LENGTH

<a id="c3ca78107135d4ad"></a>
### 구문

```
OCTET_LENGTH( str )  

BYTE_LENGTH( str )     

LENGTHB( str )
```

<a id="68b672923f7f02ad"></a>
### 설명

OCTET_LENGTH는 str의 바이트 수를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

str의 타입이 CHARACTER면 공백문자도 계산에 포함된다.  
str이 NULL이면 결과값도 NULL이다.

OCTET_LENGTH의 alias로는 [BYTE_LENGTH](#6df1a08d7fc63870)와 [LENGTHB](#ab2de866cc92bd9f) 함수가 있다.

<a id="a234624cd1772b9f"></a>
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

<a id="a536ee0e10ecc5e7"></a>
## OVERLAY

<a id="9e65f24ab4b2fd92"></a>
### 구문

```
OVERLAY( str1 PLACING str2 FROM start_position  [ FOR string_length ] )
```

<a id="e57542de7148838e"></a>
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

자세한 내용은 [SUBSTRING](#cea95faba7ada96f)을 참조한다.

결과 타입은 다음 표와 같다.

**OVERLAY의 결과 타입**

<a id="780d4cae14ec444c"></a>
| str1, str2 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="7cc74ca61f69ab48"></a>
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

<a id="d332475d0e6d5fab"></a>
## PERCENT_RANK() OVER

<a id="70370f1db32ac89e"></a>
### 구문

```
PERCENT_RANK( ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="1782df164eda6ee2"></a>
### 설명

Window function PERCENT_RANK는 전체 row 개수에 대해 각 row가 갖는 순위의 비율을 계산한다.

PERCENT_RANK 함수의 결과는 0부터 1 사이의 숫자이고, row 값이 같으면 비율 값도 같다.

window frame은 사용할 수 없다.

<a id="a1ea909041b94bba"></a>
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

<a id="7ce593ba28b91c56"></a>
## PERCENTILE_CONT() OVER

<a id="71f732ed4924a1ef"></a>
### 구문

```
PERCENTILE_CONT( expr ) WITHIN GROUP ( ORDER BY <sort specification> ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="420a30255b5b3577"></a>
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

- [MEDIAN() OVER](#0fe2e3d98c843ed2)
- [PERCENTILE_DISC() OVER](#e19b8811d8fafe81)

<a id="3aa50195b737bd57"></a>
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

<a id="e19b8811d8fafe81"></a>
## PERCENTILE_DISC() OVER

<a id="8cc01cc07fca67ef"></a>
### 구문

```
PERCENTILE_DISC( expr ) WITHIN GROUP ( ORDER BY <sort specification> ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="08463b54fe852682"></a>
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

관련 내용은 [CUME_DIST() OVER](#086281afc9e11656)를 참조한다.

<a id="9dd81df5bba9b1e7"></a>
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

<a id="f8fadd0d36ab7483"></a>
## PHYSICAL_LENGTH

<a id="9051c3e958701703"></a>
### 구문

```
PHYSICAL_LENGTH( expr )
```

<a id="57305b7f639f0278"></a>
### 설명

PHYSICAL_LENGTH 함수는 expr의 내부 표현 정보 byte 수를 반환한다.

인자 expr에는 모든 데이터 타입이 올 수 있다.

입력 인자가 NULL이면 결과는 0 이다.

<a id="3a278212d8ea60b4"></a>
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

<a id="1f2d630603e0531f"></a>
## PI

<a id="5e158b1d096366a7"></a>
### 구문

```
PI()
```

<a id="e282831dcd3f8152"></a>
### 설명

PI는 "π" constant를 반환한다.

<a id="4ddda9a59d968cde"></a>
### 사용 예

```
gSQL> SELECT PI() AS RESULT FROM DUAL;
              RESULT
--------------------
3.141592653589793E+0
1 row selected.
```

<a id="a18e75976eb4b7ad"></a>
## POSITION

<a id="0b165a8dbcc0365f"></a>
### 구문

```
POSITION( str1 IN str2 )
```

<a id="2044d84e2c116086"></a>
### 설명

POSITION 함수는 str2에서 첫 번째 str1을 찾아 그 위치를 반환하는 함수이다.

str1과 str2에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

str2에서 str1을 찾을 수 없는 경우, 리턴값 0이 반환된다.  
str2에서 str1을 찾은 경우, 1을 시작으로 그 찾은 위치를 반환한다.  
반환되는 위치값은 CHARACTER 단위로 계산된 값이다. (byte 단위가 아님)  
str1 또는 str2가 NULL이면, 반환되는 값도 NULL 이다.

<a id="32c33e1be64fcfcb"></a>
### 사용 예

```
gSQL> SELECT POSITION( 'CHAR' IN 'LONG CHAR 2000' ) AS RESULT FROM DUAL;
RESULT
------
     6
1 row selected.
```

<a id="16d2c296bc2d2a7c"></a>
## POWER

<a id="657f97301c278e15"></a>
### 구문

```
POWER( num1, num2 )
```

<a id="793016d2aacf74f3"></a>
### 설명

POWER 함수는 num1에 num2를 제곱한 값을 반환한다.

인수 num1과 num2에는 숫자 타입이 올 수 있다.  

num1이 음수이면, num2는 정수여야 한다.  
num1 또는 num2의 값이 NULL이면, 결과값도 NULL이다.

<a id="69bad026c2439868"></a>
### 사용 예

```
gSQL> SELECT POWER( 2, 3 ) AS RESULT FROM DUAL;
RESULT
------
     8
1 row selected.
```

<a id="fc5d89f7f66046fa"></a>
## RADIANS

<a id="7f2f4f8929469e56"></a>
### 구문

```
RADIANS( degrees )
```

<a id="b7e4ac6825f0cf28"></a>
### 설명

RADIANS 함수는 degrees의 라디안을 반환한다.  

인자 degrees에는 숫자 타입이 올 수 있다.  
인자 degrees가 NULL이면 NULL을 반환한다.

<a id="fe7507ee30f96ebd"></a>
### 사용 예

```
gSQL> SELECT RADIANS( 180 ) AS RESULT FROM DUAL;
          RESULT
----------------
3.14159265358979
1 row selected.
```

<a id="0534cdebff5c32cf"></a>
## RANDOM

<a id="65f75c2da0d4f622"></a>
### 구문

```
RANDOM( min, max )
```

<a id="e55a01d6e41c7dc6"></a>
### 설명

RANDOM은 min 이상 max 이하의 random 값을 반환한다.  

인자 min, max에는 숫자 타입이 올 수 있다.  
인자 min 또는 max가 NULL이면 NULL을 반환한다.

<a id="71f2b6e6acec7e3f"></a>
### 사용 예

```
gSQL> SELECT RANDOM( 1, 100 ) AS RESULT FROM DUAL;
          RESULT
----------------
34.1870528003201
1 row selected.
```

<a id="adc272a8e13a73a4"></a>
## RANK() OVER

<a id="4a3e82fc63b8bb2c"></a>
### 구문

```
RANK( ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="b7d58017cab34127"></a>
### 설명

Window function RANK는 순위를 계산하는 함수이다.

순위는 1부터 시작하는 정수이고, 값이 같은 row는 순위도 동일하다.

window frame은 사용할 수 없다.

<a id="c8f13fe3e8b82a6d"></a>
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

<a id="bb7c5b72e4efa259"></a>
## RATIO_TO_REPORT() OVER

<a id="2bedb58474e46150"></a>
### 구문

```
RATIO_TO_REPORT ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="4986e4de9398e77e"></a>
### 설명

Window function RATIO_TO_REPORT는 expr 값의 합에서 각 row 값이 차지하는 비율을 계산한다.  
row 값이 NULL인 경우, 결과값으로 NULL을 반환한다.

window 절 내에서 order by는 사용할 수 없다.  
window frame은 사용할 수 없다.

<a id="65df7276f6cf3a72"></a>
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

<a id="e00eb03057c69ca3"></a>
## REGR_AVGX() OVER

<a id="adae33e5d117b377"></a>
### 구문

```
REGR_AVGX( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="1fdcffeff2d7b3c1"></a>
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

<a id="b5e51e24860133a0"></a>
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

<a id="f34354559d730656"></a>
## REGR_AVGY() OVER

<a id="5b209e296524d4eb"></a>
### 구문

```
REGR_AVGY( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="329432f4cd195f4a"></a>
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

<a id="281f594532231264"></a>
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

<a id="bfe272c0f7eb1c25"></a>
## REGR_COUNT() OVER

<a id="fff737e9e5489d10"></a>
### 구문

```
REGR_COUNT( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="b51e5bd9aea613f4"></a>
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

<a id="9c83adc5bfd8c20e"></a>
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

<a id="58865d41bc167acf"></a>
## REGR_INTERCEPT() OVER

<a id="bbc329dd80808d94"></a>
### 구문

```
REGR_INTERCEPT( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="6ecadd031f6172d5"></a>
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

<a id="6da1a55342db2b1a"></a>
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

<a id="3ca155a9214302b2"></a>
## REGR_R2() OVER

<a id="44706c9b2c6bffbd"></a>
### 구문

```
REGR_R2( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="1d0437a93dbb0121"></a>
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

<a id="7defe9ddb0df0f7c"></a>
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

<a id="cf3b4d0157191663"></a>
## REGR_SLOPE() OVER

<a id="9b8a47320a42c754"></a>
### 구문

```
REGR_SLOPE( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="24ad4717b0df1686"></a>
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

<a id="3f7b58da1685cd38"></a>
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

<a id="73c7f61059ebb509"></a>
## REGR_SXX() OVER

<a id="8ea3e5ab530875c8"></a>
### 구문

```
REGR_SXX( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="d229a7c97bff666f"></a>
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

<a id="5dce15f8c3534dd6"></a>
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

<a id="085d4279ff5e84aa"></a>
## REGR_SXY() OVER

<a id="803b8d0004ef9670"></a>
### 구문

```
REGR_SXY( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="d85d1e9337f3c7cc"></a>
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

<a id="e3ac9b7ad273a701"></a>
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

<a id="bf7a5868881d64d7"></a>
## REGR_SYY() OVER

<a id="ba05fd0d90ebe4d9"></a>
### 구문

```
REGR_SYY( expr1, expr2 ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="d57c274d93a04723"></a>
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

<a id="bbbbb6af9c8fdf0e"></a>
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

<a id="99ca5639b4fd8dbe"></a>
## REPEAT

<a id="791061e08a5c6d38"></a>
### 구문

```
REPEAT( str, num )
```

<a id="5d69a4fce5d64804"></a>
### 설명

REPEAT 함수는 num에 지정된 수만큼 str을 반복한 string을 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARCATER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

인자 num에는 숫자 타입이 올 수 있다.

str 또는 num 중의 하나라도 NULL이면, 결과값도 NULL이다.  
num의 값이 0 또는 음수인 경우에도 결과값은 NULL이다.

결과 타입은 다음 표와 같다.

**REPEAT의 결과 타입**

<a id="40c816533df18ac7"></a>
| str 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="c7cbf8ea0840ea6c"></a>
### 사용 예

```
gSQL> SELECT REPEAT( 'ab', 3 ) AS RESULT FROM DUAL;
RESULT
------
ababab
1 row selected.
```

<a id="b47fe4455fb5fc10"></a>
## REPLACE

<a id="43768b4d38534398"></a>
### 구문

```
REPLACE( str, from, to )
```

<a id="28ee193fd0c0b7c3"></a>
### 설명

REPLACE는 str string 내의 모든 from string을 to string으로 치환하여 반환한다.

인자 str, from, to에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str 값이 NULL인 경우, 결과값은 NULL이다.  
from 값이 NULL인 경우, str 값을 변환하지 않고 반환한다.  
to 값이 생략되었거나 NULL인 경우, str에서 from을 제거한 값이 반환된다.

결과 타입은 다음 표와 같다.

**REPLACE의 결과 타입**

<a id="f3616cba14184381"></a>
| str 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="3af5a24f3c99e33a"></a>
### 사용 예

```
gSQL> SELECT REPLACE( 'HI GLIESE', 'HI', 'HELLO' ) AS RESULT FROM DUAL;
RESULT      
------------
HELLO GLIESE
1 row selected.
```

<a id="7fb8a48fa4905d51"></a>
## REVERSE

<a id="f2cfb0439381ae62"></a>
### 구문

```
REVERSE( str )
```

<a id="50485fd0bfda098e"></a>
### 설명

REVERSE는 str의 문자를 역순으로 반환한다.

인자로는 character string 타입 또는 binary string 타입으로 변환될 수 있는 타입이 올 수 있으며  
character string 타입은 해당 문자 단위로, binary string 타입은 byte 단위로 수행된다.

str이 NULL일 경우 NULL을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**REVERSE 인자와 결과 타입**

<a id="abc50b7c9f8849ca"></a>
| str | 결과 타입 |
| --- | --- |
| CHAR | CHAR |
| VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY | BINARY |
| VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="1d3c43ba081add97"></a>
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

<a id="2c8c7e8310ba521b"></a>
## ROUND( number )

<a id="2962ee730f9838f6"></a>
### 구문

```
ROUND( num [, scale ] )
```

<a id="b51c3e9eeb525b27"></a>
### 설명

ROUND는 scale을 기준으로 num을 반올림한 값을 반환한다.

인자 num, scale에는 숫자 타입이 올 수 있다.

scale이 생략된 경우, scale은 0이 되어 ROUND( num, 0 )와 같이 수행된다.  
scale이 양수인 경우 소수점 오른쪽 자리수를 기준으로 반올림되고, scale이 음수인 경우 소수점 왼쪽 자리수를 기준으로 반올림된다.  

인자 num 또는 scale이 NULL이면 NULL을 반환한다.

<a id="a3f0e6c958364ef2"></a>
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

<a id="fe0ef4dbf5f78863"></a>
## ROUND( date )

<a id="009cd7fbf02b397c"></a>
### 구문

```
ROUND( date [ , fmt ] )
```

<a id="f146eee1ee12ddf4"></a>
### 설명

ROUND( date ) 함수는 date를 지정된 fmt 단위로 반올림한 값을 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
인자 date 또는 fmt가 NULL이면 NULL을 반환한다.  

결과 타입은 인자로 받은 date 타입과 관계없이 항상 DATE 타입이다.

fmt가 생략되었을 경우의 기본값은 DAY 이며, 사용 가능한 형식문자열은 다음 표와 같다.

**fmt에 사용가능한 형식문자열**

<a id="30177de00663a8be"></a>
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

<a id="820d29744d222aa6"></a>
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

<a id="a5ce32599a146693"></a>
## ROW_NUMBER() OVER

<a id="38894db03c4af9ef"></a>
### 구문

```
ROW_NUMBER( ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="883a7d7f32fe4152"></a>
### 설명

Window function ROW_NUMBER는 각 row에 고유 번호를 할당한다.  
고유 번호는 1부터 시작하는 연속적인 정수이다.

window frame은 사용할 수 없다.

<a id="c0e6d75d206bab51"></a>
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

<a id="04fb7638541472a1"></a>
## ROWID_GRID_BLOCK_ID

<a id="a3bd9cb7182d1e16"></a>
### 구문

```
ROWID_GRID_BLOCK_ID( rowid )
```

<a id="9ea461ab4ffe788e"></a>
### 설명

GRID block ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="dc80c59c15f579fe"></a>
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

<a id="9161dc277dceef02"></a>
## ROWID_GRID_BLOCK_SEQ

<a id="ffa2fdd048bd0aad"></a>
### 구문

```
ROWID_GRID_BLOCK_SEQ( rowid )
```

<a id="1e64f30960814d6a"></a>
### 설명

GRID block sequence를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="271f7e3019706b4b"></a>
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

<a id="bab730f3b3d1ee80"></a>
## ROWID_MEMBER_ID

<a id="0210cc956abc1df6"></a>
### 구문

```
ROWID_MEMBER_ID( rowid )
```

<a id="932200752d218e49"></a>
### 설명

Member ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="1518be0ed2c74c6b"></a>
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

<a id="4f7ed74b7b4b79d4"></a>
## ROWID_OBJECT_ID

<a id="b7abf638330da39f"></a>
### 구문

```
ROWID_OBJECT_ID( rowid )
```

<a id="9e13cc69410b3612"></a>
### 설명

Object ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="347f0ec4b7f2ef81"></a>
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

<a id="b707a739152a3d4e"></a>
## ROWID_PAGE_ID

<a id="df50da9c8ef9a6b6"></a>
### 구문

```
ROWID_PAGE_ID( rowid )
```

<a id="1499c947b4ec7cfe"></a>
### 설명

Page ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="c76a70a3b507389a"></a>
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

<a id="bddb251e3eec0268"></a>
## ROWID_ROW_NUMBER

<a id="76675325cc73591f"></a>
### 구문

```
ROWID_ROW_NUMBER( rowid )
```

<a id="6c6bfe9cd8332f96"></a>
### 설명

Row number를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="4bf820708ec4d975"></a>
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

<a id="98328e85c639163f"></a>
## ROWID_SHARD_ID

<a id="72c7e04bec904f4b"></a>
### 구문

```
ROWID_SHARD_ID( rowid )
```

<a id="e8f5a39ceb1e7945"></a>
### 설명

Shard ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="b081f762ba24bafd"></a>
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

<a id="23a80173f06ef320"></a>
## ROWID_TABLESPACE_ID

<a id="c4ac39f6b1de4aa2"></a>
### 구문

```
ROWID_TABLESPACE_ID( rowid )
```

<a id="001300cd3b93552f"></a>
### 설명

Tablespace ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="079ec2e792d27f1f"></a>
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

<a id="ecee853b277bbf48"></a>
## ROWNUM

<a id="9ac5e6128b526760"></a>
### 구문

```
ROWNUM
```

<a id="782ab656edf3d6c2"></a>
### 설명

WHERE 조건을 만족하는 row에 대하여 1부터 순차적으로 번호를 부여한다.

Oracle과의 호환성을 위해 WHERE 절에 ROWNUM 사용을 허용한다.

그러나 질의 결과의 개수를 제한하려면 다음과 같이 SQL 표준의 [offset limit clause](20-sql-references-h-z.md#fe18ee55c139acb6)를 사용할 것을 권장한다.

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

<a id="0cab5fe3f0b85f07"></a>
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

<a id="37b66bc35710f864"></a>
## RPAD

<a id="3facfdacc0af9fab"></a>
### 구문

```
RPAD( str, length, [, fill] )
```

<a id="e882560f589eb704"></a>
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

<a id="62afb88feddf9523"></a>
| 인자 str의 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="53fa9eaa7543399c"></a>
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

<a id="02156ecdd39df9cd"></a>
## RTRIM

<a id="833d8571deb20b61"></a>
### 구문

```
RTRIM( trim_source [, trim_character ] )
```

<a id="b715a4bfe7fcfcbe"></a>
### 설명

RTRIM 함수는 trim_source에서 trim_character를 오른쪽 방향에서 비교하여 일치하는 문자가 없을 때까지 제거한 결과를 반환한다.

인자 trim_character와 trim_source에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

trim_character, trim_source 중 하나라도 NULL이면, 결과값은 NULL이다.  
trim_character가 생략된 경우에는 기본적으로 single blank space (' ')가 지정된다.

결과 타입은 다음과 같다.

**RTRIM의 결과 타입**

<a id="951b867fc954c37b"></a>
| trim_source, trim_character 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="8734443b3577866c"></a>
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

<a id="8b0b84a308db30d6"></a>
## SESSION_ID

<a id="38c1b23e265797aa"></a>
### 구문

```
SESSION_ID()
```

<a id="ab32515338124b24"></a>
### 설명

현재 session의 ID를 얻는다.

<a id="b39627034bb5109b"></a>
### 사용 예

```
gSQL> SELECT SESSION_ID() FROM dual;

SESSION_ID()
------------
           4

1 row selected.
```

<a id="8b9c98fb5252f314"></a>
## SESSION_SERIAL

<a id="1d38510b8a058d59"></a>
### 구문

```
SESSION_SERIAL()
```

<a id="0d31aec77d52d2a9"></a>
### 설명

현재 session의 serial 번호를 얻는다.

<a id="ad7c2e7ca603f24e"></a>
### 사용 예

```
gSQL> SELECT SESSION_SERIAL() FROM dual;

SESSION_SERIAL()
----------------
              16

1 row selected.
```

<a id="e654c1c310af8fc0"></a>
## SESSION_USER

<a id="05d0f0b2eeb2efb9"></a>
### 구문

```
SESSION_USER[()]
```

<a id="ab4cf3b8fc738651"></a>
### 설명

세션 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다. 
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다. 
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다. 
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="64091257694824f6"></a>
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

<a id="2fc1c7ed2c2b786a"></a>
## SESSIONTIMEZONE

<a id="f66346d2f66db44d"></a>
### 구문

```
SESSIONTIMEZONE()
```

<a id="04e48ccdd1cae3d4"></a>
### 설명

SESSIONTIMEZONE은 현재 session의 time zone을 반환한다.  
반환되는 값은 '[+|-]TZH:TZM' format 형식의 문자이다.  
반환되는 타입은 varchar 이다.

<a id="f260b981f982abf7"></a>
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

<a id="19d3ffc377961b38"></a>
## SHARD_GROUP_ID

<a id="9551573aa4bf645b"></a>
### 구문

```
SHARD_GROUP_ID( table_name, shard_key_value [, ... ] )
```

<a id="554ab485cf539e01"></a>
### 설명

SHARD_GROUP_ID 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard를 관리하는 group ID를 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 NATIVE_BIGINT이다.

> Cluster system에서 유효한 정보이다.

<a id="155ed84af273925d"></a>
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

<a id="e718a93989668a51"></a>
## SHARD_GROUP_NAME

<a id="98554a583f9ebeaa"></a>
### 구문

```
SHARD_GROUP_NAME( table_name, shard_key_value [, ... ] )
```

<a id="39afb93fb3e1d3d0"></a>
### 설명

SHARD_GROUP_NAME 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard를 관리하는 group NAME을 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 VARCHAR이다.

> Cluster system에서 유효한 정보이다.

<a id="2aea47c6350f6e7c"></a>
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

<a id="9f3880617b412ca4"></a>
## SHARD_ID

<a id="f392538d6397a903"></a>
### 구문

```
SHARD_ID( table_name, shard_key_value [, ... ] )
```

<a id="573a9b43324abceb"></a>
### 설명

SHARD_ID 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard에 대한 ID를 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 NATIVE_BIGINT이다.

> Cluster system에서 유효한 정보이다.

<a id="679099e05658b28a"></a>
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

<a id="8c1d2cc50802a1bb"></a>
## SHARD_NAME

<a id="b4ae4c6d4cb494af"></a>
### 구문

```
SHARD_NAME( table_name, shard_key_value [, ... ] )
```

<a id="750c6e30e39e0e3f"></a>
### 설명

SHARD_NAME 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard에 대한 NAME을 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 VARCHAR이다.

> Cluster system에서 유효한 정보이다.

<a id="bc1e3e7f7ed9d829"></a>
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

<a id="e13e9d7ec5338e98"></a>
## SHIFT_LEFT

<a id="46df3e048d6b5c24"></a>
### 구문

```
SHIFT_LEFT( num, cnt )
```

<a id="03543f7a56f66c6b"></a>
### 설명

SHIFT_LEFT 함수는 num을 cnt 비트만큼 왼쪽으로 이동시킨 값을 반환한다.

입력 인자 num, cnt에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환하면 소수점은 TRUNCATE 된다.

연산 시 cnt는 6 bit로 마스킹하여 6 bit 범위 내의 값으로 처리한다.

num 또는 cnt가 NULL이면 NULL을 반환한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="c3a059d5a530c68b"></a>
### 사용 예

```
gSQL> SELECT SHIFT_LEFT(1, 3) FROM DUAL;
SHIFT_LEFT(1, 3)
----------------
               8
1 row selected.
```

<a id="f6ded56685f3d32f"></a>
## SHIFT_RIGHT

<a id="291121e9721cb1ae"></a>
### 구문

```
SHIFT_RIGHT( num, cnt )
```

<a id="3ae3d18dae60c973"></a>
### 설명

SHIFT_RIGHT 함수는 num을 cnt 비트만큼 오른쪽으로 이동시킨 값을 반환한다.

입력 인자 num, cnt에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환하면 소수점은 TRUNCATE 된다.

연산 시 cnt는 6 bit로 마스킹하여 6 bit 범위내의 값으로 처리한다.

num 또는 cnt가 NULL이면 NULL을 반환한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="27f9e40a7613c4dc"></a>
### 사용 예

```
gSQL> SELECT SHIFT_RIGHT(8, 3) FROM DUAL;
SHIFT_RIGHT(8, 3)
-----------------
                1
1 row selected.
```

<a id="5e09c8638cdad3ca"></a>
## SIGN

<a id="75e482de7afa2428"></a>
### 구문

```
SIGN( num )
```

<a id="65b4f7c1d09ea36a"></a>
### 설명

SIGN 함수는 num의 부호를 반환한다.

인자 num에는 숫자타입이 올 수 있다.

반환값은 다음과 같다.  
• num < 0 이면 -1  
• num = 0 이면 0  
• num > 0 이면 1

num이 NULL이면 NULL을 반환한다.

<a id="1d8e036afbda0f56"></a>
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

<a id="aaf6a38956ed098c"></a>
## SIN

<a id="8bbe632dbf939119"></a>
### 구문

```
SIN( num )
```

<a id="672a28ba00ce9ef3"></a>
### 설명

SIN 함수는 num의 sine 값을 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="9427b299783e0497"></a>
### 사용 예

```
gSQL> SELECT SIN( 0 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="82a0ffea4129e120"></a>
## SPLIT_PART

<a id="58e7ce17714a3b92"></a>
### 구문

```
SPLIT_PART( string, delimiter, field )
```

<a id="338d1730355b6a99"></a>
### 설명

SPLIT_PART 함수는 string 내에서 delimiter로 지정된 문자를 구분자로 하여 field의 문자열을 반환한다.

인자 string, delimiter에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

인자 field에는 숫자 타입이 올 수 있다.

string, delimiter, field 중에 하나라도 NULL인 경우에는 결과값도 NULL이다.  
field에는 1 이상의 숫자값만 올 수 있고, 0 또는 음수일 경우에는 에러를 반환한다.

결과 타입은 다음 표와 같다.

**SPLIT_PART의 결과 타입**

<a id="e31cb7e8bfb0f168"></a>
| string 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="fc0b0b4aff103b81"></a>
### 사용 예

```
gSQL> SELECT SPLIT_PART( 'AB;CD;EF;GH', ';', 3  ) AS RESULT FROM DUAL;
RESULT
------
EF    
1 row selected.
```

<a id="587556e0b32b0986"></a>
## SQRT

<a id="e327dabccdd3e0c0"></a>
### 구문

```
SQRT( num )
```

<a id="6c087f82820881d9"></a>
### 설명

SQRT 함수는 num의 제곱근을 반환한다.  

인자 num에는 숫자 타입이 올 수 있고, 음수가 아닌 0 이상의 값이어야 한다.  
인자 num이 NULL이면 NULL을 반환한다.

<a id="8576c5bce6649511"></a>
### 사용 예

```
gSQL> SELECT SQRT( 9 ) AS RESULT FROM DUAL;
RESULT
------
     3
1 row selected.
```

<a id="e988c79b5a748b7e"></a>
## STATEMENT_DATE

<a id="f2107e1d164bb5ff"></a>
### 구문

```
STATEMENT_DATE()
CURRENT_DATE [()]
```

<a id="dd508641ffbbf8ae"></a>
### 설명

현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="bdd1c33818cbe09a"></a>
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

<a id="5bab9f6863319163"></a>
## STATEMENT_LOCALTIME

<a id="f0caedb4054d68e7"></a>
### 구문

```
STATEMENT_LOCALTIME()
LOCALTIME [()]
```

<a id="f2a0cc06baa1c354"></a>
### 설명

Session 시간을 기준으로 현재 TIME WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="0a3deee2c4f63c0f"></a>
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

<a id="fb0173aa0ae59d6a"></a>
## STATEMENT_LOCALTIMESTAMP

<a id="9fe313a0d78f97d2"></a>
### 구문

```
STATEMENT_LOCALTIMESTAMP()
LOCALTIMESTAMP [()]
```

<a id="5c3e2427d938d3f8"></a>
### 설명

Session 시간을 기준으로 현재 TIMESTAMP WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="4781edf66aca91de"></a>
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

<a id="6156c515ebce3de6"></a>
## STATEMENT_TIME

<a id="5d169eb7730d23ee"></a>
### 구문

```
STATEMENT_TIME()
CURRENT_TIME [()]
```

<a id="d4a0b7eb24f49ab3"></a>
### 설명

TIME ZONE이 있는 현재 TIME (TIME WITH TIME ZONE type) 값을 얻는다.

CURRENT_TIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="4d4c688cba41326d"></a>
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

<a id="514a0a74b158903b"></a>
## STATEMENT_TIMESTAMP

<a id="ca3122d490e06add"></a>
### 구문

```
STATEMENT_TIMESTAMP()
CURRENT_TIMESTAMP [()]
```

<a id="898e64b942929652"></a>
### 설명

TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

CURRENT_TIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="ce8517708760d29f"></a>
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

<a id="4c572540255a3aff"></a>
## STATEMENT_VIEW_SCN

<a id="2650d8973b7777a0"></a>
### 구문

```
STATEMENT_VIEW_SCN()
```

<a id="283e6ce546d09400"></a>
### 설명

현재 STATEMENT의 VIEW SCN을 얻는다.

<a id="f79313a0f1c7b51a"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN() FROM dual;

STATEMENT_VIEW_SCN()
--------------------
17697.658.17880     

1 row selected.
```

<a id="149eb280305fd7f9"></a>
## STATEMENT_VIEW_SCN_DCN

<a id="e83baac4b1ff3041"></a>
### 구문

```
STATEMENT_VIEW_SCN_DCN()
```

<a id="6441ee356d77842e"></a>
### 설명

현재 STATEMENT의 VIEW SCN의 Domain Change Number (DCN) 값을 얻는다.

<a id="13e6618d6fa6d19c"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_DCN() FROM dual;

STATEMENT_VIEW_SCN_DCN()
------------------------
                     658

1 row selected.
```

<a id="9512af1fc034cd22"></a>
## STATEMENT_VIEW_SCN_GCN

<a id="0da398aa79108e96"></a>
### 구문

```
STATEMENT_VIEW_SCN_GCN()
```

<a id="a85f9d5b43ccae01"></a>
### 설명

현재 STATEMENT의 VIEW SCN의 Global Change Number (GCN) 값을 얻는다.

<a id="03172b430828ab7c"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_GCN() FROM dual;

STATEMENT_VIEW_SCN_GCN()
------------------------
                   17697

1 row selected.
```

<a id="753e884f2ebd6c97"></a>
## STATEMENT_VIEW_SCN_LCN

<a id="3d676774d4b69305"></a>
### 구문

```
STATEMENT_VIEW_SCN_LCN()
```

<a id="dc0a73d3c0a45455"></a>
### 설명

현재 STATEMENT의 VIEW SCN의 Local Change Number (LCN) 값을 얻는다.

<a id="db18c65370399e1d"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_LCN() FROM dual;

STATEMENT_VIEW_SCN_LCN()
------------------------
                   17880

1 row selected.
```

<a id="dcec3bdd8df082a8"></a>
## STDDEV

<a id="0884a161e1327331"></a>
### 구문

```
STDDEV( [ ALL | DISTINCT ] expr )
```

<a id="cf23b07df06112e4"></a>
### 설명

Aggregation 함수로써 expr set의 표준편차 (standard deviation)를 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 수행하고, DISTINCT를 명시한 경우 중복을 제거한 값들에 대해 수행한다. 둘 다 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

NULL 값을 제외하고 DISTINCT로 중복을 제거한 후의 expr set의 개수가 한 개일 경우, [VARIANCE](#ccc328bc968556f6)와 같이 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV 인자와 결과 타입**

<a id="75d0fd28bd70bab9"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

GOLDILOCKS는 다음과 같이 표준편차를 계산한다.  
　• expr set의 개수가 1이면 0을 반환한다.  
　• expr set의 개수가 1보다 크면 [STDDEV_SAMP( expr )](#309b751135ffa362) 값을 반환한다.

> 표준편차는, 분산의 양의 제곱근으로써 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV 함수는 [VARIANCE](#ccc328bc968556f6) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV( [ ALL ] expr )  
>  = SQRT( VARIANCE( [ ALL ] expr ) )  
>   
> STDDEV( DISTINCT expr )  
>  = SQRT( VARIANCE( DISTINCT expr ) )

<a id="6421f400515115fa"></a>
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

<a id="0106131ece39a63a"></a>
## STDDEV() OVER

<a id="c1d8244bbe2730f9"></a>
### 구문

```
STDDEV ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="bafce267bd9b9f1f"></a>
### 설명

Window function STDDEV는 expr의 표준편차 (standard deviation)를 구하는 함수이다.  
NULL 값을 제외한 expr의 개수가 한 개일 경우, 결과로 0을 반환한다.

<a id="1ca96ef2e8ea780f"></a>
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

<a id="b3030e7eca2e9e99"></a>
## STDDEV_POP

<a id="6c165dedd26daf5a"></a>
### 구문

```
STDDEV_POP( expr )
```

<a id="d96112d7c3db8b5e"></a>
### 설명

Aggregation 함수로써 expr set의 모 표준편차 (population standard deviation)를 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV_POP의 인자와 결과 타입**

<a id="c021c0be7f67736b"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 표준편차는 모 분산의 양의 제곱근으로써 모 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV_POP 함수는 [VAR_POP](#46b007f1a76910c5) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV_POP( expr )  
>  = SQRT( VAR_POP( expr ) )

<a id="bfc2b012d690ef32"></a>
### 사용 예

```
gSQL> SELECT STDDEV_POP(c1) FROM t1;

 STDDEV_POP(C1)
---------------
10.283968105746

1 row selected.
```

<a id="6b137710cee09e58"></a>
## STDDEV_POP() OVER

<a id="1b1910c3abb9d6ed"></a>
### 구문

```
STDDEV_POP ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="b0edb5938def26c5"></a>
### 설명

Window function STDDEV_POP은 expr의 모 표준편차 (population standard deviation)를 구하는 함수이다.  
NULL 값을 제외한 expr의 개수가 한 개일 경우, 결과로 0을 반환한다.

<a id="a98a6722bc1aed16"></a>
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

<a id="309b751135ffa362"></a>
## STDDEV_SAMP

<a id="94a7bf5d2404f4c4"></a>
### 구문

```
STDDEV_SAMP( expr )
```

<a id="7d5312cac9e93025"></a>
### 설명

Aggregation 함수로써 expr set의 표본 표준편차 (sample standard deviation)를 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 NULL값을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV_SAMP의 인자와 결과 타입**

<a id="10dad79e8503acdb"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 표본 표준편차는 표본 분산의 양의 제곱근으로써 표본 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV_SAMP 함수 [VAR_SAMP](#46ad098e54d32427) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV_SAMP( expr )  
>  = SQRT( VAR_SAMP( expr ) )

<a id="451936729456b1d6"></a>
### 사용 예

```
gSQL> SELECT STDDEV_SAMP(c1) FROM t1;

 STDDEV_SAMP(C1)
----------------
11.4978258814438

1 row selected.
```

<a id="409e0de519578dfd"></a>
## STDDEV_SAMP() OVER

<a id="12af230dc1443a6f"></a>
### 구문

```
STDDEV_SAMP ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="987474b788ce817d"></a>
### 설명

Window function STDDEV_SAMP은 expr의 표본 표준편차 (sample standard deviation)를 구하는 함수이다.  
NULL 값을 제외한 expr의 개수가 한 개일 경우, 결과로 NULL을 반환한다.

<a id="278d22af18002725"></a>
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

<a id="afcf76f85de9ec48"></a>
## STRING_AGG() OVER

<a id="af1cf72d97e8c2f6"></a>
### 구문

```
STRING_AGG( str [, delimiter] ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="ebbbaa2a75729e98"></a>
### 설명

Window function STRING_AGG는 OVER 절에 정의된 함수의 수행 범위에 따라 str을 연결하는 함수이다.

str이 NULL인 경우에는 제외된다.

delimiter는 str 연결 구분자이며, 생략할 경우 기본값은 NULL 이다.

str에는 character string 또는 binary string이 올 수 있다.  
str이 character string 이면, 결과타입은 varchar 이다.  
str이 binary string 이면, 결과타입은 varbinary 이다.

<a id="9fc9ac90af331fcc"></a>
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

<a id="782bc245837c146d"></a>
## SUBSTR

<a id="31ad25af85f60243"></a>
### 구문

```
SUBSTR( str FROM start_position [ FOR string_length ] )
SUBSTR( str, start_position [ , string_length ] )
```

<a id="a7c06eb5197a9c49"></a>
### 설명

[SUBSTRING](#cea95faba7ada96f)의 alias이다.

<a id="2ae30dac34499d4c"></a>
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

<a id="c8b95bb8de636ab2"></a>
## SUBSTRB

<a id="93612adca8850c0b"></a>
### 구문

```
SUBSTRB( str, start_position [ , string_length ] )
```

<a id="a60281d16150a9d7"></a>
### 설명

SUBSTRB 함수는 str에 대해 start_position으로부터 string_length 범위의 문자를 추출하여 반환한다.

SUBSTRB 함수는 start_position과 string_length가 byte 단위로 계산된다는 점 외에는 [SUBSTRING](#cea95faba7ada96f) 함수와 동일하다.

<a id="650f54d688870b89"></a>
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

<a id="cea95faba7ada96f"></a>
## SUBSTRING

<a id="c709424818112d55"></a>
### 구문

```
SUBSTRING( str FROM start_position [ FOR string_length ] )  
SUBSTRING( str, start_position [ , string_length ] )
```

<a id="44bf96e3cda2253c"></a>
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
자세한 내용은 [SUBSTR](#782bc245837c146d)과 [SUBSTRB](#c8b95bb8de636ab2)를 참조한다.

결과 타입은 다음 표와 같다.

**SUBSTRING의 결과 타입**

<a id="28c377448d30e239"></a>
| str | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="4441c57739e7593a"></a>
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

<a id="03fe0d1bde8dd785"></a>
## SUM

<a id="cd71c151a656b65c"></a>
### 구문

```
SUM( [ ALL | DISTINCT ] expr )
```

<a id="a1af638579c53c7c"></a>
### 설명

Aggregation 함수로써 expr 값들의 합을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복을 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

<a id="b6bc2bd8b179bca2"></a>
### 사용 예

```
gSQL> SELECT SUM(c1) FROM t1;

SUM(C1)
-------
      6

1 row selected.
```

<a id="1edaab1323c7bf27"></a>
## SUM() OVER

<a id="b917529e5952bae1"></a>
### 구문

```
SUM ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="2219664b86a4951b"></a>
### 설명

Window function SUM은 expr 값의 합을 구하는 함수이다.  
NULL 값은 연산에서 제외된다.

<a id="6d8e6042459cc70f"></a>
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

<a id="47edaca0e1596a9e"></a>
## SYSDATE

<a id="b7e9de96ecc77db4"></a>
### 구문

```
SYSDATE
```

<a id="09c701d0d91959ef"></a>
### 설명

Database server가 위치하는 OS 시간을 기준으로 현재의 DATE type 값을 얻는다.

<a id="96a9c5d613c50217"></a>
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

<a id="9f5fd6eabb6461f6"></a>
## SYS_EXTRACT_UTC

<a id="3783e11757374f31"></a>
### 구문

```
SYS_EXTRACT_UTC( datetime_with_timezone )
```

<a id="b04d80d9d3ffb227"></a>
### 설명

SYS_EXTRACT_UTC 는  UTC (Coordinated Universal Time—formerly Greenwich Mean Time) 값을 반환한다.  
timezone이 명시되지 않은 경우, session time zone으로 계산된다.

입력 인자에는 time, time with time zone, timestamp, timestamp with time zone 타입이 올 수 있다.  
결과 타입은 time 또는 timestamp 타입이다.

<a id="7272e8e59789e595"></a>
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

<a id="be97a8d4a96c19f5"></a>
## SYSTIME

<a id="b954300713a13651"></a>
### 구문

```
SYSTIME
```

<a id="608701a69c46f943"></a>
### 설명

Database server가 위치하는 OS 시간을 기준으로 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

<a id="4f7a81e13c5456f6"></a>
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

<a id="a559d8c550d7951e"></a>
## SYSTIMESTAMP

<a id="da97605df4fd3a12"></a>
### 구문

```
SYSTIMESTAMP
```

<a id="d0c837f8faf64f1a"></a>
### 설명

Database server가 위치하는 OS 시간을 기준으로 TIME ZONE이 있는 현재 TIMESTAMP WITH TIME ZONE type 값을 얻는다.

<a id="7549ef063c890a9a"></a>
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

<a id="1d9026bb9bee32c4"></a>
## TAN

<a id="30bf34699f8a7e54"></a>
### 구문

```
TAN( num )
```

<a id="946a91f7c8b6f544"></a>
### 설명

TAN 함수는 num의 tangent 값을 라디안 단위로 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="9b610ada265dd9d3"></a>
### 사용 예

```
gSQL> SELECT TAN( 1 ) AS RESULT FROM DUAL;
         RESULT
---------------
1.5574077246549
1 row selected.
```

<a id="0be5effb386e026c"></a>
## TO_BASE64

<a id="0ec5ce45d2dddf6d"></a>
### 구문

```
TO_BASE64( str )
```

<a id="5de5c0d75b072896"></a>
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

자세한 내용은 [FROM_BASE64](#c27d56064ad6329e)를 참조한다.

<a id="525dd21ed587565a"></a>
### 사용 예

```
gSQL> SELECT TO_BASE64( 'abc' ), TO_BASE64( 'abcd' ) FROM DUAL;

TO_BASE64( 'abc' ) TO_BASE64( 'abcd' )
------------------ -------------------
YWJj               YWJjZA==           
1 row selected.
```

<a id="86840e4a2b48b1cd"></a>
## TO_CHAR( datetime )

<a id="0ae590797f48c1b2"></a>
### 구문

```
TO_CHAR( datetime [, fmt ] )
```

<a id="4d174d68937dfd5d"></a>
### 설명

TO_CHAR( datetime ) 함수는 datetime을 명시된 fmt 형식의 문자열로 변환하여 반환한다.

인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  

입력 인자의 값이 하나라도 NULL이면 NULL을 반환한다.

fmt가 생략된 경우, default format 형식을 따른다.  
• DATE: [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#c4633f85f0eaaed9)  
• TIMESTAMP: [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#75b47cb73b3a190a)  
• TIMESTAMP WITH TIME ZONE: [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#f2873b18cb78ac0d)  
• TIME: [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#87c4cf7cbfe4f6d9)  
• TIME WITH TIME ZONE: [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#ff631fe160c25550)

인자 datetime이 INTERVAL 타입인 경우, fmt와 무관하게 string으로 변환하여 반환한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#eb35da7b15a57fad)을 참조한다.

결과 타입은 CHARACTER VARYING 이다.

<a id="6bcd318b4b10b7ef"></a>
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

<a id="dad3543b9fee1287"></a>
## TO_CHAR( number )

<a id="4b5624e7c7920adc"></a>
### 구문

```
TO_CHAR( number [, fmt ] )
```

<a id="1f1efc0b8c60cfb0"></a>
### 설명

TO_CHAR( number ) 함수는 number를 명시된 fmt 형식의 문자열로 변환하여 반환한다.

인자 number에는 숫자 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, 모든 유효 숫자를 문자열로 변환하여 반환한다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#71ad83b6ec3df20a)을 참조한다.  
입력 인자의 값이 하나라도 NULL이면 NULL을 반환한다.

결과 타입은 CHARACTER VARYING 이다.

<a id="693940861df296e3"></a>
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

<a id="bfa35d682d82f11d"></a>
## TO_DATE

<a id="a166b0c0136339c8"></a>
### 구문

```
TO_DATE( str [, fmt ] )
```

<a id="4fff7a396b4280ea"></a>
### 설명

TO_DATE 함수는 명시된 fmt 형식의 문자열 str을 DATE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_DATE_FORMAT은 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#eb35da7b15a57fad)을 참조한다.  
자세한 내용은 [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#c4633f85f0eaaed9)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

결과 타입은 DATE 이다.

<a id="67ae3d50cf7ba16c"></a>
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

<a id="95976ca3e77b73ce"></a>
## TO_NATIVE_BIGINT

<a id="507a58a960fafcae"></a>
### 구문

```
TO_NATIVE_BIGINT( str [, fmt ] )
```

<a id="04e68d1167642972"></a>
### 설명

TO_NATIVE_BIGINT 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_BIGINT 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#71ad83b6ec3df20a)을 참조한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="bc767d689f5e7866"></a>
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

<a id="94de5a0105c1279b"></a>
## TO_NATIVE_DOUBLE

<a id="c93ad6721e991ac4"></a>
### 구문

```
TO_NATIVE_DOUBLE( str [, fmt ] )
```

<a id="0a73426f43914fff"></a>
### 설명

TO_NATIVE_DOUBLE 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_DOUBLE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#71ad83b6ec3df20a)을 참조한다.

결과 타입은 NATIVE_DOUBLE이다.

<a id="84016634e1330021"></a>
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

<a id="033ab919094a9e43"></a>
## TO_NATIVE_INTEGER

<a id="f3bcea2696f797d7"></a>
### 구문

```
TO_NATIVE_INTEGER( str [, fmt ] )
```

<a id="85ed2ebba75087c5"></a>
### 설명

TO_NATIVE_INTEGER 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_INTEGER 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#71ad83b6ec3df20a)을 참조한다.

결과 타입은 NATIVE_INTEGER이다.

<a id="99e786f0204a5bbb"></a>
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

<a id="92db0202b2546bd0"></a>
## TO_NATIVE_REAL

<a id="f7bcd41bb12e1075"></a>
### 구문

```
TO_NATIVE_REAL( str [, fmt ] )
```

<a id="21ce08b0079b9388"></a>
### 설명

TO_NATIVE_REAL 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_REAL 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#71ad83b6ec3df20a)을 참조한다.

결과 타입은 NATIVE_REAL이다.

<a id="30fb1e11298eb895"></a>
### 사용 예

```
gSQL> SELECT TO_NATIVE_REAL( '123.45' ) AS RESULT1, 
             TO_NATIVE_REAL( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
```

<a id="0b9cbcaf8d2e662a"></a>
## TO_NATIVE_SMALLINT

<a id="4ae1c8b79a818c71"></a>
### 구문

```
TO_NATIVE_SMALLINT( str [, fmt ] )
```

<a id="a670e9740485f79c"></a>
### 설명

TO_NATIVE_SMALLINT 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_SMALLINT 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYIN과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#71ad83b6ec3df20a)을 참조한다.

결과 타입은 NATIVE_SMALLINT이다.

<a id="d85bfeed5c419237"></a>
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

<a id="3213da14584430f8"></a>
## TO_NUMBER

<a id="562fe0d99fac033c"></a>
### 구문

```
TO_NUMBER( str [, fmt] )
```

<a id="b42b0242cbaad941"></a>
### 설명

TO_NUMBER 함수는 명시된 fmt 형식의 문자열 str을 NUMBER 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#71ad83b6ec3df20a)을 참조한다.

결과 타입은 NUMBER이다.

<a id="8331802170c90b3d"></a>
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

<a id="8d6b0f2b251ec128"></a>
## TO_TIME

<a id="8fa779e35c18b765"></a>
### 구문

```
TO_TIME( str [, fmt ] )
```

<a id="be3bfc75a490daeb"></a>
### 설명

TO_TIME 함수는 명시된 fmt 형식의 문자열 str을 TIME 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIME_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#eb35da7b15a57fad)을 참조한다.  
자세한 내용은 [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#87c4cf7cbfe4f6d9)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

결과 타입은 TIME 이다.

<a id="1050138336fd9a4e"></a>
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

<a id="d76e036ea5b1e85c"></a>
## TO_TIME_TZ

<a id="ada0cdd1fc6e17b3"></a>
### 구문

```
TO_TIME_TZ( str [, fmt ] )
```

<a id="e04fb81269733c5c"></a>
### 설명

TO_TIME_WITH_TIME_ZONE의 alias이다.  
자세한 내용은 [TO_TIME_WITH_TIME_ZONE](#9f814a9eca8d9ad7)과 [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#ff631fe160c25550)을 참조한다.

<a id="a1003a0db7338284"></a>
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

<a id="9f814a9eca8d9ad7"></a>
## TO_TIME_WITH_TIME_ZONE

<a id="e44ef021b882c7d4"></a>
### 구문

```
TO_TIME_WITH_TIME_ZONE( str [, fmt ] )
TO_TIME_TZ( str [, fmt ] )
```

<a id="a7bcef7096fe48b0"></a>
### 설명

TO_TIME_WITH_TIME_ZONE 함수는 명시된 fmt 형식의 문자열 str을 TIME WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIME_WITH_TIME_ZONE_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#eb35da7b15a57fad)을 참조한다.  
자세한 내용은 [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#ff631fe160c25550)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

TO_TIME_WITH_TIME_ZONE의 alias로는 [TO_TIME_TZ](#d76e036ea5b1e85c) 함수가 있다.

결과 타입은 TIME WITH TIME ZONE 이다.

<a id="f3e5fde6d0962872"></a>
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

<a id="b0ac130c937546ed"></a>
## TO_TIMESTAMP

<a id="eff0bc14f1acaba9"></a>
### 구문

```
TO_TIMESTAMP( str [, fmt ] )
```

<a id="3ebc37e583af1981"></a>
### 설명

TO_TIMESTAMP 함수는 명시된 fmt 형식의 문자열 str을 TIMESTAMP 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIMESTAMP_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#eb35da7b15a57fad)을 참조한다.  
자세한 내용은 [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#75b47cb73b3a190a)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

결과 타입은 TIMESTAMP 이다.

<a id="cb59f8bea92e285e"></a>
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

<a id="18163e4dae48b277"></a>
## TO_TIMESTAMP_TZ

<a id="d6d7dea70437d143"></a>
### 구문

```
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="a759031135335108"></a>
### 설명

TO_TIMESTAMP_WITH_TIME_ZONE의 alias 이다.  
자세한 내용은 [TO_TIMESTAMP_WITH_TIME_ZONE](#26e80619590d76cb)과 [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#f2873b18cb78ac0d)을 참조한다.

<a id="4e39116fe3b8756a"></a>
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

<a id="26e80619590d76cb"></a>
## TO_TIMESTAMP_WITH_TIME_ZONE

<a id="f8e45a69aaea5490"></a>
### 구문

```
TO_TIMESTAMP_WITH_TIME_ZONE( str [, fmt ] )
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="f5aebde9121661d8"></a>
### 설명

TO_TIMESTAMP_WITH_TIME_ZONE 함수는 명시된 fmt 형식의 문자열 str을 TIMESTAMP WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#eb35da7b15a57fad)을 참조한다.  
자세한 내용은 [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#f2873b18cb78ac0d)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

TO_TIMESTAMP_WITH_TIME_ZONE의 alias로는 [TO_TIMESTAMP_TZ](#18163e4dae48b277) 함수가 있다.

결과 타입은 TIMESTAMP WITH TIME ZONE 이다.

<a id="4282a8675c80e940"></a>
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

<a id="ded9eb34b0c43c29"></a>
## TRANSACTION_DATE

<a id="a57375b824762321"></a>
### 구문

```
TRANSACTION_DATE()
```

<a id="642b651eab4b607a"></a>
### 설명

Session 시간을 기준으로 현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="1d5cf153c5734e91"></a>
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

<a id="1ba3d2240ddb32a0"></a>
## TRANSACTION_LOCALTIME

<a id="816095ab38531eff"></a>
### 구문

```
TRANSACTION_LOCALTIME()
```

<a id="434cde9c30967c26"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 없는 현재 시간 (TIME WITHOUT TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="63c3cc7f9432347d"></a>
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

<a id="3f6ac5b21ef7e4f0"></a>
## TRANSACTION_LOCALTIMESTAMP

<a id="b3090ad38bddf355"></a>
### 구문

```
TRANSACTION_LOCALTIMESTAMP()
```

<a id="59595f8dfbac708a"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 없는 현재 TIMESTAMP (TIMESTAMP WITHOUT TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="cc0327f6434d446a"></a>
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

<a id="0cacc0373099fba2"></a>
## TRANSACTION_TIME

<a id="a019852c43cfae42"></a>
### 구문

```
TRANSACTION_TIME()
```

<a id="a0371c52c74a45d8"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="a95a2ca6da367b3c"></a>
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

<a id="297bdcce6ef145cc"></a>
## TRANSACTION_TIMESTAMP

<a id="7ecb0beb5c56ca6b"></a>
### 구문

```
TRANSACTION_TIMESTAMP()
```

<a id="a50f9dfd2a28c18d"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="1d06ed9aa0019066"></a>
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

<a id="ce76e78577c764fc"></a>
## TRANSLATE

<a id="731949b7cf076f0d"></a>
### 구문

```
TRANSLATE( string, from, to )
```

<a id="7be4b06f9de9f00b"></a>
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

<a id="2671ac43b312f1b9"></a>
| string 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="8afdcb66269e61ac"></a>
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

<a id="2b19e1f2e000a0c7"></a>
## TRIM

<a id="b2ae8a39ba379ad0"></a>
### 구문

```
TRIM([ [ LEADING | TRAILING | BOTH ]  [trim_character] FROM ] trim_source)
```

<a id="3d9c0e8b6005b80b"></a>
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

<a id="bbb15e1fe714428e"></a>
| trim_character, trim_source 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="bdb1566b4db522b6"></a>
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

<a id="37b4bc7fa8be4194"></a>
## TRUNC( number )

<a id="291bf65d70f9cc77"></a>
### 구문

```
TRUNC( num [ , scale ] )
```

<a id="78f46c73a8ec0877"></a>
### 설명

TRUNC( number ) 함수는 scale 기준으로 num을 버림한 값을 반환한다.

인자 num과 scale에는 숫자 타입이 올 수 있다.  
인자 num 또는 scale이 NULL이면 NULL을 반환한다.

scale이 생략된 경우, scale은 0이 되어 TRUNC( num, 0 )일 때와 같이 실행된다.  
scale이 양수인 경우, 소수점 오른쪽 자리수를 기준으로 버림한다.  
scale이 음수인 경우, 소수점 왼쪽 자리수를 기준으로 버림한다.

<a id="0ea7af76eda0000a"></a>
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

<a id="7a3bfa007d444c6c"></a>
## TRUNC( date )

<a id="1d291505e97345d1"></a>
### 구문

```
TRUNC( date [ , fmt ] )
```

<a id="d38f78dc316ce9f4"></a>
### 설명

TRUNC( date ) 함수는 date를 지정된 fmt 단위로 버림한 값을 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
인자 date 또는 fmt이 NULL이면 NULL을 반환한다.

결과 타입은 인자로 받은 date 타입과 관계없이 항상 DATE 타입이다.

fmt가 생략되었을 경우의 기본값은 DAY이며, 사용 가능한 형식문자열은 다음 표와 같다.

**fmt에 사용가능한 형식문자열**

<a id="225fe1355e20d315"></a>
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

<a id="5d7cab92eaf444dd"></a>
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

<a id="4840652cf5cde87f"></a>
## UPPER

<a id="f24cc13b1406ce0d"></a>
### 구문

```
UPPER( str )
```

<a id="6852053490889e9a"></a>
### 설명

UPPER 함수는 str의 대문자를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.  
str이 NULL이면 결과값도 NULL이다.

반환되는 타입은 인자 str과 동일한 타입이다.

<a id="b80f43d0ec915a72"></a>
### 사용 예

```
gSQL> SELECT UPPER( 'spring' ) AS RESULT FROM DUAL;
RESULT
------
SPRING
1 row selected.
```

<a id="2f7997bd53d13aae"></a>
## UNHEX

<a id="98821357b29343a3"></a>
### 구문

```
UNHEX( str )
```

<a id="07c264975b58990d"></a>
### 설명

인자 str은 16진수 문자이며, 이를 각 byte로 표현하여 binary string으로 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 BINARY VARYING이나 BINARY LONG VARYING과 같은 BINARY 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 16진수 범위에 속하지 않는 문자가 포함되면 에러를 반환한다.

자세한 내용은 [HEX](#52d5e89a219d4ad8)를 참조한다.

<a id="606445b8fb9e2e39"></a>
### 사용 예

```
gSQL> SELECT UNHEX( HEX( 'abc' ) ) FROM DUAL;
UNHEX( HEX( 'abc' ) )
---------------------
616263               
1 row selected.
```

<a id="88eda26b981c9962"></a>
## UNHEX_TO_CHARSTR

<a id="2d40d856cc628cfe"></a>
### 구문

```
UNHEX_TO_CHARSTR( str )
```

<a id="51c915938440c127"></a>
### 설명

인자 str은 16진수 문자이며 이를 각 byte로 표현하여 character string으로 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 CHARACTER VARYING이나 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 16진수 범위에 속하지 않는 문자가 포함되면 에러를 반환한다.

자세한 내용은 [HEX](#52d5e89a219d4ad8)와 [UNHEX](#2f7997bd53d13aae)를 참조한다.

<a id="9189bfbb53cc5eac"></a>
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

<a id="09c91db11157e6f8"></a>
## USER_ID

<a id="4d9f1db122249d79"></a>
### 구문

```
USER_ID ()
```

<a id="9da81df866cd1905"></a>
### 설명

현재 사용자의 number ID를 얻는다.

> Cluster system에서는 접속한 server에 따라 다른 값을 가질 수 있다.  
> 현재 사용자의 이름을 얻는 [CURRENT_USER](#4075373efcce5443) 함수 사용을 권장한다.

<a id="c6399c4b570deb1b"></a>
### 사용 예

```
% gsql test test

gSQL> SELECT USER_ID() FROM dual;

USER_ID()
---------
        6

1 row selected.
```

<a id="9466b20723e3577b"></a>
## UUID

<a id="34cf6c9775aecbb5"></a>
### 구문

```
UUID()
```

<a id="631872e90187ce7f"></a>
### 설명

UUID 함수는 전역고유식별자 (Universal Unique Identifier) 를 생성하여 반환한다.  
반환되는 타입은 VARBINARY 이며 내부적으로 16 바이트로 구성된다.

<a id="ea1f4d96c8b50e08"></a>
### 사용 예

```
gSQL> SELECT HEX( UUID() ) FROM DUAL;
HEX( UUID() )                   
--------------------------------
E6F0A5C2387511E8B95259E479C2FD50
1 row selected.
```

<a id="46b007f1a76910c5"></a>
## VAR_POP

<a id="b3fa39400fee91a9"></a>
### 구문

```
VAR_POP( expr )
```

<a id="9f3e8b9a94722c95"></a>
### 설명

Aggregation 함수로써 expr set의 모 분산 (population variance)을 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**VAR_POP 인자와 결과 타입**

<a id="93eb8e956120f9ba"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 분산은 모 집단 (전체)의 분산이며 분산은 편차 제곱의 평균이다. 즉, 데이터의 각 값에서 모 평균 (전체의 평균)을 빼고 제곱해서 모두 더한 뒤 모 집단의 데이터 개수로 나눈다.  
> 이는 각 관찰값들이 평균으로부터 얼마나 많이 퍼져있는지 파악하는데 사용된다.

자세한 내용은 [STDDEV_POP](#b3030e7eca2e9e99)을 참조한다.

<a id="1ff66fbd0209b392"></a>
### 사용 예

```
gSQL> SELECT VAR_POP(c1) FROM t1;

VAR_POP(C1)
-----------
     105.76

1 row selected.
```

<a id="cbb5a4f63c78944c"></a>
## VAR_POP() OVER

<a id="91f8a1e61bf333a2"></a>
### 구문

```
VAR_POP ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="23c3a3e79bad76fd"></a>
### 설명

Window function VAR_POP은 expr의 모 분산 (population variance)을 구하는 함수이다.  
NULL 값을 제외한 expr이 한 개일 경우, 결과로 0을 반환한다.

<a id="62e737ca5a50bccf"></a>
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

<a id="46ad098e54d32427"></a>
## VAR_SAMP

<a id="34f6573358c735d1"></a>
### 구문

```
VAR_SAMP( expr )
```

<a id="c4f872b94082bd3e"></a>
### 설명

Aggregation 함수로써 expr set의 표본 분산 (sample variance)을 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 NULL값을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**VAR_SAMP 인자와 결과 타입**

<a id="76e9253fa62a0d40"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 집단 (전체)을 다루는 모 분산과 달리, 표본 분산은 추출한 표본으로 평균과 편차를 다룬다. 즉, 데이터의 각 값에서 표본의 평균을 빼고 제곱해서 모두 더한 뒤, 표본 집단의 데이터 개수 - 1로 나눈다.  
> 이는 모 집단의 분산을 추정하는 데 사용된다.

자세한 내용은 [STDDEV_SAMP](#309b751135ffa362)을 참조한다.

<a id="b379ef63df31edaf"></a>
### 사용 예

```
gSQL> SELECT VAR_SAMP(c1) FROM t1;

VAR_SAMP(C1)
------------
       132.2

1 row selected.
```

<a id="b962db03eb6d54ee"></a>
## VAR_SAMP() OVER

<a id="c036840d30c19be9"></a>
### 구문

```
VAR_SAMP ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="132ad2975e54ef92"></a>
### 설명

Window function VAR_SAMP는 expr의 표본 분산 (sample variance)을 구하는 함수이다.  
NULL 값을 제외한 expr이 한 개일 경우, 결과로 NULL을 반환한다.

<a id="06b5a52378c46f4f"></a>
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

<a id="ccc328bc968556f6"></a>
## VARIANCE

<a id="30cd8eee302d038c"></a>
### 구문

```
VARIANCE( [ ALL | DISTINCT ] expr )
```

<a id="5ee5aca36da2a4fb"></a>
### 설명

Aggregation 함수로써 expr set의 분산 (variance)을 얻는다.

ALL을 명시한 경우 모든 값들에 대해 수행하고, DISTINCT를 명시한 경우 중복을 제거한 값들에 대해 수행한다. 둘 다 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

NULL 값을 제외하고 DISTINCT로 중복을 제거한 후의 expr set의 개수가 한 개일 경우, 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**VARIANCE 인자와 결과 타입**

<a id="f7885780f68c5563"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> GOLDILOCKS는 분산을 다음과 같이 계산한다.  
> 　• expr set의 개수가 1이면 0을 반환한다.  
> 　• expr set의 개수가 1보다 크면, [STDDEV_SAMP( expr )](#309b751135ffa362) 값을 반환한다.

자세한 내용은 [STDDEV](#dcec3bdd8df082a8)를 참조한다.

<a id="1e4cb65f7de2a7c7"></a>
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

<a id="1efcfef19e2fab14"></a>
## VARIANCE() OVER

<a id="ba85c74504130418"></a>
### 구문

```
VARIANCE ( expr ) OVER < window name or specification >
```

&lt; window name or specification &gt;에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#9676d213f7da2ef0)를 참조한다.

<a id="f472c6ee1147701d"></a>
### 설명

Window function VARIANCE는 expr의 분산 (variance)을 구하는 함수이다.  
NULL 값을 제외한 expr이 한 개일 경우, 결과로 0을 반환한다.

<a id="984b9b9597555758"></a>
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

<a id="f695ad723add999c"></a>
## VERSION

<a id="bade0743b6545bfd"></a>
### 구문

```
VERSION()
```

<a id="499df7b912180113"></a>
### 설명

제품의 version string을 얻는다.

<a id="b6a7fb1b814fd694"></a>
### 사용 예

```
gSQL> SELECT VERSION() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="3575eae4d0423216"></a>
## WIDTH_BUCKET

<a id="a796784d89ea837c"></a>
### 구문

```
WIDTH_BUCKET( num, min, max, cnt )
```

<a id="d1b65b1765afd413"></a>
### 설명

WIDTH_BUCKET 함수는 명시된 min, max 범위에서 cnt와 동일한 넓이를 갖는 구간을 생성하고, num이 속하는 구간의 위치를 반환한다.

인자 num, min, max, cnt에는 숫자 타입이 올 수 있다.

min, max는 구간에 대한 범위를 의미하며, min, max 값이 같은 경우에는 에러를 반환한다.  
cnt는 구간 개수를 의미하고 양의 정수이어야 하며 0 이거나 음수인 경우에는 에러를 반환한다.  
구간의 위치에는 1부터 시작하는 번호가 부여된다.

num, min, max, cnt 중 하나라도 NULL인 경우, 결과값도 NULL이다.

<a id="a10fae449a1d4221"></a>
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
