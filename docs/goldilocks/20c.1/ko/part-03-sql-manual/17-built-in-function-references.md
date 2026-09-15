<a id="9ab81cd8b622c054"></a>

# 17. Built-in Function References

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/9ab81cd8b622c054)  
> 태그: `20c.1_30_tag`

[← 16. Built-in Data Type References](16-built-in-data-type-references.md) · [전체 목차](../README.md) · [18. SQL References →](18-sql-references.md)

<a id="fad9a0fb63da9e30"></a>
## * (MULTIPLICATION)

<a id="d6dbf16618fce077"></a>
### 구문

```
expr1 * expr2
```

<a id="0fbe3f36522f0ee6"></a>
### 설명

expr1과 expr2의 곱하기 연산 결과를 반환한다.

곱하기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#07646aa9949781c3)을 참조한다.

**숫자형 * 연산**

<a id="030483097b159f4a"></a>
| expr1 (expr2) | expr2 (expr1) | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="e548250c7eda8994"></a>
<table class="table column_count_3"><caption>INTERVAL * 연산 </caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>숫자형 타입</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>숫자형 타입</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_left" colspan="3"><div>자세한 내용은 <a class="reference text" href="#1402e51bdbf57c1e">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

**표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입**

<a id="1402e51bdbf57c1e"></a>
<table><thead><tr><th align="center">INTERVAL YEAR TO MONTH</th><th align="center">INTERVAL DAY TO SECOND</th></tr></thead><tbody><tr><td valign="middle"><ul><li>INTERVAL YEAR</li><li>INTERVAL MONTH</li><li>INTERVAL YEAR TO MONTH</li></ul></td><td valign="middle"><ul><li>INTERVAL DAY</li><li>INTERVAL HOUR</li><li>INTERVAL MINUTE</li><li>INTERVAL SECOND</li><li>INTERVAL DAY TO HOUR</li><li>INTERVAL DAY TO MINUTE</li><li>INTERVAL DAY TO SECOND</li><li>INTERVAL HOUR TO MINUTE</li><li>INTERVAL HOUR TO SECOND</li><li>INTERVAL MINUTE TO SECOND</li></ul></td></tr></tbody></table>

<a id="2bd0cf7ce5a38062"></a>
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

<a id="56899a78835fb201"></a>
## + (ADDITION)

<a id="551ea1a58ec7747d"></a>
### 구문

```
expr1 + expr2
```

<a id="9b69c668c141b21d"></a>
### 설명

expr1과 expr2의 더하기 연산 결과를 반환한다.

더하기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#07646aa9949781c3)을 참조한다.

**숫자형 + 연산**

<a id="0fef58c10ac5575e"></a>
| expr1 (expr2) | expr2 (expr1) | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="72eb5e347ef2398d"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) + 연산</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#1402e51bdbf57c1e">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="290380d5d397a5b0"></a>
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

<a id="f2a00d7e7ae5b96f"></a>
## + (POSITIVE)

<a id="08a0fca50f5dc418"></a>
### 구문

```
+ expr
```

<a id="eeafb24f3caba6be"></a>
### 설명

expr에 + 부호를 표시한다.

<a id="31cfbaad04bbc4cd"></a>
### 사용 예

```
gSQL> SELECT +3 AS RESULT1, +(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      3      -3
1 row selected.
```

<a id="b3e82f0107863a21"></a>
## - (NEGATIVE)

<a id="d7d5bd3a7d0dd0c8"></a>
### 구문

```
- expr
```

<a id="3197968e05bf6bc5"></a>
### 설명

expr에 - 부호를 표시한다.

<a id="5f14feb46193e4da"></a>
### 사용 예

```
gSQL> SELECT -3 AS RESULT1, -(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     -3       3
1 row selected.
```

<a id="62a61dfa79308362"></a>
## - (SUBTRACTION)

<a id="da5775c41349eef5"></a>
### 구문

```
expr1 - expr2
```

<a id="f37d66161e197691"></a>
### 설명

expr1과 expr2의 뺄셈 연산 결과를 반환한다.

뺄셈 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#07646aa9949781c3)을 참조한다.

**숫자형 - 연산**

<a id="ac36ff1664b64fce"></a>
| expr1 | expr2 | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="d6fb7e3934eb4ee1"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) - 연산</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMBER</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#1402e51bdbf57c1e">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="76177fd9a277f437"></a>
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

<a id="f812a57fc35a9de4"></a>
## / (DIVISION)

<a id="c3047bb3de55f9c6"></a>
### 구문

```
expr1 / expr2
```

<a id="549163706bf4ba4b"></a>
### 설명

expr1과 expr2의 나누기 연산 결과를 반환한다.

나누기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#07646aa9949781c3)을 참조한다.

**숫자형/ 연산**

<a id="34ad33fcfd300398"></a>
| expr1 | expr2 | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER | NUMBER |
| NATIVE_DOUBLE | NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="179efea0472e6373"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL)/ 연산</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(결과 타입은 interval type 이다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#1402e51bdbf57c1e">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="20522438b37ee8f4"></a>
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

<a id="e72ca95b1d94da0e"></a>
## || (CONCATENATE)

<a id="8ff49bb2da35b137"></a>
### 구문

```
str1 || str2
```

<a id="861efb17eb5e2f77"></a>
### 설명

CONCATENATE는 str1과 str2를 연결한 문자열을 반환한다.

str1과 str2 중 하나가 null인 경우 null이 아닌 나머지 str이 반환되고, str1과 str2가 모두 null인 경우 NULL이 반환된다.

인자로는 character string 타입 또는 binary string 타입으로 변환될 수 있는 타입이 올 수 있다.  
자세한 내용은 [타입간 변환](11-sql-elements.md#07646aa9949781c3)을 참조한다.

[CONCAT](#a9fb83a876b717d9), [CONCATENATE](#b04073e8a9e83240)의 alias 이다.

결과 타입은 다음 표와 같다.

**|| (CONCATENATE)의 결과 타입**

<a id="4d499353693dcc6d"></a>
| Data type | CHAR | VARCHAR | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR | CHAR | VARCHAR | LONG VARCHAR |
| VARCHAR | VARCHAR | VARCHAR | LONG VARCHAR |
| LONG VARCHAR | LONG VARCHAR | LONG VARCHAR | LONG VARCHAR |
| Data type | BINARY | VARBINARY | LONG VARBINARY |
| BINARY | BINARY | VARBINARY | LONG VARBINARY |
| VARBINARY | VARBINARY | VARBINARY | LONG VARBINARY |
| LONG VARBINARY | LONG VARBINARY | LONG VARBINARY | LONG VARBINARY |

<a id="8c725c02fb630e47"></a>
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

<a id="2b6afdb6d28566b4"></a>
## ABS

<a id="a585ea06147109c6"></a>
### 구문

```
ABS( num )
```

<a id="7812d2fcdf7a5d2a"></a>
### 설명

ABS는 num의 절대값을 반환한다.  

인자 num에는 숫자 타입 또는 숫자로 변환될 수 있는 타입이 올 수 있다.  
num이 NULL이면 NULL을 반환한다.

<a id="91631f6bd3ff7e7e"></a>
### 사용 예

```
gSQL> SELECT ABS(-1) AS RESULT1, ABS(1) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1       1
1 row selected.
```

<a id="ecdb650a6b8661c2"></a>
## ACOS

<a id="61581f355695db5b"></a>
### 구문

```
ACOS( num )
```

<a id="25093c7c5e468ed0"></a>
### 설명

ACOS 함수는 num의 arc cosine 값을 반환한다.  

인자 num은 -1 이상 1 이하의 값이어야 한다.  
num이 NULL이면 NULL을 반환한다.  

0 ~ pi 사이의 라디안 값을 반환한다.

<a id="84b9a943a19088a2"></a>
### 사용 예

```
gSQL> SELECT ACOS( 1 ) FROM DUAL;
ACOS( 1 )
---------
        0
1 row selected.
```

<a id="441090925f082310"></a>
## ADDDATE

<a id="1051496e73b8b7f5"></a>
### 구문

```
ADDDATE( date, INTERVAL expr unit  )
ADDDATE( expr, days )
```

<a id="8d3a352eae03979c"></a>
### 설명

ADDDATE는 입력받은 첫 번째 인자에 두 번째 인자를 더하기 연산하여 그 결과를 반환한다.  

첫 번째 인자에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있고, 두 번째 인자에는 INTERVAL 또는 숫자 타입이 올 수 있다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.

결과 타입은 [(DATETIME/INTERVAL) + 연산](#72eb5e347ef2398d)과 동일하다.

<a id="e02855073dc51f33"></a>
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

<a id="ea5ffc510f0a29b9"></a>
## ADDTIME

<a id="4204b1951336e6b1"></a>
### 구문

```
ADDTIME( expr1, expr2 )
```

<a id="e1139f93cabbee94"></a>
### 설명

ADDTIME은 입력받은 expr2를 expr1에 더하여 그 결과를 반환한다.

expr1에는 TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE TYPE이 올 수 있고, expr2에는 INTERVAL DAY TO SECOND TYPE이 올 수 있다.  

expr1이나 expr2가 NULL이면 결과값은 NULL이다.

결과 타입은 [(DATETIME/INTERVAL) + 연산](#72eb5e347ef2398d)과 동일하다.

<a id="871d7312b3815c7b"></a>
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

<a id="b4bb9ce42541b64d"></a>
## ADD_MONTHS

<a id="35ace6de34e49ebb"></a>
### 구문

```
ADD_MONTHS( date, number )
```

<a id="f66eb140512955da"></a>
### 설명

ADD_MONTHS는 date에 number 숫자만큼의 달을 더한 값을 반환한다.  
만약 ADD_MONTHS 연산 후에 날짜가 그 달의 마지막 날보다 큰 경우에는 마지막 날짜로 조정한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있으며 인자 number에는 숫자타입이 올 수 있다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.

결과 타입은 입력 인자 date 타입과 관계없이 항상 DATE 타입이다.

<a id="fca394218adf4d7a"></a>
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

<a id="56c32c5dadd6452f"></a>
## ASCII

<a id="a8149de444b2dbf2"></a>
### 구문

```
ASCII( char )
```

<a id="64b2635b93a9bd50"></a>
### 설명

char의 첫 번째 문자에 대한 database character set code를 십진수로 반환한다.

char에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있고, 반환되는 타입은 NUMBER 이다.  
char가 NULL이면 NULL을 반환한다.

<a id="12880fb057ca6c06"></a>
### 사용 예

```
gSQL> SELECT ASCII( 'G' ) AS RESULT FROM DUAL;
RESULT
------
    71
1 row selected.
```

<a id="4833418524efb2a8"></a>
## ASIN

<a id="f3bd2fca912da792"></a>
### 구문

```
ASIN( num )
```

<a id="bd05863f2820e7c1"></a>
### 설명

ASIN 함수는 num의 arc sin 값을 반환한다.

인자 num은 -1 이상 1 이하의 값이어야 한다.  
num이 NULL이면 NULL을 반환한다.

-pi/2 ~ pi/2 사이의 라디안 값을 반환한다.

<a id="bc3f78a3873a4ae1"></a>
### 사용 예

```
gSQL> SELECT ASIN( 0 ) FROM DUAL;
ASIN( 0 )
---------
        0
1 row selected.
```

<a id="4662c67032984a00"></a>
## ATAN

<a id="68d1aa862a70f35d"></a>
### 구문

```
ATAN( num )
```

<a id="02375b6abeb3e042"></a>
### 설명

ATAN 함수는 num의 arc tangent 값을 반환한다.

num 값 범위의 제한은 없으며, -pi/2 ~ pi/2 사이의 라디안 값을 반환한다.   
num이 NULL이면 NULL을 반환한다.

<a id="e57fbd066aaf11ff"></a>
### 사용 예

```
gSQL> SELECT ATAN(0.5) FROM DUAL;
       ATAN(0.5)
----------------
.463647609000806
1 row selected.
```

<a id="aa92618acb0d4aa2"></a>
## ATAN2

<a id="2b83006603bcf3df"></a>
### 구문

```
ATAN2( num1, num2 )
```

<a id="d0ec896157f2cfdd"></a>
### 설명

ATAN2 함수는 num1과 num2의 arc tangent 값을 반환한다.

인자 num1 값 범위의 제한은 없으며 -pi ~ pi 사이의 라디안 값을 반환한다.   
num1 또는 num2 중 하나라도 NULL이면 NULL을 반환한다.

<a id="3f1e831f31e0c0ec"></a>
### 사용 예

```
gSQL> SELECT ATAN2(1,2) FROM DUAL; 
      ATAN2(1,2)
----------------
.463647609000806
1 row selected.
```

<a id="508fdfccb1d4afc3"></a>
## AVG

<a id="835b929e4aaeb3dd"></a>
### 구문

```
AVG( [ ALL | DISTINCT ] num )
```

<a id="a55c6286c1716138"></a>
### 설명

Aggregation 함수로써 expr 들의 평균값을 얻는데 사용된다.

ALL을 명시한 경우, 모든 값들에 대한 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복 제거한 값들에 대한 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

<a id="f8aa0f05f28df777"></a>
### 사용 예

```
gSQL> SELECT AVG(c1) FROM t1;

AVG(C1)
-------
      2

1 row selected.
```

<a id="1154feda9405cb0b"></a>
## BITAND

<a id="65f935333e274e6f"></a>
### 구문

```
BITAND( num1, num2 )
```

<a id="2187dcdb752c3de3"></a>
### 설명

num1과 num2의 비트에 대한 AND 연산 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.

결과 타입은 NATIVE_BIGINT이다.

<a id="257ea8c94d95074d"></a>
### 사용 예

```
gSQL> SELECT BITAND(2, 4) FROM DUAL;
BITAND(2, 4)
------------
           0
1 row selected.
```

<a id="b75d190540619c02"></a>
## BITNOT

<a id="316b85ada38c9d3c"></a>
### 구문

```
BITNOT( num )
```

<a id="55eb0d07e08185db"></a>
### 설명

num의 비트에 대해 NOT 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자가 NULL이면 결과값도 NULL이다.

결과 타입은 다음과 같다.  
• 입력 인자가 NATIVE_SMALLINT인 경우, NATIVE_SMALLINT  
• 입력 인자가 NATIVE_INTEGER인 경우, NATIVE_INTEGER  
• 입력 인자가 NATIVE_BIGINT인 경우, NATIVE_BIGINT

<a id="3041586a4b64115c"></a>
### 사용 예

```
gSQL> SELECT BITNOT( 5 ) AS RESULT FROM DUAL;
RESULT
------
    -6
1 row selected.
```

<a id="0d276f0eef4a5adb"></a>
## BITOR

<a id="844d6ee7e1573963"></a>
### 구문

```
BITOR( num1, num2 )
```

<a id="6a6accfbff9fbb81"></a>
### 설명

num1과 num2의 비트에 대해 OR 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자의 값이 하나라도 NULL이면 결과는 NULL이다.

결과 타입은 NATIVE_BIGINT이다.

<a id="713a5f5ba699ca9c"></a>
### 사용 예

```
gSQL> SELECT BITOR( 2, 4 ) FROM DUAL;
BITOR( 2, 4 )
-------------
            6
1 row selected.
```

<a id="34f572a6fa6e089a"></a>
## BITXOR

<a id="54d640f815f36e6d"></a>
### 구문

```
BITXOR( num1, num2 )
```

<a id="52c7c259551d4139"></a>
### 설명

num1과 num2의 비트에 대해 XOR 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.  
입력 인자의 값이 하나라도 NULL이면 결과는 NULL이다.

결과 타입은 NATIVE_BIGINT이다.

<a id="9bb7d511c98878a7"></a>
### 사용 예

```
gSQL> SELECT BITXOR( 5, 3 ) FROM DUAL;
BITXOR( 5, 3 )
-------------
            6
1 row selected.
```

<a id="de539a00415063b3"></a>
## BIT_LENGTH

<a id="8cca5ed5450e8ea6"></a>
### 구문

```
BIT_LENGTH( str )
```

<a id="e4e852cd605601cb"></a>
### 설명

BIT_LENGTH는 str의 비트 수를 반환한다.  
str이 NULL이면 NULL을 반환한다.

<a id="76bd9a0b1bbee663"></a>
### 사용 예

```
gSQL> SELECT BIT_LENGTH( 'LIKE' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
             32
    1 row selected.
```

<a id="75d9967da5addf6b"></a>
## BYTE_LENGTH

<a id="f3f108e73cb1bebe"></a>
### 구문

```
BYTE_LENGTH( str )
```

<a id="0d481970353aa613"></a>
### 설명

OCTET_LENGTH의 alias이다.  
자세한 내용은 [OCTET_LENGTH](#efc6be7a196cd804), [LENGTHB](#3c531ddc38355109)를 참조한다.

<a id="e96de885aaf373e5"></a>
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

<a id="4a7aa86c6e3377f7"></a>
## CASE2

<a id="372f9d019b1a8b66"></a>
### 구문

```
CASE2( condition1, result1
      [, condition2, result2
       , ...
       , conditionN, resultN ]
      [, default ] )
```

<a id="2ea5a47818bb9605"></a>
### 설명

CASE2는 기술된 순서대로 condition을 평가한다.  
비교 결과가 FALSE이면 TRUE가 나올 때까지 평가한다.  
비교 결과가 TRUE이면 대응되는 result를 반환하고, 이후는 평가하지 않는다.  
비교 결과가 모두 FALSE인 경우에는 default를 반환하고, default가 생략된 경우에는 NULL을 반환한다.

result에 여러 type이 오는 경우, [결과 타입 조합 규칙](11-sql-elements.md#933953bbf127dad3)에 따라 result type이 결정된다.

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

<a id="7169bf567fecb94b"></a>
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

<a id="d22ca9da93eeaad8"></a>
## CBRT

<a id="05c97d696b9f9c6c"></a>
### 구문

```
CBRT( num )
```

<a id="73bef902e02ab0e2"></a>
### 설명

num의 세제곱근을 반환한다.  
num이 NULL이면 결과값도 NULL이 반환된다.

<a id="deb3df6c36b1330c"></a>
### 사용 예

```
gSQL> SELECT CBRT( 27 ) FROM DUAL;
CBRT( 27 )
----------
         3
1 row selected.
```

<a id="b680b186a63b3b2b"></a>
## CEIL

<a id="17a516a09742b174"></a>
### 구문

```
CEIL( num )
CEILING( num )
```

<a id="f01f489f1e790353"></a>
### 설명

CEIL 함수는 num 보다 크거나 같은 가장 작은 정수를 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="754d9a70175c4d3b"></a>
### 사용 예

```
gSQL> SELECT CEIL( 3.5 ) AS RESULT1, CEIL( -3.5 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      4      -3
1 row selected.
```

<a id="6fba33a6d3e98937"></a>
## CHAR_LENGTH

<a id="d4958e7d1eb4288b"></a>
### 구문

```
CHAR_LENGTH( str )            
CHARACTER_LENGTH( str )
```

<a id="eb415330a5c03958"></a>
### 설명

CHAR_LENGTH는 str에 대해 character set에 따른 문자수를 반환한다.

str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있고, 반환되는 타입은 NATIVE_BIGINT 이다.

str의 타입이 CHARACTER 타입이면 공백문자 (trailing blank)를 포함하여 계산한다.  
str이 NULL이면 NULL이 반환된다.

[LENGTH](#45df1dbd6c5b6d9a)의 alias이다.

<a id="18211108643b2112"></a>
### 사용 예

Multi byte character set: (예:UTF8)

```
gSQL> SELECT CHAR_LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="019b8157cbcb19a0"></a>
## CHR

<a id="a2c746eaaeb35616"></a>
### 구문

```
CHR( num )
```

<a id="583aa0cd7df027e8"></a>
### 설명

num에 대응하는 database character set code 내의 charater를 반환한다.

num은 숫자 타입이다.  
num이 NULL이면 NULL을 반환한다.  

결과 타입은 VARCHAR 이다.

<a id="dca4cd21c7c62f73"></a>
### 사용 예

```
gSQL> SELECT CHR(71) FROM DUAL;
CHR(71)
-------
G      
1 row selected.
```

<a id="0c40087b7a9c2a37"></a>
## CLOCK_DATE

<a id="a9897dec2c977a08"></a>
### 구문

```
CLOCK_DATE()
```

<a id="9d303a29c7f69496"></a>
### 설명

함수가 호출될 때마다 현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="cd52e9cfdf2d961d"></a>
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

<a id="8e4a2491e3df3c06"></a>
## CLOCK_LOCALTIME

<a id="e805c4037fd5c103"></a>
### 구문

```
CLOCK_LOCALTIME()
```

<a id="cea95e79a50540f6"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 없는 현재 시간 (TIME WITHOUT TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="cd9a963b945ef624"></a>
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

<a id="f8a81f1510396294"></a>
## CLOCK_LOCALTIMESTAMP

<a id="13d3d2f19a5f8ca4"></a>
### 구문

```
CLOCK_LOCALTIMESTAMP()
```

<a id="4b9e366842300cbd"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 없는 현재 TIMESTAMP (TIMESTAMP WITHOUT TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="e5a1589f3e480b87"></a>
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

<a id="57dfc48820a167ce"></a>
## CLOCK_TIME

<a id="0e6b97faf0c1ca02"></a>
### 구문

```
CLOCK_TIME()
```

<a id="c3c73d090c2dba75"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="80ec74ac91cb03bb"></a>
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

<a id="d7b378623c4bd14e"></a>
## CLOCK_TIMESTAMP

<a id="9093ed73f5020392"></a>
### 구문

```
CLOCK_TIMESTAMP()
```

<a id="c87f4cb85e12caa5"></a>
### 설명

함수가 호출될 때마다 TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="221f6e1a35680d11"></a>
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

<a id="aeb25577697c2128"></a>
## COALESCE

<a id="e53646266edca20b"></a>
### 구문

```
COALESCE( expr1, ..., exprN )
```

<a id="2d4139e1e7f256d8"></a>
### 설명

expr list들 중에 null이 아닌 첫 번째 expr을 반환한다.  
expr list들이 모두 null인 경우에는 null을 반환한다.  
expr은 두 개 이상이어야 한다.

expr list에 여러 type들이 오는 경우에는 [결과 타입 조합 규칙](11-sql-elements.md#933953bbf127dad3)에 따라 result type이 결정된다.

- COALESCE는 CASE를 사용해서 동일하게 표현할 수 있다.

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

<a id="b4f6a286e751f24a"></a>
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

<a id="a9fb83a876b717d9"></a>
## CONCAT

<a id="9620ca39f45a58a7"></a>
### 구문

```
CONCAT( str1, str2, ... )
```

<a id="8291d58640ee4b56"></a>
### 설명

\|| ( CONCATENATE )의 alias 이다.  
CONCAT 함수의 argument로써 2 ~ 254 개까지 설정할 수 있다.  
자세한 내용은 [|| (CONCATENATE)](#e72ca95b1d94da0e), [CONCATENATE](#b04073e8a9e83240)를 참조한다.

<a id="a80de0e376a66a50"></a>
### 사용 예

```
gSQL> SELECT CONCAT( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="b04073e8a9e83240"></a>
## CONCATENATE

<a id="5ab6a23023ea3c69"></a>
### 구문

```
CONCATENATE( str1, str2, ... )
```

<a id="40f0fa5d63aa1475"></a>
### 설명

\|| ( CONCATENATE ) 의 alias 이다.  
CONCATENATE 함수의 argument로 2 ~ 254 개까지 설정할 수 있다.  
자세한 내용은 [CONCAT](#a9fb83a876b717d9), [|| (CONCATENATE)](#e72ca95b1d94da0e)를 참조한다.

<a id="1b0dcc5653519a78"></a>
### 사용 예

```
gSQL> SELECT CONCATENATE( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="7ae5adee2b5ffeb4"></a>
## COS

<a id="c59a659d091afd1a"></a>
### 구문

```
COS(num)
```

<a id="6e223a9cbfc8bc23"></a>
### 설명

num의 COSINE 값을 반환한다.  
인자값 num이 NULL이면 결과값도 NULL이다.

<a id="a31d7605528a8411"></a>
### 사용 예

```
gSQL> SELECT COS( 0 ) FROM DUAL;
COS( 0 )
--------
       1
1 row selected.
```

<a id="52eb3609f8be03a0"></a>
## COT

<a id="0fc7bd54458f5994"></a>
### 구문

```
COT(num)
```

<a id="7093511ec00c4e53"></a>
### 설명

num의 COTANGENT 값을 반환한다.  
인자값 num이 NULL이면 결과값도 NULL이다.

<a id="a8979c0fb90e831a"></a>
### 사용 예

```
gSQL> SELECT COT( 1 ) FROM DUAL;
        COT( 1 )
----------------
.642092615934331
1 row selected.
```

<a id="39cbfb0dcaff5e1d"></a>
## COUNT

<a id="bdad5f0ad19db7a0"></a>
### 구문

```
COUNT( [ ALL | DISTINCT ] expr )
```

<a id="154734397bf7a3be"></a>
### 설명

Aggregation 함수로써 expr이 NULL 값이 아닌 row의 개수를 얻는다.

ALL을 명시한 경우, 모든 값들에 대한 aggregation을 수행한다.  
DISTINCT을 명시한 경우, 중복 제거한 값들에 대한 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

<a id="9459e3f79506dbc3"></a>
### 사용 예

```
gSQL> SELECT COUNT(c1) FROM t1;

COUNT(C1)
---------
        3

1 row selected.
```

<a id="a13672e170033862"></a>
## COUNT(*)

<a id="2a9d08969419e4de"></a>
### 구문

```
COUNT(*)
```

<a id="a4e3cf44ffca0d81"></a>
### 설명

Aggregation 함수로써 row의 개수를 얻는다.   
별도의 expression을 지정하지 않으므로 값의 NULL 여부와 무관하다.

<a id="45b2230a4504f948"></a>
### 사용 예

```
gSQL> SELECT COUNT(*) FROM t1;

COUNT(*)
--------
       4

1 row selected.
```

<a id="ddf459a10d33119b"></a>
## CURRENT_CATALOG

<a id="da062898e1669a17"></a>
### 구문

```
CURRENT_CATALOG [()]
```

<a id="d2acc01c8fe4bcb1"></a>
### 설명

catalog name (database 이름)을 얻는다.

<a id="ee55bb1ff5f894f0"></a>
### 사용 예

```
gSQL> SELECT CURRENT_CATALOG FROM dual;

CURRENT_CATALOG
---------------
TEST_DB        

1 row selected.
```

<a id="ded9d6f2e7bd80f0"></a>
## CURRENT_DATE

<a id="119e548042665141"></a>
### 구문

```
CURRENT_DATE [()]
STATEMENT_DATE()
```

<a id="7742e8dacf0f4ed1"></a>
### 설명

현재 날짜 (DATE type) 값을 얻는다.

CURRENT_DATE는 SQL 표준 함수이다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• CURRENT_DATE, STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="9ebf11fd2cc22ce5"></a>
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

<a id="8c9bf7e541e58fb7"></a>
## CURRENT_SCHEMA

<a id="13f4abe067e99956"></a>
### 구문

```
CURRENT_SCHEMA [()]
```

<a id="73ad4ea3d2dd1f81"></a>
### 설명

사용자의 현재 SCHEMA를 얻는다.

<a id="80a797100e8c4566"></a>
### 사용 예

```
gSQL> SELECT CURRENT_SCHEMA FROM dual;

CURRENT_SCHEMA
--------------
PUBLIC        

1 row selected.
```

<a id="6f0c3028f6461836"></a>
## CURRENT_TIME

<a id="1b016f3e913cefee"></a>
### 구문

```
CURRENT_TIME [()]
STATEMENT_TIME()
```

<a id="6e5721f83ff56892"></a>
### 설명

Session 시간을 기준으로 현재 TIME WITH TIME ZONE type 값을 얻는다.

CURRENT_TIME은 SQL 표준 함수이다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• CURRENT_TIME, STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="9432ec799cf46cb2"></a>
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

<a id="d8795b1505198a32"></a>
## CURRENT_TIMESTAMP

<a id="fe0bef7a439a0ad7"></a>
### 구문

```
CURRENT_TIMESTAMP [()]
STATEMENT_TIMESTAMP()
```

<a id="155a9c438bd80e0a"></a>
### 설명

Session 시간을 기준으로 TIMESTAMP WITH TIME ZONE type 값을 얻는다.

CURRENT_TIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• CURRENT_TIMESTAMP, STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="454966a9340f8805"></a>
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

<a id="c806d6efc62f415a"></a>
## CURRENT_USER

<a id="673baa803e4f36b6"></a>
### 구문

```
CURRENT_USER [()]
```

<a id="e609c44b589d20a3"></a>
### 설명

현재 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다.
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다.
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다.
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="5208ac7a6431517e"></a>
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

<a id="6b00b628498e23d6"></a>
## CURRVAL

<a id="8f7ea733d2d5577d"></a>
### 구문

```
seq_name.CURRVAL
CURRVAL(seq_name)
```

<a id="db44f453b720067e"></a>
### 설명

시퀀스 객체의 현재 값을 얻는다.

최소 한 번은 NEXTVAL(seq_name) 등으로 시퀀스 값을 설정해야 한다.

<a id="ad4a94888ae08e91"></a>
### 사용 예

```
gSQL> SELECT seq.CURRVAL FROM dual;

SEQ.CURRVAL
-----------
          1

1 row selected.
```

<a id="61f38c2b4d02b2ce"></a>
## DATEADD

<a id="3bb3d1d73acf9fdc"></a>
### 구문

```
DATEADD( datepart, number, date )
```

<a id="f445ff9f400492ea"></a>
### 설명

date의 지정된 datepart에 number를 더한 값을 반환한다.

number가 소수점인 경우 반올림되지 않는다.  
date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE 타입이 올 수 있다.  
number 또는 date가 NULL인 경우에는 결과값도 NULL이다.

인자로 받은 date의 타입과 동일한 결과 타입이 반환된다.

**datepart에 사용 가능한 형식문자열**

<a id="674c286d954729e0"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">설명</th></tr><tr><td>YEAR</td><td>년</td></tr><tr><td>QUARTER</td><td>분기</td></tr><tr><td>MONTH</td><td>월</td></tr><tr><td>DAYOFYEAR</td><td>일</td></tr><tr><td>DAY</td><td>요일</td></tr><tr><td>WEEK</td><td>주</td></tr><tr><td>WEEKDAY</td><td>평일</td></tr><tr><td>HOUR</td><td>시</td></tr><tr><td>MINUTE</td><td>분</td></tr><tr><td>SECOND</td><td>초</td></tr><tr><td>MILLISECOND</td><td>밀리세컨드</td></tr><tr><td>MICROSECOND</td><td>마이크로세컨드</td></tr></tbody></table>

<a id="c83fcaaba947d70e"></a>
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

<a id="819ababb5d9c70ac"></a>
## DATEDIFF

<a id="bdb7cf790b30a06c"></a>
### 구문

```
DATEDIFF( datepart, startdate, enddate )
```

<a id="bc43ed584a9e6309"></a>
### 설명

enddate에서 startdate를 뺀 값을 지정된 datepart로 반환한다.

startdate와 enddate에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME TYPE이 올 수 있다.  
startdate 또는 enddate가 NULL이면 결과값도 NULL이다.

결과 타입은 NUMBER이다.

**datepart에 사용 가능한 형식문자열**

<a id="112726f1ca46a02d"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">설명</th></tr><tr><td>YEAR</td><td>년</td></tr><tr><td>QUARTER</td><td>분기</td></tr><tr><td>MONTH</td><td>월</td></tr><tr><td>DAYOFYEAR</td><td>일</td></tr><tr><td>DAY</td><td>요일</td></tr><tr><td>HOUR</td><td>시</td></tr><tr><td>MINUTE</td><td>분</td></tr><tr><td>SECOND</td><td>초</td></tr><tr><td>MILLISECOND</td><td>밀리세컨트</td></tr><tr><td>MICROSECOND</td><td>마이크로세컨드</td></tr></tbody></table>

<a id="1dbfd9564a942c2c"></a>
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

<a id="95ae0ba30c34a837"></a>
## DATE_ADD

<a id="19241b65a708977b"></a>
### 구문

```
DATE_ADD( date, INTERVAL expr unit  )
```

<a id="a169f34a5482e3ef"></a>
### 설명

[ADDDATE](#441090925f082310) ( date, INTERVAL expr unit )와 동일한 함수이다.

<a id="3853d6a902b9feb9"></a>
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

<a id="ea420adbc4d8a5b9"></a>
## DATE_PART

<a id="b9d5e5d9262ce68d"></a>
### 구문

```
DATE_PART( field, datetime )
```

<a id="b00295612b8af9f5"></a>
### 설명

DATE_PART는 EXTRACT 함수와 결과값이 같은 함수로써 입력한 datetime 타입에서 지정된 field를 찾아 반환한다.

인자 field에는 문자 literal만 올 수 있으며, YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, TIMEZONE_HOUR, TIMEZONE_MINUTE를 문자 literal로 지정할 수 있다.  
인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.

field가 datetime의 범위에 있지 않는 경우 에러를 반환한다.  
또한, DATE 타입인 경우에는 field에 YEAR, MONTH, DAY 만 올 수 있고, 그 외에는 에러를 반환한다.  
datatime이 NULL이면 NULL을 반환한다.  

반환되는 타입은 NUMBER이다.

자세한 내용은 [EXTRACT](#9426b123a329beab)를 참조한다.

<a id="7e821576b9628dd3"></a>
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

<a id="05826b18bdaba90e"></a>
## DECODE

<a id="d336600bc71398a7"></a>
### 구문

```
DECODE( expr, comparison_expr1, result1
           [, comparison_expr2, result2
            , ...
            , comparison_exprN, resultN ]
           [, default ] )
```

<a id="64acd8121110e0f8"></a>
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

<a id="452aab30ec95e932"></a>
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

<a id="2b46e598f27f67a9"></a>
## DEGREES

<a id="6fe217ac9626c194"></a>
### 구문

```
DEGREES( radians )
```

<a id="2798459bf8602ffe"></a>
### 설명

라디안 단위로 표시된 각도 radians를 도 단위로 변환한 값을 반환한다.  
radians가 NULL이면 NULL이 반환된다.

<a id="407dbd8f541f46b3"></a>
### 사용 예

```
gSQL> SELECT DEGREES( PI() ) AS RESULT FROM DUAL;
RESULT
------
   180
1 row selected.
```

<a id="e25c62592a4caee6"></a>
## DIGEST

<a id="238ad2fb13b1a47e"></a>
### 구문

```
DIGEST( data, type )
```

<a id="e465cbea9daa024b"></a>
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

<a id="37567e42f1deed72"></a>
### 사용 예

```
gSQL> SELECT HEX( DIGEST( 'my password', 'SHA256' ) ) AS RESULT FROM DUAL;

RESULT                                                          
----------------------------------------------------------------
BB14292D91C6D0920A5536BB41F3A50F66351B7B9D94C804DFCE8A96CA1051F2

1 row selected.
```

<a id="351562a24ce94c08"></a>
## DUMP

<a id="a9c824dc202b791b"></a>
### 구문

```
DUMP( expr )
```

<a id="7fe5d22c793b1d29"></a>
### 설명

DUMP 함수는 expr의 내부 표현정보를 반환한다.  
내부 표현정보는 데이터 타입, 길이 (byte length), 데이터 정보로 보여준다.

expr에는 모든 타입이 가능하다.  
expr이 NULL이면 NULL을 반환한다.  

반환되는 타입은 CHARACTER VARYING이다.

<a id="1fd7e23ab7c054a0"></a>
### 사용 예

```
gSQL> SELECT DUMP( 'DUMP' ) AS RESULT FROM DUAL;
RESULT                           
---------------------------------
Type=CHAR Len=4 : Str=68,85,77,80
1 row selected.
```

<a id="bf969764a55a9f7c"></a>
## EXP

<a id="d2c0b0e8895cad8d"></a>
### 구문

```
EXP( num )
```

<a id="a5de5c697e8b6778"></a>
### 설명

EXP 함수는 e (자연로그 베이스)의 num의 제곱값을 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="552396da56c0c5ae"></a>
### 사용 예

```
gSQL> SELECT EXP( 1 ) AS RESULT FROM DUAL;
          RESULT
----------------
2.71828182845905
1 row selected.
```

<a id="9426b123a329beab"></a>
## EXTRACT

<a id="7b90f5639e786c81"></a>
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

<a id="a73fc488743efde4"></a>
### 설명

EXTRACT는 입력한 datetime 타입에서 지정된 field를 찾아 반환한다.

인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.

field가 datetime의 범위에 있지 않는 경우에는 에러를 반환한다.  
또, DATE 타입인 경우에는 field에 YEAR, MONTH, DAY만 올 수 있고, 그 외의 경우에는 에러를 반환한다.  
반환되는 타입은 NUMBER이다.

EXTRACT 함수의 결과는 [DATE_PART](#ea420adbc4d8a5b9)와 동일하다.

<a id="0a1c0fbb59e2e4e2"></a>
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

<a id="6ddcda3a0a6ec66b"></a>
## FACTORIAL

<a id="55134f3dabc0374d"></a>
### 구문

```
FACTORIAL( num )
```

<a id="984d55c05aa5361b"></a>
### 설명

FACTORIAL 함수는 1 ~ num 까지의 연속된 자연수를 차례로 곱한 값을 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="d0798d05f6ac3799"></a>
### 사용 예

```
gSQL> SELECT FACTORIAL( 5 ) AS RESULT FROM DUAL;
RESULT
------
   120
1 row selected.
```

<a id="84a75960cb409117"></a>
## FLOOR

<a id="40b59956ca63f6ca"></a>
### 구문

```
FLOOR( num )
```

<a id="7465e060b7c0e6a9"></a>
### 설명

FLOOR 함수는 num 보다 크지 않은 가장 큰 정수를 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="97e037dc52fa0ea3"></a>
### 사용 예

```
gSQL> SELECT FLOOR(42.8) AS RESULT1, FLOOR(-42.8) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     42     -43
1 row selected.
```

<a id="1e3bfc258744dd18"></a>
## FROM_BASE64

<a id="d08adacc6404862b"></a>
### 구문

```
FROM_BASE64( str )
```

<a id="73eab48cb08c0cb8"></a>
### 설명

FROM_BASE64는 base64 인코딩으로 변환된 문자를 입력 받아 디코딩된 binary string을 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 BINARY VARYING 또는 BINARY LONG VARYING과 같은 BINARY 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 base64 문자 범위에 속하지 않는 문자가 포함되면, 에러를 반환한다.  
디코딩 할 때 str의 newline, carriage return, tab, space는 무시된다.

자세한 내용은 [TO_BASE64](#03ddcec68a879061)를 참조한다.

<a id="a2072b4b32de427f"></a>
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

<a id="8dda308b18de124f"></a>
## GREATEST

<a id="9c8cae4348d70004"></a>
### 구문

```
GREATEST( expr1 [, expr2, ... exprn ] )
```

<a id="89ede3cf8e592ea2"></a>
### 설명

GREATEST 함수는 인자로 받은 expr들 중에 가장 큰 값을 반환한다.

인자로 받은 expr들 중 하나라도 NULL인 경우, 결과값은 NULL이다.

결과 타입은 expr1 (첫 번째 expr)의 데이터 타입이다.  
expr1 (첫 번째 expr)의 데이터 타입이 숫자형인 경우와 문자형인 경우는 각각 expr1, ..., exprN의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, ..., exprN에 모두 CHAR 타입이 기술된 경우, 모든 expr은 VARCHAR 타입으로 비교되고, 결과 타입은 VARCHAR 타입으로 결정된다.

<a id="c1e2396c1a3d1584"></a>
### 사용 예

```
gSQL> SELECT GREATEST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
   200
1 row selected.
```

<a id="29ae504b98ddc73d"></a>
## HEX

<a id="567dfd9c76d2f9ce"></a>
### 구문

```
HEX( str )
```

<a id="1d9083dffd7629af"></a>
### 설명

인자 str을 16진수 문자로 반환한다.  
인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입 또는 문자 타입으로 변환될 수 있는 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.  
결과 타입은 CHARACTER VARYING 또는 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.

HEX 함수의 인자로 숫자타입이 오는 경우에는 에러를 반환한다.  
10진수 숫자를 16진수로 변환하고자 하는 경우에는  'X' number format을 이용한 TO_CHAR() 함수를 사용할 수 있다.  
예: TO_CHAR( 255, 'XX' )

자세한 내용은 [UNHEX](#d46e348c108bc31a)를 참조한다.

<a id="7284faf9987afc5c"></a>
### 사용 예

```
gSQL> SELECT HEX( 'abc' ) FROM DUAL;
HEX( 'abc' )
------------
616263      
1 row selected.
```

<a id="d0066b9ecb068fd8"></a>
## INITCAP

<a id="38ff5d8096a5a5a0"></a>
### 구문

```
INITCAP( str )
```

<a id="b75163be9f6fc4e6"></a>
### 설명

INITCAP 함수는 주어진 문자열 str의 각 단어들의 첫 번째 문자를 대문자로 변환하고 첫 번째 문자 이후의 문자를 소문자로 변환하여 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.

문자열의 각 단어는 white space, 알파벳 또는 숫자가 아닌 문자로 구분한다.  
str이 NULL이면 결과값도 NULL이다.

인자로 받는 str의 타입과 동일한 타입이 반환된다.

<a id="6a1e5ef04c627df4"></a>
### 사용 예

```
gSQL> SELECT INITCAP( 'hi GLIESE' ) AS RESULT FROM DUAL;
RESULT   
---------
Hi Gliese
1 row selected.
```

<a id="688630b899f0ad69"></a>
## INSTR

<a id="06ff7f5184133b4a"></a>
### 구문

```
INSTR( str, substr [, position [, occurrence ] ] )
```

<a id="c25554c8aa903f7a"></a>
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

<a id="2ef9593019a00943"></a>
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

<a id="3b926ff5e22014e6"></a>
## LAST_DAY

<a id="064362083aefc49b"></a>
### 구문

```
LAST_DAY( date )
```

<a id="cd524d86caed8cd4"></a>
### 설명

LAST_DAY 함수는 date에 포함된 월의 마지막 날짜를 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
반환되는 타입은 인자 date의 타입에 상관없이 항상 DATE이다.  

date가 NULL이면 NULL을 반환한다.

<a id="75dac867cdcb0082"></a>
### 사용 예

```
gSQL> SELECT 
      LAST_DAY( TO_DATE( '2012-07-10', 'YYYY-MM-DD' ) ) AS RESULT FROM DUAL;
RESULT    
----------
2012-07-31
1 row selected.
```

<a id="a6e5d3dbfa265092"></a>
## LAST_IDENTITY_VALUE

<a id="bd37b2d12bc44291"></a>
### 구문

```
LAST_IDENTITY_VALUE()
```

<a id="9684bd66dfd9340b"></a>
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

INSERT 할 때 생성된 identity column의 값을 얻으려면 다음과 같이 [INSERT INTO name RETURNING .. INTO](18-sql-references.md#52c48e84ccf07d95) 구문을 사용한다.

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

<a id="9ba27d0d629674c2"></a>
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

<a id="e7e917c6a12122df"></a>
## LEAST

<a id="9dcf438ecf8360b7"></a>
### 구문

```
LEAST( expr1 [, expr2, ... exprn ] )
```

<a id="8aa685b9aca54fe4"></a>
### 설명

LEAST 함수는 인자로 받은 expr들 중에 가장 작은 값을 반환한다.

인자로 받은 expr들 중 하나라도 NULL인 경우, 결과값은 NULL이다.

결과 타입은 expr1 (첫 번째 expr)의 데이터 타입에 따라 결정된다.  
expr1 (첫 번째 expr)의 데이터 타입이 숫자형인 경우와 문자형인 경우에는 각각 expr1, ..., exprN의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, ..., exprN에 모두 CHAR 타입이 기술된 경우, 모든 expr은 VARCHAR 타입으로 비교되고, 결과 타입은 VARCHAR 타입이 된다.

<a id="e2453779007ea2d9"></a>
### 사용 예

```
gSQL> SELECT LEAST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="45df1dbd6c5b6d9a"></a>
## LENGTH

<a id="7112a66ffff965c3"></a>
### 구문

```
LENGTH( str )
```

<a id="c808b9831b880242"></a>
### 설명

[CHAR_LENGTH](#6fba33a6d3e98937)의 alias 이다.

<a id="a2d7796e33022055"></a>
### 사용 예

Multi byte character set: (예: UTF8)

```
gSQL> SELECT LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="3c531ddc38355109"></a>
## LENGTHB

<a id="a6cdf02a7ed738ea"></a>
### 구문

```
LENGTHB( str )
```

<a id="2704b3c342fcdbe3"></a>
### 설명

OCTET_LENGTH의 alias이다.  
자세한 내용은 [OCTET_LENGTH](#efc6be7a196cd804), [BYTE_LENGTH](#75d9967da5addf6b)를 참조한다.

<a id="b5319d7fa70f53d3"></a>
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

<a id="9d359a582dbdc25c"></a>
## LN

<a id="d9c8f8838cd469f2"></a>
### 구문

```
LN( num )
```

<a id="98ea0e469284171f"></a>
### 설명

LN 함수는 num의 자연 로그 값을 반환하는 함수이다.  

num은 0보다 큰 값이어야 한다.  
num이 NULL이면 NULL을 반환한다.

<a id="7f4b9d1bc26dc076"></a>
### 사용 예

```
gSQL> SELECT LN( 2.71828182845905 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="49068bf73aaf985b"></a>
## LNNVL

<a id="96f96afba7fd7916"></a>
### 구문

```
LNNVL( expr )
```

<a id="9b74926a8a1c2d6c"></a>
### 설명

Logical Not Null VaLue (LNNVL) 함수는 NOT logical operator와 유사하지만 다음 예제와 같이 입력값이 null일 경우 TRUE를 반환한다는 차이가 있다.

<a id="6899dfe6165482ef"></a>
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

<a id="436222f8341b1345"></a>
## LOCALTIME

<a id="b87c2ef5ae600906"></a>
### 구문

```
LOCALTIME [()]
STATEMENT_LOCALTIME()
```

<a id="a4b31442490e808d"></a>
### 설명

Session 시간을 기준으로 현재 TIME WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• LOCALTIME, STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="32e33cf120be175a"></a>
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

<a id="4996dddc37478f57"></a>
## LOCALTIMESTAMP

<a id="36205ad8e6a0e85f"></a>
### 구문

```
LOCALTIMESTAMP [()]
STATEMENT_LOCALTIMESTAMP()
```

<a id="96e3e66ae15022bd"></a>
### 설명

Session 시간을 기준으로 현재 TIMESTAMP WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• LOCALTIMESTAMP, STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="e94ac94e8ecdcab4"></a>
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

<a id="6b7181d4c5670aef"></a>
## LOCAL_GROUP_ID

<a id="64982f3067d6727d"></a>
### 구문

```
LOCAL_GROUP_ID()
```

<a id="ac15e6fb32cd08be"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster group ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="dd7c84e798140e5b"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_GROUP_ID() FROM DUAL;

LOCAL_GROUP_ID()
----------------
               1

1 row selected.
```

<a id="fc2e0cdaaf1f2f81"></a>
## LOCAL_GROUP_NAME

<a id="ba744432e4e45998"></a>
### 구문

```
LOCAL_GROUP_NAME()
```

<a id="ad1077aa98c4777f"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster group name을 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="78f767ace99f841e"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_GROUP_NAME() FROM DUAL;

LOCAL_GROUP_NAME()
------------------
G1                

1 row selected.
```

<a id="3f3c2af9ef249f74"></a>
## LOCAL_MEMBER_ID

<a id="2204e60109060369"></a>
### 구문

```
LOCAL_MEMBER_ID()
```

<a id="4377f16a1c8d3eb9"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster member ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="3ad06f43a342ffc2"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_MEMBER_ID() FROM DUAL;

LOCAL_MEMBER_ID()
-----------------
                1

1 row selected.
```

<a id="d9f73b56185d22dd"></a>
## LOCAL_MEMBER_NAME

<a id="00e6f1a9c5073f51"></a>
### 구문

```
LOCAL_MEMBER_NAME()
```

<a id="56d828da25942c4e"></a>
### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster member name을 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="2babe1f805be182e"></a>
### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_MEMBER_NAME() FROM DUAL;

LOCAL_MEMBER_NAME()
-------------------
G1N1               

1 row selected.
```

<a id="ea9a2c5eb2dd8b5e"></a>
## LOG

<a id="6fe735f0496b585b"></a>
### 구문

```
LOG( num2 )
LOG( num1, num2 )
```

<a id="04226ec92a1d2c17"></a>
### 설명

LOG 함수는 밑이 num1인 num2의 로그값을 반환한다.  
num1이 생략된 경우에는 밑이 10으로 계산된 값이 반환된다.

num1은 1과 0이 아닌 양수이어야 하고, num2는 양수이어야 한다.  

num1 또는 num2가 NULL이면 NULL을 반환한다.

<a id="9fe287ffa1746976"></a>
### 사용 예

```
gSQL> SELECT LOG( 100 ) AS RESULT1, LOG( 4, 16 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      2       2
1 row selected.
```

<a id="e49dffe98c9e9356"></a>
## LOGON_USER

<a id="cc5564db37d7e466"></a>
### 구문

```
LOGON_USER()
```

<a id="637dbeaf5e9ffaa2"></a>
### 설명

로그인 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다.
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다.
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다.
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="e86b7fe612d0b987"></a>
### 사용 예

```
% gsql test test

gSQL> SELECT LOGON_USER() AS result FROM DUAL;

RESULT
------
TEST  

1 row selected.
```

<a id="9a81a6ccdf6d2b82"></a>
## LOWER

<a id="d7924a3dd72510fe"></a>
### 구문

```
LOWER( str )
```

<a id="319e27166bdc0257"></a>
### 설명

LOWER 함수는 str의 소문자를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.  
str이 NULL이면 결과값도 NULL이다.

인자 str과 동일한 타입이 반환된다.

<a id="12fbf778d201e538"></a>
### 사용 예

```
gSQL> SELECT LOWER( 'SPRING' ) AS RESULT FROM DUAL;
RESULT
------
spring
1 row selected.
```

<a id="0cb417d8d3ab34a0"></a>
## LPAD

<a id="e1e0820f031ac5b3"></a>
### 구문

```
LPAD( str, length, [, fill] )
```

<a id="e3c90404276e91cc"></a>
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

<a id="c72cbbdfd0ec643d"></a>
| 인자 str의 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="c5b28236c8731639"></a>
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

<a id="2ceea524cfe974a6"></a>
## LTRIM

<a id="25d9b2563a6dfafe"></a>
### 구문

```
LTRIM( trim_source [, trim_character ] )
```

<a id="1bd302084a7d4e21"></a>
### 설명

LTRIM 함수는 trim_source에서 trim_character를 왼쪽 방향에서 비교하여 일치하는 문자가 없을 때까지 제거한 결과를 반환한다.

인자 trim_character와 trim_source에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

trim_character, trim_source 중 하나라도 NULL이면, 결과값은 NULL이다.  
trim_character가 생략된 경우에는 기본적으로 single blank space (' ')가 지정된다.

결과 타입은 다음과 같다.

**LTRIM의 결과 타입**

<a id="1e376bc17430482f"></a>
| trim_source, trim_character 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="5f43ac2929e39984"></a>
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

<a id="7949d0584926f17b"></a>
## MAX

<a id="5ae8f281734b0942"></a>
### 구문

```
MAX( [ ALL | DISTINCT ] expr )
```

<a id="d9cdbe35b53e23bb"></a>
### 설명

Aggregation 함수로써 row들의 expr 중 최대값을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복을 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

MAX는 ALL과 DISTINCT에 영향을 받지 않고 동일한 결과를 낸다.

<a id="eedbc8c5d114b3e1"></a>
### 사용 예

```
gSQL> SELECT MAX(c1) FROM t1;

MAX(C1)
-------
      3

1 row selected.
```

<a id="df013296d65d98cb"></a>
## MIN

<a id="83e2ecf7d8679a36"></a>
### 구문

```
MIN( [ ALL | DISTINCT ] expr )
```

<a id="eb9a1767c9cf95e9"></a>
### 설명

Aggregation 함수로써 row들의 expr 중 최소값을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

MIN은 ALL과 DISTINCT에 영향을 받지 않고 동일한 결과를 낸다.

<a id="813d61a5e8dff7ef"></a>
### 사용 예

```
gSQL> SELECT MIN(c1) FROM t1;

MIN(C1)
-------
      1

1 row selected.
```

<a id="e37be12b25d1865a"></a>
## MOD

<a id="3f03090e98d6a9fb"></a>
### 구문

```
MOD( num1, num2 )
```

<a id="10f0adbdfc8a89db"></a>
### 설명

MOD는 num1을 num2로 나눈 나머지를 반환한다.  

인자 num1, num2에는 숫자타입이 올 수 있다.  
num2가 0이면 에러를 반환한다.  
인자 num1 또는 num2가 NULL이면 NULL을 반환한다.

<a id="86abd7e2bb338cdc"></a>
### 사용 예

```
gSQL> SELECT MOD(5, 4) AS RESULT1, MOD(-5, 4) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1      -1
1 row selected.
```

<a id="5d80a6a3a0b2bb51"></a>
## MONTHS_BETWEEN

<a id="67e70d82afe985be"></a>
### 구문

```
MONTHS_BETWEEN( date1, date2 )
```

<a id="6d7506c11005ad24"></a>
### 설명

MONTHS_BETWEEN은 date2와 date1 사이의 일수를 31로 나눈 개월 수를 반환한다.

date1 또는 date2가 NULL이면 결과도 NULL이다.  
인자 date1, date2에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.

결과 타입은 NUMBER 이다.

> date1과 date2 모두에 동일한 날짜가 포함되어 있거나 (예: 2014-01-15 와 2014-02-15) 월의 마지막 날짜가 포함되어 있는 경우 (예: 2014-08-31와 2014-09-30), 타임스탬프 구간 (있는 경우)의 일치 여부와 상관없이 정수 결과를 반환한다.

<a id="dae0059ace456d04"></a>
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

<a id="06b43a3e4651eec0"></a>
## NEXT_DAY

<a id="ede13fe1b01e8584"></a>
### 구문

```
NEXT_DAY( date, day )
```

<a id="196c69b4df1283b7"></a>
### 설명

인자로 주어진 date (날짜)를 지나 처음으로 도래하는 day (요일)의 날짜를 구한다.

두 번째 인자 day에는 day를 지칭하는 스트링 또는 숫자가 올 수 있다.  
• 스트링:  SUNDAY ~ SATURDAY  또는 SUN ~ SAT  
• 숫자:  1 (sunday) ~ 7 (saturday)  

입력 인자 중 하나라도 NULL이면 결과값도 NULL이다.

반환되는 타입은 date의 입력 타입에 상관없이 항상 DATE 타입이다.  
결과값의 시분초는 입력 인자 date의 시분초를 동일하게 반환한다.

<a id="d5b62310bba403e9"></a>
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

<a id="c73afcf37cccda71"></a>
## NEXTVAL

<a id="c5d90f7fc1c42746"></a>
### 구문

```
seq_name.NEXTVAL
NEXTVAL( seq_name )
NEXT VALUE FOR seq_name
```

<a id="0edea959cd26e121"></a>
### 설명

시퀀스 객체의 다음 값을 얻는다.

<a id="8eea21b1ff5a3713"></a>
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

<a id="1a0eb6819456e426"></a>
## NULLIF

<a id="5e9663bcf9bc591a"></a>
### 구문

```
NULLIF( expr1, expr2 )
```

<a id="c01f156ffbbde2f6"></a>
### 설명

expr1과 expr2가 같으면 null을 반환하고, 같지 않으면 첫 번째 인자인 expr1을 반환한다.

expr1과 expr2의 타입이 서로 다를 경우, [결과 타입 조합 규칙](11-sql-elements.md#933953bbf127dad3)에 따라 result type이 결정된다.

NULLIF는 CASE를 사용해서 동일하게 표현할 수 있다.

- NULLIF( expr1, expr2 )

```
CASE WHEN expr1 = expr2 THEN NULL 
       ELSE expr1 
  END
```

<a id="a50b11199704b65d"></a>
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

<a id="d37de1ba15fe628b"></a>
## NUMTODSINTERVAL

<a id="39c29782e9e865e1"></a>
### 구문

```
NUMTODSINTERVAL( num, interval_indicator )
```

<a id="784bff3b8071a7d5"></a>
### 설명

interval_indicator 단위인 number를 interval day to second 타입으로 변환하여 반환한다.

인자 number는 숫자 타입이다.

인자 interval_indicator는 CHAR, VARCHAR와 같은 문자 타입이며, 대소문자 구분없이 'DAY', 'HOUR', 'MINUTE', 'SECOND' 중 하나여야 한다.

인자 중 하나라도 NULL이면 결과로 NULL이 반환된다.

interval day(6) to second(6) 타입의 결과를 반환하며 precision은 사용자가 임의로 변경할 수 없다. 변환된 결과의 leading precision이 기본 precision을 초과하면 에러가 반환되며, fraction precision이 기본 precision을 초과하면 반올림한 결과를 반환한다.

<a id="3db00bfe3f5ec3c0"></a>
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

<a id="403c620fa29a8d5a"></a>
## NUMTOYMINTERVAL

<a id="a8e886238d3709ee"></a>
### 구문

```
NUMTOYMINTERVAL( num, interval_indicator )
```

<a id="94794aa835d25959"></a>
### 설명

interval_indicator 단위인 number를 interval year to month 타입으로 변환하여 반환한다.

인자 number는 숫자 타입이다.

인자 interval_indicator는 CHAR, VARCHAR와 같은 문자 타입이며, 대소문자 구분없이 'YEAR', 'MONTH' 중 하나여야 한다.

인자 중 하나라도 NULL이면 결과로 NULL이 반환된다.

interval year(6) to month 타입을 결과로 반환하며 precision은 사용자가 임의로 변경할 수 없다. 변환된 결과의 leading precision이 기본 precision을 초과하면 에러가 반환된다.

<a id="925bff9dd71cdc3f"></a>
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

<a id="cd58b7ac439d7044"></a>
## NVL

<a id="099e3b01750b23c7"></a>
### 구문

```
NVL( expr1, expr2 )
```

<a id="6e1ffcc21172e413"></a>
### 설명

expr1이 null이 아니면 expr1을 반환하고, expr1이 null이면 expr2를 반환한다.

결과 타입은 expr1의 데이터 타입에 따라 결정된다.  
expr1에 NULL이 기술된 경우에는 expr2의 타입에 따라 결과 타입이 결정된다.  
expr1의 데이터 타입이 숫자형 타입인 경우와 문자형 타입인 경우는 각각 expr1, expr2의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, expr2의 데이터 타입이 모두 CHAR 타입인 경우, 결과 타입은 VARCHAR로 결정된다.

<a id="73577776707e1fbd"></a>
### 사용 예

```
gSQL> SELECT I1, NVL( I1, 0 ) FROM T1;
  I1 NVL( I1, 0 )
---- ------------
   1            1
null            0
2 rows selected.
```

<a id="4c314d8391c02bca"></a>
## NVL2

<a id="d07aaf3079cc0594"></a>
### 구문

```
NVL2( expr1, expr2, expr3 )
```

<a id="8180a73cce4651d3"></a>
### 설명

expr1이 null이 아니면 expr2를 반환하고, expr1이 null이면 expr3을 반환한다.

결과 타입은 expr2의 데이터 타입에 따라 결정된다.  
expr2에 NULL이 기술된 경우에는 expr3의 타입에 따라 결과 타입이 결정된다.  
expr2의 데이터 타입이 숫자형인 경우와 문자형인 경우에는 각각 expr2, expr3의 범위를 포함할 수 있는 타입으로 결정된다.  
expr2, expr3의 데이터 타입이 모두 CHAR 타입인 경우, 결과 타입은 VARCHAR가 된다.

<a id="0b8c7e5e8310995f"></a>
### 사용 예

```
gSQL> SELECT I1, NVL2( I1, I1 * 1000, 0 ) FROM T1;
  I1 NVL2( I1, I1 * 1000, 0 )
---- ------------------------
   1                     1000
null                        0
2 rows selected.
```

<a id="efc6be7a196cd804"></a>
## OCTET_LENGTH

<a id="7890cf55cd5f60c7"></a>
### 구문

```
OCTET_LENGTH( str )  

BYTE_LENGTH( str )     

LENGTHB( str )
```

<a id="af43ab8c27f44a14"></a>
### 설명

OCTET_LENGTH는 str의 바이트 수를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

str의 타입이 CHARACTER면 공백문자도 계산에 포함된다.  
str이 NULL이면 결과값도 NULL이다.

OCTET_LENGTH의 alias로는 [BYTE_LENGTH](#75d9967da5addf6b)와 [LENGTHB](#3c531ddc38355109) 함수가 있다.

<a id="d34eaa8c31c08326"></a>
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

<a id="300e6c6428fb2f72"></a>
## OVERLAY

<a id="dd8accb2a10ed6c3"></a>
### 구문

```
OVERLAY( str1 PLACING str2 FROM start_position  [ FOR string_length ] )
```

<a id="7de53b6fb1e9b984"></a>
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

자세한 내용은 [SUBSTRING](#8ee7fdd0b07ae871)을 참조한다.

결과 타입은 다음 표와 같다.

**OVERLAY의 결과 타입**

<a id="f2a1d472821b9c5f"></a>
| str1, str2 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="2d42a293ec8d29f7"></a>
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

<a id="107a84e0e38c9710"></a>
## PHYSICAL_LENGTH

<a id="98636411e35be967"></a>
### 구문

```
PHYSICAL_LENGTH( expr )
```

<a id="4bc8421c00b2fe02"></a>
### 설명

PHYSICAL_LENGTH 함수는 expr의 내부 표현 정보 byte 수를 반환한다.

인자 expr에는 모든 데이터 타입이 올 수 있다.

입력 인자가 NULL이면 결과는 0 이다.

<a id="f4f8cf7b28ee548e"></a>
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

<a id="f3d7a516fcd28b5c"></a>
## PI

<a id="397d47e0ec3193fb"></a>
### 구문

```
PI()
```

<a id="6fddb24e1d4bdc0f"></a>
### 설명

PI는 "π" constant를 반환한다.

<a id="c2f4937c984f19b4"></a>
### 사용 예

```
gSQL> SELECT PI() AS RESULT FROM DUAL;
              RESULT
--------------------
3.141592653589793E+0
1 row selected.
```

<a id="24f04da084362731"></a>
## POSITION

<a id="ab965ee3ba9eeb1f"></a>
### 구문

```
POSITION( str1 IN str2 )
```

<a id="b1a84bad7eaaf5d1"></a>
### 설명

POSITION 함수는 str2에서 첫 번째 str1을 찾아 그 위치를 반환하는 함수이다.

str1과 str2에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

str2에서 str1을 찾을 수 없는 경우, 리턴값 0이 반환된다.  
str2에서 str1을 찾은 경우, 1을 시작으로 그 찾은 위치를 반환한다.  
반환되는 위치값은 CHARACTER 단위로 계산된 값이다. (byte 단위가 아님)  
str1 또는 str2가 NULL이면, 반환되는 값도 NULL 이다.

<a id="dd738394cd1123b6"></a>
### 사용 예

```
gSQL> SELECT POSITION( 'CHAR' IN 'LONG CHAR 2000' ) AS RESULT FROM DUAL;
RESULT
------
     6
1 row selected.
```

<a id="d03682bac268946a"></a>
## POWER

<a id="1b84e4fde6fef846"></a>
### 구문

```
POWER( num1, num2 )
```

<a id="533b7b95c384536d"></a>
### 설명

POWER 함수는 num1에 num2를 제곱한 값을 반환한다.

인수 num1과 num2에는 숫자 타입이 올 수 있다.  

num1이 음수이면, num2는 정수여야 한다.  
num1 또는 num2의 값이 NULL이면, 결과값도 NULL이다.

<a id="d8d5fd147d069dc6"></a>
### 사용 예

```
gSQL> SELECT POWER( 2, 3 ) AS RESULT FROM DUAL;
RESULT
------
     8
1 row selected.
```

<a id="a1c5806a676b274b"></a>
## RADIANS

<a id="587a675d0d203ccb"></a>
### 구문

```
RADIANS( degrees )
```

<a id="8c88887ceed11def"></a>
### 설명

RADIANS 함수는 degrees의 라디안을 반환한다.  

인자 degrees에는 숫자 타입이 올 수 있다.  
인자 degrees가 NULL이면 NULL을 반환한다.

<a id="debc9e4e1cb4d9e4"></a>
### 사용 예

```
gSQL> SELECT RADIANS( 180 ) AS RESULT FROM DUAL;
          RESULT
----------------
3.14159265358979
1 row selected.
```

<a id="d8c373526e895389"></a>
## RANDOM

<a id="e96b499947391293"></a>
### 구문

```
RANDOM( min, max )
```

<a id="597dcc6b5973e047"></a>
### 설명

RANDOM은 min 이상 max 이하의 random 값을 반환한다.  

인자 min, max에는 숫자 타입이 올 수 있다.  
인자 min 또는 max가 NULL이면 NULL을 반환한다.

<a id="51e0170e908b7a3a"></a>
### 사용 예

```
gSQL> SELECT RANDOM( 1, 100 ) AS RESULT FROM DUAL;
          RESULT
----------------
34.1870528003201
1 row selected.
```

<a id="e735b34d6307a737"></a>
## REPEAT

<a id="7ec7f55dce0b5383"></a>
### 구문

```
REPEAT( str, num )
```

<a id="61d3d53acfe7d46b"></a>
### 설명

REPEAT 함수는 num에 지정된 수만큼 str을 반복한 string을 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARCATER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

인자 num에는 숫자 타입이 올 수 있다.

str 또는 num 중의 하나라도 NULL이면, 결과값도 NULL이다.  
num의 값이 0 또는 음수인 경우에도 결과값은 NULL이다.

결과 타입은 다음 표와 같다.

**REPEAT의 결과 타입**

<a id="349da7715c0a2b41"></a>
| str 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="db67efa732f52552"></a>
### 사용 예

```
gSQL> SELECT REPEAT( 'ab', 3 ) AS RESULT FROM DUAL;
RESULT
------
ababab
1 row selected.
```

<a id="4b27ef660974af19"></a>
## REPLACE

<a id="bc226077b4b37487"></a>
### 구문

```
REPLACE( str, from, to )
```

<a id="7eb7de48b11f7130"></a>
### 설명

REPLACE는 str string 내의 모든 from string을 to string으로 치환하여 반환한다.

인자 str, from, to에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str 값이 NULL인 경우, 결과값은 NULL이다.  
from 값이 NULL인 경우, str 값을 변환하지 않고 반환한다.  
to 값이 생략되었거나 NULL인 경우, str에서 from을 제거한 값이 반환된다.

결과 타입은 다음 표와 같다.

**REPLACE의 결과 타입**

<a id="27b6e34b360f2068"></a>
| str 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="0d7e22cf943dced6"></a>
### 사용 예

```
gSQL> SELECT REPLACE( 'HI GLIESE', 'HI', 'HELLO' ) AS RESULT FROM DUAL;
RESULT      
------------
HELLO GLIESE
1 row selected.
```

<a id="2ed783c153c3ed1a"></a>
## REVERSE

<a id="4b3be3a8d13891cc"></a>
### 구문

```
REVERSE( str )
```

<a id="e26b3b23ccaa570d"></a>
### 설명

REVERSE는 str의 문자를 역순으로 반환한다.

인자로는 character string 타입 또는 binary string 타입으로 변환될 수 있는 타입이 올 수 있으며  
character string 타입은 해당 문자 단위로, binary string 타입은 byte 단위로 수행된다.

str이 NULL일 경우 NULL을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**REVERSE 인자와 결과 타입**

<a id="11e746b9206b0dd7"></a>
| str | 결과 타입 |
| --- | --- |
| CHAR | CHAR |
| VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY | BINARY |
| VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="a9ddcac5cd9211f2"></a>
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

<a id="c7c9ba9e02aa45e9"></a>
## ROUND( number )

<a id="7801ef8270e6aa02"></a>
### 구문

```
ROUND( num [, scale ] )
```

<a id="87a04e1f9acea3bf"></a>
### 설명

ROUND는 scale을 기준으로 num을 반올림한 값을 반환한다.

인자 num, scale에는 숫자 타입이 올 수 있다.

scale이 생략된 경우, scale은 0이 되어 ROUND( num, 0 )와 같이 수행된다.  
scale이 양수인 경우 소수점 오른쪽 자리수를 기준으로 반올림되고, scale이 음수인 경우 소수점 왼쪽 자리수를 기준으로 반올림된다.  

인자 num 또는 scale이 NULL이면 NULL을 반환한다.

<a id="64fe8c6b112f9caa"></a>
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

<a id="eb944ab89f98b707"></a>
## ROUND( date )

<a id="62d05787c2cdef6c"></a>
### 구문

```
ROUND( date [ , fmt ] )
```

<a id="a71b6d2a88c20c8e"></a>
### 설명

ROUND( date ) 함수는 date를 지정된 fmt 단위로 반올림한 값을 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
인자 date 또는 fmt가 NULL이면 NULL을 반환한다.  

결과 타입은 인자로 받은 date 타입과 관계없이 항상 DATE 타입이다.

fmt가 생략되었을 경우의 기본값은 DAY 이며, 사용 가능한 형식문자열은 다음 표와 같다.

**fmt에 사용가능한 형식문자열**

<a id="055a063e56e3c86f"></a>
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

<a id="6f214976c8d54b5c"></a>
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

<a id="5094b18e0b5310db"></a>
## ROWID_GRID_BLOCK_ID

<a id="af6b4b8b36d08c66"></a>
### 구문

```
ROWID_GRID_BLOCK_ID( rowid )
```

<a id="183c86e69ccbb83e"></a>
### 설명

GRID block ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="54ce0fa61d248156"></a>
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

<a id="88b241dbab2cf2c4"></a>
## ROWID_GRID_BLOCK_SEQ

<a id="e61c5991c560fd8a"></a>
### 구문

```
ROWID_GRID_BLOCK_SEQ( rowid )
```

<a id="72e5bc2a68ef8060"></a>
### 설명

GRID block sequence를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="aed73a9b40db75ab"></a>
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

<a id="491cf1642b2825bb"></a>
## ROWID_MEMBER_ID

<a id="3191fa494b35edf3"></a>
### 구문

```
ROWID_MEMBER_ID( rowid )
```

<a id="d0046b780b806e44"></a>
### 설명

Member ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="73fc7eb8eaede82e"></a>
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

<a id="58e3a5bd0def5c9a"></a>
## ROWID_OBJECT_ID

<a id="cd7a421eccebaf93"></a>
### 구문

```
ROWID_OBJECT_ID( rowid )
```

<a id="cb60f7aec76953e5"></a>
### 설명

Object ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="ab0be4c253c4a84b"></a>
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

<a id="2f604dcd124fb135"></a>
## ROWID_PAGE_ID

<a id="1055a476d83ea973"></a>
### 구문

```
ROWID_PAGE_ID( rowid )
```

<a id="e26908600000c071"></a>
### 설명

Page ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="b8815744f2cb6f0a"></a>
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

<a id="7a77be578809282d"></a>
## ROWID_ROW_NUMBER

<a id="8ba8f70f102f1990"></a>
### 구문

```
ROWID_ROW_NUMBER( rowid )
```

<a id="6ae62f30cf74240c"></a>
### 설명

Row number를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="7d2fca7be837b11e"></a>
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

<a id="5449cb99e218c681"></a>
## ROWID_SHARD_ID

<a id="f52647986dab0732"></a>
### 구문

```
ROWID_SHARD_ID( rowid )
```

<a id="42cffb7b40d9912a"></a>
### 설명

Shard ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="cf5c19bb341bf406"></a>
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

<a id="07d4c357b5fc362a"></a>
## ROWID_TABLESPACE_ID

<a id="0a322465f02eb2a6"></a>
### 구문

```
ROWID_TABLESPACE_ID( rowid )
```

<a id="9267bbf636e59c7e"></a>
### 설명

Tablespace ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="020d43ac87ae6c33"></a>
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

<a id="de83f2cf7fcb4fc7"></a>
## ROWNUM

<a id="603445f1a74c5789"></a>
### 구문

```
ROWNUM
```

<a id="e6f041d1413837b3"></a>
### 설명

WHERE 조건을 만족하는 row에 대하여 1부터 순차적으로 번호를 부여한다.

Oracle과의 호환성을 위해 WHERE 절에 ROWNUM 사용을 허용한다.

그러나 질의 결과의 개수를 제한하려면 다음과 같이 SQL 표준의 [offset limit clause](18-sql-references.md#2e8423d8813ebc76)를 사용할 것을 권장한다.

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

<a id="d59ea22a79a9ca93"></a>
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

<a id="473a6134cf8242c2"></a>
## RPAD

<a id="cc4793ac2dfe5128"></a>
### 구문

```
RPAD( str, length, [, fill] )
```

<a id="9549abd402a868b7"></a>
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

<a id="d2a91f9445f00c78"></a>
| 인자 str의 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="4df71d9d498647a2"></a>
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

<a id="e0b41913fdb9726a"></a>
## RTRIM

<a id="bd768194e185f131"></a>
### 구문

```
RTRIM( trim_source [, trim_character ] )
```

<a id="2393bbc8bcf1b168"></a>
### 설명

RTRIM 함수는 trim_source에서 trim_character를 오른쪽 방향에서 비교하여 일치하는 문자가 없을 때까지 제거한 결과를 반환한다.

인자 trim_character와 trim_source에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

trim_character, trim_source 중 하나라도 NULL이면, 결과값은 NULL이다.  
trim_character가 생략된 경우에는 기본적으로 single blank space (' ')가 지정된다.

결과 타입은 다음과 같다.

**RTRIM의 결과 타입**

<a id="15cf215ba20fd080"></a>
| trim_source, trim_character 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="3f8ffde56471edd6"></a>
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

<a id="1b7c0b750961d7f7"></a>
## SESSION_ID

<a id="10e17a725685a828"></a>
### 구문

```
SESSION_ID()
```

<a id="e1807b91c61a1c61"></a>
### 설명

현재 session의 ID를 얻는다.

<a id="38aa89080aa13481"></a>
### 사용 예

```
gSQL> SELECT SESSION_ID() FROM dual;

SESSION_ID()
------------
           4

1 row selected.
```

<a id="6940db2b4a41c5f0"></a>
## SESSION_SERIAL

<a id="7f4b21d5221b6d38"></a>
### 구문

```
SESSION_SERIAL()
```

<a id="8ebcdfb7bd9d27fa"></a>
### 설명

현재 session의 serial 번호를 얻는다.

<a id="7d4d2dbc826b0cf8"></a>
### 사용 예

```
gSQL> SELECT SESSION_SERIAL() FROM dual;

SESSION_SERIAL()
----------------
              16

1 row selected.
```

<a id="85daf59be974e642"></a>
## SESSION_USER

<a id="cf87298da70e2b71"></a>
### 구문

```
SESSION_USER[()]
```

<a id="0d4dca5830edca30"></a>
### 설명

세션 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다. 
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다. 
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다. 
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="f5b90748fafdb4cf"></a>
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

<a id="1a5c7cf05f8eee64"></a>
## SHARD_GROUP_ID

<a id="2fb86925e07a5243"></a>
### 구문

```
SHARD_GROUP_ID( table_name, shard_key_value [, ... ] )
```

<a id="bfa32390ad6cea4d"></a>
### 설명

SHARD_GROUP_ID 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard를 관리하는 group ID를 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 NATIVE_BIGINT이다.

> Cluster system에서 유효한 정보이다.

<a id="d2742dd6509bffbd"></a>
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

<a id="e3a04d756e8ee40d"></a>
## SHARD_GROUP_NAME

<a id="c183e2d4ea5b306c"></a>
### 구문

```
SHARD_GROUP_NAME( table_name, shard_key_value [, ... ] )
```

<a id="fb3e9fa4e648f054"></a>
### 설명

SHARD_GROUP_NAME 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard를 관리하는 group NAME을 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 VARCHAR이다.

> Cluster system에서 유효한 정보이다.

<a id="1a247e0c965f29be"></a>
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

<a id="f5eca2e78ed397dc"></a>
## SHARD_ID

<a id="e4e07aafc2e40390"></a>
### 구문

```
SHARD_ID( table_name, shard_key_value [, ... ] )
```

<a id="c306a29d76b93325"></a>
### 설명

SHARD_ID 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard에 대한 ID를 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 NATIVE_BIGINT이다.

> Cluster system에서 유효한 정보이다.

<a id="7f8e015799126e7c"></a>
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

<a id="22d19011c90deda0"></a>
## SHARD_NAME

<a id="781335c039c02ee5"></a>
### 구문

```
SHARD_NAME( table_name, shard_key_value [, ... ] )
```

<a id="bbec54b453bafae1"></a>
### 설명

SHARD_NAME 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard에 대한 NAME을 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 VARCHAR이다.

> Cluster system에서 유효한 정보이다.

<a id="723f0c26f6bbbd5f"></a>
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

<a id="02f9dd54b8fa5fc1"></a>
## SHIFT_LEFT

<a id="c68011001ae0ce47"></a>
### 구문

```
SHIFT_LEFT( num, cnt )
```

<a id="15025a74e0627526"></a>
### 설명

SHIFT_LEFT 함수는 num을 cnt 비트만큼 왼쪽으로 이동시킨 값을 반환한다.

입력 인자 num, cnt에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환하면 소수점은 TRUNCATE 된다.

연산 시 cnt는 6 bit로 마스킹하여 6 bit 범위 내의 값으로 처리한다.

num 또는 cnt가 NULL이면 NULL을 반환한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="f9f65221ed753079"></a>
### 사용 예

```
gSQL> SELECT SHIFT_LEFT(1, 3) FROM DUAL;
SHIFT_LEFT(1, 3)
----------------
               8
1 row selected.
```

<a id="b3968c38e9e8929d"></a>
## SHIFT_RIGHT

<a id="b2e3cb78b19cbaaa"></a>
### 구문

```
SHIFT_RIGHT( num, cnt )
```

<a id="fc69e8c748d85f1d"></a>
### 설명

SHIFT_RIGHT 함수는 num을 cnt 비트만큼 오른쪽으로 이동시킨 값을 반환한다.

입력 인자 num, cnt에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환하면 소수점은 TRUNCATE 된다.

연산 시 cnt는 6 bit로 마스킹하여 6 bit 범위내의 값으로 처리한다.

num 또는 cnt가 NULL이면 NULL을 반환한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="88c6c901e09b62c4"></a>
### 사용 예

```
gSQL> SELECT SHIFT_RIGHT(8, 3) FROM DUAL;
SHIFT_RIGHT(8, 3)
-----------------
                1
1 row selected.
```

<a id="842ccb40a1076da9"></a>
## SIGN

<a id="053eef5641c376f6"></a>
### 구문

```
SIGN( num )
```

<a id="33e70746a8a67fac"></a>
### 설명

SIGN 함수는 num의 부호를 반환한다.

인자 num에는 숫자타입이 올 수 있다.

반환값은 다음과 같다.  

• num < 0 이면 -1  
• num = 0 이면 0  
• num > 0 이면 1  

num이 NULL이면 NULL을 반환한다.

<a id="fef4d89a05814bc0"></a>
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

<a id="dc26a246aa47fdb5"></a>
## SIN

<a id="425c39fc21a20fdc"></a>
### 구문

```
SIN( num )
```

<a id="aadb1cda1e211d02"></a>
### 설명

SIN 함수는 num의 sine 값을 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="514ac0e3b394cd2c"></a>
### 사용 예

```
gSQL> SELECT SIN( 0 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="99a53f6e194ede23"></a>
## SPLIT_PART

<a id="e1bb6c1413d26253"></a>
### 구문

```
SPLIT_PART( string, delimiter, field )
```

<a id="e06aeea03bd12fea"></a>
### 설명

SPLIT_PART 함수는 string 내에서 delimiter로 지정된 문자를 구분자로 하여 field의 문자열을 반환한다.

인자 string, delimiter에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

인자 field에는 숫자 타입이 올 수 있다.

string, delimiter, field 중에 하나라도 NULL인 경우에는 결과값도 NULL이다.  
field에는 1 이상의 숫자값만 올 수 있고, 0 또는 음수일 경우에는 에러를 반환한다.

결과 타입은 다음 표와 같다.

**SPLIT_PART의 결과 타입**

<a id="5c03a6318b741372"></a>
| string 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="1d0fbca1c9e01208"></a>
### 사용 예

```
gSQL> SELECT SPLIT_PART( 'AB;CD;EF;GH', ';', 3  ) AS RESULT FROM DUAL;
RESULT
------
EF    
1 row selected.
```

<a id="f43bf802d8823c6d"></a>
## SQRT

<a id="e33c09f9791ad466"></a>
### 구문

```
SQRT( num )
```

<a id="862f1aacb3819f59"></a>
### 설명

SQRT 함수는 num의 제곱근을 반환한다.  

인자 num에는 숫자 타입이 올 수 있고, 음수가 아닌 0 이상의 값이어야 한다.  
인자 num이 NULL이면 NULL을 반환한다.

<a id="cf5eb88ac863a8c4"></a>
### 사용 예

```
gSQL> SELECT SQRT( 9 ) AS RESULT FROM DUAL;
RESULT
------
     3
1 row selected.
```

<a id="e0db7e4b814701b9"></a>
## STATEMENT_DATE

<a id="17c494cf4d6ce1cf"></a>
### 구문

```
STATEMENT_DATE()
CURRENT_DATE [()]
```

<a id="22c2695a055c4023"></a>
### 설명

현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="cb35f440294d001f"></a>
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

<a id="1b646c7eaaf08d0a"></a>
## STATEMENT_LOCALTIME

<a id="b238896df6d158f6"></a>
### 구문

```
STATEMENT_LOCALTIME()
LOCALTIME [()]
```

<a id="f08ccecce8c211d5"></a>
### 설명

Session 시간을 기준으로 현재 TIME WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="23e27d868db6c07f"></a>
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

<a id="c8242dda8b1d9add"></a>
## STATEMENT_LOCALTIMESTAMP

<a id="639bef34a85060ac"></a>
### 구문

```
STATEMENT_LOCALTIMESTAMP()
LOCALTIMESTAMP [()]
```

<a id="65d5670a302fe75d"></a>
### 설명

Session 시간을 기준으로 현재 TIMESTAMP WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="22cfde2638b892ef"></a>
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

<a id="c1369b47f50bd366"></a>
## STATEMENT_TIME

<a id="f8c966fd76f037d3"></a>
### 구문

```
STATEMENT_TIME()
CURRENT_TIME [()]
```

<a id="77c86de767366555"></a>
### 설명

TIME ZONE이 있는 현재 TIME (TIME WITH TIME ZONE type) 값을 얻는다.

CURRENT_TIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="900f94a13b2b1e1d"></a>
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

<a id="4bbe90a1d33f4975"></a>
## STATEMENT_TIMESTAMP

<a id="1950ccbfd50d31dd"></a>
### 구문

```
STATEMENT_TIMESTAMP()
CURRENT_TIMESTAMP [()]
```

<a id="ba0ffae20f950469"></a>
### 설명

TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

CURRENT_TIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="43983230925c7a8a"></a>
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

<a id="1e1bf5e3049aa0eb"></a>
## STATEMENT_VIEW_SCN

<a id="322ec9c05e18714e"></a>
### 구문

```
STATEMENT_VIEW_SCN()
```

<a id="5ba0fbea4c3545c3"></a>
### 설명

현재 STATEMENT의 VIEW SCN을 얻는다.

<a id="8997ca68c0a8d327"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN() FROM dual;

STATEMENT_VIEW_SCN()
--------------------
17697.658.17880     

1 row selected.
```

<a id="309f254c39886336"></a>
## STATEMENT_VIEW_SCN_DCN

<a id="e23177ed613f629d"></a>
### 구문

```
STATEMENT_VIEW_SCN_DCN()
```

<a id="f61e1b94cd029e9e"></a>
### 설명

현재 STATEMENT의 VIEW SCN의 Domain Change Number (DCN) 값을 얻는다.

<a id="0eba9bd111a9134e"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_DCN() FROM dual;

STATEMENT_VIEW_SCN_DCN()
------------------------
                     658

1 row selected.
```

<a id="e084cde7e53ad2ad"></a>
## STATEMENT_VIEW_SCN_GCN

<a id="f06bebee0f863c2a"></a>
### 구문

```
STATEMENT_VIEW_SCN_GCN()
```

<a id="9b799675d19a45a3"></a>
### 설명

현재 STATEMENT의 VIEW SCN의 Global Change Number (GCN) 값을 얻는다.

<a id="3e37d1ba4c6a52c7"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_GCN() FROM dual;

STATEMENT_VIEW_SCN_GCN()
------------------------
                   17697

1 row selected.
```

<a id="f7da402584359e48"></a>
## STATEMENT_VIEW_SCN_LCN

<a id="9b93fb5c51f9e879"></a>
### 구문

```
STATEMENT_VIEW_SCN_LCN()
```

<a id="ad53867d3795f4e3"></a>
### 설명

현재 STATEMENT의 VIEW SCN의 Local Change Number (LCN) 값을 얻는다.

<a id="eba17ae35319988c"></a>
### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_LCN() FROM dual;

STATEMENT_VIEW_SCN_LCN()
------------------------
                   17880

1 row selected.
```

<a id="710271af985cd947"></a>
## STDDEV

<a id="6ce2caf757fd0e12"></a>
### 구문

```
STDDEV( [ ALL | DISTINCT ] expr )
```

<a id="3c0a722d6a71b09d"></a>
### 설명

Aggregation 함수로써 expr set의 표준편차 (standard deviation)를 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 수행하고, DISTINCT를 명시한 경우 중복을 제거한 값들에 대해 수행한다. 둘 다 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

NULL 값을 제외하고 DISTINCT로 중복을 제거한 후의 expr set의 개수가 한 개일 경우, [VARIANCE](#fe7ab65e1a6c5b53)와 같이 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV 인자와 결과 타입**

<a id="aed1060055a52c90"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

GOLDILOCKS는 다음과 같이 표준편차를 계산한다.  
　• expr set의 개수가 1이면 0을 반환한다.  
　• expr set의 개수가 1보다 크면 [STDDEV_SAMP( expr )](#5048db9c0886f2f3) 값을 반환한다.

> 표준편차는, 분산의 양의 제곱근으로써 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV 함수는 [VARIANCE](#fe7ab65e1a6c5b53) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV( [ ALL ] expr )  
>  = SQRT( VARIANCE( [ ALL ] expr ) )  
>   
> STDDEV( DISTINCT expr )  
>  = SQRT( VARIANCE( DISTINCT expr ) )

<a id="ecf2f8f5cb466152"></a>
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

<a id="9cf33dd4c3767fa7"></a>
## STDDEV_POP

<a id="af618889e054f380"></a>
### 구문

```
STDDEV_POP( expr )
```

<a id="442ddafcf20e2373"></a>
### 설명

Aggregation 함수로써 expr set의 모 표준편차 (population standard deviation)를 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV_POP의 인자와 결과 타입**

<a id="2bba9218001f5ed6"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 표준편차는 모 분산의 양의 제곱근으로써 모 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV_POP 함수는 [VAR_POP](#b236ef352055656d) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV_POP( expr )  
>  = SQRT( VAR_POP( expr ) )

<a id="f86e078d2ca83bde"></a>
### 사용 예

```
gSQL> SELECT STDDEV_POP(c1) FROM t1;

 STDDEV_POP(C1)
---------------
10.283968105746

1 row selected.
```

<a id="5048db9c0886f2f3"></a>
## STDDEV_SAMP

<a id="9332c2194db456fa"></a>
### 구문

```
STDDEV_SAMP( expr )
```

<a id="dca59ec1b2cbc402"></a>
### 설명

Aggregation 함수로써 expr set의 표본 표준편차 (sample standard deviation)를 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 NULL값을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV_SAMP의 인자와 결과 타입**

<a id="56ed1a9d55237fca"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 표본 표준편차는 표본 분산의 양의 제곱근으로써 표본 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV_SAMP 함수는 [VAR_SAMP](#ceed8a819f8dd64d) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV_SAMP( expr )  
>  = SQRT( VAR_SAMP( expr ) )

<a id="bbd38d06655c6efc"></a>
### 사용 예

```
gSQL> SELECT STDDEV_SAMP(c1) FROM t1;

 STDDEV_SAMP(C1)
----------------
11.4978258814438

1 row selected.
```

<a id="088cbfd5cb643df6"></a>
## SUBSTR

<a id="3a22bd390e9bce18"></a>
### 구문

```
SUBSTR( str FROM start_position [ FOR string_length ] )
SUBSTR( str, start_position [ , string_length ] )
```

<a id="bf42e61a1031871b"></a>
### 설명

[SUBSTRING](#8ee7fdd0b07ae871)의 alias이다.

<a id="7dda0a26e9304897"></a>
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

<a id="a8a6ec8a9639b059"></a>
## SUBSTRB

<a id="479b0b02b79a72dc"></a>
### 구문

```
SUBSTRB( str, start_position [ , string_length ] )
```

<a id="8603ab81ab298069"></a>
### 설명

SUBSTRB 함수는 str에 대해 start_position으로부터 string_length 범위의 문자를 추출하여 반환한다.

SUBSTRB 함수는 start_position과 string_length가 byte 단위로 계산된다는 점 외에는 [SUBSTRING](#8ee7fdd0b07ae871) 함수와 동일하다.

<a id="c4324e237bf5c932"></a>
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

<a id="8ee7fdd0b07ae871"></a>
## SUBSTRING

<a id="d27701990817ddc9"></a>
### 구문

```
SUBSTRING( str FROM start_position [ FOR string_length ] )  
SUBSTRING( str, start_position [ , string_length ] )
```

<a id="324f259c9f479704"></a>
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
자세한 내용은 [SUBSTR](#088cbfd5cb643df6)과 [SUBSTRB](#a8a6ec8a9639b059)를 참조한다.

결과 타입은 다음 표와 같다.

**SUBSTRING의 결과 타입**

<a id="ba72138d6a967e08"></a>
| str | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="8c60f6f55c9dcf19"></a>
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

<a id="f9aa343d3860da32"></a>
## SUM

<a id="8bf3c0f9ad1b3773"></a>
### 구문

```
SUM( [ ALL | DISTINCT ] expr )
```

<a id="390de1aa4c27ff88"></a>
### 설명

Aggregation 함수로써 expr 값들의 합을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복을 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

<a id="3c2525e93d8c080a"></a>
### 사용 예

```
gSQL> SELECT SUM(c1) FROM t1;

SUM(C1)
-------
      6

1 row selected.
```

<a id="7cd347863588d3fb"></a>
## SYSDATE

<a id="a25fd8e7002a327a"></a>
### 구문

```
SYSDATE
```

<a id="b999a820653acce8"></a>
### 설명

Database server가 위치하는 OS 시간을 기준으로 현재의 DATE type 값을 얻는다.

<a id="61a6eb1f8b39358a"></a>
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

<a id="8b6e93955536f79c"></a>
## SYS_EXTRACT_UTC

<a id="46b87c0887fc0874"></a>
### 구문

```
SYS_EXTRACT_UTC( datetime_with_timezone )
```

<a id="8f8ce0b119218d41"></a>
### 설명

SYS_EXTRACT_UTC 는  UTC (Coordinated Universal Time—formerly Greenwich Mean Time) 값을 반환한다.  
timezone이 명시되지 않은 경우, session time zone으로 계산된다.

입력 인자에는 time, time with time zone, timestamp, timestamp with time zone 타입이 올 수 있다.  
결과 타입은 time 또는 timestamp 타입이다.

<a id="0ca778bd41d29345"></a>
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

<a id="a5d70afe0da7d254"></a>
## SYSTIME

<a id="dc8be4cd53043290"></a>
### 구문

```
SYSTIME
```

<a id="402e1e8df00c4523"></a>
### 설명

Database server가 위치하는 OS 시간을 기준으로 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

<a id="01037645e6e00d45"></a>
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

<a id="3aab6136b131a50a"></a>
## SYSTIMESTAMP

<a id="f329a06d1773666f"></a>
### 구문

```
SYSTIMESTAMP
```

<a id="f4626955ab96577d"></a>
### 설명

Database server가 위치하는 OS 시간을 기준으로 TIME ZONE이 있는 현재 TIMESTAMP WITH TIME ZONE type 값을 얻는다.

<a id="6053e8c5ed0b9773"></a>
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

<a id="40f8d8af2e77cecd"></a>
## TAN

<a id="1aea8936f92b22b2"></a>
### 구문

```
TAN( num )
```

<a id="9a39648f6afc973a"></a>
### 설명

TAN 함수는 num의 tangent 값을 라디안 단위로 반환한다.  
num이 NULL이면 NULL을 반환한다.

<a id="4da9d73b16130ac6"></a>
### 사용 예

```
gSQL> SELECT TAN( 1 ) AS RESULT FROM DUAL;
         RESULT
---------------
1.5574077246549
1 row selected.
```

<a id="03ddcec68a879061"></a>
## TO_BASE64

<a id="c9806683e5859e4e"></a>
### 구문

```
TO_BASE64( str )
```

<a id="5a2479a967255eb1"></a>
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

자세한 내용은 [FROM_BASE64](#1e3bfc258744dd18)를 참조한다.

<a id="2d3e6c96e4a8c5f9"></a>
### 사용 예

```
gSQL> SELECT TO_BASE64( 'abc' ), TO_BASE64( 'abcd' ) FROM DUAL;

TO_BASE64( 'abc' ) TO_BASE64( 'abcd' )
------------------ -------------------
YWJj               YWJjZA==           
1 row selected.
```

<a id="6a95099dcd5efb32"></a>
## TO_CHAR( datetime )

<a id="955ea27c397b3222"></a>
### 구문

```
TO_CHAR( datetime [, fmt ] )
```

<a id="0a9757fb9a9278db"></a>
### 설명

TO_CHAR( datetime ) 함수는 datetime을 명시된 fmt 형식의 문자열로 변환하여 반환한다.

인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  

입력 인자의 값이 하나라도 NULL이면 NULL을 반환한다.

fmt가 생략된 경우, default format 형식을 따른다.  
• DATE: [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#ec78df636da07fb6)  
• TIMESTAMP: [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#15c05b1b42192d13)  
• TIMESTAMP WITH TIME ZONE: [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#7dad2bb0bce4c28d)  
• TIME: [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#1793ce4c56053b95)  
• TIME WITH TIME ZONE: [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#0a90eef2149e893a)

인자 datetime이 INTERVAL 타입인 경우, fmt와 무관하게 string으로 변환하여 반환한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#33b8ffdce1d3bfd9)을 참조한다.

결과 타입은 CHARACTER VARYING 이다.

<a id="8f994066d616cd2d"></a>
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

<a id="3b3cd1288d7889b5"></a>
## TO_CHAR( number )

<a id="ff92aecf9558d914"></a>
### 구문

```
TO_CHAR( number [, fmt ] )
```

<a id="45f18a7e741b55c2"></a>
### 설명

TO_CHAR( number ) 함수는 number를 명시된 fmt 형식의 문자열로 변환하여 반환한다.

인자 number에는 숫자 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, 모든 유효 숫자를 문자열로 변환하여 반환한다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#1600ba7580e6ec90)을 참조한다.  
입력 인자의 값이 하나라도 NULL이면 NULL을 반환한다.

결과 타입은 CHARACTER VARYING 이다.

<a id="a94786f0003e1e09"></a>
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

<a id="df568ff4577a76a5"></a>
## TO_DATE

<a id="274d04f6ae050375"></a>
### 구문

```
TO_DATE( str [, fmt ] )
```

<a id="3be17e938f975fc3"></a>
### 설명

TO_DATE 함수는 명시된 fmt 형식의 문자열 str을 DATE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_DATE_FORMAT은 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#33b8ffdce1d3bfd9)을 참조한다.  
자세한 내용은 [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#ec78df636da07fb6)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

결과 타입은 DATE 이다.

<a id="9e33fb496af013d6"></a>
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

<a id="b11ead8c69613a1b"></a>
## TO_NATIVE_BIGINT

<a id="4e13a835741c946e"></a>
### 구문

```
TO_NATIVE_BIGINT( str [, fmt ] )
```

<a id="15649bf25894cddd"></a>
### 설명

TO_NATIVE_BIGINT 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_BIGINT 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#1600ba7580e6ec90)을 참조한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="214e38a44c70bbb3"></a>
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

<a id="f52bafc2e71c1d8c"></a>
## TO_NATIVE_DOUBLE

<a id="bfb3be6130f27de9"></a>
### 구문

```
TO_NATIVE_DOUBLE( str [, fmt ] )
```

<a id="4be4fe3051b865ac"></a>
### 설명

TO_NATIVE_DOUBLE 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_DOUBLE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#1600ba7580e6ec90)을 참조한다.

결과 타입은 NATIVE_DOUBLE이다.

<a id="71322429f7f68d12"></a>
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

<a id="c2469a52fabc4b1e"></a>
## TO_NATIVE_INTEGER

<a id="3672e44d05ffed6f"></a>
### 구문

```
TO_NATIVE_INTEGER( str [, fmt ] )
```

<a id="670acd487c0f1c86"></a>
### 설명

TO_NATIVE_INTEGER 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_INTEGER 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#1600ba7580e6ec90)을 참조한다.

결과 타입은 NATIVE_INTEGER이다.

<a id="e5f7bc2fdb1a6bf8"></a>
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

<a id="876e14c5cbf8499f"></a>
## TO_NATIVE_REAL

<a id="c9dcede8d8159bbf"></a>
### 구문

```
TO_NATIVE_REAL( str [, fmt ] )
```

<a id="7e674c43530c8278"></a>
### 설명

TO_NATIVE_REAL 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_REAL 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#1600ba7580e6ec90)을 참조한다.

결과 타입은 NATIVE_REAL이다.

<a id="e79808949bd21f9b"></a>
### 사용 예

```
gSQL> SELECT TO_NATIVE_REAL( '123.45' ) AS RESULT1, 
             TO_NATIVE_REAL( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
```

<a id="b14c8133f703798a"></a>
## TO_NATIVE_SMALLINT

<a id="84a276d7851bc70d"></a>
### 구문

```
TO_NATIVE_SMALLINT( str [, fmt ] )
```

<a id="76e2e6e74c7880ca"></a>
### 설명

TO_NATIVE_SMALLINT 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_SMALLINT 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYIN과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#1600ba7580e6ec90)을 참조한다.

결과 타입은 NATIVE_SMALLINT이다.

<a id="9208424ff8e34cfe"></a>
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

<a id="067b6a80dbba0c22"></a>
## TO_NUMBER

<a id="bcd36a5ed2c00ae9"></a>
### 구문

```
TO_NUMBER( str [, fmt] )
```

<a id="2e59a36679ee2537"></a>
### 설명

TO_NUMBER 함수는 명시된 fmt 형식의 문자열 str을 NUMBER 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](11-sql-elements.md#1600ba7580e6ec90)을 참조한다.

결과 타입은 NUMBER이다.

<a id="ce34bff7b8fe3aca"></a>
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

<a id="acb02dbbdf32b2dd"></a>
## TO_TIME

<a id="f32ac74f3e505b5d"></a>
### 구문

```
TO_TIME( str [, fmt ] )
```

<a id="7801480f2fff8ee6"></a>
### 설명

TO_TIME 함수는 명시된 fmt 형식의 문자열 str을 TIME 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIME_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#33b8ffdce1d3bfd9)을 참조한다.  
자세한 내용은 [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#1793ce4c56053b95)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

결과 타입은 TIME 이다.

<a id="cf529c8a6f956775"></a>
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

<a id="2c8cee3ecac352ee"></a>
## TO_TIME_TZ

<a id="67c6fcb371fc75c8"></a>
### 구문

```
TO_TIME_TZ( str [, fmt ] )
```

<a id="1d554937dd7c40d3"></a>
### 설명

TO_TIME_WITH_TIME_ZONE의 alias이다.  
자세한 내용은 [TO_TIME_WITH_TIME_ZONE](#2bc444fb42cdd6a2)과 [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#0a90eef2149e893a)을 참조한다.

<a id="096b27ab48b4ef7e"></a>
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

<a id="2bc444fb42cdd6a2"></a>
## TO_TIME_WITH_TIME_ZONE

<a id="2bac99a339ccfbf4"></a>
### 구문

```
TO_TIME_WITH_TIME_ZONE( str [, fmt ] )
TO_TIME_TZ( str [, fmt ] )
```

<a id="d78f5838176ea4c4"></a>
### 설명

TO_TIME_WITH_TIME_ZONE 함수는 명시된 fmt 형식의 문자열 str을 TIME WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIME_WITH_TIME_ZONE_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#33b8ffdce1d3bfd9)을 참조한다.  
자세한 내용은 [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#0a90eef2149e893a)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

TO_TIME_WITH_TIME_ZONE의 alias로는 [TO_TIME_TZ](#2c8cee3ecac352ee) 함수가 있다.

결과 타입은 TIME WITH TIME ZONE 이다.

<a id="4b1cf488c2e721aa"></a>
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

<a id="9b24efe199e4c67b"></a>
## TO_TIMESTAMP

<a id="c62ac9eae505ba7b"></a>
### 구문

```
TO_TIMESTAMP( str [, fmt ] )
```

<a id="c1c5b85f61db7725"></a>
### 설명

TO_TIMESTAMP 함수는 명시된 fmt 형식의 문자열 str을 TIMESTAMP 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIMESTAMP_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#33b8ffdce1d3bfd9)을 참조한다.  
자세한 내용은 [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#15c05b1b42192d13)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

결과 타입은 TIMESTAMP 이다.

<a id="5c4ea01705f7aaac"></a>
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

<a id="ed65dccded47eca7"></a>
## TO_TIMESTAMP_TZ

<a id="fa8021ef56a90c6b"></a>
### 구문

```
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="d305187ddcf8d3ae"></a>
### 설명

TO_TIMESTAMP_WITH_TIME_ZONE의 alias 이다.  
자세한 내용은 [TO_TIMESTAMP_WITH_TIME_ZONE](#f50291e3f07ed587)과 [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#7dad2bb0bce4c28d)을 참조한다.

<a id="8e556ab227976fce"></a>
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

<a id="f50291e3f07ed587"></a>
## TO_TIMESTAMP_WITH_TIME_ZONE

<a id="386a39f8ec7e6978"></a>
### 구문

```
TO_TIMESTAMP_WITH_TIME_ZONE( str [, fmt ] )
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="0dfafc985d7a0a48"></a>
### 설명

TO_TIMESTAMP_WITH_TIME_ZONE 함수는 명시된 fmt 형식의 문자열 str을 TIMESTAMP WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](11-sql-elements.md#33b8ffdce1d3bfd9)을 참조한다.  
자세한 내용은 [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#7dad2bb0bce4c28d)을 참조한다.  

str 또는 fmt가 NULL이면 NULL을 반환한다.

TO_TIMESTAMP_WITH_TIME_ZONE의 alias로는 [TO_TIMESTAMP_TZ](#ed65dccded47eca7) 함수가 있다.

결과 타입은 TIMESTAMP WITH TIME ZONE 이다.

<a id="2e3649d1027e14e7"></a>
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

<a id="0bc76aea67fa8413"></a>
## TRANSACTION_DATE

<a id="598d48610975fd93"></a>
### 구문

```
TRANSACTION_DATE()
```

<a id="e24fe3f1fa95b715"></a>
### 설명

Session 시간을 기준으로 현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="67e7d413511d9cf5"></a>
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

<a id="4563686bf922c0bd"></a>
## TRANSACTION_LOCALTIME

<a id="fbede1348dc7b799"></a>
### 구문

```
TRANSACTION_LOCALTIME()
```

<a id="393db52ebae299bc"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 없는 현재 시간 (TIME WITHOUT TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="504091a0b8da6f6f"></a>
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

<a id="069b770b657fc5e1"></a>
## TRANSACTION_LOCALTIMESTAMP

<a id="f4d72385d2e6866e"></a>
### 구문

```
TRANSACTION_LOCALTIMESTAMP()
```

<a id="db2a4cc875aa077d"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 없는 현재 TIMESTAMP (TIMESTAMP WITHOUT TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="84d5b9c758aff086"></a>
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

<a id="0ff656b3e06e603d"></a>
## TRANSACTION_TIME

<a id="1e95d187eafe76a6"></a>
### 구문

```
TRANSACTION_TIME()
```

<a id="d61732cbc93e62e7"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="68a82871fdeb5daf"></a>
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

<a id="dbe1c4ab1d0ac244"></a>
## TRANSACTION_TIMESTAMP

<a id="efbc3fd7b535e44f"></a>
### 구문

```
TRANSACTION_TIMESTAMP()
```

<a id="58988b225a5d35ff"></a>
### 설명

Session 시간을 기준으로 TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="6db63a76db8aa568"></a>
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

<a id="c3b99612e17ec2ce"></a>
## TRANSLATE

<a id="0dc46abcd40da153"></a>
### 구문

```
TRANSLATE( string, from, to )
```

<a id="5029b2ce4b153da5"></a>
### 설명

TRANSLATE 함수는 문자를 치환하는 함수로, from의 문자와 일치하는 string의 문자를 from의 문자와 같은 위치에 있는 to의 문자로 치환하여 반환한다.

인자 string, from, to에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

string, from, to 중의 하나라도 NULL이면 결과값도 NULL이다.

- from의 문자와 일치하는 string 문자가 있을 경우
    - from의 길이와 to의 길이가 같으면 from의 문자와 같은 위치에 있는 to의 문자로 치환한다.
    - from의 길이가 to의 길이보다 길면 to의 문자 길이 이후의 위치에 있는 from의 문자는 string에서 제거된다.
    - from의 문자가 중복된 문자로 이뤄져 있으면 from의 중복되는 문자의 첫 위치와 동일한 위치에 있는 to의 문자로 치환된다.
- from의 문자와 일치하는 string 문자가 없을 경우, string은 치환되지 않는다.

결과 타입은 다음 표와 같다.

**TRANSLATE의 결과 타입**

<a id="9795df5a80df9086"></a>
| string 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="26b855acd09d66e5"></a>
### 사용 예

- from의 문자와 일치하는 string 문자가 있으면, 같은 위치의 to의 문자로 치환된다.
    - A → Z, C → Y, E → X, G → W

```
gSQL> SELECT TRANSLATE('ABCDEFG', 'ACEG', 'ZYXW') AS RESULT
FROM DUAL;
RESULT 
-------
ZBYDXFW
1 row selected.
```

- from의 문자열 길이가 to의 문자열 길이보다 길면, to의 문자열 길이 이후 위치한 from의 문자는 string에서 제거되고 치환된다.
    - A → Z, C → Y, E 제거, G 제거

```
gSQL> SELECT TRANSLATE('ABCDEFG', 'ACEG', 'ZY') AS RESULT
      FROM DUAL;
RESULT
------
ZBYDF 
1 row selected.
```

<a id="cb54da70d0db3b75"></a>
## TRIM

<a id="de04af4657f30b6f"></a>
### 구문

```
TRIM([ [ LEADING | TRAILING | BOTH ]  [trim_character] FROM ] trim_source)
```

<a id="aafda1d540a7c39b"></a>
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

<a id="9608bac5c822cdc6"></a>
| trim_character, trim_source 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="dd252fee9222b2c7"></a>
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

<a id="2e0f8d04a2200181"></a>
## TRUNC( number )

<a id="ce95990ed4868332"></a>
### 구문

```
TRUNC( num [ , scale ] )
```

<a id="a21b3445e4c01b36"></a>
### 설명

TRUNC( number ) 함수는 scale 기준으로 num을 버림한 값을 반환한다.

인자 num과 scale에는 숫자 타입이 올 수 있다.  
인자 num 또는 scale이 NULL이면 NULL을 반환한다.

scale이 생략된 경우, scale은 0이 되어 TRUNC( num, 0 )일 때와 같이 실행된다.  
scale이 양수인 경우, 소수점 오른쪽 자리수를 기준으로 버림한다.  
scale이 음수인 경우, 소수점 왼쪽 자리수를 기준으로 버림한다.

<a id="34159b0060caab9d"></a>
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

<a id="2b6a711af913ef79"></a>
## TRUNC( date )

<a id="168c596411fe9ba4"></a>
### 구문

```
TRUNC( date [ , fmt ] )
```

<a id="a06bd7fb93b86710"></a>
### 설명

TRUNC( date ) 함수는 date를 지정된 fmt 단위로 버림한 값을 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
인자 date 또는 fmt이 NULL이면 NULL을 반환한다.

결과 타입은 인자로 받은 date 타입과 관계없이 항상 DATE 타입이다.

fmt가 생략되었을 경우의 기본값은 DAY이며, 사용 가능한 형식문자열은 다음 표와 같다.

**fmt에 사용가능한 형식문자열**

<a id="4842855fc84fa843"></a>
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

<a id="b40826109d20e350"></a>
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

<a id="ae6e3aa65d222bc9"></a>
## UPPER

<a id="3d2f4fdc5d9a9260"></a>
### 구문

```
UPPER( str )
```

<a id="3911f99d1b8efd29"></a>
### 설명

UPPER 함수는 str의 대문자를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.  
str이 NULL이면 결과값도 NULL이다.

반환되는 타입은 인자 str과 동일한 타입이다.

<a id="66bd40da6310b25b"></a>
### 사용 예

```
gSQL> SELECT UPPER( 'spring' ) AS RESULT FROM DUAL;
RESULT
------
SPRING
1 row selected.
```

<a id="d46e348c108bc31a"></a>
## UNHEX

<a id="34606c690f8b5750"></a>
### 구문

```
UNHEX( str )
```

<a id="17cc540bea8d2e21"></a>
### 설명

인자 str은 16진수 문자이며, 이를 각 byte로 표현하여 binary string으로 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 BINARY VARYING이나 BINARY LONG VARYING과 같은 BINARY 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 16진수 범위에 속하지 않는 문자가 포함되면 에러를 반환한다.

자세한 내용은 [HEX](#29ae504b98ddc73d)를 참조한다.

<a id="9bf9294b09dede7b"></a>
### 사용 예

```
gSQL> SELECT UNHEX( HEX( 'abc' ) ) FROM DUAL;
UNHEX( HEX( 'abc' ) )
---------------------
616263               
1 row selected.
```

<a id="8f9a823ff10351b5"></a>
## UNHEX_TO_CHARSTR

<a id="4eb11b41a8a8c68a"></a>
### 구문

```
UNHEX_TO_CHARSTR( str )
```

<a id="f09bd4449006b90d"></a>
### 설명

인자 str은 16진수 문자이며 이를 각 byte로 표현하여 character string으로 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 CHARACTER VARYING이나 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 16진수 범위에 속하지 않는 문자가 포함되면 에러를 반환한다.

인자 str가 어떤 데이터의 16진수 문자표현인지 알 수 없으므로 character string으로 반환할 때 현재 적용할 수 있는 character set을 적용하여 결과값을 반환한다.  
현재 적용할 수 있는 character set에 포함되지 않는 경우, 에러를 반환한다.

자세한 내용은 [HEX](#29ae504b98ddc73d)와 [UNHEX](#d46e348c108bc31a)를 참조한다.

<a id="c742dee748e798aa"></a>
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

<a id="ceaad10397d2ba2f"></a>
## USER_ID

<a id="742b0d896b8f90f6"></a>
### 구문

```
USER_ID ()
```

<a id="6f298ba46585a7ec"></a>
### 설명

현재 사용자의 number ID를 얻는다.

> Cluster system에서는 접속한 server에 따라 다른 값을 가질 수 있다.  
> 현재 사용자의 이름을 얻는 [CURRENT_USER](#c806d6efc62f415a) 함수 사용을 권장한다.

<a id="f22c7cd85f50e1f0"></a>
### 사용 예

```
% gsql test test

gSQL> SELECT USER_ID() FROM dual;

USER_ID()
---------
        6

1 row selected.
```

<a id="db698238284cf9be"></a>
## UUID

<a id="3f0b83bbb95d9d2e"></a>
### 구문

```
UUID()
```

<a id="b69aa35e5ac022a1"></a>
### 설명

UUID 함수는 전역고유식별자 (Universal Unique Identifier) 를 생성하여 반환한다.  
반환되는 타입은 VARBINARY 이며 내부적으로 16 바이트로 구성된다.

<a id="b2c856d651a953f4"></a>
### 사용 예

```
gSQL> SELECT HEX( UUID() ) FROM DUAL;
HEX( UUID() )                   
--------------------------------
E6F0A5C2387511E8B95259E479C2FD50
1 row selected.
```

<a id="b236ef352055656d"></a>
## VAR_POP

<a id="f9cc312a3d02d2bf"></a>
### 구문

```
VAR_POP( expr )
```

<a id="9de32fc3d5781611"></a>
### 설명

Aggregation 함수로써 expr set의 모 분산 (population variance)을 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**VAR_POP 인자와 결과 타입**

<a id="4caeb302ac45915d"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 분산은 모 집단 (전체)의 분산이며 분산은 편차 제곱의 평균이다. 즉, 데이터의 각 값에서 모 평균 (전체의 평균)을 빼고 제곱해서 모두 더한 뒤 모 집단의 데이터 개수로 나눈다.  
> 이는 각 관찰값들이 평균으로부터 얼마나 많이 퍼져있는지 파악하는데 사용된다.

자세한 내용은 [STDDEV_POP](#9cf33dd4c3767fa7)을 참조한다.

<a id="621fb805418a0fcd"></a>
### 사용 예

```
gSQL> SELECT VAR_POP(c1) FROM t1;

VAR_POP(C1)
-----------
     105.76

1 row selected.
```

<a id="ceed8a819f8dd64d"></a>
## VAR_SAMP

<a id="6116bdd420f9d637"></a>
### 구문

```
VAR_SAMP( expr )
```

<a id="f998d6a3164a0b3a"></a>
### 설명

Aggregation 함수로써 expr set의 표본 분산 (sample variance)을 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 NULL값을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**VAR_SAMP 인자와 결과 타입**

<a id="f069300141bae01b"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 집단 (전체)을 다루는 모 분산과 달리, 표본 분산은 추출한 표본으로 평균과 편차를 다룬다. 즉, 데이터의 각 값에서 표본의 평균을 빼고 제곱해서 모두 더한 뒤, 표본 집단의 데이터 개수 - 1로 나눈다.  
> 이는 모 집단의 분산을 추정하는 데 사용된다.

자세한 내용은 [STDDEV_SAMP](#5048db9c0886f2f3)을 참조한다.

<a id="f464aaa136220586"></a>
### 사용 예

```
gSQL> SELECT VAR_SAMP(c1) FROM t1;

VAR_SAMP(C1)
------------
       132.2

1 row selected.
```

<a id="fe7ab65e1a6c5b53"></a>
## VARIANCE

<a id="35682bf6c942f5b9"></a>
### 구문

```
VARIANCE( [ ALL | DISTINCT ] expr )
```

<a id="0f17a7749b18f368"></a>
### 설명

Aggregation 함수로써 expr set의 분산 (variance)을 얻는다.

ALL을 명시한 경우 모든 값들에 대해 수행하고, DISTINCT를 명시한 경우 중복을 제거한 값들에 대해 수행한다. 둘 다 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

NULL 값을 제외하고 DISTINCT로 중복을 제거한 후의 expr set의 개수가 한 개일 경우, 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**VARIANCE 인자와 결과 타입**

<a id="499284e4adc7e11b"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> GOLDILOCKS는 분산을 다음과 같이 계산한다.
> 
> - expr set의 개수가 1이면 0을 반환한다.
> - expr set의 개수가 1보다 크면, [VAR_SAMP( expr )](#ceed8a819f8dd64d) 값을 반환한다.
> 

자세한 내용은 [STDDEV](#710271af985cd947)를 참조한다.

<a id="8207b1dbb9dbf26e"></a>
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

<a id="38cde8c6fcd22905"></a>
## VERSION

<a id="47ad5a68ae3da88b"></a>
### 구문

```
VERSION()
```

<a id="61abae38c9894244"></a>
### 설명

제품의 version string을 얻는다.

<a id="bcdb7d4ad058ed4d"></a>
### 사용 예

```
gSQL> SELECT VERSION() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="324628402e81b43e"></a>
## WIDTH_BUCKET

<a id="23f3c4f0b3772a94"></a>
### 구문

```
WIDTH_BUCKET( num, min, max, cnt )
```

<a id="9ca397fdd642d797"></a>
### 설명

WIDTH_BUCKET 함수는 명시된 min, max 범위에서 cnt와 동일한 넓이를 갖는 구간을 생성하고, num이 속하는 구간의 위치를 반환한다.

인자 num, min, max, cnt에는 숫자 타입이 올 수 있다.

min, max는 구간에 대한 범위를 의미하며, min, max 값이 같은 경우에는 에러를 반환한다.  
cnt는 구간 개수를 의미하고 양의 정수이어야 하며 0 이거나 음수인 경우에는 에러를 반환한다.  
구간의 위치에는 1부터 시작하는 번호가 부여된다.

num, min, max, cnt 중 하나라도 NULL인 경우, 결과값도 NULL이다.

<a id="5451af4bdc11160a"></a>
### 사용 예

```
gSQL> SELECT WIDTH_BUCKET( 5, 1, 20, 5 ) AS RESULT FROM DUAL;
RESULT
------
     2
1 row selected.
```

---

[← 16. Built-in Data Type References](16-built-in-data-type-references.md) · [전체 목차](../README.md) · [18. SQL References →](18-sql-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
