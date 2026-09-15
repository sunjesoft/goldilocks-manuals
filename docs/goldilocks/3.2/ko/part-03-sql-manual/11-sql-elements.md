<a id="b5266f2008bb2c7b"></a>

# 11. SQL Elements

> 원본: [GOLDILOCKS 3.2 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/3_2_x/manual/ko/b5266f2008bb2c7b)  
> 태그: `GOLDILOCKS_Venus_3_2_14_retagged`

[← 10. Server Property](../part-02-administration-manual/10-server-property.md) · [전체 목차](../README.md) · [12. SQL Languages →](12-sql-languages.md)

<a id="bf81af964b966c29"></a>
## Syntax Elements

<a id="f589d599cc92f25f"></a>
### Identifiers

Identifier는 ordinary identifier와 delimited identifier로 나뉜다.  
Ordinary identifier는 문자 또는 문자와 숫자로 구성된 identifier로써 내부적으로 모든 문자를 대문자로 치환하여 사용한다. 따라서 대소문자를 구분하지 않는다.

다음은 ordinary identifier의 예이다.

```
GOLDILOCKS
GoldiLocks
```

Delimited identifier는 double quote (")를 시작과 끝에 기술한 문자 또는 문자와 숫자로 구성된 identifier로써 내부적으로 해당 문자를 모두 기술한 그대로 사용한다. 따라서 delimited identifer를 사용할 경우 대소문자를 구분한다.

다음은 delimited identifier의 예이다.

```
"GOLDILOCKS"
"GoldiLocks"
```

<a id="883ce6c883c33aba"></a>
### Literals

Literals는 null이 아닌 값을 기술한 것이다.

<a id="9b6eb6e4d74a5ff9"></a>
#### Text Literals

Text literals는 string이나 binary string을 기술한 것이다.

String의 시작과 끝에 single quote (')를 작성하여 string에 대한 text literals를 사용할 수 있다. Double quote (") 뿐만 아니라 single quote (')를 제외한 모든 문자열이 single quote (') 안에 작성하는 string이 될 수 있다. 만약 string에 single quote (')를 사용하려면 single quote (')를 공백없이 연속으로 두 번 작성해야 한다. String에는 최대 4,000 문자까지 작성할 수 있다.

다음은 string에 대한 text literals를 작성하는 예이다.

```
'GOLDILOCKS'
'Sunje''s DBMS'
```

Binary string에 대한 text literals는 x' 또는 X'로 시작하고 '로 끝나는 16진수의 string을 기술한다. 16진수의 string은 각 자리에 0 ~ 9, A (a) ~ F (f)에 해당하는 문자만 기술할 수 있으며, 두 자리의 문자가 하나의 byte를 의미하므로 항상 짝수 자리를 작성해야 한다. Binary string은 최대 4,000 문자까지 작성할 수 있다.

다음은 binary string에 대한 text literals를 작성하는 예이다.

```
x'001f'
X'FF0A'
x'aF37BBc013'
```

<a id="1efa5e0039149d37"></a>
#### Numeric Literals

Numeric literals는 숫자타입의 literals를 작성하는 형식으로써 정수나 소수점 이하의 자리를 갖는 숫자를 작성할 수 있다. Numeric literals에 대한 문법은 다음과 같다.

```
[ + | - ] <digits> [ . <digits> ] [ E | e [ + | - ] <digits> ] [ f | F | d | D ]
```

- 제일 앞에 나오는 +, - 는 숫자 전체의 부호가 양수인지 음수인지를 나타낸다. +, -는 생략 가능하며 생략시 +로 간주된다.
- &lt;digits&gt;에는 0 ~ 9 사이의 숫자들을 공백없이 나열할 수 있고, .을 이용하여 소수점 이하의 숫자까지 작성할 수 있다.
- 첫 번째 &lt;digits&gt; 뒤에는 exponent 형식으로 작성할 수 있는데, 이를 위해 exponent를 의미하는 E 또는 e를 작성한다. 그 뒤에는 exponent의 부호인 +, -를 작성하고 다음으로 &lt;digits&gt;를 작성한다. Exponent의 부호도 생략 가능하며 생략시 +로 간주한다.
- 마지막으로 f, F, d, D 등의 문자가 숫자 뒤에 올 수 있는데 이 문자는 BINARY_FLOAT, BINARY_DOUBLE의 숫자임을 알려준다. 이런 문자를 기술하지 않는 경우 NUMBER 타입의 숫자인 것으로 간주한다.

다음은 numeric literals를 작성하는 예이다.

```
20
+123.45
0.03
+1.23E-02
-1.5

10f
+123.45F
1.2E-3F
-22d
123.45D
-1.23E+05D
```

<a id="dc7ac61da8cec806"></a>
#### Datetime Literals

Datetime literals는 날짜/ 시간 타입에 대한 literals를 작성하는 형식이다. Datetime value는 string literal을 사용하여 지정하거나 TO_* 함수(TO_DATE 등)를 이용해 character 또는 numeric value를 변환하여 지정할 수도 있다.

날짜/시간 타입에는 DATE, TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 이 있다.

<a id="50cfb81da3af2ea1"></a>
##### Date Literals

Date literals는 DATE'string literal' 또는 TO_DATE(string_literal [, format]) 의 형태로 작성할 수 있다.

- DATE'string literal'
    - Date 타입 format은 'SYYYY-MM-DD' 이다.
    - DATE'2002-07-15'
- TO_DATE(string_literal [, format])
    - Format을 지정하지 않은 경우, date 타입의 format은 NLS_DATE_FORMAT이고,
    - Format을 지정한 경우, 지정된 format을 적용한다.

- Date 타입은 년월일시분초를 포함한다. (fractional seconds (소수점이하초)는 제외)
- 날짜를 기술하지 않으면, 현재 월의 첫째날로 설정된다.
- 시분초를 기술하지 않으면 기본값인 자정으로 설정된다.
    - HH24 format인 경우 '00:00:00' 이다.
    - HH12 format인 경우 '12:00:00' 이다.
- 시분초가 포함된 DATE value의 시분초를 기본값인 자정으로 설정하려면 TRUNC(date)를 이용해야 한다.
    - 예를 들어 TRUNC(SYSDATE): SYSDATE는 년월일시분초가 모두 포함된 값이다.
- Date value들을 시분초를 제외하고 년월일값만 비교하고자 하는 경우, TRUNC 함수를 이용해서 시분초값을 자정으로 설정해야 한다.

자세한 내용은 [TO_DATE](#45c8ee60f5aa8084), [Datetime Format 문자열](#6c90db97831852f6), [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#39cb46c447575199)을 참조한다.

다음은 date literals를 작성하는 예이다.

```
DATE'2002-07-15'
```

- Format을 지정하지 않은 경우로 NLS_DATE_FORMAT = 'YYYY-MM-DD' 일 때

```
TO_DATE( '2002-07-15' )
```

- Format을 지정한 경우

```
TO_DATE( '15-JUL-02', 'DD-MON-RR' )
TO_DATE( '2002-07-15 00:00:00', 'YYYY-MM-DD HH24:MI:SS' )
TO_DATE( '2002-07-15 13:25:30', 'YYYY-MM-DD HH24:MI:SS' )
```

- DATE 타입에 날짜를 기술하지 않은 경우 (현재 월의 첫째날로 저장)

```
gSQL> SELECT TO_DATE( '2000-07', 'YYYY-MM' ) FROM DUAL;
  TO_DATE( '2000-07', 'YYYY-MM' )
  -------------------------------
  2000-07-01
```

- DATE 타입에 시분초를 기술하지 않은 경우 (시분초값이 자정으로 저장됨)

```
gSQL> SELECT 
        TO_CHAR( DATE'2002-07-15', 'YYYY-MM-DD HH24:MI:SS' ) AS RESULT
        FROM DUAL;
  RESULT             
  -------------------
  2002-07-15 00:00:00
```

- 시분초가 포함된 DATE value(SYSDATE)의 시분초를 기본값인 자정으로 설정한 경우

```
gSQL> SELECT 
        TO_CHAR( SYSDATE, 
                 'YYYY-MM-DD HH24:MI:SS' ) AS RESULT_SYSDATE,
        TO_CHAR( TRUNC( SYSDATE ),
                 'YYYY-MM-DD HH24:MI:SS' ) AS RESULT_TRUNC_SYSDATE 
        FROM DUAL;
  RESULT_SYSDATE      RESULT_TRUNC_SYSDATE
  ------------------- --------------------
  2014-08-19 10:06:49 2014-08-19 00:00:00
```

- Date value에서 시분초를 제외하고 년월일만 비교하는 경우

```
gSQL> SELECT 
        TO_DATE( '2002-08-12' ) = 
        TRUNC( TO_DATE( '2002-08-12 23:59:59', 'YYYY-MM-DD HH24:MI:SS' ) )
        AS RESULT FROM DUAL;
  RESULT
  ------
  TRUE
```

<a id="7bc449ae26138f1e"></a>
##### Time Literals

Time literals는 TIME'string literal' 또는 TO_TIME(string_literal [, format])의 형태로 작성할 수 있다.

- TIME'string literal'
    - Time 타입 format은 'HH24:MI:SS[.[FF6]]'이다.
    - TIME'15:30:59.999999'
- TO_TIME(string_literal [, format])
    - Format을 지정하지 않은 경우, time 타입의 format은 NLS_TIME_FORMAT 이고,
    - Format을 지정한 경우, 지정된 format을 적용한다.

Time 타입은 시분초, fractional seconds (소수점이하초)를 포함한다.  
Fractional seconds는 최대 여섯 자리 숫자의 형식을 지정하여 작성할 수 있다.

자세한 내용은 [TO_TIME](#c6462fe8a092223a), [Datetime Format 문자열](#6c90db97831852f6), [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#2524063f770de1b8)을 참조한다.

다음은 time literals를 작성하는 예이다.

```
TIME'15:30:59.999999'
```

- Format을 지정하지 않은 경우로써 NLS_TIME_FORMAT = 'HH24:MI:SS.FF6' 일 때

```
TO_TIME( '15:30:59.999999' )
```

- Format을 지정한 경우

```
TO_TIME( '09.45.03.546873 AM', 'HH12.MI.SS.FF6 AM' )
TO_TIME( '09:45:03', 'HH12:MI:SS' )
```

<a id="1a1e19946e2775d4"></a>
##### Time with Time Zone Literals

Time with time zone literals는 TIME'string literal', TIME WITH TIME ZONE'string literal' 또는 TO_TIME_WITH_TIME_ZONE(string_literal [, format] ) , TO_TIME_TZ(string_literal [, format] )의 형태로 작성할 수 있다.

- TIME'string literal' 또는 TIME WITH TIME ZONE'string literal'
    - Time with time zone 타입의 format은 'HH24:MI:SS[.[FF6]] TZH:TZM' 이다.
    - TIME'15:30:59.999999 +09:00'
    - TIME WITH TIME ZONE'15:30:59.999999 +09:00'
+
- TO_TIME_WITH_TIME_ZONE(string_literal [, format] )
    - Format을 지정하지 않은 경우, time with time zone 타입의 format은 NLS_TIME_WITH_TIME_ZONE_FORMAT 이고,
    - Format을 지정한 경우, 지정된 format을 적용한다.

Time with time zone 타입은 시분초, fractional seconds (소수점이하초), time zone offset (time zone hour, time zone minute)를 포함한다.  
Fractional seconds는 최대 여섯 자리 숫자의 형식을 지정하여 작성할 수 있다.

자세한 내용은 [TO_TIME_WITH_TIME_ZONE](#132b267c45037442), [Datetime Format 문자열](#6c90db97831852f6), [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#838ff7f06a1cc0ac)을 참조한다.

다음은 time with time zone literals를 작성하는 예이다.

```
TIME'15:30:59.999999 +09:00'
TIME WITH TIME ZONE'15:30:59.999999 +09:00'
```

- Format을 지정하지 않은 경우로써 NLS_TIME_WITH_TIME_ZONE_FORMAT = 'HH24:MI:SS.FF6 TZH:TZM' 일 때

```
TO_TIME_WITH_TIME_ZONE( '15:30:59.999999 +09:00' )
TO_TIME_TZ( '15:30:59.999999 +09:00' )
```

- Format을 지정한 경우

```
TO_TIME_WITH_TIME_ZONE( '09.45.03.546873 +09:00 AM', 
                        'HH12.MI.SS.FF6 TZH:TZM AM' )
```

<a id="6ded9709553c29d8"></a>
##### Timestamp Literals

Timestamp literals는 TIMESTAMP'string literal' 또는 TO_TIMESTAMP(string_literal [, format] )의 형태로 작성할 수 있다.

- TIMESTAMP'string literal'
    - Timestamp 타입의 format은 'SYYYY-MM-DD HH24:MI:SS[.[FF6]]' 이다.
    - TIMESTAMP'2002-07-15 15:39:59.999999'
- TO_TIMESTAMP(string_literal [, format] )
    - Format을 지정하지 않은 경우, timestamp 타입의 format은 NLS_TIMESTAMP_FORMAT이고
    - Format을 지정한 경우, 지정된 format을 적용한다.

Timestamp 타입은 년월일, 시분초, fractional seconds (소수점이하초)를 포함한다.  
Fractional seconds는 최대 여섯 자리 숫자의 형식을 지정하여 작성할 수 있다.

자세한 내용은 [TO_TIMESTAMP](#e11d27a423dbc46c), [Datetime Format 문자열](#6c90db97831852f6), [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#db86968fe3d06d6e)을 참조한다.

다음은 timestamp literals를 작성하는 예이다.

```
TIMESTAMP'2002-07-15 15:39:59.999999'
```

- Format을 지정하지 않은 경우로써 NLS_TIMESTAMP_FORMAT = 'YYYY-MM-DD HH24:MI:SS.FF6' 일 때

```
TO_TIMESTAMP( '2002-07-15 15:39:59.999999' )
```

- Format을 지정한 경우

```
TO_TIMESTAMP( '15-JUL-02 11.06.30.123456 AM', 
              'DD-MON-RR HH12.MI.SS.FF6 AM' )
```

<a id="c4f6475f9736fb4f"></a>
##### Timestamp with Time Zone Literals

Timestamp with time zone literals는 TIMESTAMP'string literal',  TIMESTAMP WITH TIME ZONE'string literal' 또는 TO_TIMESTAMP_WITH_TIME_ZONE(string_literal [, formt] ), TO_TIMESTAMP_TZ(string_literal [, format])의 형태로 작성할 수 있다.

- TIMESTAMP'string literal' 또는 TIMESTAMP WITH TIME ZONE'string literal'
    - Timestamp with time zone 타입의 format은 'SYYYY-MM-DD HH24:MI:SS[.[FF6]] TZH:TZM'이다.
    - TIMESTAMP'2002-07-15 15:39:59.999999 +09:00'
    - TIMESTAMP WITH TIME ZONE'2002-07-15 15:39:59.999999 +09:00'
- TO_TIMESTAMP_WITH_TIME_ZONE(string_literal [, formt] )
    - Format을 지정하지 않은 경우, timestamp with time zone 타입의 format은 NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT 이고,
    - Format을 지정한 경우, 지정된 format을 적용한다.

Timestamp with time zone 타입은 년월일, 시분초, fractional seconds (소수점이하초), time zone offset (timezone hour, timezone minute)을 포함한다.  
Fractional seconds는 최대 여섯 자리 숫자의 형식을 지정하여 작성할 수 있다.

자세한 내용은 [TO_TIMESTAMP_WITH_TIME_ZONE](#deb069ec65b335a1), [Datetime Format 문자열](#6c90db97831852f6), [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#3356e96838139b8a)을 참조한다.

다음은 timestamp with time zone literals를 작성하는 예이다.

```
TIMESTAMP'2002-07-15 15:39:59.999999 +09:00'
TIMESTAMP WITH TIME ZONE'2002-07-15 15:39:59.999999 +09:00'
```

- FORMAT을 지정하지 않은 경우로써 NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT = 'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM' 일 때

```
TO_TIMESTAMP_WITH_TIME_ZONE( '2002-07-15 15:39:59.999999 +09:00' )
TO_TIMESTAMP_TZ( '2002-07-15 15:39:59.999999 +09:00' )
```

- FORMAT을 지정한 경우

```
TO_TIMESTAMP_WITH_TIME_ZONE( '15-JUL-02 11.06.30.123456 +09:00 AM',
                             'DD-MON-RR HH12.MI.SS.FF6 TZH:TZM AM' )
TO_TIMESTAMP_TZ( '15-JUL-02 11.06.30.123456 +09:00 AM',
                 'DD-MON-RR HH12.MI.SS.FF6 TZH:TZM AM' )
```

<a id="074711f4a241633b"></a>
#### Interval Literals

Interval literals는 시간의 간격을 지정한다.

Interval은 크게 두 가지로 분류되며 다음과 같이 표현한다.

- Year-month INTERVAL values
    - YEAR와 MONTH를 포함한다.
    - Display string 표현: 'year-month'
- Day-time INTERVAL values
    - DAY, HOUR, MINUTE, SECOND (fractional seconds 포함)를 포함한다.
    - Display string 표현: 'day hour:minute:second.fractional_seconds'
- Interval value의 부호는 string 표현의 제일 앞에 한 번만 지정할 수 있다.  
  예: INTERVAL'+3 11:22:33.999999'DAY TO SECOND ( O )  
  INTERVAL'-3 +11:22:33.999999'DAY TO SECOND ( X )

Interval 타입 목록은 다음과 같다.

- INTERVAL YEAR (leading precision)
- INTERVAL MONTH (leading precision)
- INTERVAL YEAR (leading precision) TO MONTH
- INTERVAL DAY (leading precision)
- INTERVAL HOUR (leading precision)
- INTERVAL MINUTE (leading precision)
- INTERVAL SECOND (leading precision[, fractional seconds precision] )
- INTERVAL DAY (leading precision) TO HOUR
- INTERVAL DAY (leading precision) TO MINUTE
- INTERVAL DAY (leading precision) TO SECOND (fractional seconds precision )
- INTERVAL HOUR (leading precision) TO MINUTE
- INTERVAL HOUR (leading precision) TO SECOND (fractional seconds precision )
- INTERVAL MINUTE (leading precision) TO SECOND (fractional seconds precision )

Leading precision  
•  해당 field의 자리수로써 2 ~ 6까지 지정할 수 있으며, 지정하지 않을 경우의 기본값은 2이다.  
•  Leading field 값이 leading precision 값을 초과하면 에러를 반환한다.

Fractional seconds precision  
• Fractional seconds의 자리수로써 0 ~ 6까지 지정할 수 있으며, 지정하지 않을 경우의 기본값은 6이다.  
• Fractional second field 값이 fractional seconds precision 값을 초과하면 반올림된다.

자세한 내용은 [INTERVAL](#4ec69af3c45c98df), [INTERVAL * TO * 에서 두 번째 이후 field의 precision과 값의 범위 ](#75ce4e51b242fc31)를 참조한다.

<a id="d76c4aad9d944abc"></a>
#### Interval literals의 사용 예

다음은 interval literals를 사용하는 예들이다.

<a id="59664ee869da8cd6"></a>
##### Interval YEAR

다음은 interval YEAR literals를 사용하는 예이다.

<a id="89fbd850345eea17"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'YEAR INTERVAL'01-00'YEAR | 1 year | +01-00 |
| INTERVAL'100'YEAR | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100'YEAR(3) | 100 year | +100-00 |
| INTERVAL'+999999'YEAR(6) | 999999 year | +999999-00 |
| INTERVAL'-999999'YEAR(6) | -(999999 year) | -999999-00 |

<a id="b71ff6b1e8fadb3e"></a>
##### Interval MONTH

다음은 interval MONTH literals를 사용하는 예이다.

<a id="44d656a585184db7"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'MONTH INTERVAL'00-01'MONTH | 1 month | +00-01 |
| INTERVAL'100'MONTH | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100'MONTH(3) | 8 year 4 month | +008-04 |
| INTERVAL'+999999'MONTH(6) | 83333 year 3 month | +083333-03 |
| INTERVAL'-999999'MONTH(6) | -(83333 year 3 month) | -083333-03 |

<a id="0739cf1f487c3e50"></a>
##### Interval YEAR TO MONTH

다음은 interval YEAR TO MONTH literals를 사용하는 예이다.

<a id="bee67350667fda40"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1-06'YEAR TO MONTH | 1 year 6 month | +01-06 |
| INTERVAL'1-12'YEAR TO MONTH | Month value가 11을 초과하여 에러가 반환된다. | - |
| INTERVAL'100-11'YEAR TO MONTH | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100-11'YEAR(3) TO MONTH | 100 year 11 month | +100-11 |
| INTERVAL'+999999-11'YEAR(6) TO MONTH | 999999 year 11 month | +999999-11 |
| INTERVAL'-999999-11'YEAR(6) TO MONTH | -(999999 year 11 month) | -999999-11 |

<a id="b546782a1b124408"></a>
##### Interval DAY

다음은 interval DAY literals를 사용하는 예이다.

<a id="30c817b1176e7ccc"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'DAY INTERVAL'01 00:00:00'DAY | 1 day | +01 00:00:00 |
| INTERVAL'100'DAY | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100'DAY(3) | 100 day | +100 00:00:00 |
| INTERVAL'+999999'DAY(6) | 999999 day | +999999 00:00:00 |
| INTERVAL'-999999'DAY(6) | -(999999 day) | -999999 00:00:00 |

<a id="7a04f88577dbe434"></a>
##### Interval HOUR

다음은 interval HOUR literals를 사용하는 예이다.

<a id="5ba53965c7be2860"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'HOUR INTERVAL'00 01:00:00'HOUR | 1 hour | +00 01:00:00 |
| INTERVAL'1000'HOUR(3) | Leading precision 3을 초과하여 에러가 반환된다. | - |
| INTERVAL'1000'HOUR(4) | 41 day 16 hour | +0041 16:00:00 |
| INTERVAL'+999999'HOUR(6) | 41666 day 15 hour | +041666 15:00:00 |
| INTERVAL'-999999'HOUR(6) | -(41666 day 15 hour) | -041666 15:00:00 |

<a id="486b61522db633c0"></a>
##### Interval MINUTE

다음은 interval MINUTE literals를 사용하는 예이다.

<a id="3a0851ea83eb68ed"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'MINUTE INTERVAL'00 00:01:00'MINUTE | 1 minute | +00 00:01:00 |
| INTERVAL'12345'MINUTE(4) | Leading precision 4를 초과하여 에러가 반환된다. | - |
| INTERVAL'12345'MINUTE(5) | 8 day 13 hour 45 minute | +00008 13:45:00 |
| INTERVAL'+999999'MINUTE(6) | 694 day 10 hour 39 minute | +000694 10:39:00 |
| INTERVAL'-999999'MINUTE(6) | -(694 day 10 hour 39 minute) | -000694 10:39:00 |

<a id="76c3a5b4903fa2be"></a>
##### Interval SECOND

다음은 interval SECOND literals를 사용하는 예이다.

<a id="c22b90247d882e51"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'SECOND INTERVAL'00 00:00:01.000000'SECOND | 1 second | +00 00:00:01.000000 |
| INTERVAL'100'SECOND | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'99.9999999'SECOND INTERVAL'99.9999999'SECOND(2,6) | Fractional seconds가 반올림되어 100 second가 되므로 leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'99.9999999'SECOND(3) | 1 minute 40 second | +000 00:01:40.000000 |
| INTERVAL'29.506167'SECOND(2, 2) | 29.51 second | +00 00:00:29.51 |
| INTERVAL'999999.999999'SECOND(6,6) | 11day 13 hour 46 minute 39.999999 second | +000011 13:46:39.999999 |
| INTERVAL'-999999.999999'SECOND(6,6) | -( 11day 13 hour 46 minute 39.999999 second) | -000011 13:46:39.999999 |

<a id="6dad5e28071c0c8e"></a>
##### Interval DAY TO HOUR

다음은 interval DAY TO HOUR literals를 사용하는 예이다.

<a id="ddb69a81b98e30d9"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1 23'DAY TO HOUR INTERVAL'01 23:00:00'DAY TO HOUR | 1 day 23 hour | +01 23:00:00 |
| INTERVAL'1 24'DAY TO HOUR | Hour value가 23을 초과한 invalid 값으로써 에러를 반환한다. | - |
| INTERVAL'100 23'DAY TO HOUR | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100 23'DAY(3) TO HOUR | 100 day 23 hour | +100 23:00:00 |
| INTERVAL'+999999 23'DAY(6) TO HOUR | 999999 day 23 hour | +999999 23:00:00 |
| INTERVAL'-999999 23'DAY(6) TO HOUR | -(999999 day 23 hour) | -999999 23:00:00 |
| INTERVAL'-999999 +23'DAY(6) TO HOUR | 부호 지정 오류로 인한 에러이다. | - |

<a id="de0c1061ffa2c483"></a>
##### Interval DAY TO MINUTE

다음은 interval DAY TO MINUTE literals를 사용하는 예이다.

<a id="473103a45a4012c1"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1 23:59'DAY TO MINUTE INTERVAL'01 23:59:00'DAY TO MINUTE | 1 day 23 hour 59 second | +01 23:59:00 |
| INTERVAL'1 24:59'DAY TO MINUTE | Hour value가 23을 초과한 invalid 값으로써 에러가 반환된다. | - |
| INTERVAL'1 23:60'DAY TO MINUTE | Minute value가 59를 초과한 invalid 값으로써 에러가 반환된다. | - |
| INTERVAL'100 23:59'DAY TO MINUTE | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100 23:59'DAY(3) TO MINUTE | 100 day 23 hour 59 minute | +100 23:59:00 |
| INTERVAL'+999999 23:59'DAY(6) TO MINUTE | 999999 day 23 hour 59 minute | +999999 23:59:00 |
| INTERVAL'-999999 23:59'DAY(6) TO MINUTE | -(999999 day 23 hour 59 minute) | -999999 23:59:00 |

<a id="5a0753b12e36ea4d"></a>
##### Interval DAY TO SECOND

다음은 interval DAY TO SECOND literals를 사용하는 예이다.

<a id="1a666eadc79e9a35"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL '1 23:59:59.999999'DAY TO SECOND | 1 day 23 hour 59 minute 59.999999 second | +01 23:59:59.999999 |
| INTERVAL '1 24:59:59.999999'DAY TO SECOND | Hour value가 23을 초과하여 에러가 반환된다. | - |
| INTERVAL '1 23:60:59.999999'DAY TO SECOND | Minute value가 59를 초과하여 에러가 반환된다. | - |
| INTERVAL '1 23:59:60.999999'DAY TO SECOND | Second value가 60을 초과하여 에러가 반환된다. | - |
| INTERVAL '99 23:59:59.9999999'DAY TO SECOND | Fractional seconds가 반올림되어 100 day가 되므로 leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL '99 23:59:59.9999999'DAY(3) TO SECOND | 100 day | +100 00:00:00.000000 |
| INTERVAL '1 11:22:33.567890'DAY(2) TO SECOND(2) | 1 day 11 hour 22 minute 33.57 second | +01 11:22:33.57 |
| INTERVAL '+999999 23:59:59.999999'DAY(6) TO SECOND(6) | 999999 day 23 hour 59 minute 59.999999 hour | +999999 23:59:59.999999 |
| INTERVAL '-999999 23:59:59.999999'DAY(6) TO SECOND(6) | -(999999 day 23 hour 59 minute 59.999999 hour) | -999999 23:59:59.999999 |

<a id="f037d88b1e6a1ef9"></a>
##### Interval HOUR TO MINUTE

다음은 interval HOUR TO MINUTE literals를 사용하는 예이다.

<a id="f848eb8af310e91e"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'23:59'HOUR TO MINUTE INTERVAL'00 23:59:00'HOUR TO MINUTE | 23 hour 59 minute | +00 23:59:00 |
| INTERVAL'23:60'HOUR TO MINUTE | Minute value가 59를 초과하여 에러가 반환된다. | - |
| INTERVAL'100:59'HOUR TO MINUTE | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100:59'HOUR(3) TO MINUTE | 4 day 4 hour 59 minute | +004 04:59:00 |
| INTERVAL'+999999:59'HOUR(6) TO MINUTE | 41666 day 15 hour 59 minute | +041666 15:59:00 |
| INTERVAL'-999999:59'HOUR(6) TO MINUTE | -(41666 day 15 hour 59 minute) | -041666 15:59:00 |

<a id="285c3630013352b3"></a>
##### Interval HOUR TO SECOND

다음은 interval HOUR TO SECOND literals를 사용하는 예이다.

<a id="893ed64579cdcc7c"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL '23:59:59.999999'HOUR TO SECOND INTERVAL '00 23:59:59.999999'HOUR TO SECOND | 23 hour 59 minute 59.999999 second | +00 23:59:59.999999 |
| INTERVAL '23:60:59.999999'HOUR TO SECOND | Minute value가 59를 초과하여 에러가 반환된다. | - |
| INTERVAL '23:59:60.999999'HOUR TO SECOND | Second value가 59를 초과하여 에러가 반환된다. | - |
| INTERVAL '99:59:59.9999999'HOUR TO SECOND | Fractional seconds가 반올림되어 100 hour가 되므로 leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL '99:59:59.9999999'HOUR(3) TO SECOND | 4 day 4 hour | +004 04:00:00.000000 |
| INTERVAL '11:22:29.569'HOUR(3) TO SECOND(1) | 11 hour 22 minute 29.6 second | +000 11:22:29.6 |
| INTERVAL '+999999:59:59.999999'HOUR(6) TO SECOND(6) | 41666 day 15 hour 59 minute 59.999999 second | +041666 15:59:59.999999 |
| INTERVAL '-999999:59:59.999999'HOUR(6) TO SECOND(6) | -(41666 day 15 hour 59 minute 59.999999 second) | -041666 15:59:59.999999 |

<a id="04173dd8885ca9da"></a>
##### Interval MINUTE TO SECOND

다음은 interval MINUTE TO SECOND literals를 사용하는 예이다.

<a id="bb90176ec4de585f"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL '15:23.123456'MINUTE TO SECOND INTERVAL '00 00:15:23.123456'MINUTE TO SECOND | 15 minute 23.123456 second | +00 00:15:23.123456 |
| INTERVAL '15:60.123456'MINUTE TO SECOND | second value가 59를 초과하여 에러가 반환된다. | - |
| INTERVAL '99:59.999999'MINUTE TO SECOND(2) | fractional seconds가 반올림되어 100 minute가 되므로, leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL '99:59.999999'MINUTE(3) TO SECOND(2) | 1 hour 40 minute | +000 01:40:00.00 |
| INTERVAL '+999999:59.999999'MINUTE(6) TO SECOND(6) | 694 day 10 hour 39 minute 59.999999 second | +000694 10:39:59.999999 |
| INTERVAL '-999999:59.999999'MINUTE(6) TO SECOND(6) | -(694 day 10 hour 39 minute 59.999999 second) | -000694 10:39:59.999999 |

<a id="bb4ad711fede1ecb"></a>
### Null Value

Null value는 알 수 없는 값 또는 정의되지 않은 값이다. 모든 data type 값이 null value가 될 수 있다.   
Boolean type의 unknown 값은 null value로 대체되어 표현된다.  
Null value는 keyword로 정의되어 있으며 대소문자 구분없이 사용한다.

다음은 null value를 기술하는 예이다.

```
NULL
Null
```

<a id="ce1ba3f06cc825a0"></a>
### Comments

<a id="29a6e645413dcc5e"></a>
#### Single Line Comments

Single line comments는 -- 또는 //로 시작하는 comment 이다. Single line comments는 해당 comment 기호 뒤부터 해당 라인의 끝까지를 comment로 처리한다.

다음은 single line comments를 사용하는 예이다.

```
gSQL> SELECT I1, -- I2, I3,
2 I4, I5
3 FROM T1;

I1        I4        I5       
--------- --------- ---------
column i1 column i4 column i5

1 row selected.


gSQL> SELECT I1, // I2, I3,
2 I4, I5
3 FROM T1;

I1        I4        I5       
--------- --------- ---------
column i1 column i4 column i5

1 row selected.
```

<a id="c76e6cfdd63652d9"></a>
#### Multiple Line Comments

Multiple line comments는 /*로 시작해서 */로 끝나는 comment 이다. Multiple line comments는 /*부터 */까지를 comment로 설정하며 여러 라인에 걸쳐 comment를 기술할 수 있다.

다음은 multiple line comments를 사용하는 예이다.

```
gSQL> SELECT I1, I2, I3, I4, I5
2 /* TABLE T1에 대하여
3    모든 COLUMN들을 출력한다. */
4 FROM T1;

I1        I2        I3        I4        I5       
--------- --------- --------- --------- ---------
column i1 column i2 column i3 column i4 column i5

1 row selected.
```

<a id="fd27bb81cab49e52"></a>
#### Hint Comments

Hint comments는 /*+로 시작하고, */로 끝나는 comment 이다. Hint comments는 multiple line comments와 비슷하지만 시작 기호에 +가 더 있다는 점이 다르다. Hint comments에서 시작기호의 *와 + 사이에 공백이 존재하면 multiple line comments로 처리되는 것에 주의한다.

Hint comments는 다른 comment들과 달리 사용 가능한 위치가 SELECT 키워드의 바로 다음으로 지정되어 있다. Hint comments에는 사용자가 GOLDILOCKS의 optimizer에게 처리 방법 등을 지정하는 내용이 기술되어 있는데 자세한 내용은 [hint clause](16-sql-references.md#a12a3515f3dbcd31)를 참조한다.

다음은 hint comments를 사용하는 예이다.

```
gSQL> SELECT /*+ FULL(T1) */ * FROM T1;

I1        I2        I3        I4        I5       
--------- --------- --------- --------- ---------
column i1 column i2 column i3 column i4 column i5

1 row selected.
```

<a id="d8f816b300dde887"></a>
### SQL Reserved Words and Keywords

<a id="f57ee56262dcc1e9"></a>
#### SQL Reserved Words

GOLDILOCKS에는 SQL reserved words로 지정된 reserved word가 있으며, 해당 SQL reserved words들은 해당 사용 위치가 아닌 곳에서 single quote (') 없이 사용할 수 없다. 하지만 single quote (')를 이용한 SQL reserved words의 사용은 권장하지 않는다.

다음은 GOLDILOCKS SQL reserved words인데 * 표시한 것은 SQL standard에서 명시한 reserved words이다. 해당 리스트는 [V$RESERVED_WORDS](../part-02-administration-manual/9-database-information.md#cdfe387213bbdd08) view를 통해 검색할 수 있다.

ABSOLUTE  
ACCESS  
ALL *  
ALLOCATE *  
ALTER *  
AND *  
ANY *  
ARE *  
AS *  
ASYMMETRIC *  
AT *  
AUTHORIZATION *  
BEGIN *  
BETWEEN *  
BOTH *  
BY *  
CALL *  
CASE *  
CHECK *  
CLOSE *  
COLUMN *  
COMMENT  
COMMIT *  
CONNECT *  
CONSTRAINT *  
CREATE *  
CROSS *  
CURRENT *  
CURRENT_CATALOG *  
CURRENT_DATE *  
CURRENT_DEFAULT_TRANSFORM_GROUP *  
CURRENT_PATH *  
CURRENT_ROLE *  
CURRENT_ROW *  
CURRENT_SCHEMA *  
CURRENT_TIME *  
CURRENT_TIMESTAMP *  
CURRENT_TRANSFORM_GROUP_FOR_TYPE *  
CURRENT_USER *  
DATABASE  
DEALLOCATE *  
DECLARE *  
DEFAULT *  
DELETE *  
DEREF *  
DESCRIBE *  
DETERMINISTIC *  
DISCONNECT *  
DISTINCT *  
DROP *  
ELSE *  
END *  
END_EXEC *  
ESCAPE *  
EXCEPT *  
EXEC *  
EXECUTE *  
EXISTS *  
FALSE *  
FETCH *  
FILTER *  
FIRST  
FOR *  
FOREIGN *  
FREE *  
FROM *  
FULL *  
FUNCTION *  
GET *  
GLOBAL *  
GRANT *  
GROUP *  
HAVING *  
HOLD *  
IDENTIFIED  
IF  
IMMEDIATE  
IN *  
INDICATOR *  
INNER *  
INOUT *  
INSERT *  
INTERSECT *  
INTO *  
IS *  
JOIN *  
LAST  
LEADING *  
LEFT *  
LIKE *  
LIMIT  
LOCAL *  
LOCALTIME *  
LOCALTIMESTAMP *  
MATCH *  
MEMBER *  
MERGE *  
MINUS  
NATURAL *  
NEW *  
NEXT  
NOT *  
NULL *  
OF *  
OFFSET *  
OLD *  
ON *  
OPEN *  
OR *  
ORDER *  
OUT *  
PREPARE *  
PRIMARY *  
PRIOR  
PROCEDURE *  
PROFILE  
REF *  
REFERENCES *  
RELATIVE  
RELEASE *  
RENAME  
RETURN *  
RETURNING  
RETURNS *  
REVOKE *  
RIGHT *  
ROLLBACK *  
ROW *  
ROWID  
ROWS *  
ROW_NUMBER *  
SAVEPOINT *  
SELECT *  
SESSION_USER *  
SET *  
SOME *  
SQL *  
SQLEXCEPTION *  
SQLSTATE *  
SQLWARNING *  
START *  
SYMMETRIC *  
SYNONYM  
SYSDATE  
SYSTEM *  
SYSTEM_USER *  
SYSTIME  
SYSTIMESTAMP  
TABLE *  
THEN *  
TO *  
TRAILING *  
TRIGGER *  
TRUE *  
TRUNCATE *  
UNION *  
UNIQUE *  
UNKNOWN *  
UPDATE *  
UPPER *  
USER *  
USING *  
VALUES *  
VIEW  
WHEN *  
WHENEVER *  
WHERE *  
WINDOW *  
WITH *  
WITHOUT *

<a id="8db95f0b9c509f6c"></a>
#### SQL Keywords

GOLDILOCKS SQL keywords는 reserved word가 아니다. 그러나 GOLDILOCKS 내부적으로 사용하는 keyword이므로 GOLDILOCKS SQL keywords를 사용할 경우 결과의 가독성이 떨어질 수 있어 사용을 권장하지 않는다.

GOLDILOCKS SQL keywords 목록은 [V$KEYWORDS](../part-02-administration-manual/9-database-information.md#e519aa54d5f8822e) view를 통해 검색할 수 있다.

<a id="1743153c8f2afe6a"></a>
### 호환성

Syntax element에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="93756d4903af6872"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| E021-03 | Character literals | O |
| E131 | Null value support (nulls in lieu of values) | O |
| E161 | SQL comments using leading double minus | O |
| F051-01 | DATE data type (including support of DATE literal) | O |
| F051-02 | TIME data type (including support of TIME literal) with fractional seconds precision of at least 0 | O |
| F051-03 | TIMESTAMP data type (including support of TIMESTAMP literal) with fractional seconds precision of at least 0 and 6 | O |
| F271 | Compound character literals | X |
| F383 | Set column not null clause | O |
| F391 | Long identifiers | X |
| F392 | Unicode escapes in identifiers | X |
| F393 | Unicode escapes in literals | X |
| T023 | Compound binary literals | X |
| T024 | Spaces in binary literals | X |
| T101 | Enhanced nullability determination | X |
| T351 | Bracketed comments | X |
| T591 | UNIQUE constraints of possibly null columns | O |
| X041 | Basic table mapping: null absent | X |
| X042 | Basic table mapping: null as nil | X |
| X051 | Advanced table mapping: null absent | X |
| X052 | Advanced table mapping: null as nil | X |
| X170 | XML null handling options | X |
| X400 | Name and identifier mapping | X |

<a id="ff81d005bda1af76"></a>
## Data Type

<a id="bed02aed5e55d00c"></a>
### 숫자 타입

숫자 타입은 크게 저장 방식과 소수부 표현 방식에 따라 구분할 수 있다.

- 저장 방식에 따른 분류 
    - 십진 숫자 타입
        - 십진수 숫자를 100 진법 형태로 저장하는 방식
        - 타입 예: NUMBER, NUMERIC, FLOAT
    - 이진 숫자 타입
        - C 언어의 숫자를 그대로 저장하는 방식
        - 타입 예: NATIVE_INTEGER, NATIVE_DOUBLE

- 소수부 표현 방식에 따른 분류
    - 고정 소수점 타입 (exact numeric)
        - Scale이 고정되어 있는 숫자 타입
        - 타입 예: NUMERIC(precision, scale), NATIVE_INTEGER
    - 부동 소수점 타입 (approximate numeric)
        - Scale이 정해지지 않은 숫자 타입
        - 타입 예: FLOAT (precision), NATIVE_DOUBLE

<a id="3917f51769ee93f1"></a>
#### 십진 숫자 타입

유효 숫자의 정밀도를 나타내는 precision과 소수점의 범위를 나타내는 scale이 십진수 (decimal)를 기반으로 한다.

<a id="0b9b3d4a52571144"></a>
##### 십진 고정 소수점 타입

십진 고정 소수점 타입은 SQL에서 정의한 타입이다.

**십진 고정 소수점 타입**

<a id="712957b2efc247ac"></a>
| Type | Decimal precision | Decimal scale | 참조 |
| --- | --- | --- | --- |
| NUMBER( p ) | p | 0 | [NUMBER](#f5ef3006756aba88) |
| NUMBER( p, s ) | p | s | [NUMBER](#f5ef3006756aba88) |
| NUMERIC( p ) | p | 0 | [NUMERIC](#0f4910fcc7908fb7) |
| NUMERIC( p, s ) | p | s | [NUMERIC](#0f4910fcc7908fb7) |
| DECIMAL( p ) | p | 0 | [NUMERIC](#0f4910fcc7908fb7) 타입의 alias |
| DECIMAL( p, s ) | p | s | [NUMERIC](#0f4910fcc7908fb7) 타입의 alias |
| DEC( p ) | p | 0 | [NUMERIC](#0f4910fcc7908fb7) 타입의 alias |
| DEC( p, s ) | p | s | [NUMERIC](#0f4910fcc7908fb7) 타입의 alias |
| SMALLINT | 5 | 0 | [NUMBER](#f5ef3006756aba88) 타입의 alias |
| INTEGER | 10 | 0 | [NUMBER](#f5ef3006756aba88) 타입의 alias |
| BIGINT | 19 | 0 | [NUMBER](#f5ef3006756aba88) 타입의 alias |
| INT2 | 5 | 0 | [NUMBER](#f5ef3006756aba88) 타입의 alias |
| INT4 | 10 | 0 | [NUMBER](#f5ef3006756aba88) 타입의 alias |
| INT8 | 19 | 0 | [NUMBER](#f5ef3006756aba88) 타입의 alias |

<a id="f531172da90ed784"></a>
##### 십진 부동 소수점 타입

십진 부동 소수점 타입은 SQL에서 정의한 타입이다.

**십진 부동 소수점 타입**

<a id="b80919a5faa0df6b"></a>
| Type | Decimal precision | Decimal scale | 참조 |
| --- | --- | --- | --- |
| NUMBER | 38 | N/A | [NUMBER](#f5ef3006756aba88) |
| FLOAT( p ) | ceil( log<sub>10</sub> 2<sup>p</sup> ) | N/A | [FLOAT](#e13294813a67476a) |
| REAL | ceil( log<sub>10</sub> 2<sup>24</sup> ) = 8 | N/A | [FLOAT](#e13294813a67476a) 타입의 alias |
| DOUBLE | ceil( log<sub>10</sub> 2<sup>53</sup> ) = 16 | N/A | [FLOAT](#e13294813a67476a) 타입의 alias |
| FLOAT4 | ceil( log<sub>10</sub> 2<sup>24</sup> ) = 8 | N/A | [FLOAT](#e13294813a67476a) 타입의 alias |
| FLOAT8 | ceil( log<sub>10</sub> 2<sup>53</sup> ) = 16 | N/A | [FLOAT](#e13294813a67476a) 타입의 alias |

<a id="f284ccc4722b3623"></a>
#### 이진 숫자 타입

유효 숫자의 정밀도를 나타내는 precision과 소수점의 범위를 나타내는 scale이 이진수 (binary)를 기반으로 한다.

<a id="ea1a1191f4ae827f"></a>
##### 이진 고정 소수점 타입

이진 고정 소수점 타입은 C 언어의 signed integer 계열 타입을 참조한다.  
Sign bit를 표시하기 위해 1 bit를 사용하고 나머지 bit들은 precision을 표현하는데 사용하며 scale을 표현할 때는 bit를 사용하지 않는다.

**이진 고정 소수점 타입**

<a id="91a61b41d58e6034"></a>
| Type | Binary precision | Binary scale | 참조 |
| --- | --- | --- | --- |
| NATIVE_SMALLINT | 15 | 0 | [NATIVE_SMALLINT](#ea064187ad5185d3) |
| NATIVE_INTEGER | 31 | 0 | [NATIVE_INTEGER](#63474202cfdaa631) |
| NATIVE_BIGINT | 63 | 0 | [NATIVE_BIGINT](#b67a00fdebfeeee9) |

<a id="ff89989752a3c151"></a>
##### 이진 부동 소수점 타입

이진 부동 소수점 타입은 C 언어의 float과 double 타입을 참조한다.  
Sign bit를 표시하기 위해 1 bit를 사용하고 나머지 bit들은 precision과 scale을 표현하기 위해 사용한다.

**이진 부동 소수점 타입**

<a id="632e41f872333764"></a>
| Type | Binary precision | Binary scale | 참조 |
| --- | --- | --- | --- |
| NATIVE_REAL | 23 | 8 | [NATIVE_REAL](#ed1f221dbc872429) |
| NATIVE_DOUBLE | 52 | 11 | [NATIVE_DOUBLE](#ffb3593324c1f9be) |

> 이진 부동 소수점 타입에 대한 precision과 scale은 OS 및 compiler의 환경에 따라 변동될 수 있다.

<a id="57bbfcc45c9a0694"></a>
### CHARACTER STRING 타입

CHARACTER STRING 타입은 가변길이 문자열 여부와 문자열의 최대 길이에 따라 구분할 수 있다.

- 가변길이 문자열 여부에 따른 분류
    - 고정 길이 문자열
        - [CHARACTER](#0319fe09b264cec3)
    - 가변 길이 문자열
        - [CHARACTER VARYING](#81c2c3704f1da6e2), [CHARACTER LONG VARYING](#1f0e795dfcc56d6a)
- 문자열의 최대 길이에 따른 분류
    - 2000 [ characters 또는 bytes ]
        - [CHARACTER](#0319fe09b264cec3)
    - 4000 [ characters 또는 bytes ]
        - [CHARACTER VARYING](#81c2c3704f1da6e2)
    - 100 megabytes
        - [CHARACTER LONG VARYING](#1f0e795dfcc56d6a)

<a id="69ff0cd18c154045"></a>
### BINARY STRING 타입

BINARY STRING 타입은 가변길이 이진 문자열 여부와 이진 문자열의 최대 길이에 따라 구분할 수 있다.

- 가변길이 이진 문자열 여부에 따른 분류
    - 고정 길이 이진 문자열
        - [BINARY](#56a204fe4b3d1c89)
    - 가변 길이 이진 문자열
        - [BINARY VARYING](#8028b0efef2db632), [BINARY LONG VARYING](#2940bef6c30ffc14)
- 이진 문자열의 최대 길이 따른 분류
    - 2000 
        - [BINARY](#56a204fe4b3d1c89)
    - 4000 
        - [BINARY VARYING](#8028b0efef2db632)
    - 100 megabytes
        - [BINARY LONG VARYING](#2940bef6c30ffc14)

<a id="4462db56759a5475"></a>
### 날짜/ 시간 타입

날짜/ 시간 타입은 년, 월, 일, 시, 분, 초, time zone offset을 각 타입의 표현방식에 맞게 지정한다.  
날짜/ 시간 타입에는 [DATE](#d88d47b21d661aa7), [TIME](#76e4f67c334555fb), [TIMESTAMP](#ed6eadaa110af187) 타입이 있다.

<a id="8ca22f73e379bce8"></a>
### INTERVAL 타입

INTERVAL 타입은 시간 간격을 지정한다.  
년, 월, 일, 시, 분, 초의 시간 간격을 각 타입의 표현방식에 맞게 지정한다.

[INTERVAL](#4ec69af3c45c98df) 타입은 값의 표현 범위에 따라 YEAR TO MONTH 계열과 DAY TO SECOND 계열로 구분할 수 있다.

<a id="512c7e199e74dd01"></a>
### BOOLEAN 타입

BOOLEAN 타입은 TRUE, FALSE, UNKNOWN 값을 저장하며 UNKNOWN일 경우 null 값으로 표현한다. Condition으로 사용된 모든 expression들은 BOOLEAN 값을 반환하며, BOOLEAN type으로 정의된 column 또는 value는 condition으로 사용할 수 있다.

자세한 내용은 [BOOLEAN](#aca2201d031abe41)을 참조한다.

<a id="c06f9fc2bd448628"></a>
### ROWID 타입

데이터베이스에 저장된 모든 레코드는 각기 다른 위치정보를 가지고 있으며, 각각의 레코드를 구분하기 위해 레코드 식별자 (ROWID)를 사용한다.

ROWID 타입은 레코드 식별자 (ROWID)를 저장 관리하기 위한 타입이다.   
ROWID pseudo column을 사용한 질의를 통해 레코드 식별자 (ROWID)를 얻을 수 있다.

자세한 내용은 [ROWID](#e7fd0a43c7fa5340)를 참조한다.

<a id="be2c78a9fcad0b86"></a>
### 타입간 비교

두 타입간의 비교는 하나의 대표 타입을 기준으로 수행된다. 비교 대상 타입이 대표 타입과 다를 경우 타입 변환을 통해 비교할 수도 있다.  
[타입간 비교를 위한 대표 타입](#db9a923724cae7e5)에서는 두 타입간의 비교를 위한 대표 타입을 정의한다.

다음 표에서는 각 대표 타입별로 비교를 위해 대상 타입들을 변환하는 것에 대해 설명한다.

- [VC 에서의 비교를 위한 타입 변환](#227473c0de7c9497)
- [LC 에서의 비교를 위한 타입 변환](#5ed65831f503b83d)
- [VB 에서의 비교를 위한 타입 변환](#853b4079db2c3261)
- [LB 에서의 비교를 위한 타입 변환](#befe01cbbe2daa7d)
- [NB 에서의 비교를 위한 타입 변환](#15fa23e92fbc7cea)
- [ND 에서의 비교를 위한 타입 변환](#b96738c15c602b29)
- [NU 에서의 비교를 위한 타입 변환](#13b4b637a86fe1cc)
- [DA 에서의 비교를 위한 타입 변환](#241844d1abb58b47)
- [TI 에서의 비교를 위한 타입 변환](#c3506b171a4d1ec3)
- [TZ 에서의 비교를 위한 타입 변환](#63acdbaff2ff26a5)
- [TS 에서의 비교를 위한 타입 변환](#fb98dcd262927d0d)
- [SZ 에서의 비교를 위한 타입 변환](#0fe975d58236412e)
- [YM 에서의 비교를 위한 타입 변환](#84cab985377075cf)
- [DS 에서의 비교를 위한 타입 변환](#9be6bfd837063a23)
- [BO 에서의 비교를 위한 타입 변환](#6916535fd7e09492)
- [RI 에서의 비교를 위한 타입 변환](#e16da5989097c0d0)

> 다음은 타입간 비교를 위해 사용하는 약어이다.
> 
> - "`VC`" : CHARACTER VARYING
> - "`LC`" : CHARACTER LONG VARYING
> - "`VB`" : BINARY VARYING
> - "`LB`" : BINARY LONG VARYING
> - "`NB`" : NATIVE_BIGINT
> - "`ND`" : NATIVE_DOUBLE
> - "`NU`" : NUMBER
> - "`DA`" : DATE
> - "`TI`" : TIME
> - "`TZ`" : TIME WITH TIMEZONE
> - "`TS`" : TIMESTAMP
> - "`SZ`" : TIMESTAMP WITH TIMEZONE
> - "`YM`" : INTERVAL YEAR TO MONTH
> - "`DS`" : INTERVAL DAY TO SECOND
> - "`BO`" : BOOLEAN
> - "`RI`" : ROWID
> 

> 타입간 비교 표에서 built-in data type은 축약된 단어를 double quote (")로 묶어서 표기한다. 
> 
> - "CHAR": CHARACTER
> - "VARCHAR": CHARACTER VARYING
> - "LONG VARCHAR": CHARACTER LONG VARYING
> - "VARBINARY": BINARY VARYING
> - "LONG VARBINARY": BINARY LONG VARYING
> - "TIME_TZ": TIME WITH TIMEZONE
> - "TIMESTAMP_TZ": TIMESTAMP WITH TIMEZONE
> - "INTERVAL_YM": INTERVAL YEAR TO MONTH
> - "INTERVAL_DS": INTERVAL DAY TO SECOND
> 

**타입간 비교를 위한 대표 타입**

<a id="db9a923724cae7e5"></a>
| Data type | C H A R | V A R C H A R | L O N G  V A R C H A R | B I N A R Y | V A R B I N A R Y | L O N G  V A R B I N A R Y | N A T I V E  S M A L L I N T | N A T I V E  I N T E G E R | N A T I V E  B I G I N T | N A T I V E  R E A L | N A T I V E  D O U B L E | N U M B E R | N U M E R I C | F L O A T | D A T E | T I M E | T I M E    T Z | T I M E S T A M P | T I M E S T A T M P   T Z | I N T E R V A L  Y M | I N T E R V A L  D S | B O O L E A N | R O W I D |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CHAR | `VC` | `VC` | `LC` |  |  |  | `NU` | `NU` | `NU` | `NU` | `ND` | `NU` | `NU` | `NU` | `DA` | `TI` | `TZ` | `TS` | `SZ` | `YM` | `DS` | `BO` | `RI` |
| VARCHAR | `VC` | `VC` | `LC` |  |  |  | `NU` | `NU` | `NU` | `NU` | `ND` | `NU` | `NU` | `NU` | `DA` | `TI` | `TZ` | `TS` | `SZ` | `YM` | `DS` | `BO` | `RI` |
| LONG VARCHAR | `LC` | `LC` | `LC` |  |  |  | `NU` | `NU` | `NU` | `NU` | `ND` | `NU` | `NU` | `NU` | `DA` | `TI` | `TZ` | `TS` | `SZ` | `YM` | `DS` | `BO` | `RI` |
| BINARY |  |  |  | `VB` | `VB` | `LB` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| VARBINARY |  |  |  | `VB` | `VB` | `LB` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| LONG VARBINARY |  |  |  | `LB` | `LB` | `LB` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| NATIVE_SMALLINT | `NU` | `NU` | `NU` |  |  |  | `NB` | `NB` | `NB` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  | `YM` | `DS` |  |  |
| NATIVE_INTEGER | `NU` | `NU` | `NU` |  |  |  | `NB` | `NB` | `NB` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  | `YM` | `DS` |  |  |
| NATIVE_BIGINT | `NU` | `NU` | `NU` |  |  |  | `NB` | `NB` | `NB` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  | `YM` | `DS` |  |  |
| NATIVE_REAL | `NU` | `NU` | `NU` |  |  |  | `ND` | `ND` | `ND` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  |  |  |  |  |
| NATIVE_DOUBLE | `ND` | `ND` | `ND` |  |  |  | `ND` | `ND` | `ND` | `ND` | `ND` | `ND` | `ND` | `ND` |  |  |  |  |  |  |  |  |  |
| NUMBER | `NU` | `NU` | `NU` |  |  |  | `NU` | `NU` | `NU` | `NU` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  | `YM` | `DS` |  |  |
| NUMERIC | `NU` | `NU` | `NU` |  |  |  | `NU` | `NU` | `NU` | `NU` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  | `YM` | `DS` |  |  |
| FLOAT | `NU` | `NU` | `NU` |  |  |  | `NU` | `NU` | `NU` | `NU` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  | `YM` | `DS` |  |  |
| DATE | `DA` | `DA` | `DA` |  |  |  |  |  |  |  |  |  |  |  | `DA` |  |  | `TS` | `SZ` |  |  |  |  |
| TIME | `TI` | `TI` | `TI` |  |  |  |  |  |  |  |  |  |  |  |  | `TI` | `TZ` |  |  |  |  |  |  |
| TIME_TZ | `TZ` | `TZ` | `TZ` |  |  |  |  |  |  |  |  |  |  |  |  | `TZ` | `TZ` |  |  |  |  |  |  |
| TIMESTAMP | `TS` | `TS` | `TS` |  |  |  |  |  |  |  |  |  |  |  | `TS` |  |  | `TS` | `SZ` |  |  |  |  |
| TIMESTAMP_TZ | `SZ` | `SZ` | `SZ` |  |  |  |  |  |  |  |  |  |  |  | `SZ` |  |  | `SZ` | `SZ` |  |  |  |  |
| INTERVAL_YM | `YM` | `YM` | `YM` |  |  |  | `YM` | `YM` | `YM` |  |  | `YM` | `YM` | `YM` |  |  |  |  |  | `YM` |  |  |  |
| INTERVAL_DS | `DS` | `DS` | `DS` |  |  |  | `DS` | `DS` | `DS` |  |  | `DS` | `DS` | `DS` |  |  |  |  |  |  | `DS` |  |  |
| BOOLEAN | `BO` | `BO` | `BO` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `BO` |  |
| ROWID | `RI` | `RI` | `RI` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `RI` |

**`VC` 에서의 비교를 위한 타입 변환**

<a id="227473c0de7c9497"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | CHAR (변환 없음) |
| VARCHAR | VARCHAR (변환 없음) |

**`LC` 에서의 비교를 위한 타입 변환**

<a id="5ed65831f503b83d"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | CHAR (변환 없음) |
| VARCHAR | VARCHAR (변환 없음) |
| LONG VARCHAR | LONG VARCHAR (변환 없음) |

**`VB` 에서의 비교를 위한 타입 변환**

<a id="853b4079db2c3261"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| BINARY | BINARY (변환 없음) |
| VARBINARY | VARBINARY (변환 없음) |

**`LB` 에서의 비교를 위한 타입 변환**

<a id="befe01cbbe2daa7d"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| BINARY | BINARY (변환 없음) |
| VARBINARY | VARBINARY (변환 없음) |
| LONG VARBINARY | LONG VARBINARY (변환 없음) |

**`NB` 에서의 비교를 위한 타입 변환**

<a id="15fa23e92fbc7cea"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | NATIVE_BIGINT |
| VARCHAR | NATIVE_BIGINT |
| LONG VARCHAR | NATIVE_BIGINT |
| NATIVE_SMALLINT | NATIVE_SMALLINT (변환 없음) |
| NATIVE_INTEGER | NATIVE_INTEGER (변환 없음) |
| NATIVE_BIGINT | NATIVE_BIGINT (변환 없음) |

**`ND` 에서의 비교를 위한 타입 변환**

<a id="b96738c15c602b29"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | NATIVE_DOUBLE |
| VARCHAR | NATIVE_DOUBLE |
| LONG VARCHAR | NATIVE_DOUBLE |
| NATIVE_SMALLINT | NATIVE_SMALLINT (변환 없음) |
| NATIVE_INTEGER | NATIVE_INTEGER (변환 없음) |
| NATIVE_BIGINT | NATIVE_BIGINT (변환 없음) |
| NATIVE_REAL | NATIVE_REAL (변환 없음) |
| NATIVE_DOUBLE | NATIVE_DOUBLE (변환 없음) |
| NUMBER | NUMBER (변환 없음) |
| NUMERIC | NUMERIC (변환 없음) |
| FLOAT | FLOAT (변환 없음) |

**`NU` 에서의 비교를 위한 타입 변환**

<a id="13b4b637a86fe1cc"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | NUMBER |
| VARCHAR | NUMBER |
| LONG VARCHAR | NUMBER |
| NATIVE_SMALLINT | NATIVE_SMALLINT (변환 없음) |
| NATIVE_INTEGER | NATIVE_INTEGER (변환 없음) |
| NATIVE_BIGINT | NATIVE_BIGINT (변환 없음) |
| NATIVE_REAL | NATIVE_REAL (변환 없음) |
| NATIVE_DOUBLE | NATIVE_DOUBLE (변환 없음) |
| NUMBER | NUMBER (변환 없음) |
| NUMERIC | NUMERIC (변환 없음) |
| FLOAT | FLOAT (변환 없음) |

**`DA` 에서의 비교를 위한 타입 변환**

<a id="241844d1abb58b47"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | DATE |
| VARCHAR | DATE |
| LONG VARCHAR | DATE |
| DATE | DATE (변환 없음) |

**`TI` 에서의 비교를 위한 타입 변환**

<a id="c3506b171a4d1ec3"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | TIME |
| VARCHAR | TIME |
| LONG VARCHAR | TIME |
| TIME | TIME (변환 없음) |

**`TZ` 에서의 비교를 위한 타입 변환**

<a id="63acdbaff2ff26a5"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | TIME_TZ |
| VARCHAR | TIME_TZ |
| LONG VARCHAR | TIME_TZ |
| TIME | TIME_TZ |
| TIME_TZ | TIME_TZ (변환 없음) |

**`TS` 에서의 비교를 위한 타입 변환**

<a id="fb98dcd262927d0d"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | TIMESTAMP |
| VARCHAR | TIMESTAMP |
| LONG VARCHAR | TIMESTAMP |
| DATE | DATE (변환 없음) |
| TIMESTAMP | TIMESTAMP (변환 없음) |

**`SZ` 에서의 비교를 위한 타입 변환**

<a id="0fe975d58236412e"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | TIMESTAMP_TZ |
| VARCHAR | TIMESTAMP_TZ |
| LONG VARCHAR | TIMESTAMP_TZ |
| DATE | TIMESTAMP_TZ |
| TIMESTAMP | TIMESTAMP_TZ |
| TIMESTAMP_TZ | TIMESTAMP_TZ (변환 없음) |

**`YM` 에서의 비교를 위한 타입 변환**

<a id="84cab985377075cf"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | INTERVAL_YM |
| VARCHAR | INTERVAL_YM |
| LONG VARCHAR | INTERVAL_YM |
| NATIVE_SMALLINT | INTERVAL_YM |
| NATIVE_INTEGER | INTERVAL_YM |
| NATIVE_BIGINT | INTERVAL_YM |
| NUMBER | INTERVAL_YM |
| NUMERIC | INTERVAL_YM |
| FLOAT | INTERVAL_YM |
| INTERVAL_YM | INTERVAL_YM (변환 없음) |

**`DS` 에서의 비교를 위한 타입 변환**

<a id="9be6bfd837063a23"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | INTERVAL_DS |
| VARCHAR | INTERVAL_DS |
| LONG VARCHAR | INTERVAL_DS |
| NATIVE_SMALLINT | INTERVAL_DS |
| NATIVE_INTEGER | INTERVAL_DS |
| NATIVE_BIGINT | INTERVAL_DS |
| NUMBER | INTERVAL_DS |
| NUMERIC | INTERVAL_DS |
| FLOAT | INTERVAL_DS |
| INTERVAL_DS | INTERVAL_DS (변환 없음) |

**`BO` 에서의 비교를 위한 타입 변환**

<a id="6916535fd7e09492"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | BOOLEAN |
| VARCHAR | BOOLEAN |
| LONG VARCHAR | BOOLEAN |
| BOOLEAN | BOOLEAN (변환 없음) |

**`RI` 에서의 비교를 위한 타입 변환**

<a id="e16da5989097c0d0"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | ROWID |
| VARCHAR | ROWID |
| LONG VARCHAR | ROWID |
| ROWID | ROWID (변환 없음) |

<a id="e2c21b3a3eaedfd1"></a>
### 타입간 변환

타입간 변환은 내부 변환 (implicit type conversion)과 외부 변환 (explicit type conversion)으로 구분된다.

- 내부 변환 (implicit type conversion)은 select, insert, delete, update를 위한 expression, operator, function, condition 들에서 발생한다.
- 외부 변환 (explicit type conversion)은 CAST operator를 통해 이루어진다.

[타입간 변환](#401ee086b2f694c7)에서는 한 data type에서 다른 data type으로의 변환 가능 여부를 설명한다.

> 타입간 변환 표에서 built-in data type은 축약된 문자열을 double quote (")로 묶어서 표기한다. 
> 
> - "CHAR": CHARACTER
> - "VARCHAR": CHARACTER VARYING
> - "LONG VARCHAR": CHARACTER LONG VARYING
> - "VARBINARY": BINARY VARYING
> - "LONG VARBINARY": BINARY LONG VARYING
> - "TIME_TZ": TIME WITH TIMEZONE
> - "TIMESTAMP_TZ": TIMESTAMP WITH TIMEZONE
> - "INTERVAL_YM": INTERVAL YEAR TO MONTH
> - "INTERVAL_DS": INTERVAL DAY TO SECOND
> 

**타입간 변환**

<a id="401ee086b2f694c7"></a>
| Data type | C H A R | V A R C H A R | L O N G  V A R C H A R | B I N A R Y | V A R B I N A R Y | L O N G  V A R B I N A R Y | N A T I V E  S M A L L I N T | N A T I V E  I N T E G E R | N A T I V E  B I G I N T | N A T I V E  R E A L | N A T I V E  D O U B L E | N U M B E R | N U M E R I C | F L O A T | D A T E | T I M E | T I M E    T Z | T I M E S T A M P | T I M E S T A T M P   T Z | I N T E R V A L  Y M | I N T E R V A L  D S | B O O L E A N | R O W I D |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CHAR | O | O | O |  |  |  | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O |
| VARCHAR | O | O | O |  |  |  | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O |
| LONG VARCHAR | O | O | O |  |  |  | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O | O |
| BINARY |  |  |  | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| VARBINARY |  |  |  | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| LONG VARBINARY |  |  |  | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| NATIVE_SMALLINT | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  | O | O |  |  |
| NATIVE_INTEGER | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  | O | O |  |  |
| NATIVE_BIGINT | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  | O | O |  |  |
| NATIVE_REAL | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  |  |  |  |  |
| NATIVE_DOUBLE | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  |  |  |  |  |
| NUMBER | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  | O | O |  |  |
| NUMERIC | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  | O | O |  |  |
| FLOAT | O | O | O |  |  |  | O | O | O | O | O | O | O | O |  |  |  |  |  | O | O |  |  |
| DATE | O | O | O |  |  |  |  |  |  |  |  |  |  |  | O |  |  | O | O |  |  |  |  |
| TIME | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  | O | O |  |  |  |  |  |  |
| TIME_TZ | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  | O | O |  |  |  |  |  |  |
| TIMESTAMP | O | O | O |  |  |  |  |  |  |  |  |  |  |  | O | O |  | O | O |  |  |  |  |
| TIMESTAMP_TZ | O | O | O |  |  |  |  |  |  |  |  |  |  |  | O | O | O | O | O |  |  |  |  |
| INTERVAL_YM | O | O | O |  |  |  | O | O | O |  |  | O | O | O |  |  |  |  |  | O |  |  |  |
| INTERVAL_DS | O | O | O |  |  |  | O | O | O |  |  | O | O | O |  |  |  |  |  |  | O |  |  |
| BOOLEAN | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | O |  |
| ROWID | O | O | O |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | O |

- CHARACTER 타입으로의 변환
    - 원본 타입이 CHARACTER 타입인 경우
        - 원본 타입의 precision이 CHARACTER 타입의 precision보다 큰 경우 에러가 발생한다.
        - 원본 타입의 precision이 CHARACTER 타입의 precision과 같은 경우 문자열이 갱신되지 않는다.
        - 원본 타입의 precision이 CHARACTER 타입의 precision보다 작은 경우 precision 차이만큼 문자열 뒤에 공백 문자가 추가된다.
    - 원본 타입이 CHARACTER VARYING 타입 또는 CHARACTER LONG VARYING 타입인 경우
        - 원본 타입의 문자열 길이가 CHARACTER 타입의 precision보다 큰 경우 에러가 발생한다.
        - 원본 타입의 문자열 길이가 CHARACTER 타입의 precision과 같은 경우 문자열이 갱신되지 않는다.
        - 원본 타입의 문자열 길이가 CHARACTER 타입의 precision보다 작은 경우 precision 차이만큼 문자열 뒤에 공백 문자가 추가된다.
    - 원본 타입이 숫자형 타입, 날짜/시간 타입, INTERVAL 타입, BOOLEAN 타입, ROWID 타입인 경우
        - 원본 타입의 변환 문자열 길이가 CHARACTER 타입의 precision보다 큰 경우 에러가 발생한다.
        - 원본 타입의 변환 문자열 길이가 CHARACTER 타입의 precision과 같으면 문자열이 갱신되지 않는다.
        - 원본 타입의 변환 문자열 길이가 CHARACTER 타입의 precision보다 작은 경우 precision 차이만큼 문자열 뒤에 공백 문자가 추가된다.

- CHARACTER VARYING 타입으로의 변환
    - 원본 타입이 CHARACTER 타입인 경우
        - 원본 타입의 precision이 CHARACTER VARYING 타입의 precision보다 큰 경우 에러가 발생한다.
        - 원본 타입의 precision이 CHARACTER VARYING 타입의 precision과 같거나 작은 경우 문자열이 갱신되지 않는다.
    - 원본 타입이 CHARACTER VARYING 타입, CHARACTER LONG VARYING 타입인 경우
        - 원본 타입의 문자열의 길이가 CHARACTER VARYING 타입의 precision보다 큰 경우 에러가 발생한다.
        - 원본 타입의 문자열의 길이가 CHARACTER VARYING 타입의 precision과 같거나 작은 경우 문자열이 갱신되지 않는다.
    - 원본 타입이 숫자형 타입, 날짜/ 시간 타입, INTERVAL 타입, BOOLEAN 타입, ROWID 타입인 경우
        - 원본 타입의 변환 문자열 길이가 CHARACTER VARYING 타입의 precision보다 큰 경우 에러가 발생한다. 
        - 원본 타입의 변환 문자열 길이가 CHARACTER VARYING 타입의 precision과 같거나 작은 경우 문자열이 갱신되지 않는다.

- CHARACTER LONG VARYING 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - 원본 타입의 문자열이 갱신되지 않는다.
    - 원본 타입이 숫자형 타입, 날짜/시간 타입, INTERVAL 타입, BOOLEAN 타입, ROWID 타입인 경우
        - 원본 타입의 변환 문자열이 갱신되지 않는다.

- BINARY 타입으로의 변환
    - 원본 타입이 BINARY 타입인 경우
        - 원본 타입의 precision이 BINARY 타입의 precision보다 큰 경우 에러가 발생한다.
        - 원본 타입의 precision이 BINARY 타입의 precision과 같은 경우 이진 문자열이 갱신되지 않는다.
        - 원본 타입의 precision이 BINARY 타입의 precision보다 작은 경우 precision 차이만큼 이진 문자열 뒤에 X'00' 문자가 추가된다.
    - 원본 타입이 BINARY VARYING 타입 또는 BINARY LONG VARYING 타입인 경우
        - 원본 타입의 이진 문자열의 길이가 BINARY 타입의 precision보다 큰 경우 에러가 발생한다.
        - 원본 타입의 이진 문자열의 길이가 BINARY 타입의 precision과 같은 경우 이진 문자열이 갱신되지 않는다.
        - 원본 타입의 이진 문자열의 길이가 BINARY 타입의 precision보다 작은 경우 precision 차이만큼 이진 문자열 뒤에 X'00' 문자가 추가된다.

- BINARY VARYING 타입으로의 변환
    - 원본 타입이 BINARY 타입인 경우
        - 원본 타입의 precision이 BINARY VARYING 타입의 precision보다 큰 경우 에러가 발생한다.
        - 원본 타입의 precision이 BINARY VARYING 타입의 precision과 같거나 작은 경우 이진 문자열이 갱신되지 않는다.
    - 원본 타입이 BINARY VARYING 타입, BINARY LONG VARYING 타입인 경우
        - 원본 타입의 이진 문자열의 길이가 BINARY VARYING 타입의 precision보다 큰 경우 에러가 발생한다.
        - 원본 타입의 이진 문자열의 길이가 BINARY VARYING 타입의 precision과 같거나 작은 경우 이진 문자열이 갱신되지 않는다.

- BINARY LONG VARYING 타입으로의 변환
    - 원본 타입이 BINARY STRING 타입인 경우 원본 타입의 이진 문자열이 갱신되지 않는다.

- 숫자형 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - 숫자 형식에 맞지 않는 문자열이 오는 경우 에러가 발생한다.
        - 변환 타입에 정의된 precision 및 scale에 의해 overflow가 발생하거나 반올림 될 수 있다.
    - 원본 타입이 숫자형 타입인 경우
        - 변환 타입에 정의된 precision 및 scale에 의해 overflow가 발생하거나 반올림 될 수 있다.
    - 원본 타입이 INTERVAL 타입인 경우
        - 원본 타입이 single field (YEAR, MONTH, DAY, HOUR, MINUTE, SECOND)인 경우만 숫자형 타입으로 변환할 수 있다.
        - 변환 타입에 정의된 precision 및 scale에 의해 overflow가 발생하거나 반올림 될 수 있다.

- DATE 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - DATE format 형식에 맞지 않는 문자열이 오는 경우 에러가 발생한다.
        - 변환 타입에 정의된 값의 범위에 의해 overflow가 발생할 수 있다.
    - 원본 타입이 DATE 타입, TIMESTAMP 타입인 경우
        - 에러가 발생하지 않는다.
    - 원본 타입이 TIMESTAMP WITH TIME ZONE 타입인 경우
        - time zone offset을 고려하여 DATE 타입 값으로 변환한다.

- TIME 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - TIME format 형식에 맞지 않는 문자열이 오는 경우 에러가 발생한다.
        - 변환 타입에 정의된 값의 범위에 의해 반올림될 수 있다.
    - 원본 타입이 TIME 타입, TIMESTAMP 타입인 경우
        - 에러가 발생하지 않는다.
    - 원본 타입이 TIME WITH TIME ZONE 타입, TIMESTAMP WITH TIME ZONE 타입인 경우
        - time zone offset을 고려하여 TIME 타입 값으로 변환한다.

- TIME WITH TIME ZONE 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - TIME WITH TIME ZONE format 형식에 맞지 않는 문자열이 오는 경우 에러가 발생한다.
        - 변환 타입에 정의된 값의 범위에 의해 반올림될 수 있다.
    - 원본 타입이 TIME 타입, TIME WITH TIME ZONE 타입, TIMESTAMP WITH TIME ZONE 타입인 경우
        - time zone offset을 고려하여 TIME WITH TIME ZONE 타입 값으로 변환한다.

- TIMESTAMP 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - TIMESTAMP format 형식에 맞지 않는 문자열이 오는 경우 에러가 발생한다.
        - 변환 타입에 정의된 값의 범위에 의해 overflow가 발생하거나 반올림될 수 있다.
    - 원본 타입이 DATE 타입, TIMESTAMP 타입인 경우
        - 에러가 발생하지 않는다.
    - 원본 타입이 TIMESTAMP WITH TIME ZONE 타입인 경우
        - time zone offset을 고려하여 TIMESTAMP 타입 값으로 변환한다.

- TIMESTAMP WITH TIME ZONE 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - TIMESTAMP WITH TIME ZONE format 형식에 맞지 않는 문자열이 오는 경우 에러가 발생한다.
        - 변환 타입에 정의된 값의 범위에 의해 overflow가 발생하거나 반올림될 수 있다.
    - 원본 타입이 DATE 타입, TIMESTAMP 타입, TIMESTAMP WITH TIME ZONE 타입인 경우
        - time zone offset을 고려하여 TIMESTAMP WITH TIME ZONE 타입 값으로 변환한다.

- INTERVAL YEAR TO MONTH 계열 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - year-month interval literal 형식에 맞지 않는 문자열이 오는 경우 에러가 발생한다.
        - 자세한 내용은 [Interval Literals](#074711f4a241633b)를 참조한다.
        - 변환 타입에 정의된 precision에 의해 overflow가 발생할 수 있다.
    - 원본 타입이 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, NUMBER, NUMERIC, FLOAT 타입인 경우
        - 변환 타입이 single field (YEAR, MONTH)이어야 한다.
        - 변환 타입에 정의된 precision에 의해 overflow가 발생할 수 있다.
    - 원본 타입이 INTERVAL YEAR TO MONTH 계열 타입인 경우
        - 변환 타입에 정의된 precision에 의해 overflow가 발생할 수 있다.

- INTERVAL DAY TO SECOND 계열 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - day-time interval literal 형식에 맞지 않는 문자열이 오는 경우 에러가 발생한다.
        - 자세한 내용은 [Interval Literals](#074711f4a241633b)를 참조한다.
        - 변환 타입에 정의된 precision에 의해 overflow가 발생하거나 반올림될 수 있다.
    - 원본 타입이 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, NUMBER, NUMERIC, FLOAT 타입인 경우
        - 변환 타입이 single field (DAY, HOUR, MINUTE, SECOND)이어야 한다.
        - 변환 타입에 정의된 precision에 의해 overflow가 발생하거나 반올림이 발생할 수 있다.
    - 원본 타입이 INTERVAL DAY TO SECOND 계열 타입인 경우
        - 변환 타입에 정의된 precision에 의해 overflow가 발생하거나 반올림이 발생할 수 있다.

- BOOLEAN 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - 대소문자 구분 없이 문자열이 "TRUE" 또는 "FALSE"인 경우에 변환할 수 있다. (앞뒤에 공백이 있는 경우에도 변환 가능)
    - 원본 타입이 BOOLEAN 타입인 경우
        - 에러가 발생하지 않는다.

- ROWID 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - ROWID format 형식에 맞지 않는 문자열이 오는 경우 에러가 발생한다.
    - 원본 타입이 ROWID 타입인 경우
        - 에러가 발생하지 않는다.

<a id="7485cb6ab1cbfdec"></a>
### 타입간 조합

<a id="448eca632344c03c"></a>
#### 타입간 조합이 필요한 경우

CASE 연산자와 집합 연산자 ([set operator](16-sql-references.md#96acd09fad234c3f))는 다수의 expression을 연산 결과로 가진다.  
다음 예와 같이 각 expression들이 서로 다른 타입을 가질 경우, 결과 타입을 결정해 주어야 한다.

- CASE 연산자

```
SELECT CASE expr WHEN expr THEN char(3)
                 WHEN expr THEN char(5)
                 ELSE char(1)
       END   
  FROM t1;
```

- 집합 연산자

```
SELECT float_column
  FROM t1
UNION ALL
SELECT number_precision_column
  FROM t2
UNION ALL
SELECT native_integer_column
  FROM t3;
```

타입간 조합에 의한 결과 타입 결정에 적용되는 규칙이 있는데 다음은 그 규칙을 적용하는 예이다.

- 결과 타입 조합 규칙
    - 집합 연산자 ([set operator](16-sql-references.md#96acd09fad234c3f))
    - CASE 연산자 
        - [CASE Expression](#25a5758ca7ff8136)
        - [COALESCE](#ec78cb861c06c7fb)
        - [NULLIF](#4d135921ffce1c85)

<a id="08f567244d3c0586"></a>
#### 결과 타입 조합 규칙

각 expression의 data type은 조합 가능한 동일한 계열의 타입이어야 한다.

- 결과 타입 조합 규칙이 적용되는 예
    - 집합 연산자 ([set operator](16-sql-references.md#96acd09fad234c3f))
    - CASE 연산자 
        - [CASE Expression](#25a5758ca7ff8136)
        - [COALESCE](#ec78cb861c06c7fb)
        - [NULLIF](#4d135921ffce1c85)

결과 타입 조합 규칙에 따른 결과 타입은 아래 표에서 설명한다.

> 다음은 결과 타입 조합 규칙을 설명하기 위해 사용하는 약어이다.
> 
> - "`VC`" : CHARACTER VARYING
> - "`LC`" : CHARACTER LONG VARYING
> - "`VB`" : BINARY VARYING
> - "`LB`" : BINARY LONG VARYING
> - "`NS`" : NATIVE_SMALLINT
> - "`NI`" : NATIVE_INTEGER
> - "`NB`" : NATIVE_BIGINT
> - "`NR`" : NATIVE_REAL
> - "`ND`" : NATIVE_DOUBLE
> - "`FL`" : FLOAT
> - "`NU`" : NUMBER
> - "`DA`" : DATE
> - "`TI`" : TIME
> - "`TZ`" : TIME WITH TIMEZONE
> - "`TS`" : TIMESTAMP
> - "`SZ`" : TIMESTAMP WITH TIMEZONE
> - "`YM`" : INTERVAL YEAR TO MONTH
> - "`DS`" : INTERVAL DAY TO SECOND
> - "`BO`" : BOOLEAN
> - "`RI`" : ROWID
> 

> 결과 타입 조합 규칙에 따른 결과 타입 표에서 built-in data type은 축약된 문자열을 double quote (")로 묶어서 표기한다. 
> 
> - "CHAR": CHARACTER
> - "VARCHAR": CHARACTER VARYING
> - "LONG VARCHAR": CHARACTER LONG VARYING
> - "BINARY": BINARY
> - "VARBINARY": BINARY VARYING
> - "LONG VARBINARY": BINARY LONG VARYING
> - "TIME_TZ": TIME WITH TIMEZONE
> - "TIMESTAMP_TZ": TIMESTAMP WITH TIMEZONE
> - "INTERVAL_YM": INTERVAL YEAR TO MONTH
> - "INTERVAL_DS": INTERVAL DAY TO SECOND
> 

**결과 타입 조합 규칙에 따른 결과 타입**

<a id="278cd9c6ae66504e"></a>
| Data type | C H A R | V A R C H A R | L O N G  V A R C H A R | B I N A R Y | V A R B I N A R Y | L O N G  V A R B I N A R Y | N A T I V E  S M A L L I N T | N A T I V E  I N T E G E R | N A T I V E  B I G I N T | N A T I V E  R E A L | N A T I V E  D O U B L E | N U M B E R | N U M E R I C | F L O A T | D A T E | T I M E | T I M E    T Z | T I M E S T A M P | T I M E S T A T M P   T Z | I N T E R V A L  Y M | I N T E R V A L  D S | B O O L E A N | R O W I D |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CHAR | `VC` | `VC` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| VARCHAR | `VC` | `VC` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| LONG VARCHAR |  |  | `LC` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| BINARY |  |  |  | `VB` | `VB` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| VARBINARY |  |  |  | `VB` | `VB` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| LONG VARBINARY |  |  |  |  |  | `LB` |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| NATIVE_SMALLINT |  |  |  |  |  |  | `NS` | `NI` | `NB` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  |  |  |  |  |
| NATIVE_INTEGER |  |  |  |  |  |  | `NI` | `NI` | `NB` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  |  |  |  |  |
| NATIVE_BIGINT |  |  |  |  |  |  | `NB` | `NB` | `NB` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  |  |  |  |  |
| NATIVE_REAL |  |  |  |  |  |  | `ND` | `ND` | `ND` | `NR` | `ND` | `ND` | `ND` | `ND` |  |  |  |  |  |  |  |  |  |
| NATIVE_DOUBLE |  |  |  |  |  |  | `ND` | `ND` | `ND` | `ND` | `ND` | `ND` | `ND` | `ND` |  |  |  |  |  |  |  |  |  |
| NUMBER |  |  |  |  |  |  | `NU` | `NU` | `NU` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  |  |  |  |  |
| NUMERIC |  |  |  |  |  |  | `NU` | `NU` | `NU` | `ND` | `ND` | `NU` | `NU` | `NU` |  |  |  |  |  |  |  |  |  |
| FLOAT |  |  |  |  |  |  | `NU` | `NU` | `NU` | `ND` | `ND` | `NU` | `NU` | `FL ` |  |  |  |  |  |  |  |  |  |
| DATE |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `DA` |  |  | `TS` | `SZ` |  |  |  |  |
| TIME |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `TI` | `TZ` |  |  |  |  |  |  |
| TIME_TZ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `TZ` | `TZ` |  |  |  |  |  |  |
| TIMESTAMP |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `TS` |  |  | `TS` | `SZ` |  |  |  |  |
| TIMESTAMP_TZ |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `SZ` |  |  | `SZ` | `SZ` |  |  |  |  |
| INTERVAL_YM |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `YM` |  |  |  |
| INTERVAL_DS |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `DS` |  |  |
| BOOLEAN |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `BO` |  |
| ROWID |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | `RI` |

- 모두 CHAR 타입인 경우의 결과 타입 결정
    - Length가 다를 경우, VARCHAR
    - Length가 같을 경우, CHAR
- 모두 BINARY 타입인 경우의 결과 타입 결정
    - Length가 다를 경우, VARBINARY
    - Length가 같을 경우, BINARY
- INTERVAL YEAR TO MONTH 형의 결과 타입 결정
    - YEAR와 MONTH가 혼재되어 있다면, INTERVAL YEAR TO MONTH
    - YEAR만 존재할 경우, INTERVAL YEAR
    - MONTH만 존재할 경우, INTERVAL MONTH
- INTERVAL DAY TO SECOND 형의 결과 타입 결정
    - Start field는 각 대상 expression 중 가장 큰 범위의 start field
    - End field는 각 대상 expression 중 가장 작은 범위의 end field
    - 예: {INTERVAL DAY, INTERVAL HOUR} → INTERVAL DAY TO HOUR
- 결과 타입의 precision, scale 결정
    - CHARACTER STRING 형
        - 대상 expression 중 최대 문자 길이
    - BINARY STRING 형
        - 대상 expression 중 최대 문자 길이
    - 숫자형
        - 해당 타입의 value를 최대로 수용할 수 있는 범위로 지정한다.
    - TIME/TIMESTAMP 형
        - 대상 expression 중 최대 fractional seconds precision
    - INTERVAL YEAR TO MONTH
        - 대상 expression 중 최대 leading precision
    - INTERVAL DAY TO SECOND
        - Leading precision은 start field의 maximum leading precision
        - Fractional seconds precision은 maximum fractional seconds precision
- 자세한 내용은 [타입간 비교](#be2c78a9fcad0b86)를 참조한다.

<a id="c2e29747facb56ef"></a>
### 호환성

Data type에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="32a59171e8707727"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B033 | Untyped SQL-invoked function arguments | X |
| E011-01 | INTEGER and SMALLINT data types | O |
| E011-02 | REAL, DOUBLE PRECISION, and FLOAT data types | O |
| E011-03 | DECIMAL and NUMERIC data types | X |
| E011-04 | Arithmetic operators | O |
| E011-05 | Numeric comparison | O |
| E011-06 | Implicit casting among the numeric data types | O |
| E021-01 | CHARACTER data type | O |
| E021-02 | CHARACTER VARYING data type | O |
| E021-03 | Character literals | O |
| E021-04 | CHARACTER_LENGTH function | O |
| E021-05 | OCTET_LENGTH function | O |
| E021-06 | SUBSTRING function | O |
| E021-07 | Character concatenation | O |
| E021-08 | UPPER and LOWER functions | O |
| E021-09 | TRIM function | O |
| E021-10 | Implicit casting among the fixed-length and variable-length character string types | O |
| E021-11 | POSITION function | O |
| E021-12 | Character comparison | O |
| E071-05 | Columns combined via table operators need not have exactly the same data type | O |
| F051-01 | DATE data type (including support of DATE literal) | O |
| F051-02 | TIME data type (including support of TIME literal) with fractional seconds precision of at least 0 | O |
| F051-03 | TIMESTAMP data type (including support of TIMESTAMP literal) with fractional seconds precision of at least 0 and 6 | O |
| F051-04 | Comparison predicate on DATE, TIME, and TIMESTAMP data types | X |
| F051-05 | Explicit CAST between datetime types and character string types | O |
| F054 | TIMESTAMP in DATE type precedence list | X |
| F382 | Alter column data type | O |
| F611 | Indicator data types | X |
| F741 | Referential MATCH types | X |
| J521 | JDBC data types | X |
| J622 | external Java types | X |
| S011-01 | USER_DEFINED_TYPES view | X |
| S023 | Basic structured types | X |
| S024 | Enhanced structured types | X |
| S025 | Final structured types | X |
| S026 | Self-referencing structured types | X |
| S041 | Basic reference types | X |
| S043 | Enhanced reference types | X |
| S051 | Create table of type | X |
| S071 | SQL paths in function and type name resolution | X |
| S091-01 | Arrays of built-in data types | X |
| S091-02 | Arrays of distinct types | X |
| S092 | Arrays of user-defined types | X |
| S094 | Arrays of reference types | X |
| S161 | Subtype treatment | X |
| S162 | Subtype treatment for references | X |
| S201-02 | Array as result type of functions | X |
| S231 | Structured type locators | X |
| S261 | Specific type method | X |
| S272 | Multisets of user-defined types | X |
| S274 | Multisets of reference types | X |
| S281 | Nested collection types | X |
| S401 | Distinct types based on array types | X |
| S402 | Distinct types based on distinct types | X |
| T021 | BINARY and VARBINARY data types | O |
| T022 | Advanced support for BINARY and VARBINARY data types | O |
| T031 | BOOLEAN data type | O |
| T041 | Basic LOB data type support | X |
| T042 | Extended LOB data type support | X |
| T051 | Row types | X |
| T071 | BIGINT data type | O |
| T201 | Comparable data types for referential constraints | X |
| T322 | Declared data type attributes | X |
| X010 | XML type | X |
| X011 | Arrays of XML type | X |
| X012 | XMultisets of XML type | X |
| X013 | Distinct types of XML type | X |
| X014 | Attributes of XML type | X |
| X015 | Fields of XML type | X |
| X181 | XML(DOCUMENT(UNTYPED)) type | X |
| X182 | XML(DOCUMENT(ANY)) type | X |
| X190 | XML(SEQUENCE) type | X |
| X191 | XML(DOCUMENT(XMLSCHEMA)) type | X |
| X192 | XML(CONTENT(XMLSCHEMA)) type | X |
| X231 | XML(CONTENT(UNTYPED)) type | X |
| X232 | XML(CONTENT(ANY)) type | X |
| X251 | Persistent XML values of XML(DOCUMENT(UNTYPED)) type | X |
| X252 | Persistent XML values of XML(DOCUMENT(ANY)) type | X |
| X253 | Persistent XML values of XML(CONTENT(UNTYPED)) type | X |
| X254 | Persistent XML values of XML(CONTENT(ANY)) type | X |
| X255 | Persistent XML values of XML(SEQUENCE) type | X |
| X256 | Persistent XML values of XML(DOCUMENT(XMLSCHEMA)) type | X |
| X257 | Persistent XML values of XML(CONTENT(XMLSCHEMA)) type | X |
| X260 | XML type: ELEMENT clause | X |
| X261 | XML type: NAMESPACE without ELEMENT clause | X |
| X263 | XML type: NO NAMESPACE with ELEMENT clause | X |
| X264 | XML type: schema location | X |
| X410 | Alter column data type: XML type | X |

<a id="1a41de329d17e6ed"></a>
## Format 문자열

Format 문자열은 숫자 타입이나 날짜/ 시간 타입을 문자열로 변환하거나 문자열을 숫자 타입이나 날짜/ 시간 타입으로 변환하기 위한 형식을 정의한 문자열이다.

- 숫자 타입이나 날짜/시간 타입을 문자열로 변환할 때 다음과 같은 형식으로 문자열을 표현한다.
    - [TO_CHAR( number )](#d0f1dcb76f6a4884), [TO_CHAR( datetime )](#1aa9ef481e07ad64)
    - 숫자 타입: TO_CHAR( 1234.56, 'S9,999.99' ) → '+1,234.56'
    - 날짜/시간 타입: TO_CHAR( SYSDATE, 'YYYY-MM-DD' ) → '2012-07-15'
- 문자열을 숫자 타입이나 날짜/ 시간 타입으로 변환할 때 다음과 같은 형식으로 문자열을 표현한다.
    - [TO_NUMBER](#391976f1ebfbe1b4), [TO_NATIVE_REAL](#9227dcb27754ec3b), [TO_NATIVE_DOUBLE](#e2adb0785ea15c2a) 
    - [TO_DATE](#45c8ee60f5aa8084) 
    - [TO_TIMESTAMP](#e11d27a423dbc46c), [TO_TIMESTAMP_WITH_TIME_ZONE](#deb069ec65b335a1)
    - [TO_TIME](#c6462fe8a092223a), [TO_TIME_WITH_TIME_ZONE](#132b267c45037442) 
    - 숫자 타입: TO_NUMBER( '+1,234.56', 'S9,999.99' ) → NUMBER TYPE
    - 날짜/ 시간 타입: TO_DATE( '2012-07-15', 'YYYY-MM-DD' ) → DATE TYPE

Format 문자열은 다음과 같은 타입으로 구분된다.  
• 숫자 타입: [Number Format 문자열](#5f09922ffd9417b0)  
• 날짜/ 시간 타입: [Datetime Format 문자열](#6c90db97831852f6)

<a id="5f09922ffd9417b0"></a>
### Number Format 문자열

Number format 문자열은 숫자 타입을 문자열로 변환하거나 문자열을 숫자 타입으로 변환하기 위한 형식을 정의한 문자열이다.

Number format 문자열은 [TO_CHAR( number )](#d0f1dcb76f6a4884), [TO_NUMBER](#391976f1ebfbe1b4), [TO_NATIVE_REAL](#9227dcb27754ec3b), [TO_NATIVE_DOUBLE](#e2adb0785ea15c2a) 함수의 인자로 사용된다.

Number format 문자열에는 표현하고자 하는 형식에 따라 여러 개의 format element를 지정할 수 있다.

모든 number format element는 그 형식에 맞게 반올림하여 적용한다.  
변환하고자 하는 value의 소수점 이전 digit 개수가 format 문자열에 지정된 숫자의 자리수보다 큰 경우, '#' 문자로 대체된다.  
MI, S, PR의 부호를 표현하는 format element를 지정하지 않은 경우, 음수는 숫자 앞에 '-' 부호를 양수는 공백을 반환하는 방식으로 부호를 표현한다.

**Number format elements**

<a id="e2970d7f9ad0a1a2"></a>
| Format  element | 예제 | 설명 |
| --- | --- | --- |
| , (comma) | 9,999 | 지정한 위치에 comma를 반환한다.  Comma를 여러 개 지정할 수 있다.  Format 문자열은 comma로 시작할 수 없고 소수점 (.) 이후에도 올 수 없다. |
| . (period) | 99.99 | 지정한 위치에 소수점 (.)을 반환한다. Format 문자열 내에서 소수점은 한 번만 지정할 수 있다. |
| $ | $9999 | 숫자 앞에 $ 기호를 반환한다. |
| 0 | 0999  9990 | 숫자 앞이나 끝에 0을 반환한다. 변환하고자 하는 value의 digit 개수가 format 문자열의 0 위치까지의 digit 개수보다 작은 경우, 차이나는 부분을 0으로 채워 반환한다. |
| 9 | 9999 | 부호와 명시된 9의 개수에 맞게 공백과 숫자를 반환한다. 변환하고자 하는 value의 digit 개수가 명시된 9의 개수보다 작은 경우, 차이나는 부분을 공백으로 채워 반환한다. 음수인 경우 숫자 앞에 '-' 부호를 양수는 공백을 반환하는 방식으로 부호를 표현한다. Format 문자열 소수점 이전의 정수부로 표현되는 값이 0인 경우, 이 0은 공백으로 반환된다. 예: TO_CHAR( 0.123, '9.999' ) → .123 예: TO_CHAR( 0, '9' ) → 0 |
| B | B9999 | 값이 0이 되는 경우, 공백을 반환한다. |
| EEEE | 9.9EEEE | 지수 표기법으로 반환한다. Format 문자열의 맨 마지막에 오거나, S, MI, PR 앞에 올 수 있다. Comma (,)와 함께 지정할 수 없다. |
| MI | 9999MI | 음수인 경우 숫자 끝에 '-' 를 양수인 경우 공백을 반환한다. Format 문자열의 마지막에만 지정할 수 있고, S, PR과 함께 지정할 수 없다. |
| PR | 9999PR | 음수인 경우 꺽쇠 괄호 안에 숫자를 반환한다. &lt;숫자&gt; 양수인 경우 숫자 앞뒤에 공백을 반환한다. Format 문자열의 마지막에만 지정할 수 있고, S, MI와 함께 지정할 수 없다. |
| RN  rn | RN rn | 로마 숫자를 대문자로 반환한다. 로마 숫자를 소문자로 반환한다. 1 ~ 3999 사이의 숫자에서만 반환된다. FM format element 이외의 다른 format element와는 함께 지정할 수 없다. TO_NUMBER 함수에는 사용할 수 없다. |
| S | S9999 9999S | 양수인 경우 숫자 앞에 '+' 부호를 음수인 경우 '-' 부호를 반환한다. (S9999) 양수인 경우 숫자 끝에 '+' 부호를 음수인 경우 '-' 부호를 반환한다. (9999S) Format 문자열의 맨처음 또는 맨마지막에만 지정할 수 있다. MI, PR과 함께 지정할 수 없다. |
| V | 999V99 | V format element 뒤에 오는 9의 digit 개수가 n일 때, value에 10<sup>n</sup> 을 곱한 값을 반환한다.  소수점 (.)과 함께 지정할 수 없다. TO_NUMBER 함수에는 사용할 수 없다. |
| X | XXXX xxxx | 지정된 X digit 수에 맞게 공백과 16 진수를 반환한다. 정수값을 16 진수로 반환한다. (정수가 아닌 경우, 반올림하여 정수값을 만든다.) XXXX는 16 진수 대문자를 xxxx는 16 진수 소문자를 반환한다. 변환된 16 진수의 digit 개수가 명시된 X의 개수보다 작은 경우, 차이나는 부분을 공백으로 채워 반환한다. 0과 양의 정수만 처리하고, 음수인 경우 '#' 문자로 대체된다. Format element 0 및 FM과만 함께 지정할 수 있으며, 다른 format element와는 함께 지정할 수 없다. |
| FM | FM | 앞 뒤 공백을 제거하여 왼쪽 정렬되는 효과를 반환한다. 숫자 앞뒤에 붙는 공백을 제거한다. 9 format element에 의해 소수점 이하에 추가된 0을 제거한다. |

다음은 number format 문자열을 사용하는 예이다.

```
TO_CHAR( 12345, '99,999' )           : ' 12,345'
TO_CHAR( 123456789, '999,999,999' )  : ' 123,456,789'
TO_CHAR( 12.345, '99.999' )          : ' 12.345'
TO_CHAR( 1234.56, '$9,999.99' )      : ' $1,234.56'
TO_CHAR( 123, '099999' )             : ' 000123'
TO_CHAR( 0.2, '0.9' )                : ' 0.2'
TO_CHAR( 123.45, '999999.99' )       : '    123.45'
TO_CHAR( -123.45, '999999.99' )      : '   -123.45'
TO_CHAR( 123.45, 'FM999999.99' )     : '123.45'
TO_CHAR( -123.45, 'FM999999.99' )    : '-123.45'
TO_CHAR( 12345.67, '999.99' )        : '#######'
TO_CHAR( 123.100567, '999.999' )     : ' 123.101'
TO_CHAR( 0.2, '90.99' )              : '  0.20'
TO_CHAR( 0.2, '99.99' )              : '   .20'
TO_CHAR( 0, '90.99' )                : '  0.00'
TO_CHAR( 0, 'B90.99' )               : '      '
TO_CHAR( 123.45, '9.9EEEE' )         : '  1.2E+02'
TO_CHAR( 123.45, '999.99MI' )        : '123.45 '
TO_CHAR( -123.45, '999.99MI' )       : '123.45-'
TO_CHAR( 123.45, '999.99PR' )        : ' 123.45 '
TO_CHAR( -123.45, '999.99PR' )       : '<123.45>'
TO_CHAR( 123, 'RN' )                 : '         CXXIII'
TO_CHAR( 123, 'rn' )                 : '         cxxiii'
TO_CHAR( 123, 'FMRN' )               : 'CXXIII'
TO_CHAR( 4000, 'RN' )                : '###############'
TO_CHAR( 123.45, 'S999.99' )         : '+123.45'
TO_CHAR( -123.45, 'S999.99' )        : '-123.45'
TO_CHAR( 123.45, '999.99S' )         : '123.45+'
TO_CHAR( -123.45, '999.99S' )        : '123.45-'
TO_CHAR( 123.45, '999V999' )         : ' 123450'
TO_CHAR( 123, 'XX' )                 : ' 7B'
TO_CHAR( 123, 'xx' )                 : ' 7b'
TO_CHAR( 45678, 'XXXXXXX' )          : '    B26E'
TO_CHAR( 45678, 'FMXXXXXXX' )        : 'B26E'
TO_CHAR( 123.45, '99,999.999999' )   : '    123.450000'
TO_CHAR( 123.45, 'FM99,999.999999' ) : '123.45'
```

<a id="6c90db97831852f6"></a>
### Datetime Format 문자열

Datetime format 문자열은 날짜/ 시간 타입을 문자열로 변환하거나 문자열을 날짜/ 시간 타입으로 변환하기 위한 형식을 정의한 문자열이다.

Datetime format 문자열은 [TO_CHAR( datetime )](#1aa9ef481e07ad64), [TO_DATE](#45c8ee60f5aa8084), [TO_TIMESTAMP](#e11d27a423dbc46c), [TO_TIMESTAMP_WITH_TIME_ZONE](#deb069ec65b335a1), [TO_TIME](#c6462fe8a092223a), [TO_TIME_WITH_TIME_ZONE](#132b267c45037442) 함수의 인자로 사용된다.

날짜/ 시간 타입의 경우, format 문자열을 지정하지 않으면 default 값으로 처리되는데, 각 타입의 default 값은 session property인 NLS_*_FORMAT에 지정된 값이다.

- DATE: [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#39cb46c447575199)
- TIMESTAMP: [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#db86968fe3d06d6e)
- TIMESTAMP WITH TIME ZONE: [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#3356e96838139b8a)
- TIME: [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#2524063f770de1b8)
- TIME WITH TIME ZONE: [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#838ff7f06a1cc0ac)

NLS_*_FORMAT 값들은 [ALTER SESSION SET property_name](16-sql-references.md#824f5c01b1aa6faa) 구문으로 변경할 수 있다.

Datetime format 문자열에는 표현하고자 하는 형식에 따라 여러 개의 format element를 지정할 수 있다.

**Datetime format elements**

<a id="64a8b6a95bf806d2"></a>
<table><thead><tr><th align="center" valign="middle">Format<br>element</th><th align="center" valign="middle">TO_*<br>datetime<br>사용여부</th><th align="center" valign="middle">설명</th></tr></thead><tbody><tr><td valign="middle">-<br>/<br>,<br>.<br>;<br>:<br>"text"<br>특수문자</td><td valign="middle">Y</td><td valign="middle">지정된 위치에 format element의 문자를 반환한다.</td></tr><tr><td valign="middle">AD<br>A.D.</td><td valign="middle">Y</td><td valign="middle">서기</td></tr><tr><td valign="middle">AM<br>A.M.</td><td valign="middle">Y</td><td valign="middle">오전</td></tr><tr><td valign="middle">BC<br>B.C.</td><td valign="middle">Y</td><td valign="middle">기원전</td></tr><tr><td valign="middle">CC</td><td valign="middle">N</td><td valign="middle">세기<br>네 자리 연도 중 마지막 두 자리가 01 ~ 99 이면 처음 두 자리에 1을 더한 값을 반환한다. (예: 2005년도일 경우 21)<br>네 자리 연도 중 마지막 두 자리가 00 이면, 처음 두 자리 값이 반환된다. (예: 2000년도일 경우 20)</td></tr><tr><td valign="middle">D</td><td valign="middle">Y</td><td valign="middle">일주일 중 몇 번째 날인지를 반환한다. (1 ~ 7)<br>일요일 (1) ~ 토요일 (7)</td></tr><tr><td valign="middle">DAY<br>Day<br>day</td><td valign="middle">Y</td><td valign="middle">요일을 반환한다. (예: SUNDAY )<br><ul><li>DAY: 모두 대문자로 반환한다.</li><li>Day: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>day: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">DD</td><td valign="middle">Y</td><td valign="middle">달의 몇 번째 날인지를 반환한다. (1 ~ 31)</td></tr><tr><td valign="middle">DDD</td><td valign="middle">Y</td><td valign="middle">연도의 몇 번째 날인지를 반환한다. (1 ~ 366)</td></tr><tr><td valign="middle">DY<br>Dy<br>dy</td><td valign="middle">Y</td><td valign="middle">요일의 약어를 반환한다. (예: SUN)<br><ul><li>DY: 모두 대문자로 반환한다.</li><li>Dy: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>dy: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">FF[1..6]</td><td valign="middle">Y</td><td valign="middle">Fractional seconds를 FF 이후에 지정한 숫자 (1 ~ 6)의 개수만큼 반환한다.<br>숫자를 지정하지 않은 경우, 기본값은 6이다. (FF는 FF6과 같다.)<br>Fractional seconds의 digit 개수가 FF 이후에 지정한 숫자보다 많으면 버림처리된다.<br>Fractional seconds의 digit 개수가 FF 이후에 지정한 숫자보다 적으면 지정된 숫자에 맞추어 0이 추가된다.<br>DATE 타입에서는 사용할 수 없다.</td></tr><tr><td valign="middle">HH<br>HH12</td><td valign="middle">Y</td><td valign="middle">시간 (1 ~ 12)</td></tr><tr><td valign="middle">HH24</td><td valign="middle">Y</td><td valign="middle">시간 (0 ~ 23)</td></tr><tr><td valign="middle">IW</td><td align="left" valign="middle">N</td><td valign="middle">ISO 8601 표준에 정의된 calendar week (1 ~ 52주 또는 1 ~ 53주)로 지정된 연도의 첫 번째 목요일이 있는 주가 첫 번째 주가 된다.<br><ul><li>Calendar week는 monday부터 시작한다.</li><li>First calendar week는 1월 4일을 포함한다.</li><li>First calendar week는 12월 29, 30, 31을 포함할 수 있다.</li><li>Last calendar week는 1월 1, 2, 3을 포함할 수 있다.</li></ul></td></tr><tr><td valign="middle">IYYY</td><td align="left" valign="middle">N</td><td valign="middle">ISO 8601 표준에 정의된 calendar week를 수용하는 4자리 연도이다.</td></tr><tr><td valign="middle">IYY<br>IY<br>I</td><td align="left" valign="middle">N</td><td valign="middle">ISO 8601 표준에 정의된 calendar week를 수용하는 3자리 연도이다.<br>ISO 8601 표준에 정의된 calendar week를 수용하는 2자리 연도이다.<br>ISO 8601 표준에 정의된 calendar week를 수용하는 1자리 연도이다.</td></tr><tr><td valign="middle">J</td><td valign="middle">Y</td><td valign="middle">BC 4714-11-24 일부터 경과한 날짜를 반환한다.</td></tr><tr><td valign="middle">MI</td><td valign="middle">Y</td><td valign="middle">분 (0 ~ 59)</td></tr><tr><td valign="middle">MM</td><td valign="middle">Y</td><td valign="middle">월 (01 ~ 12), 1월 (01) ~ 12월 (12)</td></tr><tr><td valign="middle">MON<br>Mon<br>mon</td><td valign="middle">Y</td><td valign="middle">월의 약어 (예: JAN) 이다.<br><ul><li>MON: 모두 대문자로 반환한다.</li><li>Mon: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>mon: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">MONTH<br>Month<br>month</td><td valign="middle">Y</td><td valign="middle">월의 이름 (예: JANUARY) 이다.<br><ul><li>MONTH: 모두 대문자로 반환한다.</li><li>Month: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>month: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">PM<br>P.M.</td><td valign="middle">Y</td><td valign="middle">오후</td></tr><tr><td valign="middle">Q</td><td valign="middle">N</td><td valign="middle">연도의 분기 (1 ~ 4) 이다.<br>1월에서 3월 (1) ~ 10월에서 12월 (4) 이다.</td></tr><tr><td valign="middle">RM<br>Rm<br>rm</td><td valign="middle">Y</td><td valign="middle">월을 로마숫자로 반환한다. (예: I)<br><ul><li>RM: 모두 대문자로 반환한다.</li><li>Rm: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>rm: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">RR</td><td valign="middle">Y</td><td valign="middle">조정된 두 자리 연도이다.<br>RR로 표현된 두 자리 연도를 네 자리 연도로 표현하는 방법은 다음과 같다.<br><ul><li>RR로 표현된 두 자리 연도가 00 ~ 49인 경우<br><ul><li>현재 연도의 마지막 두 자리가 00 ~ 50 이면,<br><ul><li>현재 연도의 처음 두 자리와 RR로 표현된 두 자리 연도</li></ul></li><li>현재 연도의 마지막 두 자리가 51 ~ 99 이면,<br><ul><li>(현재 연도의 처음 두 자리 + 1)와 RR로 표현된 두 자리 연도</li></ul></li></ul></li><li>RR로 표현된 두 자리 연도가 50 ~ 99 인 경우<br><ul><li>현재 연도의 마지막 두 자리가 00 ~ 50 이면,<br><ul><li>(현재 연도의 처음 두 자리 - 1 )와 RR로 표현된 두 자리 연도</li></ul></li><li>현재 연도의 마지막 두 자리가 51 ~ 99 이면,<br><ul><li>현재 연도의 처음 두 자리와 RR로 표현된 두 자리 연도</li></ul></li></ul></li></ul></td></tr><tr><td valign="middle">RRRR</td><td valign="middle">Y</td><td valign="middle">조정된 네 자리 연도이다.<br>네 자리 또는 두 자리로 입력받을 수 있다.<br>두 자리로 입력받을 경우, RR과 동일하게 처리된다.</td></tr><tr><td valign="middle">SS</td><td valign="middle">Y</td><td valign="middle">초 (0 ~ 59)</td></tr><tr><td valign="middle">SSSSS</td><td valign="middle">Y</td><td valign="middle">지난 자정을 기준으로 경과된 초 (0 ~ 86399) 이다.</td></tr><tr><td valign="middle">TZH</td><td valign="middle">Y</td><td valign="middle">Time zone hour 이다.<br>DATE, TIMESTAMP, TIME 타입에서는 사용할 수 없고, TIMESTAMP WITH TIME ZONE, TIME WITH TIME ZONE 타입에서만 사용할 수 있다.</td></tr><tr><td valign="middle">TZM</td><td valign="middle">Y</td><td valign="middle">Time zone minute 이다.<br>DATE, TIMESTAMP, TIME 타입에서는 사용할 수 없고, TIMESTAMP WITH TIME ZONE, TIME WITH TIME ZONE 타입에서만 사용할 수 있다.</td></tr><tr><td valign="middle">WW</td><td valign="middle">N</td><td valign="middle">연도의 몇 번째 주 (1 ~ 53) 인지를 반환한다.<br>첫 번째 주 1은 1월 1일부터 7일까지이다.</td></tr><tr><td valign="middle">W</td><td valign="middle">N</td><td valign="middle">월의 몇 번째 주 (1 ~ 5)인지 반환한다.<br>첫 번째 주 1은 월의 1일부터 7일까지이다.</td></tr><tr><td valign="middle">Y,YYY</td><td valign="middle">Y</td><td valign="middle">Comma가 포함된 Y,YYY 형식의 연도를 반환한다.</td></tr><tr><td valign="middle">YYYY<br>SYYYY</td><td valign="middle">Y</td><td valign="middle">네자리 연도이다.<br>SYYYY는 BC 연도인 경우 '-' 부호를 반환한다.</td></tr><tr><td valign="middle">YYY<br>YY<br>Y</td><td valign="middle">Y</td><td valign="middle"><ul><li>YYY: 현재 연도의 마지막 3자리 연도이다.</li><li>YY: 현재 연도의 마지막 2자리 연도이다.</li><li>Y: 현재 연도의 마지막 1자리 연도이다.</li></ul></td></tr></tbody></table>

다음은 datetime format 문자열을 사용하는 예이다.

```
* - / , . ; : "text" Special character 
  • TO_CHAR( TO_DATE( '2012-07-15 03:30:30', 'YYYY-MM-DD HH12:MI:SS' ),
             'YYYY/MM/DD HH12:MI:SS' )
    ==> '2012/07/15 03:30:30'
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 
             'YYYY"year" DDD"th day"' )
    ==> '2012year 197th day'
```

```
* AD
  • TO_CHAR( TO_DATE( '2012-07-15 AD', 'YYYY-MM-DD AD' ), 'YYYY AD' )
    ==> '2012 AD'
  • TO_CHAR( TO_DATE( '0001-01-01 BC', 'YYYY-MM-DD AD'), 'YYYY AD' )
    ==> '0001 BC'

* BC 
  • TO_CHAR( TO_DATE( '0001-01-01 BC', 'YYYY-MM-DD BC'), 'YYYY BC' )
    ==> '0001 BC'
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'YYYY BC' )
    ==> '2012 AD'
```

```
* AM
  • TO_CHAR( TO_DATE( '2012-07-15 03:30:30 AM',
                      'YYYY-MM-DD HH12:MI:SS AM' ),
             'HH12:MI:SS AM' )
    ==> '03:30:30 AM'
  • TO_CHAR( TO_DATE( '2012-07-15 21:30:30', 'YYYY-MM-DD HH24:MI:SS' ),
             'HH12:MI:SS AM' )
    ==> '09:30:30 PM'

* PM 
  • TO_CHAR( TO_DATE( '2012-07-15 03:30:30', 
                      'YYYY-MM-DD HH24:MI:SS' ), 
             'HH12:MI:SS PM' )
    ==> '03:30:30 AM'
  • TO_CHAR( TO_DATE( '2012-07-15 09:30:30 PM', 
                      'YYYY-MM-DD HH12:MI:SS PM' ), 
             'HH12:MI:SS PM' )
    ==> '09:30:30 PM'
```

```
* CC
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'CC' )
    ==> '21'
```

```
* D
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'D' )
    ==> '1'

* DD
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'DD' )
    ==>  '15'

* DDD
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'DDD' )
    ==> '197'
```

```
* DAY
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'DAY' )
    ==> 'SUNDAY   '
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'Day' )
    ==> 'Sunday   '
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'day' )
    ==> 'sunday   '

* DY
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'DY' )
    ==> 'SUN'
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'Dy' )
    ==> 'Sun'
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'dy' )
    ==> 'sun'
```

```
* FF[1 ... 6]
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 03:30:45.123456', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'FF' )
    ==> '123456'
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 03:30:45.123456', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'FF5' )
    ==> '12345'
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 03:30:45.9',
                           'YYYY-MM-DD HH24:MI.SS.FF1' ) , 
             'FF6' )
    ==> '900000'
```

```
* HH HH12 HH24
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 03:30:45.123456', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'HH12' )
    ==> '03'
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 23:30:45.123456', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'HH12' )
    ==> '11'
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 23:30:45.123456', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'HH24' )
    ==> '23'
```

```
* IW
  • TO_CHAR( DATE'2016-01-01', 'IW' )
    ==> 53
  • TO_CHAR( DATE'2014-12-30', 'IW' )
    ==> 01
```

```
* IYYY
  • TO_CHAR( DATE'2016-01-01', 'IYYY' )
    ==> 2015
  • TO_CHAR( DATE'2014-12-30', 'IYYY' )
    ==> 2015

* IYY
  • TO_CHAR( DATE'2016-01-01', 'IYY' )
    ==> 015

* IY
  • TO_CHAR( DATE'2016-01-01', 'IY' )
    ==> 15

* I
  • TO_CHAR( DATE'2016-01-01', 'I' )
    ==> 5
```

```
* J
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'J' )
    ==> '2456124'
  • TO_CHAR( TO_DATE( '2456124', 'J' ), 'YYYY-MM-DD' )
    ==> '2012-07-15'
```

```
* MI
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 23:30:45.123456', 
             'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'MI' ) 
    ==> '30'
```

```
* MM
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 23:30:45.123456', 
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'MM' )
    ==> '07'
```

```
* MON
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'MON' )
    ==> 'JUL'
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'Mon' )
    ==> 'Jul'
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'mon' )
    ==> 'jul'

* MONTH
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'MONTH' )
    ==> 'JULY     '
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'Month' )
    ==> 'July     '
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'month' )
    ==> 'july     '
```

```
* Q
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'Q' )
    ==> '3'
```

```
* RM
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'RM' )
    ==> 'VII ' 
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'Rm' )
    ==> 'Vii '
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'rm' )
    ==> 'vii '
```

```
* RR, RRRR ( 현재연도가 2014 인 경우 )
  • TO_CHAR( TO_DATE( '49-07-15', 'RR-MM-DD' ), 'RRRR' )
    ==> '2049'
  • TO_CHAR( TO_DATE( '49-07-15', 'RR-MM-DD' ), 'YYYY' )
    ==> '2049'
  • TO_CHAR( TO_DATE( '50-07-15', 'RR-MM-DD' ), 'RRRR' )
    ==> '1950'
  • TO_CHAR( TO_DATE( '50-07-15', 'RR-MM-DD' ), 'YYYY' )
    ==> '1950'
  • TO_CHAR( TO_DATE( '50-07-15', 'YY-MM-DD' ), 'RRRR' )
    ==> '2050'
  • TO_CHAR( TO_DATE( '49-07-15', 'RRRR-MM-DD' ), 'YYYY' )
    ==> '2049'
  • TO_CHAR( TO_DATE( '50-07-15', 'RRRR-MM-DD' ), 'YYYY' )
    ==> '1950'

* RR, RRRR ( 현재연도가 2051 인 경우 )
  • TO_CHAR( TO_DATE( '49-07-15', 'RR-MM-DD' ), 'RRRR' )
    ==> '2149'
  • TO_CHAR( TO_DATE( '49-07-15', 'RR-MM-DD' ), 'YYYY' )
    ==> '2149'
  • TO_CHAR( TO_DATE( '50-07-15', 'RR-MM-DD' ), 'RRRR' )
    ==> '2050'
  • TO_CHAR( TO_DATE( '50-07-15', 'RR-MM-DD' ), 'YYYY' )
    ==> '2050'
  • TO_CHAR( TO_DATE( '50-07-15', 'YY-MM-DD' ), 'RRRR' )
    ==> '2050'
  • TO_CHAR( TO_DATE( '49-07-15', 'RRRR-MM-DD' ), 'YYYY' )
    ==> '2149'
  • TO_CHAR( TO_DATE( '50-07-15', 'RRRR-MM-DD' ), 'YYYY' )
    ==> '2050'
```

```
* SS
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 23:30:45.123456',
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'SS' )
    ==> '45' 

* SSSSS
  • TO_CHAR( TO_TIMESTAMP( '2012-07-15 23:30:45.123456',
                           'YYYY-MM-DD HH24:MI:SS.FF6' ), 
             'SSSSS' )
    ==> '84645'
```

```
* TZH 
  • TO_CHAR( TO_TIMESTAMP_TZ( '2012-07-15 23:30:45.123456 +09:00',
                              'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM' ),
             'TZH' )
    ==> '+09'

* TZM
  • TO_CHAR( TO_TIMESTAMP_TZ( '2012-07-15 23:30:45.123456 +09:00',
                              'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM' ),
             'TZM' )
    ==> '00'

  • TO_CHAR( TO_TIMESTAMP_TZ( '2012-07-15 23:30:45.123456 +09:00',
                              'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM' ),
             'TZH:TZM' )
    ==> '+09:00'
```

```
* WW
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'WW' )
    ==> '29'

* W
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'W' )
    ==> '3'
```

```
* Y,YYY
  • TO_CHAR( TO_DATE( '2,012-07-15', 'Y,YYY-MM-DD' ), 'Y,YYY' )
    ==> '2,012'

* YYYY
  • TO_CHAR( TO_DATE( '2012-07-15', 'YYYY-MM-DD' ), 'YYYY' )
    ==> '2012'

* SYYYY
  • TO_CHAR( TO_DATE( '-0001-01-01', 'SYYYY-MM-DD' ), 'SYYYY' )
    ==> '-0001' 

* YYY
  • TO_CHAR( TO_DATE( '012-07-15', 'YYY-MM-DD' ), 'YYY' )
    ==> '012'
  • TO_CHAR( TO_DATE( '012-07-15', 'YYY-MM-DD' ), 'YYYY' )
    ==> '2012' ( (현재 연도 / 1000년)이 2 인 경우 )

* YY
  • TO_CHAR( TO_DATE( '12-07-15', 'YY-MM-DD' ), 'YY' )
    ==> '12'
  • TO_CHAR( TO_DATE( '12-07-15', 'YY-MM-DD' ), 'YYYY' )
    ==> '2012' ( (현재 연도 / 100년)이 20 인 경우 ) 
    ==> '2112' ( (현재 연도 / 100년)이 21 인 경우 ) 

* Y
  • TO_CHAR( TO_DATE( '2-07-15', 'Y-MM-DD' ), 'Y' )
    ==> '2'
  • TO_CHAR( TO_DATE( '12-07-15', 'YY-MM-DD' ), 'YYYY' )
    ==> '2012' ( (현재 연도 / 10년)이 201 인 경우 )
    ==> '2052' ( (현재 연도 / 10년)이 205 인 경우 )
```

<a id="5fa008eecf52b881"></a>
## Expressions

Expression은 데이터 값을 얻기 위한 value, operator, function 들의 조합이다.

Expression이 사용될 수 있는 SQL 구문의 위치는 다음과 같다.  
• SELECT target절  
• SELECT의 GROUP BY절  
• SELECT의 ORDER BY절  
• SELECT의 WHERE절, HAVING절  
• INSERT VALUES절  
• UPDATE SET절  
• INSERT, DELETE, UPDATE의 RETURN절

Expression 형태는 다음과 같이 다양하다.  
• Simple expression  
• Compound expresssion  
• Boolean value expression  
• Case expression  
• Datetime expression  
• Scalar subquery expression  
• Sequence manipulation expression

Simple expression: Column, pseudo columns, literals, null value  
Compound expression: 여러 개의 expression의 조합

자세한 내용은 다음을 참조한다.  
• [Null Value](#bb4ad711fede1ecb)  
• [Literals](#883ce6c883c33aba)  
• [Pseudo Columns](#312afb1d747de97f)  
• [Operators](#fff79de2e130d4d5)  
• [Functions](#e59cfd4bcf0333be)

<a id="16df199ca75b8233"></a>
### Boolean Value Expression

<a id="cba1a3c64c558cb4"></a>
#### 구문

```
<boolean value expression> ::=
        <boolean term>
      | <boolean value expression> OR <boolean term>

<boolean term> ::=
        <boolean factor>
      | <boolean term> AND <boolean factor>

<boolean factor> ::=
        [ NOT ] <boolean test>

<boolean test> ::=
        <boolean primary> [ IS [ NOT ] <truth value> ]

<truth value> ::=
        TRUE
      | FALSE
      | UNKNOWN

<boolean primary> ::=
        <column>
        <condition>
      | <boolean predicand>

<boolean predicand> ::=
        <parenthesized boolean value expression>
      | <nonparenthesized value expression primary>

<parenthesized boolean value expression> ::=
        <left paren> <boolean value expression> <right paren>
```

<a id="b781b7ddb2313780"></a>
#### 설명

&lt;boolean value expression&gt;은 boolean value를 기술한다. Boolean value를 갖는 &lt;boolean primary&gt;는 &lt;column&gt;과 &lt;condition&gt;, &lt;boolean predicand&gt;가 있다. &lt;column&gt;의 경우 BOOLEAN type으로 선언되어야 하고 CAST를 이용하여 boolean value를 반환할 수도 있다.

&lt;boolean value expression&gt;은 AND나 OR, NOT 등과 같은 논리 연산자와 함께 사용할 수 있으며 boolean value만의 연산자인 IS, IS NOT을 지원한다.

&lt;boolean test&gt;에 기술된 IS, IS NOT 연산자는 &lt;boolean primary&gt;에 기술된 boolean value가 &lt;truth value&gt;인 TRUE, FALSE, UNKNOWN 중 하나와 일치하는지 여부를 판단한다.

자세한 내용은 [Conditions](#4900f8e290fa6cb1)를 참조한다.

<a id="d4c2985c390ad227"></a>
#### 사용 예

```
gSQL> SELECT * FROM T1 WHERE CAST('TRUE' AS BOOLEAN);

I1   
-----
TRUE 
FALSE
null 

3 rows selected.

gSQL> SELECT * FROM T1 WHERE I1;

I1  
----
TRUE

1 row selected.

gSQL> SELECT * FROM T1 WHERE I1 IS TRUE;

I1  
----
TRUE

1 row selected.

gSQL> SELECT * FROM T1 WHERE I1 IS NOT FALSE;

I1  
----
TRUE
null

2 rows selected.

gSQL> SELECT * FROM T1 WHERE I1 IS UNKNOWN;

I1  
----
null

1 row selected.
```

<a id="25a5758ca7ff8136"></a>
### CASE Expression

<a id="a890d0cb05eaeab7"></a>
#### 구문

```
<case expression> ::=
        <simple case>
      | <searched case>

<simple case> ::=
        CASE expr WHEN comparison_expr THEN result 
                 [ WHEN comparison_expr THEN result ... ] 
                 [ ELSE result ]
        END

<searched case> ::=
        CASE WHEN condition THEN result
             [ WHEN condition THEN result ... ] 
             [ ELSE result ]
        END
```

<a id="3f795c7223fddb5d"></a>
#### 설명

CASE 문에 기술된 순서대로 WHEN ... THEN 절을 평가한다.  
비교 결과가 FALSE이면, TRUE가 나올 때까지 이후의 WHEN ... THEN 절을 평가한다.  
비교 결과가 TRUE이면, result를 반환하고 이후는 평가하지 않는다.

• Simple case   
&nbsp;&nbsp;CASE expr과 WHEN ... THEN 절의 comparison_expr을 equal 연산 (expr = comparison_expr)으로 평가한다.  
• Searched case  
&nbsp;&nbsp;WHEN ... THEN 절의 condition을 평가한다.

WHEN 절을 평가한 결과가 모두 FALSE인 경우에는 ELSE 절의 result를 반환한다.  
ELSE 절이 생략된 경우, result로 NULL을 반환한다.

THEN 또는 ELSE 절의 result에 여러 type이 오는 경우, [결과 타입 조합 규칙](#08f567244d3c0586)에 따라 result type을 결정한다.

자세한 내용은 다음을 참조한다.  
• [COALESCE](#ec78cb861c06c7fb)  
• [NULLIF](#4d135921ffce1c85)

<a id="1ebfba4a956320e8"></a>
#### 사용 예

- Simple case

```
gSQL> SELECT I1,
             CASE I1 WHEN 1 THEN 'ONE'
                     WHEN 2 THEN 'TWO'
                     ELSE 'NUMBER'
             END AS CASE_RESULT1,
             CASE I1 WHEN 1 THEN 'ONE'
                     WHEN 2 THEN 'TWO'
             END AS CASE_RESULT2
        FROM T1;
I1 CASE_RESULT1 CASE_RESULT2
-- ------------ -----------
 1 ONE          ONE        
 2 TWO          TWO        
 3 NUMBER       null       
3 rows selected.
```

- Searched case

```
gSQL> SELECT I1,
             CASE WHEN I1 = 1 THEN 'ONE'
                  WHEN I1 = 2 THEN 'TWO'
                  ELSE 'NUMBER'    
             END AS CASE_RESULT1,
             CASE WHEN I1 = 1 THEN 'ONE'
                  WHEN I1 = 2 THEN 'TWO'
             END AS CASE_RESULT2 
        FROM T1;
I1 CASE_RESULT1 CASE_RESULT2
-- ------------ ------------
 1 ONE          ONE         
 2 TWO          TWO         
 3 NUMBER       null        
3 rows selected.
```

<a id="25f846dd80e02a05"></a>
### CAST specification

<a id="645f34009da43473"></a>
#### 구문

```
CAST( expression AS data_type )
```

<a id="896414d78ed2c612"></a>
#### 설명

CAST는 expression의 데이터 타입을 지정된 data_type의 데이터 타입으로 변환한다.

<a id="a6440cdab8a53c1e"></a>
#### 사용 예

```
gSQL> SELECT CAST( '1-2' AS INTERVAL YEAR TO MONTH ) AS RESULT FROM DUAL;  
RESULT
------
+01-02
1 row selected.
```

<a id="7c4c39b41b2341ba"></a>
### Scalar Subquery Expression

Scalar subquery expression은 하나의 column을 갖는 row 하나를 결과값으로 반환하는 subquery 이다. Scalar subquery expression의 결과값은 subquery의 &lt;select list&gt;에 기술한 값이다.

만약 subquery가 0개의 row를 반환한다면 결과값은 NULL이며, 둘 이상의 row를 반환한다면 에러로 처리된다.

Scalar subquery expression은 expression을 기술하는 대부분의 위치에 기술할 수 있는데 subquery를 기술할 때는 반드시 괄호로 묶어야 한다. 함수 등의 인자로 사용되어 괄호 안에 scalar subquery expression이 기술되는 경우에도 함수의 괄호와 별도로 subquery를 위한 괄호로 묶어야 하며 그렇지 않은 경우 에러로 처리된다.

다음은 scalar subquery expression을 사용하는 예이다.

```
gSQL> select * from dual where dummy = (select * from dual);

DUMMY
-----
X    

1 row selected.

gSQL> select sum(select 1 from dual) from dual;

ERR-42000(40000): syntax error 
select sum(select 1 from dual) from dual
...........^    ^
Error at line 1

gSQL> select sum((select 1 from dual)) from dual;

SUM((SELECT 1 FROM DUAL))
-------------------------
                        1

1 row selected.
```

<a id="e7e5ef045ec8fa20"></a>
### 호환성

Expression에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="cd7c2f45d160dd79"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| E121-03 | Value expressions in ORDER BY clause | O |
| F051-05 | Basic date and time Explicit CAST between datetime types and character string types | O |
| F201 | CAST function | O |
| F261-01 | Simple CASE | O |
| F261-02 | Searched CASE | O |
| F261-03 | NULLIF | O |
| F261-04 | COALESCE | O |
| F263 | Comma-separated predicates in simple CASE expression | X |
| F301 | CORRESPONDING in query expressions | X |
| F385 | Drop column generation expression clause | X |
| F561 | Full value expressions | X |
| F846 | Octet support in regular expression operators | X |
| F847 | Nonconstant regular expressions | X |
| F850 | Top-level &lt;order by clause&gt; in &lt;query expression&gt; | O |
| F855 | Nested &lt;order by clause&gt; in &lt;query expression&gt; | O |
| F856 | Nested &lt;fetch first clause&gt; in &lt;query expression&gt; | O |
| F857 | Top-level &lt;fetch first clause&gt; in &lt;query expression&gt; | O |
| F861 | Top-level &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| F863 | Nested &lt;result offset clause&gt; in &lt;query expression&gt; | O |
| S091-03 | Arrays expressions | X |
| S111 | ONLY in query expressions | X |
| T121 | WITH (excluding RECURSIVE) in query expression | X |
| T581 | Regular expression substring function | X |

<a id="312afb1d747de97f"></a>
## Pseudo Columns

Pseudo column은 function과 유사하지만, pseudo column을 수행할 때 row 단위로 매번 다른 값을 반환할 수 있다는 점에서 table의 column과도 유사하다.

**지원되는 pseudo column**

<a id="68e793146b0cd87c"></a>
<table><tbody><tr><th align="center">이름</th><th align="center">설명</th><th align="center">참고</th></tr><tr><td align="left" valign="middle">CURRVAL</td><td align="left" valign="middle">Sequence와 관련있는 pseudo column이다.</td><td align="left" valign="middle"><a href="#49d99dc28cf285f7">CURRVAL</a></td></tr><tr><td align="left" valign="middle">NEXTVAL</td><td align="left" valign="middle">Sequence와 관련있는 pseudo column이다.</td><td align="left" valign="middle"><a href="#70c21c39c64fbe45">NEXTVAL</a></td></tr><tr><td align="left" valign="middle">ROWNUM</td><td align="left" valign="middle">조건을 만족하는 row의 번호이다.</td><td align="left" valign="middle"><a href="#f113e3c31c86a705">ROWNUM</a></td></tr><tr><td align="left" valign="middle">ROWID</td><td align="left" valign="middle">데이터베이스 내의 레코드 식별자를 반환한다.</td><td align="left" valign="middle"><a href="#79cc06caf35b0f50">ROWID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_GROUP_ID</td><td align="left" valign="middle">레코드가 저장된 group의 식별자를 반환한다.</td><td align="left" valign="middle"><a href="#1f7215e3e61c9812">CLUSTER_GROUP_ID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_MEMBER_ID</td><td align="left" valign="middle">레코드가 저장된 member의 식별자를 반환한다.</td><td align="left" valign="middle"><a href="#f581814b6c369e1e">CLUSTER_MEMBER_ID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_GROUP_NAME</td><td align="left" valign="middle">레코드가 저장된 group의 이름을 반환한다.</td><td align="left" valign="middle"><a href="#31a3b4f06cbd0baf">CLUSTER_GROUP_NAME Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_MEMBER_NAME</td><td align="left" valign="middle">레코드가 저장된 member의 이름을 반환한다.</td><td align="left" valign="middle"><a href="#4e8b309790d8bf56">CLUSTER_MEMBER_NAME Pseudo Column</a></td></tr></tbody></table>

<a id="79cc06caf35b0f50"></a>
### ROWID Pseudo Column

ROWID pseudo column은 레코드 식별자로써 데이터베이스 내 각 레코드의 식별정보를 반환한다.

ROWID는 system에 따라 데이터베이스 내의 위치정보를 식별하기 위한 다음 정보들을 가진다.

Standalone system  
• OBJECT_ID  
• TABLESPACE_ID  
• PAGE_ID  
• PAGE 내 OFFSET

Cluster system  
• GRID_BLOCK_SEQUENCE  
• GRID_BLOCK_ID  
• MEMBER_ID  
• SHARD_ID

ROWID를 검색할 때 base 64 encoding으로 내부에 저장된 정보들을 A-Z, a-z, 0-9, +, / 의 value로 변환하여 출력한다.

ROWID 내에 저장된 데이터베이스 내 주소를 식별하기 위한 각각의 정보들은 ROWID-related functions 를 통해 얻을 수 있다.

레코드가 삭제되는 경우, 이 레코드의 주소는 새로 추가되는 레코드에 다시 할당될 수 있다.

ROWID pseudo column은 SELECT만 할 수 있고 INSERT, UPDATE, DELETE는 할 수 없다.

자세한 내용은 [ROWID](#e7fd0a43c7fa5340), [ROWID-related Functions](#9e953b8caa2ecc27)를 참조한다.

다음은 ROWID pseudo column을 검색하는 예이다.

```
gSQL> SELECT ROWID FROM T1;
                  ROWID
-----------------------
AAAAAAAAFpEAACAAAEAkAAA
AAAAAAAAFpEAACAAAEAkAAB
AAAAAAAAFpEAACAAAEAkAAC
AAAAAAAAFpEAACAAAEAkAAD
AAAAAAAAFpEAACAAAEAkAAE
5 rows selected.
```

<a id="1f7215e3e61c9812"></a>
### CLUSTER_GROUP_ID Pseudo Column

CLUSTER_GROUP_ID pseudo column은 레코드가 저장된 server의 group 식별자를 반환한다.

CLUSTER_GROUP_ID pseudo column은 SELECT만 할 수 있고 INSERT, UPDATE, DELETE는 할 수 없다.

> Cluster system에서 유효한 정보이다.

다음은 CLUSTER_GROUP_ID pseudo column을 검색하는 예이다.

```
gSQL> SELECT T1.C1, T1.CLUSTER_GROUP_ID FROM T1;
C1 T1.CLUSTER_GROUP_ID
-- -------------------
A                    1
B                    2
C                    3

3 rows selected.
```

<a id="f581814b6c369e1e"></a>
### CLUSTER_MEMBER_ID Pseudo Column

CLUSTER_MEMBER_ID pseudo column은 레코드가 저장된 server의 member 식별자를 반환한다.

CLUSTER_MEMBER_ID pseudo column은 SELECT만 할 수 있고 INSERT, UPDATE, DELETE는 할 수 없다.

> Cluster system에서 유효한 정보이다.

다음은 CLUSTER_MEMBER_ID pseudo column을 검색하는 예이다.

```
gSQL> SELECT T1.C1, T1.CLUSTER_MEMBER_ID FROM T1;
C1 T1.CLUSTER_MEMBER_ID
-- --------------------
A                     1
B                     3
C                     5

3 rows selected.
```

<a id="31a3b4f06cbd0baf"></a>
### CLUSTER_GROUP_NAME Pseudo Column

CLUSTER_GROUP_NAME pseudo column은 레코드가 저장된 server의 group 이름을 반환한다.

CLUSTER_GROUP_NAME pseudo column은 SELECT만 할 수 있고 INSERT, UPDATE, DELETE는 할 수 없다.

> Cluster system에서 유효한 정보이다.

다음은 CLUSTER_GROUP_NAME pseudo column을 검색하는 예이다.

```
gSQL> SELECT T1.C1, T1.CLUSTER_GROUP_NAME FROM T1;
C1 T1.CLUSTER_GROUP_NAME
-- ---------------------
A  G1                   
B  G2                   
C  G3                   

3 rows selected.
```

<a id="4e8b309790d8bf56"></a>
### CLUSTER_MEMBER_NAME Pseudo Column

CLUSTER_MEMBER_NAME pseudo column은 레코드가 저장된 server의 member 이름을 반환한다.

CLUSTER_MEMBER_NAME pseudo column은 SELECT만 할 수 있고 INSERT, UPDATE, DELETE는 할 수 없다.

> Cluster system에서 유효한 정보이다.

다음은 CLUSTER_MEMBER_NAME pseudo column을 검색하는 예이다.

```
gSQL> SELECT T1.C1, T1.CLUSTER_MEMBER_NAME FROM T1;
C1 T1.CLUSTER_MEMBER_NAME
-- ----------------------
A  G1N1                  
B  G2N1                  
C  G3N1                  

3 rows selected.
```

<a id="d8c920a42c2c75a5"></a>
### 호환성

Pseudo column에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="ad0a270ca9d2a897"></a>
<table><tbody><tr><th align="center">&nbsp;Feature ID</th><th align="center">&nbsp;설명</th><th align="center">&nbsp;지원 여부</th></tr><tr><td align="left">T176</td><td align="left">Sequence generator support</td><td align="center">O</td></tr><tr><td align="left">T177</td><td align="left">&nbsp;Sequence generator support: simple restart option</td><td align="center">O</td></tr></tbody></table>

<a id="fff79de2e130d4d5"></a>
## Operators

Operator는 구문상에서 하나 이상의 특정 기호 또는 keyword로 표현되며, 하나 이상의 argument들을 가지고 기능을 수행한다.

Operator에는 다음과 같이 다양한 형태가 있다.  
• Arithmetic operator  
• Concatenation operator  
• Set operator

<a id="5afa9e457e6cc4d8"></a>
### Arithmetic Operator

<a id="4d30cd15939b3031"></a>
#### 구문

```
<arithmetic operator> ::=
        <value term>
      | <expression> + <value term>
      | <expression> - <value term>

<value term> ::=
        <value factor>
      | <value term> * <value factor>
      | <value term> / <value factor>

<value factor> ::=
        <expression>
      | + <expression>
      | - <expression>
```

<a id="3b3b6c90cbcaafe4"></a>
#### 설명

Arithmetic operator는 숫자형, 날짜/ 시간, INTERVAL 타입의 산술 연산을 수행한다.

Arithmetic operator의 우선순위는 다음과 같다.

1. [+ (POSITIVE)](#e2ac63d1d885b4d2), [- (NEGATIVE)](#9a10c5280234a50d)
2. [* (MULTIPLICATION)](#2295658d1c028dca), [/ (DIVISION)](#de1584725d82cfa4)
3. [+ (ADDITION)](#592787f61a1066b5), [- (SUBTRACTION)](#5e8dfac15abd6dff)

<a id="5a8d9beaad309619"></a>
### Concatenation Operator

<a id="a921469a9e3dceb0"></a>
#### 구문

```
<concatenation operator> ::=
        <expression> || <expression>
```

<a id="d9a4836957a6c7f6"></a>
#### 설명

Concatenation operator는 CHARACTER STRING 타입이나 BINARY STRING 타입의 value 사이를 연결한 문자열을 반환한다.  
자세한 내용은 [|| (CONCATENATE)](#d94be4d95c59affd), [CONCATENATE](#0d6daaed8ec3a38c)를 참조한다.

<a id="847a82cef870969b"></a>
### Set Operator

<a id="1f6f49f51b7e3a10"></a>
#### 구문

```
<set operator> ::=
        <set operator term>
      | <subquery> UNION [ ALL | DISTINCT ] <set operator term>
      | <subquery> EXCEPT [ ALL | DISTINCT ] <set operator term>
      | <subquery> MINUS [ ALL | DISTINCT ] <set operator term>

<set operator term> ::=
        <subquery>
      | <subquery> INTERSECT [ ALL | DISTINCT ] <set operator term>
```

<a id="8e5c3a81d781eedf"></a>
#### 설명

[set operator](16-sql-references.md#96acd09fad234c3f)는 부질의 (subquery) 결과들에 대한 집합 (set) 연산을 수행한다.

INTERSECT ALL/ DISTINCT는 다른 set operator 보다 우선한다.

**Set operators**

<a id="a1148b217c0b520f"></a>
| Operator | 설명 |
| --- | --- |
| UNION ALL | Subquery 결과들에서 중복을 제거하지 않은 합집합이다. |
| UNION DISTINCT | Subquery 결과들에서 중복을 제거한 합집합이다. |
| EXCEPT ALL | Subquery 결과들에서 중복을 제거하지 않은 차집합이다. |
| EXCEPT DISTINCT | Subquery 결과들에서 중복을 제거한 차집합이다. |
| MINUS ALL | EXCEPT ALL과 동일하다. |
| MINUS DISTINCT | EXCEPT DISTINCT와 동일하다. |
| INTERSECT ALL | Subquery 결과들에서 중복을 제거하지 않은 교집합이다. |
| INTERSECT DISTINCT | Subquery 결과들에서 중복을 제거한 교집합이다. |

<a id="8a60a893bf865b9d"></a>
### 호환성

Operator에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="d0a46ed99550dc6d"></a>
<table><tbody><tr><th align="center">Feature ID</th><th align="center">설명</th><th align="center">지원 여부</th></tr><tr><td align="left" valign="middle">E011-04</td><td align="left" valign="middle">Arithmetic operators</td><td align="center" valign="middle">O</td></tr><tr><td valign="middle">E021-07</td><td valign="middle">Character concatenation</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-01</td><td align="left" valign="middle">UNION DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-02</td><td align="left" valign="middle">UNION ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-03</td><td align="left" valign="middle">EXCEPT DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-05</td><td align="left" valign="middle">Columns combined via table operators need not have exactly the same data type</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-06</td><td align="left" valign="middle">Table operators in subqueries</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F041-08</td><td align="left" valign="middle">All comparison operators are supported (rather than just =)</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F302-01</td><td align="left" valign="middle">INTERSECT DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F302-02</td><td align="left" valign="middle">INTERSECT ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F304</td><td align="left" valign="middle">EXCEPT ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F846</td><td align="left" valign="middle">Octet support in regular expression operators</td><td align="center" valign="middle">X</td></tr><tr><td align="left" valign="middle">J571</td><td align="left" valign="middle">NEW operator</td><td align="center" valign="middle">X</td></tr></tbody></table>

<a id="e59cfd4bcf0333be"></a>
## Functions

Operator와 기능상으로는 유사하지만, function 이름 뒤에 괄호를 사용하여 argument들을 명시한다. Function은 0개 이상의 argument를 포함할 수 있다.

Function 형태는 다음과 같이 구분된다.  
• Single row function  
• Aggregate function

<a id="b90e88343738c205"></a>
### Single Row Function

Single row function은 table이나 view의 매 row 마다 각각 하나의 결과 row를 생성하는 function이다.

Single row function의 형태는 다음과 같이 구분된다.

- Numeric function
- Character string function returning character values
- Character string function returning number values
- Datetime function
- General comparison function
- Conversion function
- Conditional function
- NULL-related function
- ROWID-related function
- Encryption function
- System information function

<a id="bfb5eb55a3eee764"></a>
#### Numeric Function

Numeric function은 숫자형 값을 입력받아 숫자형 결과를 반환하는 function이다.

Numeric function의 종류는 다음과 같다.

- [ABS](#cdc75e007d23703d)
- [ACOS](#d77b80d8e19d8536)
- [ASIN](#7c4475009f3e7ebf)
- [ATAN](#f0bb534f040bf687)
- [ATAN2](#c9188058f006314a)
- [BITAND](#5cdf6e42f3b08d6b)
- [BITNOT](#477fbc480f8f4223)
- [BITOR](#48bff810dd5edcf4)
- [BITXOR](#2d8311646e3b2ce1)
- [CBRT](#d6eca6c411286eea)
- [CEIL](#1fa24fcf52467d87)
- [COS](#ba8ec59c0d585e05)
- [COT](#29ee6c5035a97c3e)
- [DEGREES](#85e1bac58377785e)
- [EXP](#13398c36be01a534)
- [FACTORIAL](#8de7e8bc51eaefa0)
- [FLOOR](#d6b3abc03cb13652)
- [LN](#34b5e5cab0360f64)
- [LOG](#0e732f9da532f7af)
- [MOD](#dde0d487094d72e3)
- [PI](#46619b3749dcc372)
- [POWER](#363f0d0ac0cc9ad1)
- [RADIANS](#6d1605316e480090)
- [RANDOM](#c27692dda69a29bc)
- [ROUND( number )](#090988a74daf0bc0)
- [SHARD_ID](#701f3a9ae9065f21)
- [SHIFT_LEFT](#657c1b8a74a4923b)
- [SHIFT_RIGHT](#ef522f94a2be0e12)
- [SIGN](#f3f4dc33b835cfb4)
- [SIN](#b10923b221cf674f)
- [SQRT](#f3eeafb892d1e370)
- [TAN](#851194d4a59fc92d)
- [TRUNC( number )](#0fd60f39b2b5cced)
- [WIDTH_BUCKET](#9e69b4d3f99f6473)

<a id="076bcfc19daa26b8"></a>
#### Character String Functions Returning Character Values

Character string functions returning character values는 CHARACTER STRING형 값을 입력받아 CHARACTER STRING형 결과를 반환하는 function이다.

Character string functions returning character value의 종류는 다음과 같다.

- [CHR](#204884e3d6fd386c)
- [CONCAT](#537e3c54efdacfea)
- [CONCATENATE](#0d6daaed8ec3a38c)
- [INITCAP](#c71953d88af8f408)
- [LOWER](#89dc33b14c803934)
- [LPAD](#c4bfc9126f6b9094)
- [LTRIM](#4246822993541770)
- [OVERLAY](#9432eacfe6e24942)
- [REPEAT](#7488f433adb0d426)
- [REPLACE](#9b50e4bde9c8edd2)
- [REVERSE](#1809a812fddd9afb)
- [RPAD](#af49a5a736f0bf17)
- [RTRIM](#a2e95277d0b9612a)
- [SPLIT_PART](#3f92ba4885716086)
- [SUBSTR](#8f078bc6cefab9f8)
- [SUBSTRB](#ea687e1f8622d7d1)
- [TRANSLATE](#e452183b84993ce5)
- [TRIM](#be03adba17d469ce)
- [UPPER](#78a88a74025eccc4)

<a id="5112748d875c5ddb"></a>
#### Character String Functions Returning Number Values

Character string functions returning number value는 CHARACTER STRING형 값을 입력받아 숫자형 결과를 반환하는 function이다.

Character string functions returning number value의 종류는 다음과 같다.

- [ASCII](#765ca8767a695cf4)
- [BIT_LENGTH](#f2491c65ea403713)
- [BYTE_LENGTH](#43f8c447a8165c4d)
- [CHAR_LENGTH](#41c3cbeb846d0e80)
- [INSTR](#1a84fa5265b76ee2)
- [LENGTH](#21689d44ab60ac4e)
- [LENGTHB](#11bae4ba0aa6d32d)
- [OCTET_LENGTH](#35c754cbe369df47)
- [POSITION](#62366ed6216df66f)

<a id="9b50cf1d693538e8"></a>
#### Datetime Functions

Datetime function은 DATE/ TIME/ TIMESTAMP/ INTERVAL 형 값을 입력받아 DATE/ TIME TIMESTAMP/ INTERVAL형 결과를 반환하는 function이다.

Datetime function의 종류는 다음과 같다.

- [ADDDATE](#40e97b19083d297e)
- [ADDTIME](#7a026839b36e206e)
- [ADD_MONTHS](#51e0fc91626ae36e)
- [DATEADD](#9ed828d593dc6ae0)
- [DATEDIFF](#084732522318d734)
- [DATE_ADD](#3b472fb1547db027)
- [DATE_PART](#929fc4f512892cd9)
- [EXTRACT](#b923e09ee076c491)
- [LAST_DAY](#2571b0035c21570b)
- [MONTHS_BETWEEN](#08319e67af5037d1)

<a id="a8ae234980dbbdee"></a>
#### General Comparison Functions

General comparison function은 value 집합에 대한 최소값 또는 최대값을 구하는 function이다.

General comparison function의 종류는 다음과 같다.

- [GREATEST](#308c44d267e0ca91)
- [LEAST](#350d1d2339344e99)

<a id="3b5cd298608473f9"></a>
#### Conversion Functions

Conversion function은 특정 data type으로의 값을 설정하는 function이다.

Conversion function 종류는 다음과 같다.

- [TO_CHAR( datetime )](#1aa9ef481e07ad64)
- [TO_CHAR( number )](#d0f1dcb76f6a4884)
- [TO_DATE](#45c8ee60f5aa8084)
- [TO_NATIVE_DOUBLE](#e2adb0785ea15c2a)
- [TO_NATIVE_REAL](#9227dcb27754ec3b)
- [TO_NUMBER](#391976f1ebfbe1b4)
- [TO_TIME](#c6462fe8a092223a)
- [TO_TIME_TZ](#ae27f0b15daa7110)
- [TO_TIME_WITH_TIME_ZONE](#132b267c45037442)
- [TO_TIMESTAMP](#e11d27a423dbc46c)
- [TO_TIMESTAMP_TZ](#1dde6cb4411f3cf2)
- [TO_TIMESTAMP_WITH_TIME_ZONE](#deb069ec65b335a1)

<a id="f3757a8d4a5a66bb"></a>
#### Conditional Functions

Conditional function은 조건에 따라 특정값을 결과로 반환하는 function이다.

Conditional function의 종류는 다음과 같다.

- [CASE2](#4d911dd670bd919d)
- [DECODE](#97c7ea5f728b56de)

<a id="023d748721ea49bf"></a>
#### NULL-related Functions

NULL-related function은 입력값이 NULL값인지 여부에 따라 특정값을 결과로 반환하는 function이다.

NULL-related function의 종류는 다음과 같다.

- [COALESCE](#ec78cb861c06c7fb)
- [NULLIF](#4d135921ffce1c85)
- [NVL](#9ac19cfef4356d97)
- [NVL2](#58bdec34e2320a7a)

<a id="9e953b8caa2ecc27"></a>
#### ROWID-related Functions

ROWID-related function은 ROWID에 대한 정보를 얻기 위한 function이다.

ROWID-related function의 종류는 다음과 같다.

- Standalone에서 유효한 function
    - [ROWID_OBEJCT_ID](#5c38946c0a3c4e2e)
    - [ROWID_TABLESPACE_ID](#1b4522ef522e9d6f)
    - [ROWID_PAGE_ID](#3c290dc2da7759f2)
    - [ROWID_ROW_NUMBER](#f84a300892c983d0)

- Cluster에서 유효한 function
    - [ROWID_GRID_BLOCK_ID](#ca9d8df7718213ca)
    - [ROWID_GRID_BLOCK_SEQ](#cca6fe193cecd8cf)
    - [ROWID_MEMBER_ID](#3ec899ecfee01175)
    - [ROWID_SHARD_ID](#384d999841bafdb0)

<a id="a8f85620255927a9"></a>
#### Encryption Functions

Encryption function은 주어진 plain text를 특정 알고리즘으로 encrypt/ decrypt 하거나 hash한 결과값을 반환하는 function이다.

Encryption function에 대한 자세한 내용은 [DIGEST](#b58f7f38ee675bcf)를 참조한다.

<a id="09703db8c2615ef8"></a>
#### System Information Functions

System information function은 session과 system에 대한 정보를 얻기 위한 function이다.

System information function의 종류는 다음과 같다.

- [CLOCK_DATE](#8aa1a037b24b08b9)
- [CLOCK_LOCALTIME](#cab31dad1e732dd9)
- [CLOCK_LOCALTIMESTAMP](#e7935bb37b1e4649)
- [CURRENT_CATALOG](#ee088d323b9d8981)
- [CURRENT_DATE](#1aea3d5d1b193899)
- [CURRENT_SCHEMA](#6cad995b2f20e5b2)
- [CURRENT_TIME](#a4e68f37761bd434)
- [CURRENT_TIMESTAMP](#00166487940f1b96)
- [CURRENT_USER](#27bffc804504302b)
- [LAST_IDENTITY_VALUE](#762ea15e9c2071ae)
- [LOCALTIME](#14d2f9de457d10b2)
- [LOCALTIMESTAMP](#18927e9f41bda3e1)
- [LOGON_USER](#abaf386db4467942)
- [SESSION_ID](#748ef2ed123142fa)
- [SESSION_SERIAL](#e6f850d5b5ac0e5f)
- [SESSION_USER](#e67b1f1bb30429be)
- [STATEMENT_DATE](#23b9e7a0262409a5)
- [STATEMENT_LOCALTIME](#699791b88fd6ad60)
- [STATEMENT_LOCALTIMESTAMP](#d5718be94dde3972)
- [STATEMENT_TIME](#5c8d77b5856a285b)
- [STATEMENT_TIMESTAMP](#442e0c52fd4e267e)
- [STATEMENT_VIEW_SCN](#57d62b93fb6c220b)
- [SYSDATE](#bb00ec3be51cce3a)
- [SYSTIME](#8082a71cab46274b)
- [SYSTIMESTAMP](#21db95ba7e8f73c4)
- [TRANSACTION_DATE](#e76700903a4afd0e)
- [TRANSACTION_LOCALTIME](#efa6df2210cc3700)
- [TRANSACTION_LOCALTIMESTAMP](#86b48c062353324f)
- [TRANSACTION_TIME](#6ad4881bb7dd2346)
- [TRANSACTION_TIMESTAMP](#9ee4d12b971d35ad)
- [USER_ID](#871d8b18f427df1f)
- [VERSION](#de2cfe412d1f521d)

<a id="e2f4344c46040c86"></a>
### Aggregate Function

Aggregate function은 여러 row에 대해 하나의 결과 row를 생성하는 function이다.

Aggregation function의 종류는 다음과 같다.

- [COUNT](#0a35b1f2a520837b)
- [COUNT(*)](#cb884841c2d1440a)
- [SUM](#1a0c9e6b27cddbc2)
- [AVG](#d90586b18f2f93a9)
- [MIN](#3e3749fffb97164e)
- [MAX](#634a03278cea58cf)
- [STDDEV](#55362e40aae95d6a)
- [STDDEV_POP](#6402c3dcd4e4fe05)
- [STDDEV_SAMP](#3cc8ea60b60a3c12)
- [VAR_POP](#46e177e0aaffbb82)
- [VAR_SAMP](#345e88314b92a36d)
- [VARIANCE](#051de20384a5e1c8)

<a id="87adc2f12fa4c167"></a>
### 호환성

Function에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="530e6630f65d33c1"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B033 | Untyped SQL-invoked function arguments | X |
| E021-04 | CHARACTER_LENGTH function | O |
| E021-05 | OCTET_LENGTH function | O |
| E021-06 | SUBSTRING function | O |
| E021-08 | UPPER and LOWER functions | O |
| E021-09 | TRIM function | O |
| E021-11 | POSITION function | O |
| E091-01 | AVG | O |
| E091-02 | COUNT | O |
| E091-03 | MAX | O |
| E091-04 | MIN | O |
| E091-05 | SUM | O |
| E091-06 | ALL quantifier | O |
| E091-07 | DISTINCT quantifier | O |
| F131-03 | Set functions supported in queries with grouped views | O |
| F201 | CAST function | O |
| F441 | Extended set function support | X |
| F442 | Mixed column references in set functions | X |
| F801 | Full set function | X |
| F842 | OCCURRENCES_REGEX function | X |
| F843 | POSITION_REGEX function | X |
| S071 | SQL paths in function and type name resolution | X |
| S201-02 | Array as result type of functions | X |
| S211 | User-defined cast functions | X |
| S241 | Transform functions | X |
| T041-03 | POSITION, LENGTH, LOWER, TRIM, UPPER, and SUBSTRING functions for LOB data types | X |
| T312 | OVERLAY function | O |
| T321-01 | User-defined functions with no overloading | X |
| T326 | Table functions | X |
| T341 | Overloading of SQL-invoked functions and SQL-invoked procedures | X |
| T433 | Multiargument GROUPING function | X |
| T441 | ABS and MOD functions | O |
| T571 | Array-returning external SQL-invoked functions | X |
| T572 | Multiset-returning external SQL-invoked functions | X |
| T581 | Regular expression substring function | X |
| T614 | NTILE function | X |
| T615 | LEAD and LAG functions | X |
| T616 | Null treatment option for LEAD and LAG functions | X |
| T617 | FIRST_VALUE and LAST_VALUE functions | X |
| T618 | NTH_VALUE function | X |
| T619 | Nested window functions | X |
| T621 | Enhanced numeric functions | O |

<a id="4900f8e290fa6cb1"></a>
## Conditions

<a id="73812daa3f21a622"></a>
### Condition

TRUE, FALSE, UNKNOWN으로 평가되는 식이다.

Condition이 사용될 수 있는 SQL 구문의 위치는 다음과 같다.  

• DELETE, UPDATE의 WHERE 절  
• SELECT의 WHERE, HAVING 절  
• 그 외 BOOLEAN TYPE이 위치할 수 있는 곳

Condition의 종류는 다음과 같다.  

• Comparison condition  
• Logical condition  
• Null condition  
• Compound condition  
• Pattern-matching condition  
• Between condition  
• In condition  
• Exists condition

**Condition 우선순위**

<a id="7af9be7f7e53585c"></a>
| 우선순위 | Condition 종류 |
| --- | --- |
| 1 | 조건절에 쓰여진 연산자들 |
| 2 | =, !=, &lt;, &gt;, &lt;=, &gt;= |
| 3 | IS [NOT] NULL, [NOT] BETWEEN,  [NOT] IN,  LIKE, EXISTS |
| 4 | NOT |
| 5 | AND |
| 6 | OR |

<a id="794d92b055b1337f"></a>
### Comparison Conditions

양쪽 조건을 비교하여 TRUE, FALSE, UNKNOWN 값의 boolean 타입을 반환한다.

**Comparison condition**

<a id="27fe47ec9055f9e1"></a>
| Condition | 설명 |
| --- | --- |
| = | 두 식이 같은지 여부를 검사한다. |
| !=, &lt;&gt; | 두 식이 서로 같지 않은지 여부를 검사한다. |
| > | 두 식을 비교하여 큰 지 여부를 검사한다. |
| < | 두 식을 비교하여 작은 지 여부를 검사한다. |
| >= | 두 식을 비교하여 크거나 같은지 검사한다. |
| <= | 두 식을 비교하여 작거나 같은지 검사한다. |
| ANY, SOME | 왼쪽 expr이 오른쪽 expr_list (또는 subquery 결과) 중 하나 이상을 만족하는 조건이면 TRUE를 반환한다. 오른쪽 subquery의 결과가 없는 경우, FALSE를 반환한다. |
| ALL | 왼쪽 expr이 오른쪽 expr_list (또는 subquery 결과)를 모두 만족하는 조건이면 TRUE를 반환한다. 오른쪽 subquery의 결과가 없는 경우, TRUE를 반환한다. |

자세한 내용은 [타입간 비교](#be2c78a9fcad0b86)를 참조한다.

<a id="0587f7178143f549"></a>
#### &lt; Simple Comparison Conditions &gt;

<a id="8d7ec13356c29004"></a>
##### 구문

```
<simple_comparison_condition> ::=
        <expr>          <comparison_operator> <expr>
      | <expr>          <comparison_operator> ( <subquery> )
      | ( <subquery> )  <comparison_operator> <expr>
      | ( <subquery> )  <comparison_operator> ( <subquery> ) 
      | ( <expr_list> ) <comparison_operator> ( <expr_list> )
      | ( <expr_list> ) <comparison_operator> ( <subquery> )
      | ( <subquery> )  <comparison_operator> ( <expr_list> )
      | ( <subquery> )  <comparison_operator> ( <subquery> )

<comparison_operator> ::=
        <  =   >
      | <  !=  >
      | <  <   >
      | <  >   >
      | <  <=  >
      | <  >=  >

<expr_list> ::= 
        <expr>
      | <expr>, ... , <expr>
      | ( <expr> )
      | ( <expr> , ... , <expr> )
```

자세한 내용은 [Scalar Subquery Expression](#7c4c39b41b2341ba)을 참조한다.

<a id="151e333557098689"></a>
##### 설명

comparison_operator 양쪽에 expr_list 또는 subquery가 오는 경우, 비교되는 expr의 개수 또는 subquery target의 개수는 동일해야 한다.  
Subquery가 오는 경우, 결과 레코드는 한 건이어야 한다.

<a id="dfea149f6188d16e"></a>
##### 사용 예

**Simple comparison condition의 예**

<a id="56c60bfae48407a7"></a>
| Condition | 결과 |
| --- | --- |
| 'abc' = 'abc' | TRUE |
| 'abc' != 'abc' | FALSE |
| 'abc' < 'abc' | FALSE |
| 'abc' <= 'abc' | TRUE |
| 'abc' > 'abc' | FALSE |
| 'abc' >= 'abc' | TRUE |
| ( 1, 2, 3 ) = ( 1, 2, 3 ) | TRUE |
| ( 1, 2, 3 ) = ( 1, 2, 4 ) | FALSE |
| ( 1, 2, 3 ) != ( 4, 5, 6 ) | TRUE |
| ( 1, 2, 3 ) != ( 1, 2, 3 ) | FALSE |
| ( 1, 2, 3 ) < ( 1, 2, 4 ) | TRUE |
| ( 1, 2, 3 ) < ( 1, 2, 3 ) | FALSE |
| ( 1, 2, 3 ) <= ( 1, 2, 4 ) | TRUE |
| ( 1, 2, 3 ) <= ( 1, 2, 2 ) | FALSE |
| ( 1, 2, 3 ) > ( 1, 2, 2 ) | TRUE |
| ( 1, 2, 3 ) > ( 1, 2, 4 ) | FALSE |
| ( 1, 2, 3 ) >= ( 1, 2, 2 ) | TRUE |
| ( 1, 2, 3 ) >= ( 1, 2, 4 ) | FALSE |

<a id="be74e7b2cd7b32d4"></a>
#### &lt; Group Comparison Conditions &gt;

<a id="f2dc2b29e96d2208"></a>
##### 구문

```
<group_comparison_condition> ::=
   <expr>          <comparison_operator> <quantifier> ( <expr_list> )
 | <expr>          <comparison_operator> <quantifier> ( <subquery> )
 | ( <expr_list> ) <comparison_operator> <quantifier> ( <expr_list_list> )
 | ( <expr_list> ) <comparison_operator> <quantifier> ( <subquery> )
 | ( <subquery> )  <comparison_operator> <quantifier> ( <expr_list> )
 | ( <subquery> )  <comparison_operator> <quantifier> ( <expr_list_list> )
 | ( <subquery> )  <comparison_operator> <quantifier> ( <subquery> )

<comparison_operator> ::=
        <  =   >
      | <  !=  >
      | <  <   >
      | <  >   >
      | <  <=  >
      | <  >=  >

<quantifier> ::=
        ALL
      | ANY
      | SOME

<expr_list> ::= 
        <expr>
      | <expr>, ... , <expr>
      | ( <expr> )
      | ( <expr> , ... , <expr> )

<expr_list_list> ::=
        <expr_list>
      | <expr_list>, ... , <expr_list>
```

자세한 내용은 [Scalar Subquery Expression](#7c4c39b41b2341ba)을 참조한다.

<a id="faf939ecfd5f58e7"></a>
##### 설명

comparison_operator 양쪽에 expr_list 또는 subquery가 오는 경우, 비교되는 expr의 개수 또는 subquery target의 개수는 동일해야 한다.  
comparison_operator 왼쪽에 subquery가 오는 경우, 결과 레코드는 한 건이어야 한다.  
comparison_operator 오른쪽에 subquery가 오는 경우, 결과 레코드는 여러 건일 수 있다.

<a id="891ee624448981f7"></a>
##### 사용 예

<a id="63bfe8034b752a12"></a>
<table class="table column_count_2"><caption>Group comparison condition의 예</caption><thead><tr><th class="to_center"><div>Condition</div></th><th class="to_center"><div>결과</div></th></tr></thead><tbody><tr><td class="to_left"><div>1 =any ( 1, 2, 3, 4, 5 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>1 =any ( 1, 2, null, 4, 5 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>1 =any ( 2, null, 4, 5 )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td class="to_left"><div>1 =any ( 100, 2, 3, 4, 5 )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td class="to_left"><div>1 =all ( 1, +1, 1E+0 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>1 =all ( 1, +1, 1E+0, null )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td class="to_left"><div>1 =all ( 1, 2, 3, 4, 5 )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =any ( ( 0, 1 ), ( 1, 2 ), ( 3, 4 ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =any ( ( 0, 1 ), ( 1, 2 ), ( null, null ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =any ( ( 0, 1 ), ( 2, 3 ), ( 3, 4 ) )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =all ( ( 1, 2 ), ( +1, +2 ), ( 1E+0, 2E+0 ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =all ( ( 1, 2 ), ( +1, +2 ), ( null, null ) )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =all ( ( 0, 1 ), ( 2, 3 ), ( 3, 4 ) )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><th class="to_left" colspan="2"><div>comparison_operator 오른쪽 subquery의 결과 레코드가 0인 경우</div></th></tr><tr><td class="to_left"><div>( 'X' ) =any ( select dummy from dual where dummy = 'Y' )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td class="to_left"><div>( 'X' ) =all ( select dummy from dual where dummy = 'Y' )</div></td><td class="to_left"><div>TRUE</div></td></tr></tbody></table>

<a id="650deaf1740ad742"></a>
### Logical Conditions

Logical condition으로는 AND, OR, NOT이 있다.

<a id="0e221e85f224b8cc"></a>
#### AND

<a id="1796aeba81527d6a"></a>
##### 구문

```
<boolean value expression> AND <boolean value expression>
```

<a id="92f5c5eed0902d53"></a>
##### 설명

**AND boolean operator의 truth table**

<a id="0d8d10547e5073e1"></a>
| AND | True | False | Unknown |
| --- | --- | --- | --- |
| True | True | False | Unknown |
| False | False | False | False |
| Unknown | Unknown | False | Unknown |

<a id="92e8a9083e4f5465"></a>
#### OR

<a id="d7a0041c906a237d"></a>
##### 구문

```
<boolean value expression> OR <boolean value expression>
```

<a id="0a723571bb218100"></a>
##### 설명

**OR boolean operator의 truth table**

<a id="5e5b25330c7dba3a"></a>
| OR | True | False | Unknown |
| --- | --- | --- | --- |
| True | True | True | True |
| False | True | False | Unknown |
| Unknown | True | Unknown | Unknown |

<a id="afd6448679e8d335"></a>
#### NOT

<a id="130ab9b55b41628a"></a>
##### 구문

```
NOT <boolean value expression>
```

<a id="2f4910334d5df7eb"></a>
##### 설명

**NOT boolean operator의 truth table**

<a id="fdd5413a4f6804a2"></a>
| expr | NOT |
| --- | --- |
| True | False |
| False | True |
| Unknown | Unknown |

<a id="e6d7fab8e16762d1"></a>
### Null Condition

<a id="0e42a163a51191b4"></a>
#### 구문

```
<expr> IS [NOT] NULL
```

<a id="4378e0fe03334671"></a>
#### 설명

expr의 결과가 NULL 값인지 여부를 검사한다.

**Is Null 조건의 결과표**

<a id="ace0c68d89fe92cb"></a>
| expr | IS NULL | IS NOT NULL |
| --- | --- | --- |
| NULL | True | False |
| NOT NULL | False | True |

<a id="1aeba8c2b6a3e1ac"></a>
### Compound Condition

여러 조건들이 결합되어 만들어진 조건식이다.

```
compound_condition ::=
        ( condition )
      | NOT condition
      | condition < AND | OR > condition
```

<a id="1461c4c2b110e0ee"></a>
### Pattern-matching Conditions

<a id="136d720ef0b2bd96"></a>
#### LIKE Condition

<a id="2a131a6acc12272b"></a>
##### 구문

```
like_condition ::=
        string [NOT] LIKE pattern [ ESCAPE escape_character ]
```

<a id="0d601a19bc6afc67"></a>
##### 설명

string이 지정된 pattern과 일치하는지 검사한다.

인자 string, pattern, escape_charater에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있다.  
string, pattern, escape_character가 NULL인 경우,  NULL이 결과로써 반환된다.

escape_character가 생략되었을 경우, default 값은 없다.  
escape_character가 명시된 경우, escape_character는 한 개 문자여야 한다.

pattern에 '_' 또는 '%'를 포함하지 않으면, equal 연산 (string = pattern)과 동일하게 처리된다.  
pattern에 '_' 또는 '%'이 포함되면, string에서 다음과 같이 일치여부를 판단한다.  
• '_': 임의의 한 개 문자와 대응한다.  
• '%': 0개 이상의 문자를 가진 임의의 문자열과 대응한다.

pattern에 포함된 '_' 또는 '%'를 문자로 비교하고자 하는 경우, ESCAPE절을 사용한다.  
escape_character를 지정하고, 지정된 escape_character를 pattern의 '_' 또는 '%' 앞에 기술한다.

<a id="2201dba70a18d50c"></a>
##### 사용 예

```
gSQL> SELECT 'hello%' LIKE 'h%o!%' ESCAPE '!' AS RESULT FROM DUAL;
RESULT
------
TRUE

• 'represent' LIKE 'represent'   => TRUE
• 'represent' LIKE ' represent ' => FALSE
• 'represent' LIKE 'REPRESENT'   => FALSE
• 'represent' LIKE 'r_pr_s_nt'   => TRUE
• 'represent' LIKE 're%t'        => TRUE
• 'represent' LIKE 'rep'         => FALSE

• 'summer_vacation' LIKE 'summer\_vacation' ESCAPE '\'  => TRUE
• NULL LIKE 'summer\_vacation' ESCAPE '\'               => NULL
• 'summer_vacation' LIKE NULL ESCAPE '\'                => NULL
• 'summer_vacation' LIKE 'summer\_vacation' ESCAPE NULL => NULL
```

<a id="f2a7645b79d22d5c"></a>
### BETWEEN Condition

<a id="f162a39b967e85e3"></a>
#### 구문

```
<between condition> ::=
   <expr1> [ NOT ] BETWEEN [ ASYMMETRIC | SYMMETRIC ] <expr2> AND <expr3>
```

<a id="fb978ea30bfd06c7"></a>
#### 설명

expr1이 expr2와 expr3 범위 내의 조건인지 검사한다.

ASYMMETRIC이나 SYMMETRIC이 생략된 경우, default는 ASYMMETRIC 이다.  
expr1, expr2, expr3의 data type이 다른 경우, conversion이 수행된다.  
자세한 내용은 [타입간 비교](#be2c78a9fcad0b86), [타입간 변환](#e2c21b3a3eaedfd1)을 참조한다.

**Between 구문 동치**

<a id="543d9d79a43e13c6"></a>
| A | B |
| --- | --- |
| X BETWEEN ASYMMETRIC Y AND Z | X BETWEEN Y AND Z |
| X BETWEEN Y AND Z | X >= Y AND X <= Z |
| X NOT BETWEEN Y AND Z | NOT( X BETWEEN Y AND Z ) |
| X BETWEEN SYMMETRIC Y AND Z | ((X BETWEEN Y AND Z) OR (X BETWEEN Z AND Y) |
| X NOT BETWEEN SYMMETRIC Y AND Z | NOT( X BETWEEN SYMMETRIC Y AND Z ) |

<a id="c08fb4e459ea047d"></a>
#### 사용 예

<a id="f41d4dc0fdcb1318"></a>
<table class="table column_count_3"><caption>Between 구문의 예</caption><thead><tr><th class="to_center" colspan="2"><div>Condition</div></th><th class="to_center"><div>결과</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>BETWEEN [ ASYMMETRIC ]</div></td><td><div>3 BETWEEN 1 AND 5</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr><tr><td><div>NULL BETWEEN 1 AND 5
3 BETWEEN NULL AND 5
3 BETWEEN 1 AND NULL</div></td><td class="to_left to_middle"><div>NULL</div></td></tr><tr><td><div>3 BETWEEN 5 AND 1</div></td><td class="to_left to_middle"><div>FALSE</div></td></tr><tr><td class="to_middle" rowspan="3"><div>BETWEEN SYMMETRIC</div></td><td><div>3 BETWEEN SYMMETRIC 1 AND 5</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr><tr><td><div>NULL BETWEEN SYMMETRIC 1 AND 5
3 BETWEEN SYMMETRIC NULL AND 5
3 BETWEEN SYMMETRIC 1 AND NULL</div></td><td class="to_left to_middle"><div>NULL</div></td></tr><tr><td><div>3 BETWEEN SYMMETRIC 5 AND 1</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr></tbody></table>

<a id="db3354e6a012972e"></a>
### IN Condition

<a id="b943eda3ecfb27f4"></a>
#### 구문

```
<in_condition> ::=
        <expr>          [NOT] IN ( <expr_list> )  
      | <expr>          [NOT] IN ( <subquery> )  
      | ( <expr_list> ) [NOT] IN ( <expr_list_list> )  
      | ( <expr_list> ) [NOT] IN ( <subquery> )
      | ( <subquery> )  [NOT] IN ( <expr_list> )  
      | ( <subquery> )  [NOT] IN ( <expr_list_list> )  
      | ( <subquery> )  [NOT] IN ( <subquery> )  

<expr_list> ::=          
        <expr>       
      | <expr>, ... , <expr>       
      | ( <expr> )       
      | ( <expr> , ... , <expr> )  

<expr_list_list> ::=         
        <expr_list>       
      | <expr_list>, ... , <expr_list>
```

<a id="785244000bd103b6"></a>
#### 설명

IN condition은 =ANY와 동일한 결과를 반환한다.  
NOT IN condition은 !=ALL과 동일한 결과를 반환한다.

자세한 내용은 [Comparison Conditions](#794d92b055b1337f)를 참조한다.

<a id="28e766b0d2b801fc"></a>
#### 사용 예

**IN condition의 예**

<a id="ab619ba4109d26a4"></a>
| Condition | 결과 |
| --- | --- |
| 1 IN ( 1, 2, 3, 4, 5 ) | TRUE |
| 1 IN ( 1, 2, null, 4, 5 ) | TRUE |
| 1 IN ( 2, null, 4, 5 ) | NULL |
| 1 IN ( 100, 2, 3, 4, 5 ) | FALSE |
| NULL IN ( 1, 2, 3 ) | NULL |
| 1 NOT IN ( 2, 3, 4, 5 ) | TRUE |
| 1 NOT IN ( 2, null, 4, 5 ) | NULL |
| 1 NOT IN ( 1, 2, null, 4, 5 ) | FALSE |
| 1 NOT IN ( 100, 2, 3, 4, 5 ) | TRUE |
| NULL NOT IN ( 1, 2, 3 ) | NULL |

<a id="03708ac484cae4bb"></a>
### EXISTS Condition

<a id="bdfabfc3ea74bc07"></a>
#### 구문

```
exists_conditions ::= 
        EXISTS ( subquery )
```

<a id="b86c25f3c058668a"></a>
#### 설명

Subquery의 결과 레코드 존재 유무를 검사한다.  
Subquery의 결과 레코드가 존재하면 TRUE를 반환하고, 결과 레코드가 존재하지 않으면 FALSE를 반환한다.

<a id="182f30740de563e0"></a>
#### 사용 예

```
gSQL> SELECT * FROM DUAL WHERE EXISTS ( SELECT * FROM DUAL );
      DUMMY
      -----
      X    
      1 row selected.

gSQL> SELECT * FROM DUAL 
       WHERE EXISTS ( SELECT * FROM DUAL WHERE DUMMY = 'Y' );
      no rows selected.
```

<a id="f85b32b4426cb672"></a>
### 호환성

Condition에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="18c32645a3c4e233"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| E061-01 | Comparison predicate | O |
| E061-02 | BETWEEN predicate | O |
| E061-03 | IN predicate with list of values | O |
| E061-04 | LIKE predicate | O |
| E061-05 | LIKE predicate: ESCAPE clause | O |
| E061-06 | NULL predicate | O |
| E061-07 | Quantified comparison predicate | O |
| E061-08 | EXISTS predicate | O |
| E061-09 | Subqueries in comparison predicate | O |
| E061-11 | Subqueries in IN predicate | O |
| E061-12 | Subqueries in quantified comparison predicate | O |
| E061-13 | Correlated subqueries | O |
| E061-14 | Search condition | O |
| F051-04 | Comparison predicate on DATE, TIME, and TIMESTAMP data types | X |
| F053 | OVERLAPS predicate | X |
| F263 | Comma-separated predicates in simple CASE expression | X |
| F291 | UNIQUE predicate | X |
| F481 | Expanded NULL predicate | O |
| F841 | LIKE_REGEX predicate | X |
| P008 | Comma-separated predicates in a CASE statement Extended CASE | X |
| S151 | Type predicate | X |
| T141 | SIMILAR predicate | X |
| T151 | DISTINCT predicate | X |
| T152 | DISTINCT predicate with negation | X |
| T461 | Symmetric BETWEEN predicate | O |
| T501 | Enhanced EXISTS predicate | X |
| T631 | IN predicate with one list element | X |
| X090 | XML document predicate | X |
| X091 | XML content predicate | X |
| X141 | IS VALID predicate: data-driven case | X |
| X142 | IS VALID predicate: ACCORDING TO clause | X |
| X143 | IS VALID predicate: ELEMENT clause | X |
| X144 | IS VALID predicate: schema location | X |
| X145 | IS VALID predicate outside check constraints | X |
| X151 | IS VALID predicate with DOCUMENT option | X |
| X152 | IS VALID predicate with CONTENT option | X |
| X153 | IS VALID predicate with SEQUENCE option | X |
| X155 | IS VALID predicate: NAMESPACE without ELEMENT clause | X |
| X157 | IS VALID predicate: NO NAMESPACE with ELEMENT clause | X |

<a id="35b61548d50e5866"></a>
## Built-in Data Type References

<a id="5a00de23bdab942e"></a>
### Aliases of Built-in Data Types

- BIGINT
    - NUMBER(19,0)와 동일하다.
    - 자세한 내용은 [NUMBER](#f5ef3006756aba88)를 참조한다.
- BINARY
    - 자세한 내용은 [BINARY](#56a204fe4b3d1c89)를 참조한다.
- BINARY VARYING
    - 자세한 내용은 [BINARY VARYING](#8028b0efef2db632)을 참조한다.
- BINARY LONG VARYING
    - 자세한 내용은 [BINARY LONG VARYING](#2940bef6c30ffc14)을 참조한다.
- BOOLEAN
    - 자세한 내용은 [BOOLEAN](#aca2201d031abe41)을 참조한다.
- CHAR
    - CHARACTER와 동일하다.
    - 자세한 내용은 [CHARACTER](#0319fe09b264cec3)를 참조한다.
- CHARACTER
    - 자세한 내용은 [CHARACTER](#0319fe09b264cec3)를 참조한다.
- CHARACTER VARYING
    - 자세한 내용은 [CHARACTER VARYING](#81c2c3704f1da6e2)을 참조한다.
- CHARACTER LONG VARYING
    - 자세한 내용은 [CHARACTER LONG VARYING](#1f0e795dfcc56d6a)을 참조한다.
- DATE
    - 자세한 내용은 [DATE](#d88d47b21d661aa7)를 참조한다.
- DEC
    - NUMERIC과 동일하다.
    - 자세한 내용은 [NUMERIC](#0f4910fcc7908fb7)을 참조한다.
- DECIMAL
    - NUMERIC과 동일하다.
    - 자세한 내용은 [NUMERIC](#0f4910fcc7908fb7)을 참조한다.
- DOUBLE
    - FLOAT(53)과 동일하다.
    - 자세한 내용은 [FLOAT](#e13294813a67476a)을 참조한다.
- DOUBLE PRECISION
    - FLOAT(53)과 동일하다.
    - 자세한 내용은 [FLOAT](#e13294813a67476a)을 참조한다.
- FLOAT
    - 자세한 내용은 [FLOAT](#e13294813a67476a)을 참조한다.
- FLOAT4
    - FLOAT(24)과 동일하다.
    - 자세한 내용은 [FLOAT](#e13294813a67476a)을 참조한다.
- FLOAT8
    - FLOAT(53)과 동일하다.
    - 자세한 내용은 [FLOAT](#e13294813a67476a)을 참조한다.
- INT
    - NUMBER(10,0)과 동일하다.
    - 자세한 내용은 [NUMBER](#f5ef3006756aba88)를 참조한다.
- INT2
    - NUMBER(5,0)과 동일한다.
    - 자세한 내용은 [NUMBER](#f5ef3006756aba88)를 참조한다.
- INT4
    - NUMBER(10,0)와 동일하다.
    - 자세한 내용은 [NUMBER](#f5ef3006756aba88)를 참조한다.
- INT8
    - NUMBER(19,0)와 동일하다.
    - 자세한 내용은 [NUMBER](#f5ef3006756aba88)를 참조한다.
- INTEGER
    - NUMBER(10,0)와 동일하다.
    - 자세한 내용은 [NUMBER](#f5ef3006756aba88)를 참조한다.
- INTERVAL
    - 자세한 내용은 [INTERVAL](#4ec69af3c45c98df)을 참조한다.
- LONG BINARY VARYING
    - BINARY LONG VARYING과 동일하다.
    - 자세한 내용은 [BINARY LONG VARYING](#2940bef6c30ffc14)을 참조한다.
- LONG CHAR VARYING
    - CHARACTER LONG VARYING과 동일하다.
    - 자세한 내용은 [CHARACTER LONG VARYING](#1f0e795dfcc56d6a)을 참조한다.
- LONG CHARACTER VARYING
    - CHARACTER LONG VARYING과 동일하다.
    - 자세한 내용은 [CHARACTER LONG VARYING](#1f0e795dfcc56d6a)을 참조한다.
- LONG VARCHAR
    - CHARACTER LONG VARYING과 동일하다.
    - 자세한 내용은 [CHARACTER LONG VARYING](#1f0e795dfcc56d6a)을 참조한다.
- NATIVE_BIGINT
    - 자세한 내용은 [NATIVE_BIGINT](#b67a00fdebfeeee9)를 참조한다.
- NATIVE_DOUBLE
    - 자세한 내용은 [NATIVE_DOUBLE](#ffb3593324c1f9be)을 참조한다.
- NATIVE_INTEGER
    - 자세한 내용은 [NATIVE_INTEGER](#63474202cfdaa631)를 참조한다.
- NATIVE_REAL
    - 자세한 내용은 [NATIVE_REAL](#ed1f221dbc872429)을 참조한다.
- NATIVE_SMALLINT
    - 자세한 내용은 [NATIVE_SMALLINT](#ea064187ad5185d3)를 참조한다.
- NUMBER
    - 자세한 내용은 [NUMBER](#f5ef3006756aba88)를 참조한다.
- NUMERIC
    - 자세한 내용은 [NUMERIC](#0f4910fcc7908fb7)을 참조한다.
- ROWID
    - 자세한 내용은 [ROWID](#e7fd0a43c7fa5340)를 참조한다.
- SMALLINT
    - NUMBER(5,0)와 동일하다.
    - 자세한 내용은 [NUMBER](#f5ef3006756aba88)를 참조한다.
- TIME
    - 자세한 내용은 [TIME](#76e4f67c334555fb)을 참조한다.
- TIMESTAMP
    - 자세한 내용은 [TIMESTAMP](#ed6eadaa110af187)를 참조한다.
- VARBINARY
    - BINARY VARYING과 동일하다.
    - 자세한 내용은 [BINARY VARYING](#8028b0efef2db632)을 참조한다.
- VARCHAR
    - CHARACTER VARYING과 동일하다.
    - 자세한 내용은 [CHARACTER VARYING](#81c2c3704f1da6e2)을 참조한다.
- VARCHAR2
    - CHARACTER VARYING과 동일하다.
    - 자세한 내용은 [CHARACTER VARYING](#81c2c3704f1da6e2)을 참조한다.

<a id="56a204fe4b3d1c89"></a>
### BINARY

<a id="ed80be1277b9923f"></a>
#### 구문

```
BINARY [ (length) ]
```

<a id="e4b5607cdd2f9449"></a>
#### 구문 규칙 및 파라미터

- length: Binary string의 길이이다.
    - 범위: 1 ~ 2000
    - 기본값: 1

<a id="fbc66f9e4ab9f183"></a>
#### 설명

고정 길이의 binary string을 저장한다.   
명시된 length 보다 저장되는 binary string의 길이가 짧은 경우, 나머지 부분은 X'00'로 저장된다.  
• 저장 공간의 크기: length 값에 해당하는 bytes

<a id="47d73899cb574dc2"></a>
#### 참조

- [BINARY VARYING](#8028b0efef2db632)
- [BINARY LONG VARYING](#2940bef6c30ffc14)

<a id="8028b0efef2db632"></a>
### BINARY VARYING

<a id="e0a42ec685da7817"></a>
#### 구문

```
BINARY VARYING (length)
```

<a id="99aae74b8538776e"></a>
#### 구문 규칙 및 파라미터

- length: Binary string의 최대 길이이다.
    - 범위: 1 ~ 4000

<a id="d222ce85cc8cb642"></a>
#### 설명

가변 길이의 binary string을 저장한다.

- 저장 공간의 크기: 저장할 binary string의 byte 크기
- Alias name: VARBINARY

<a id="349373123b6aaf17"></a>
#### 참조

- [BINARY](#56a204fe4b3d1c89)
- [BINARY LONG VARYING](#2940bef6c30ffc14)

<a id="2940bef6c30ffc14"></a>
### BINARY LONG VARYING

<a id="c180c23f5bbda024"></a>
#### 구문

```
BINARY LONG VARYING
```

<a id="af6547575e710719"></a>
#### 설명

긴 가변 binary string 값을 저장한다.

- 최대 저장 크기: 100 megabytes
- 저장 공간의 크기: 저장할 binary string의 byte 크기
- Alias names: LONG BINARY VARYING, LONG VARBINARY

Key의 column으로 사용할 수 없어 다음과 같은 제약이 있다.

- 인덱스의 key column으로 사용할 수 없다.
- ORDER BY 절의 expression으로 사용할 수 없다.
- GROUP BY 절의 expression으로 사용할 수 없다.
- DISTINCT 절의 expression으로 사용할 수 없다.
- UNION, INTERSECT, EXCEPT 절의 expression 으로 사용할 수 없다.

<a id="330171ac2c8fd789"></a>
#### 참조

- [BINARY](#56a204fe4b3d1c89)
- [BINARY VARYING](#8028b0efef2db632)

<a id="aca2201d031abe41"></a>
### BOOLEAN

<a id="5215fbcddfbcbd1e"></a>
#### 구문

```
BOOLEAN
```

<a id="4f32ee7f6cdaf2d9"></a>
#### 설명

TRUE 또는 FALSE 값을 저장한다.  
• 저장 공간의 크기: 1 byte

<a id="0319fe09b264cec3"></a>
### CHARACTER

<a id="21c997b487a8912e"></a>
#### 구문

```
CHARACTER [ (length [ CHARACTERS | OCTETS | CHAR | BYTE ] ) ]
```

<a id="abaddb36d040d841"></a>
#### 구문 규칙 및 파라미터

- length: 문자열의 길이이다.
    - 범위: 1 ~ 2000
    - 기본값: 1

- [ CHARACTERS | OCTETS | CHAR | BYTE ]: length의 단위이다.
    - CHARACTERS
        - 문자의 개수이다.
        - CHAR는 CHARACTERS와 동일하다.
    - OCTETS
        - 바이트의 개수이다.
        - BYTE는 OCTETS와 동일하다.
    - 생략할 경우, database를 생성할 때 설정한 [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#aac7ec44c5e984a8) 프로퍼티 값을 따른다.

<a id="fb7c7124e5ecd76b"></a>
#### 설명

고정 길이의 문자열을 저장한다.  
명시된 length 보다 저장되는 string의 길이가 짧은 경우, 나머지 부분에는 공백이 저장된다.

- 저장 공간의 크기: length 값에 해당하는 bytes 크기
- Alias name: CHAR

<a id="4fd7646b6648f227"></a>
#### 참조

- [CHARACTER VARYING](#81c2c3704f1da6e2)
- [CHARACTER LONG VARYING](#1f0e795dfcc56d6a)

<a id="81c2c3704f1da6e2"></a>
### CHARACTER VARYING

<a id="fd234073dd1255de"></a>
#### 구문

```
CHARACTER VARYING ( length [ CHARACTERS | OCTETS | CHAR | BYTE ] )
```

<a id="eb710922d5c5a452"></a>
#### 구문 규칙 및 파라미터

- length: 문자열의 길이이다.
    - Range: 1 ~ 4000

- [ CHARACTERS | OCTETS | CHAR | BYTE ]: length의 단위이다.
    - CHARACTERS
        - 문자의 개수이다.
        - CHAR는 CHARACTERS 와 동일하다.
    - OCTETS
        - 바이트의 개수이다.
        - BYTE는 OCTETS와 동일하다.
    - 생략할 경우, database를 생성할 때 설정한 [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#aac7ec44c5e984a8) 프로퍼티 값을 따른다.

<a id="4b7758c73703fdc2"></a>
#### 설명

가변 길이의 문자열을 저장한다.

- 저장 공간의 크기 : 저장할 문자열의 byte 크기
- Alias names: VARCHAR, VARCHAR2

<a id="8d95cb3c7a4d575c"></a>
#### 참조

- [CHARACTER](#0319fe09b264cec3)
- [CHARACTER LONG VARYING](#1f0e795dfcc56d6a)

<a id="1f0e795dfcc56d6a"></a>
### CHARACTER LONG VARYING

<a id="8a52513f2bf08352"></a>
#### 구문

```
CHARACTER LONG VARYING
```

<a id="9e24dafaaf70cf86"></a>
#### 설명

긴 가변 문자열 값을 저장한다.

- 최대 저장 크기: 100 megabytes
- 저장 공간의 크기: 저장할 문자열의 byte 크기
- Alias names: LONG CHARACTER VARYING, LONG CHAR VARYING, LONG VARCHAR

Key의 column으로 사용할 수 없어 다음과 같은 제약이 있다.

- 인덱스의 key column으로 사용할 수 없다.
- ORDER BY 절의 expression으로 사용할 수 없다.
- GROUP BY 절의 expression으로 사용할 수 없다.
- DISTINCT 절의 expression으로 사용할 수 없다.
- UNION, INTERSECT, EXCEPT 절의 expression으로 사용할 수 없다.

<a id="3b96d6e0b2ead915"></a>
#### 참조

- [CHARACTER](#0319fe09b264cec3)
- [CHARACTER VARYING](#81c2c3704f1da6e2)

<a id="d88d47b21d661aa7"></a>
### DATE

<a id="983f097f7bf109f3"></a>
#### 구문

```
DATE
```

<a id="a831028c66451a38"></a>
#### 설명

YEAR, MONTH, DAY, HOUR, MINUTE, SECOND (fractional seconds 제외)를 포함하는 날짜 형식이다.

- 값의 범위: '4714-11-24 BC' ~ '9999-12-31 AD' 범위의 날짜값
- 저장 공간의 크기: 8 bytes

<a id="1bbb5f711f941ef0"></a>
#### 참조

- [Date Literals](#50cfb81da3af2ea1)
- [TIME](#76e4f67c334555fb)
- [TIMESTAMP](#ed6eadaa110af187)

<a id="e13294813a67476a"></a>
### FLOAT

<a id="e7417005f5f33ba1"></a>
#### 구문

```
FLOAT[ ( precision ) ]
```

<a id="a6a28238304d40f8"></a>
#### 구문 규칙 및 파라미터

- precision: 유효 숫자의 이진 정밀도이다.
    - precision의 범위: 1 ~ 126
    - 기본값: 126

<a id="ce742c3e5b527202"></a>
#### 설명

이진 정밀도를 가지는 부동 소수점 값을 저장한다.

- 지수 범위: 1E-130 ~ 1E+125
- 저장 공간의 크기: (정수자리수 + 1) / 2 + (소수자리수 + 1) / 2 + 1 (Exponent와 sign 정보)

[NUMBER](#f5ef3006756aba88), [NUMERIC](#0f4910fcc7908fb7) 타입과 달리 이진 precision 값을 갖는다.

- Alias names: REAL = FLOAT(24), DOUBLE = FLOAT(53), DOUBLE PRECISION = FLOAT(53), FLOAT4 = FLOAT(24), FLOAT8 = FLOAT(53)

<a id="334b585f6212ef3f"></a>
#### 참조

- [NUMBER](#f5ef3006756aba88)
- [NUMERIC](#0f4910fcc7908fb7)

<a id="4ec69af3c45c98df"></a>
### INTERVAL

<a id="2895c57ff7ae64ff"></a>
#### 구문

```
<interval_type> ::=
      INTERVAL YEAR [ ( leading_precision ) ] 
    | INTERVAL MONTH [ ( leading_precision ) ] 
    | INTERVAL DAY [ ( leading_precision ) ] 
    | INTERVAL HOUR [ ( leading_precision ) ] 
    | INTERVAL MINUTE [ ( leading_precision ) ]
    | INTERVAL SECOND [ ( leading_precision  [ , fractional_seconds_precision ] ) ]
    | INTERVAL YEAR [ ( leading_precision ) ] TO MONTH
    | INTERVAL DAY [ ( leading_precision ) ] TO HOUR
    | INTERVAL DAY [ ( leading_precision ) ] TO MINUTE
    | INTERVAL DAY [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]
    | INTERVAL HOUR [ ( leading_precision ) ] TO MINUTE
    | INTERVAL HOUR [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]
    | INTERVAL MINUTE [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]
```

<a id="56dc8197dff09ba7"></a>
#### 구문 규칙 및 파라미터

- INTERVAL YEAR [ ( leading_precision ) ]: YEAR의 기간을 저장한다. 
    - leading_precision
        - YEAR의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2

- INTERVAL MONTH [ ( leading_precision ) ]: MONTH의 기간을 저장한다.
    - leading_precision
        - MONTH의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2

- INTERVAL YEAR [ ( leading_precision ) ] TO MONTH: YEAR 와 MONTH 의 기간을 저장한다.
    - leading_precision
        - YEAR의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2

- INTERVAL DAY [ ( leading_precision ) ]: DAY의 기간을 저장한다.
    - leading_precision
        - DAY의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2

- INTERVAL HOUR [ ( leading_precision ) ]: HOUR의 기간을 저장한다.
    - leading_precision
        - HOUR의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2

- INTERVAL MINUTE [ ( leading_precision ) ]: MINUTE의 기간을 저장한다.
    - leading_precision
        - MINUTE의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2

- INTERVAL SECOND [ ( leading_precision [ , fractional_seconds_precision ] ) ]: SECOND의 기간을 저장한다.
    - leading_precision
        - SECOND의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2
    - fractional_seconds_precision
        - fractional seconds의 digit 수
        - 값의 범위: 0 ~ 6
        - 기본값: 6

- INTERVAL DAY [ ( leading_precision ) ] TO HOUR: DAY 와 HOUR 의 기간을 저장한다.
    - leading_precision
        - DAY의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2

- INTERVAL DAY [ ( leading_precision ) ] TO MINUTE: DAY, HOUR, MINUTE 의 기간을 저장한다.
    - leading_precision
        - DAY의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2

- INTERVAL DAY [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]: DAY, HOUR, MINUTE, SECOND의 기간을 저장한다.
    - leading_precision
        - DAY의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2
    - fractional_seconds_precision
        - fractional seconds의 digit 수
        - 값의 범위: 0 ~ 6
        - 기본값: 6

- INTERVAL HOUR [ ( leading_precision ) ] TO MINUTE: HOUR 와 MINUTE 의 기간을 저장한다.
    - leading_precision
        - HOUR의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2

- INTERVAL HOUR [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]: HOUR, MINUTE, SECOND 의 기간을 저장한다.
    - leading_precision
        - HOUR의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2
    - fractional_seconds_precision
        - fractional seconds의 digit 수
        - 값의 범위: 0 ~ 6
        - 기본값: 6

- INTERVAL MINUTE [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]: MINUTE 와 SECOND 의 기간을 저장한다.
    - leading_precision
        - MINUTE의 digit 수
        - 값의 범위: 2 ~ 6
        - 기본값: 2
    - fractional_seconds_precision
        - fractional seconds의 digit 수
        - 값의 범위: 0 ~ 6
        - 기본값: 6

<a id="d410830e74ce04d4"></a>
#### 설명

INTERVAL 타입은 값의 표현 범위에 따라 다음과 같이 YEAR TO MONTH 계열과 DAY TO SECOND 계열로 구분할 수 있다.

- YEAR TO MONTH 계열: 저장공간의 크기는 8 byte이다.
    - INTERVAL YEAR
    - INTERVAL MONTH
    - INTERVAL YEAR TO MONTH

- DAY TO SECOND 계열: 저장 공간의 크기는 16 byte이다.
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

leading_precision이 지정된 field에 지정된 digit 이상의 숫자가 올 경우, 에러를 반환한다.  
fractional_seconds_precision이 지정된 field에 지정된 digit 이상의 숫자가 올 경우, 반올림된다.

**INTERVAL * TO * 에서 두 번째 이후 field의 precision과 값의 범위**

<a id="75ce4e51b242fc31"></a>
| Field | Precision | 값의 범위 |
| --- | --- | --- |
| MONTH | 2 | 0 ~ 11 |
| HOUR | 2 | 0 ~ 23 |
| MINUTE | 2 | 0 ~ 59 |
| SECOND(소수점 이전값) | 2 | 0 ~ 59 |

<a id="22369ddf5395bf06"></a>
#### 참조

자세한 내용은 [Interval Literals](#074711f4a241633b)를 참조한다.

<a id="b67a00fdebfeeee9"></a>
### NATIVE_BIGINT

<a id="b107baceeafd41f7"></a>
#### 구문

```
NATIVE_BIGINT
```

<a id="7d503089b8624974"></a>
#### 설명

Signed 8 byte 정수를 저장한다.

C 언어의 long long (8 bytes integer)과 동일하다.

- 값의 범위: -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807
- 저장 공간의 크기: 8 bytes

<a id="ffb3593324c1f9be"></a>
### NATIVE_DOUBLE

<a id="b515d551025326f8"></a>
#### 구문

```
NATIVE_DOUBLE
```

<a id="106da3ae2a6a5638"></a>
#### 설명

Double precision floating-point number (8 bytes)를 저장한다.

C 언어의 double과 동일하다.

- 지수값의 범위: 1E-307 ~ 1E+308 
- 저장 공간의 크기: 8 bytes

<a id="63474202cfdaa631"></a>
### NATIVE_INTEGER

<a id="925273929b80e854"></a>
#### 구문

```
NATIVE_INTEGER
```

<a id="68c3144ba6902216"></a>
#### 설명

Signed 4 byte 정수를 저장한다.

C 언어의 integer (4 bytes)와 동일하다.

- 값의 범위: -2,147,483,648 ~ +2,147,483,647
- 저장 공간의 크기: 4 bytes

<a id="ed1f221dbc872429"></a>
### NATIVE_REAL

<a id="1764cad3982b9219"></a>
#### 구문

```
NATIVE_REAL
```

<a id="a532eef13b7f94ba"></a>
#### 설명

Single precision floating-point number (4 bytes)를 저장한다.

C 언어의 float과 동일하다.

- 지수값의 범위: 1E-37 ~ 1E+37 
- 저장 공간의 크기: 4 bytes

<a id="ea064187ad5185d3"></a>
### NATIVE_SMALLINT

<a id="c729aaf3c8d1aa37"></a>
#### 구문

```
NATIVE_SMALLINT
```

<a id="f6136b61d2f60bdf"></a>
#### 설명

Signed 2 byte 정수를 저장한다.

C 언어의 short과 동일하다.

- 값의 범위: -32,768 ~ 32,767
- 저장 공간의 크기: 2 bytes

<a id="f5ef3006756aba88"></a>
### NUMBER

<a id="fad1d68812c862fe"></a>
#### 구문

```
NUMBER  [ ( precision [ , scale ] ) ]
```

<a id="6325aa8403213832"></a>
#### 구문 규칙 및 파라미터

- NUMBER: precision과 scale이 없는 부동 소수점 숫자를 저장한다.
    - 유효 숫자의 범위: 38
    - 지수값의 범위: 1E-130 ~ 1E+125
    - FLOAT(126)과 동일하다.

- NUMBER(precision): precision의 유효 자리수를 가지는 정수를 저장한다.
    - Precision의 범위: 1 ~ 38
    - Scale의 값: 0
    - [FLOAT](#e13294813a67476a) 타입과 달리 십진 precision 값을 갖는다.
    - NUMBER(precision, 0), NUMERIC(precision, 0)과 동일하다.

- NUMBER(precision, scale): precision과 scale을 갖는 고정 소수점 숫자를 저장한다.
    - Precision의 범위: 1 ~ 38
    - Scale의 범위: -84 ~ 127
    - [FLOAT](#e13294813a67476a) 타입과 달리 십진 precision 값을 갖는다.
    - NUMERIC(precision, scale)과 동일하다.
    - Alias names: SMALLINT = NUMBER(5,0), INTEGER = NUMBER(10,0), BIGINT = NUMBER(19,0), INT2 = NUMBER(5,0), INT4 = NUMBER(10,0), INT8 = NUMBER(19,0)

<a id="4d22cd226f71fdef"></a>
#### 설명

NUMBER 타입은 NUMERIC 타입과 비슷하지만 precision과 scale을 모두 생략할 경우 NUMBER 타입은 precision과 scale이 정해지지 않은 부동 소수점 숫자를 저장한다는 점이 다르다.

- precision, scale이 없는 NUMBER: 부동 소수점 숫자
- precision, scale이 없는 NUMERIC: NUMERIC(38,0)의 고정 소수점 숫자
- 저장 공간의 크기: (정수자리수 + 1) / 2 + (소수자리수 + 1) / 2 + 1 (Exponent와 sign 정보)

<a id="603c7afaf5ecfca6"></a>
#### 참조

- [FLOAT](#e13294813a67476a)
- [NUMERIC](#0f4910fcc7908fb7)

<a id="0f4910fcc7908fb7"></a>
### NUMERIC

<a id="721a3fa310d9af85"></a>
#### 구문

```
NUMERIC  [ ( precision [ , scale ] ) ]
```

<a id="3883960bb766dd58"></a>
#### 구문 규칙 및 파라미터

- precision: 유효 숫자의 십진 정밀도이다.
    - precision의 범위: 1 ~ 38
    - 기본값: 38

- scale: 소수점의 범위이다.
    - scale의 범위: -84 ~ 127
    - 기본값: 0

<a id="f1f29dcdf3ac4052"></a>
#### 설명

precision과 scale을 갖는 고정 소수점 숫자를 저장한다.

precision과 scale을 생략할 경우, 다음과 같은 의미를 갖는다.

- NUMERIC = NUMERIC(38,0)
- NUMERIC(p) = NUMERIC(p,0)

NUMBER 타입은 NUMERIC 타입과 비슷하지만 precision과 scale을 모두 생략할 경우 NUMBER 타입은 precision과 scale이 정해지지 않은 부동 소수점 숫자를 저장한다는 점이 다르다.

- precision, scale이 없는 NUMBER: 부동 소수점 숫자
- precision, scale이 없는 NUMERIC: NUMERIC(38,0)의 고정 소수점 숫자
- 저장 공간의 크기: (정수자리수 + 1) / 2 + (소수자리수 + 1) / 2 + 1 (Exponent와 sign 정보)

<a id="71f0c099631c45bf"></a>
#### 참조

- [FLOAT](#e13294813a67476a)
- [NUMBER](#f5ef3006756aba88)

<a id="e7fd0a43c7fa5340"></a>
### ROWID

<a id="69669ae0ccde8870"></a>
#### 구문

```
ROWID
```

<a id="bf149efeb3864a5a"></a>
#### 설명

ROWID 타입은 레코드 식별자 (ROWID)를 저장한다.  

레코드 식별자 (ROWID)는 데이터베이스 내 각 레코드의 식별정보이다.  

ROWID pseudo column을 조회하면 각각의 레코드식별자 (ROWID) 값을 확인할 수 있는데, 이 ROWID pseudo column은 ROWID data type 정보를 갖는다.

Standalone system에서의 ROWID 타입의 구성요소는 다음과 같다.  
• OBJECT_ID   
• TABLESPACE_ID   
• PAGE_ID   
• PAGE 내 OFFSET

Cluster system에서의 ROWID 타입의 구성요소는 다음과 같다.  
• GRID_BLOCK_SEQUENCE  
• GRID_BLOCK_ID  
• MEMBER_ID  
• SHARD_ID

ROWID는 A~Z, a~z, 0~9, +, / 를 포함할 수 있는 base 64 value로 저장된다.  
ROWID-related functions를 이용하여 ROWID 각각의 구성요소 정보를 얻을 수 있다.

- 저장 공간의 크기: 16 bytes

<a id="5fa6a57d517ab1d8"></a>
#### 참조

- [ROWID Pseudo Column](#79cc06caf35b0f50)
- [ROWID-Related Functions](#9e953b8caa2ecc27)

<a id="76e4f67c334555fb"></a>
### TIME

<a id="c98a654daec37dc4"></a>
#### 구문

```
TIME [ ( fractional_seconds_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
```

<a id="de9ec1ce43b1f812"></a>
#### 구문 규칙 및 파라미터

- fractional_seconds_precision: fractional seconds의 유효자리 수이다.
    - fractional_seconds_precision의 범위: 0 ~ 6
    - 기본값: 6

- [ WITH TIME ZONE | WITHOUT TIME ZONE ]: TIME ZONE 값 저장 여부이다.
    - WITH TIME ZONE: time zone을 포함한 시간
    - WITHOUT TIME ZONE: time zone을 포함하지 않는 시간
    - 기본값: WITHOUT TIME ZONE

<a id="49dc13f9f3e004cf"></a>
#### 설명

HOUR, MINUTE, SECOND를 가지는 시간을 저장한다.

- 저장 공간의 크기 
    - TIME WITHOUT TIME ZONE: 8 bytes
    - TIME WITH TIME ZONE: 12 bytes

<a id="06e5e1d3ade95179"></a>
#### 참조

- [Time Literals](#7bc449ae26138f1e)
- [Time with time zone Literals](#1a1e19946e2775d4)
- [DATE](#d88d47b21d661aa7)
- [TIMESTAMP](#ed6eadaa110af187)

<a id="ed6eadaa110af187"></a>
### TIMESTAMP

<a id="8af3c1802656c605"></a>
#### 구문

```
TIMESTAMP [ ( fractional_seconds_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
```

<a id="7c68ddb9dfb85dc3"></a>
#### 구문 규칙 및 파라미터

- fractional_seconds_precision: fractional seconds의 유효자리 수이다.
    - fractional_seconds_precision의 범위: 0 ~ 6
    - 기본값: 6

- [ WITH TIME ZONE | WITHOUT TIME ZONE ]: TIME ZONE 값 저장 여부이다.
    - WITH TIME ZONE: time zone을 포함한 시간
    - WITHOUT TIME ZONE: time zone을 포함하지 않는 시간
    - 기본값: WITHOUT TIME ZONE

<a id="1fd94623242258bf"></a>
#### 설명

YEAR, MONTH, DATE, HOUR, MINUTE, SECOND를 가지는 시간을 저장한다.

- 저장 공간의 크기 
    - TIMESTAMP WITHOUT TIME ZONE: 8 bytes
    - TIMESTAMP WITH TIME ZONE: 12 bytes

<a id="f154731c33f69076"></a>
#### 참조

- [Timestamp Literals](#6ded9709553c29d8)
- [Timestamp with time zone Literals](#c4f6475f9736fb4f)
- [DATE](#d88d47b21d661aa7)
- [TIME](#76e4f67c334555fb)

<a id="6b04ecd3e2e99924"></a>
## Built-in Function References

<a id="2295658d1c028dca"></a>
### * (MULTIPLICATION)

<a id="bde2af5838e8a398"></a>
#### 구문

```
expr1 * expr2
```

<a id="6cf63503b9716b10"></a>
#### 설명

expr1과 expr2의 곱하기 연산결과를 반환한다.

곱하기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](#e2c21b3a3eaedfd1)을 참조한다.

**숫자형 * 연산**

<a id="9b80b3410d6ead4a"></a>
| expr1 (expr2) | expr2 (expr1) | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="7418bac6e238a7d4"></a>
<table class="table column_count_3"><caption>INTERVAL * 연산 </caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>숫자형 타입</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>숫자형 타입</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(결과 타입은 interval type 이다.)</div></td></tr><tr><td class="to_left to_middle" colspan="3"><div>자세한 내용은 <a class="reference text" href="#79fcd4f4c52365cd">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

**표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입**

<a id="79fcd4f4c52365cd"></a>
<table><thead><tr><th align="center">INTERVAL YEAR TO MONTH</th><th align="center">INTERVAL DAY TO SECOND</th></tr></thead><tbody><tr><td valign="middle"><ul><li>INTERVAL YEAR</li><li>INTERVAL MONTH</li><li>INTERVAL YEAR TO MONTH</li></ul></td><td valign="middle"><ul><li>INTERVAL DAY</li><li>INTERVAL HOUR</li><li>INTERVAL MINUTE</li><li>INTERVAL SECOND</li><li>INTERVAL DAY TO HOUR</li><li>INTERVAL DAY TO MINUTE</li><li>INTERVAL DAY TO SECOND</li><li>INTERVAL HOUR TO MINUTE</li><li>INTERVAL HOUR TO SECOND</li><li>INTERVAL MINUTE TO SECOND</li></ul></td></tr></tbody></table>

<a id="4323846224b6211e"></a>
#### 사용 예

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

<a id="592787f61a1066b5"></a>
### + (ADDITION)

<a id="bad68206a02a5ecf"></a>
#### 구문

```
expr1 + expr2
```

<a id="3c45aebebfa36247"></a>
#### 설명

expr1과 expr2의 더하기 연산 결과를 반환한다.

더하기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](#e2c21b3a3eaedfd1)을 참조한다.

**숫자형 + 연산**

<a id="e343370b96f349eb"></a>
| expr1 (expr2) | expr2 (expr1) | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="c39cfb6595d9d201"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) + 연산</caption><thead><tr><th class="to_center"><div>expr1 (expr2)</div></th><th class="to_center"><div>expr2 (expr1)</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>NUMERIC</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td class="to_middle" colspan="3"><div>자세한 내용은 <a class="reference text" href="#79fcd4f4c52365cd">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="4559c142db19fff8"></a>
#### 사용 예

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

<a id="e2ac63d1d885b4d2"></a>
### + (POSITIVE)

<a id="581bdd279e3934d9"></a>
#### 구문

```
+ expr
```

<a id="d461efaa04826ee8"></a>
#### 설명

expr에 + 부호를 표시한다.

<a id="c142dc8d505d9977"></a>
#### 사용 예

```
gSQL> SELECT +3 AS RESULT1, +(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      3      -3
1 row selected.
```

<a id="9a10c5280234a50d"></a>
### - (NEGATIVE)

<a id="e3f275356daece46"></a>
#### 구문

```
- expr
```

<a id="0af3b511924dfb0a"></a>
#### 설명

expr에 - 부호를 표시한다.

<a id="845767fa16dc2578"></a>
#### 사용 예

```
gSQL> SELECT -3 AS RESULT1, -(-3) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     -3       3
1 row selected.
```

<a id="5e8dfac15abd6dff"></a>
### - (SUBTRACTION)

<a id="0faf131a32adeba1"></a>
#### 구문

```
expr1 - expr2
```

<a id="2bbe5ca8a7f2a355"></a>
#### 설명

expr1과 expr2의 뺄셈 연산 결과를 반환한다.

뺄셈 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](#e2c21b3a3eaedfd1)을 참조한다.

**숫자형 - 연산**

<a id="c974d559298b802d"></a>
| expr1 | expr2 | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_BIGINT |
| NUMBER | NUMBER | NUMBER |
| NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="37ef14f6b01fc36c"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL) - 연산</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>NUMBER</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY</div></td><td class="to_middle"><div>DATE</div></td></tr><tr><td class="to_middle"><div>DATE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIME WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIME WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>TIMESTAMP WITH TIME ZONE</div></td></tr><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(expr1과 expr2의 interval 범위를 모두 포함할 수 있는 타입으로 결정된다.)</div></td></tr><tr><td colspan="3"><div>자세한 내용은 <a class="reference text" href="#79fcd4f4c52365cd">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="972fba50203f929d"></a>
#### 사용 예

```
gSQL> SELECT 
      TO_DATE( '2012-05-05' ) - TO_DATE( '2012-01-01' ) AS RESULT 
      FROM DUAL;
RESULT
------
   125
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
      INTERVAL'05-11'YEAR TO MONTH - INTERVAL'02-01'YEAR TO MONTH 
      AS RESULT 
      FROM DUAL;
RESULT    
----------
+000003-10
1 row selected.

gSQL> SELECT INTERVAL'15 23:59:59.999999'DAY TO SECOND 
           - INTERVAL'10 23:59:59.999999'DAY TO SECOND AS RESULT 
      FROM DUAL;
RESULT                 
-----------------------
+000005 00:00:00.000000
1 row selected.
```

<a id="de1584725d82cfa4"></a>
### / (DIVISION)

<a id="e0e9fcf7f89c17bb"></a>
#### 구문

```
expr1 / expr2
```

<a id="b21d6e34d4309952"></a>
#### 설명

expr1과 expr2의 나누기 연산 결과를 반환한다.

나누기 연산의 종류와 결과 타입은 다음 표와 같다.  
자세한 내용은 [타입간 변환](#e2c21b3a3eaedfd1)을 참조한다.

**숫자형/ 연산**

<a id="c21f0027fa0a22dd"></a>
| expr1 | expr2 | 결과 타입 |
| --- | --- | --- |
| NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER | NUMBER |
| NATIVE_DOUBLE | NATIVE_DOUBLE | NATIVE_DOUBLE |

<a id="d04659902c85e806"></a>
<table class="table column_count_3"><caption>(DATETIME/INTERVAL)/ 연산</caption><thead><tr><th class="to_center"><div>expr1</div></th><th class="to_center"><div>expr2</div></th><th class="to_center"><div>결과 타입</div></th></tr></thead><tbody><tr><td class="to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>INTERVAL YEAR TO MONTH
(결과 타입은 interval type이다.)</div></td></tr><tr><td class="to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_middle"><div>숫자 타입</div></td><td class="to_middle"><div>INTERVAL DAY TO SECOND
(결과 타입은 interval type이다.)</div></td></tr><tr><td class="to_middle" colspan="3"><div>자세한 내용은 <a class="reference text" href="#79fcd4f4c52365cd">표에 표기된 INTERVAL 타입이 포함하는 INTERVAL 세부타입 </a>을 참조한다.</div></td></tr></tbody></table>

<a id="0f93a9b8118bff1d"></a>
#### 사용 예

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

<a id="d94be4d95c59affd"></a>
### || (CONCATENATE)

<a id="d98abef4c3078218"></a>
#### 구문

```
str1 || str2
```

<a id="d1b8fa68ad4171a6"></a>
#### 설명

CONCATENATE는 str1과 str2를 연결한 문자열을 반환한다.  
str1과 str2 중 하나가 null인 경우 null이 아닌 나머지 str이 반환되고, str1과 str2가 모두 null인 경우 NULL이 반환된다.

인자로는 character string 타입 또는 binary string 타입으로 변환될 수 있는 타입이 올 수 있다.  
자세한 내용은 [타입간 변환](#e2c21b3a3eaedfd1)을 참조한다.

[CONCAT](#537e3c54efdacfea), [CONCATENATE](#0d6daaed8ec3a38c)의 alias 이다.

결과 타입은 다음 표와 같다.

**|| (CONCATENATE)의 결과 타입**

<a id="5d3451570573d876"></a>
| Data type | CHAR | VARCHAR | LONG VARCHAR |
| --- | --- | --- | --- |
| CHAR | CHAR | VARCHAR | LONG VARCHAR |
| VARCHAR | VARCHAR | VARCHAR | LONG VARCHAR |
| LONG VARCHAR | LONG VARCHAR | LONG VARCHAR | LONG VARCHAR |
| Data type | BINARY | VARBINARY | LONG VARBINARY |
| BINARY | BINARY | VARBINARY | LONG VARBINARY |
| VARBINARY | VARBINARY | VARBINARY | LONG VARBINARY |
| LONG VARBINARY | LONG VARBINARY | LONG VARBINARY | LONG VARBINARY |

<a id="eb271139214b5c4b"></a>
#### 사용 예

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

<a id="cdc75e007d23703d"></a>
### ABS

<a id="5bf245b575ca400e"></a>
#### 구문

```
ABS( num )
```

<a id="f1a9cd52c064a9a0"></a>
#### 설명

ABS는 num의 절대값을 반환한다.  
인자 num에는 숫자 타입 또는 숫자로 변환될 수 있는 타입이 올 수 있다.

<a id="9e1b9b5198736928"></a>
#### 사용 예

```
gSQL> SELECT ABS(-1) AS RESULT1, ABS(1) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1       1
1 row selected.
```

<a id="d77b80d8e19d8536"></a>
### ACOS

<a id="cd2bcb3351cb224b"></a>
#### 구문

```
ACOS( num )
```

<a id="df9eb204acc75df0"></a>
#### 설명

ACOS 함수는 num의 arc cosine 값을 반환한다.  
인자 num은 -1 이상 1 이하의 값이어야 한다.  
0 ~ pi 사이의 라디안 값을 반환한다.

<a id="08a1cd068ca4030a"></a>
#### 사용 예

```
gSQL> SELECT ACOS( 1 ) FROM DUAL;
ACOS( 1 )
---------
        0
1 row selected.
```

<a id="40e97b19083d297e"></a>
### ADDDATE

<a id="f6746b713aef8537"></a>
#### 구문

```
ADDDATE( date, INTERVAL expr unit  )
ADDDATE( expr, days )
```

<a id="2f55996e15827e50"></a>
#### 설명

ADDDATE는 입력받은 첫 번째 인자에 두 번째 인자를 더하기 연산하여 그 결과를 반환한다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.  
첫 번째 인자에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있고, 두 번째 인자에는 INTERVAL 또는 숫자 타입이 올 수 있다.

결과 타입은 [(DATETIME/INTERVAL) + 연산](#c39cfb6595d9d201)과 동일하다.

<a id="7dffc3bbeb855813"></a>
#### 사용 예

```
gSQL> SELECT ADDDATE( TO_DATE( '2012-12-12', 'YYYY-MM-DD' ), 1 ) AS RESULT
        FROM DUAL;
RESULT    
----------
2012-12-13
1 row selected.

gSQL> SELECT ADDDATE( TO_DATE( '2012-12-12', 'YYYY-MM-DD' ),
                      INTERVAL'01-01'YEAR TO MONTH ) AS RESULT 
        FROM DUAL;
RESULT    
----------
2014-01-12
1 row selected.
```

<a id="7a026839b36e206e"></a>
### ADDTIME

<a id="f71ad570e6e9203b"></a>
#### 구문

```
ADDTIME( expr1, expr2 )
```

<a id="668fc50dce29cf6d"></a>
#### 설명

ADDTIME은 입력받은 expr2를 expr1에 더하여 그 결과를 반환한다.

expr1이나 expr2가 NULL이면 결과값은 NULL이다.  
expr1에는 TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE TYPE이 올 수 있고, expr2에는 INTERVAL DAY TO SECOND TYPE이 올 수 있다.

결과 타입은 [(DATETIME/INTERVAL) + 연산](#c39cfb6595d9d201)과 동일하다.

<a id="782f1365cac6903c"></a>
#### 사용 예

```
gSQL> SELECT 
      ADDTIME( TO_TIMESTAMP( '2001-05-10 11:22:33', 
                             'YYYY-MM-DD HH24:MI:SS' ),
               INTERVAL'0 01:02:03.999999'DAY TO SECOND ) AS RESULT
        FROM DUAL;
RESULT                    
--------------------------
2001-05-10 12:24:36.999999
1 row selected.
```

<a id="51e0fc91626ae36e"></a>
### ADD_MONTHS

<a id="6745ad40e51eef67"></a>
#### 구문

```
ADD_MONTHS( date, number )
```

<a id="e09dda833a99d8dc"></a>
#### 설명

ADD_MONTHS는 date에 number 숫자만큼의 달을 더한 값을 반환한다.  
입력 인자의 값이 하나라도 NULL이면 결과값도 NULL이다.  
만약 ADD_MONTHS 연산 후에 날짜가 그 달의 마지막 날보다 큰 경우에는 마지막 날짜로 조정한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있으며 인자 number에는 숫자타입이 올 수 있다.

결과 타입은 입력 인자 date 타입과 관계없이 항상 DATE 타입이다.

<a id="f378339497c77b76"></a>
#### 사용 예

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

<a id="765ca8767a695cf4"></a>
### ASCII

<a id="40d8857438322a89"></a>
#### 구문

```
ASCII( char )
```

<a id="4ed3820cf6340d62"></a>
#### 설명

char의 첫 번째 문자에 대한 database character set code를 십진수로 반환한다.

char에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있고, 반환되는 타입은 NUMBER 이다.

<a id="1a56953f68474d95"></a>
#### 사용 예

```
gSQL> SELECT ASCII( 'G' ) AS RESULT FROM DUAL;
RESULT
------
    71
1 row selected.
```

<a id="7c4475009f3e7ebf"></a>
### ASIN

<a id="f19ad3d3b267a03c"></a>
#### 구문

```
ASIN( num )
```

<a id="685a4693df219e6d"></a>
#### 설명

ASIN 함수는 num의 arc sin 값을 반환한다.  
인자 num은 -1 이상 1 이하의 값이어야 한다.  
-pi/2 ~ pi/2 사이의 라디안 값을 반환한다.

<a id="b3f2ac0b3ed7709d"></a>
#### 사용 예

```
gSQL> SELECT ASIN( 0 ) FROM DUAL;
ASIN( 0 )
---------
        0
1 row selected.
```

<a id="f0bb534f040bf687"></a>
### ATAN

<a id="9f38fe3fa3131bf2"></a>
#### 구문

```
ATAN( num )
```

<a id="048cf57c78389ad8"></a>
#### 설명

ATAN 함수는 num의 arc tangent 값을 반환한다.  
num 값 범위의 제한은 없으며, -pi/2 ~ pi/2 사이의 라디안 값을 반환한다.

<a id="339154973c01b178"></a>
#### 사용 예

```
gSQL> SELECT ATAN( 1 ) FROM DUAL;
       ATAN( 1 )
----------------
.785398163397448
1 row selected.
```

<a id="c9188058f006314a"></a>
### ATAN2

<a id="c08bbf991c190749"></a>
#### 구문

```
ATAN2( num1, num2 )
```

<a id="2e93e3d4ed242847"></a>
#### 설명

ATAN2 함수는 num1과 num2의 arc tangent 값을 반환한다.  
인자 num1 값 범위의 제한은 없으며, -pi ~ pi 사이의 라디안 값을 반환한다.

<a id="65e22e934a68de15"></a>
#### 사용 예

```
gSQL> SELECT ATAN2( 1, 0 ) FROM DUAL;
  ATAN2( 1, 0 )
---------------
1.5707963267949
1 row selected.
```

<a id="d90586b18f2f93a9"></a>
### AVG

<a id="a7ded599cbe98453"></a>
#### 구문

```
AVG( [ ALL | DISTINCT ] num )
```

<a id="c4d899d711f0d3f6"></a>
#### 설명

Aggregation 함수로써 expr 들의 평균값을 얻는데 사용된다.

ALL을 명시한 경우, 모든 값들에 대한 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복 제거한 값들에 대한 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

<a id="8d1b7dda035c6560"></a>
#### 사용 예

```
gSQL> SELECT AVG(c1) FROM t1;

AVG(C1)
-------
      2

1 row selected.
```

<a id="5cdf6e42f3b08d6b"></a>
### BITAND

<a id="c720e097ec91a4ad"></a>
#### 구문

```
BITAND( num1, num2 )
```

<a id="a91b9526659f99fb"></a>
#### 설명

num1과 num2의 비트에 대한 AND 연산 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.

결과 타입은 NATIVE_BIGINT이다.

<a id="e2db53aa436d2476"></a>
#### 사용 예

```
gSQL> SELECT BITAND( 5, 3 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="477fbc480f8f4223"></a>
### BITNOT

<a id="ccb95ab005cc33be"></a>
#### 구문

```
BITNOT( num )
```

<a id="763309fa1e2b14a6"></a>
#### 설명

num의 비트에 대해 NOT 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.

결과 타입은 다음과 같다.  
• 입력 인자가 NATIVE_SMALLINT인 경우, NATIVE_SMALLINT  
• 입력 인자가 NATIVE_INTEGER인 경우, NATIVE_INTEGER  
• 입력 인자가 NATIVE_BIGINT인 경우, NATIVE_BIGINT

<a id="4acd9cec1e20f329"></a>
#### 사용 예

```
gSQL> SELECT BITNOT( 5 ) AS RESULT FROM DUAL;
RESULT
------
    -6
1 row selected.
```

<a id="48bff810dd5edcf4"></a>
### BITOR

<a id="258fa822841ef0a6"></a>
#### 구문

```
BITOR( num1, num2 )
```

<a id="5cc75c511bbb7c2a"></a>
#### 설명

num1과 num2의 비트에 대해 OR 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.

결과 타입은 NATIVE_BIGINT이다.

<a id="19a8dba943102650"></a>
#### 사용 예

```
gSQL> SELECT BITOR( 5, 3 ) FROM DUAL;

BITOR( 5, 3 )
-------------
            7
1 row selected.
```

<a id="2d8311646e3b2ce1"></a>
### BITXOR

<a id="c95b8c7b96e98b61"></a>
#### 구문

```
BITXOR( num1, num2 )
```

<a id="2bf52f23672e3f0d"></a>
#### 설명

num1과 num2의 비트에 대해 XOR 연산한 결과를 반환한다.

입력 인자에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환할 때 소수점은 TRUNCATE 된다.

결과 타입은 NATIVE_BIGINT이다.

<a id="d5b74ab89120dc2f"></a>
#### 사용 예

```
gSQL> SELECT BITXOR( 5, 3 ) FROM DUAL;
BITXOR( 5, 3 )
--------------
             6
1 row selected.
```

<a id="f2491c65ea403713"></a>
### BIT_LENGTH

<a id="d544622468c1b903"></a>
#### 구문

```
BIT_LENGTH( str )
```

<a id="34e49d301efbda88"></a>
#### 설명

BIT_LENGTH는 str의 비트 수를 반환한다.

<a id="a01a8647f49da5d9"></a>
#### 사용 예

```
gSQL> SELECT BIT_LENGTH( 'LIKE' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
             32
    1 row selected.
```

<a id="43f8c447a8165c4d"></a>
### BYTE_LENGTH

<a id="1d6b4d9a078975ee"></a>
#### 구문

```
BYTE_LENGTH( str )
```

<a id="fbdf31c913abd496"></a>
#### 설명

OCTET_LENGTH의 alias이다.  
자세한 내용은 [OCTET_LENGTH](#35c754cbe369df47), [LENGTHB](#11bae4ba0aa6d32d)를 참조한다.

<a id="314b0695516749e2"></a>
#### 사용 예

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

<a id="4d911dd670bd919d"></a>
### CASE2

<a id="1988e3c967cbb337"></a>
#### 구문

```
CASE2( condition1, result1
      [, condition2, result2
       , ...
       , conditionN, resultN ]
      [, default ] )
```

<a id="1d8e5e0a5eb9d364"></a>
#### 설명

CASE2는 기술된 순서대로 condition을 평가한다.  
비교 결과가 FALSE이면 TRUE가 나올 때까지 평가한다.  
비교 결과가 TRUE이면 대응되는 result를 반환하고, 이후는 평가하지 않는다.  
비교 결과가 모두 FALSE인 경우에는 default를 반환하고, default가 생략된 경우에는 NULL을 반환한다.

결과 타입은 result1 (첫 번째 result)의 데이터 타입으로 결정된다.  
result1 (첫 번째 result)의 데이터 타입이 숫자형인 경우와 문자형인 경우에는 각각 result1, ..., resultN의 범위를 포함할 수 있는 타입으로 결정된다.  
result1 (첫 번째 result)가 CHAR 타입 또는 NULL인 경우, 결과 타입은 VARCHAR 이다.

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

<a id="b66a90a8d9747666"></a>
#### 사용 예

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

<a id="d6eca6c411286eea"></a>
### CBRT

<a id="d9f2035380ada2d0"></a>
#### 구문

```
CBRT( num )
```

<a id="83f5365786bbbdc1"></a>
#### 설명

num의 세제곱근을 반환한다.  
인자값 num이 NULL이면 결과값도 NULL이다.

<a id="764c50037ec37104"></a>
#### 사용 예

```
gSQL> SELECT CBRT( 27 ) FROM DUAL;
CBRT( 27 )
----------
         3
1 row selected.
```

<a id="1fa24fcf52467d87"></a>
### CEIL

<a id="f07f981a2905d16e"></a>
#### 구문

```
CEIL( num )
CEILING( num )
```

<a id="3734d2622befe3eb"></a>
#### 설명

CEIL 함수는 num 보다 크거나 같은 가장 작은 정수를 반환한다.

<a id="ff4972087a232ea7"></a>
#### 사용 예

```
gSQL> SELECT CEIL( 3.5 ) AS RESULT1, CEIL( -3.5 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      4      -3
1 row selected.
```

<a id="41c3cbeb846d0e80"></a>
### CHAR_LENGTH

<a id="543b39b6d70a2034"></a>
#### 구문

```
CHAR_LENGTH( str )            
CHARACTER_LENGTH( str )
```

<a id="c55a06c5c8490913"></a>
#### 설명

CHAR_LENGTH는 str에 대해 character set에 따른 문자수를 반환한다.

str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있고, 반환되는 타입은 NATIVE_BIGINT 이다.

str의 타입이 CHARACTER 타입이면 공백문자 (trailing blank)를 포함하여 계산한다.  
str이 NULL이면 NULL이 반환된다.

[LENGTH](#21689d44ab60ac4e)의 alias이다.

<a id="f519262e0199a49c"></a>
#### 사용 예

Multi byte character set: (예:UTF8)

```
gSQL> SELECT CHAR_LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="204884e3d6fd386c"></a>
### CHR

<a id="0b338fad740dac93"></a>
#### 구문

```
CHR( num )
```

<a id="1cb020b01b8ffb4e"></a>
#### 설명

num에 대응하는 database character set code 내의 charater를 반환한다.

입력 인자에는 숫자형 타입이 올 수 있으며 결과 타입은 VARCHAR 이다.

<a id="4711498280efb974"></a>
#### 사용 예

```
gSQL> SELECT CHR(71) FROM DUAL;
CHR(71)
-------
G      
1 row selected.
```

<a id="8aa1a037b24b08b9"></a>
### CLOCK_DATE

<a id="42b1461952b72cdd"></a>
#### 구문

```
CLOCK_DATE()
```

<a id="f3bb880eb0c4d5e2"></a>
#### 설명

함수가 호출될 때마다 현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="ffb1174253f8d4dc"></a>
#### 사용 예

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

<a id="cab31dad1e732dd9"></a>
### CLOCK_LOCALTIME

<a id="c459a54edde95ee4"></a>
#### 구문

```
CLOCK_LOCALTIME()
```

<a id="df5d99012860f453"></a>
#### 설명

함수가 호출될 때마다 TIME ZONE이 없는 현재 시간 (TIME WITHOUT TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="56cd5d5c00fc9818"></a>
#### 사용 예

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

<a id="e7935bb37b1e4649"></a>
### CLOCK_LOCALTIMESTAMP

<a id="73808be5e0afc68f"></a>
#### 구문

```
CLOCK_LOCALTIMESTAMP()
```

<a id="c002920a7037bd60"></a>
#### 설명

함수가 호출될 때마다 TIME ZONE이 없는 현재 TIMESTAMP (TIMESTAMP WITHOUT TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="a2db570abc68e5c6"></a>
#### 사용 예

Row 마다 값이 다를 수 있다.

```
gSQL> SELECT CLOCK_LOCALTIMESTAMP() FROM t1;

CLOCK_LOCALTIMESTAMP()    
--------------------------
2013-12-12 14:46:17.309206
2013-12-12 14:46:17.309209
2013-12-12 14:46:17.309209
```

<a id="0aa363a537038257"></a>
### CLOCK_TIME

<a id="7dcc6042f3a2d29b"></a>
#### 구문

```
CLOCK_TIME()
```

<a id="0c95e47f502d2f94"></a>
#### 설명

함수가 호출될 때마다 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="ab3a1e6292c002a2"></a>
#### 사용 예

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

<a id="b5fbc9dbbd1ee0c8"></a>
### CLOCK_TIMESTAMP

<a id="4068eea1ca93547b"></a>
#### 구문

```
CLOCK_TIMESTAMP()
```

<a id="ee57987ef961d81c"></a>
#### 설명

함수가 호출될 때마다 TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="336ff362f06a1097"></a>
#### 사용 예

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

<a id="ec78cb861c06c7fb"></a>
### COALESCE

<a id="d3f003262dc7f2dd"></a>
#### 구문

```
COALESCE( expr1, ..., exprN )
```

<a id="b668590de0e4827d"></a>
#### 설명

expr list들 중에 null이 아닌 첫 번째 expr을 반환한다.  
expr list들이 모두 null인 경우에는 null을 반환한다.  
expr은 두 개 이상이어야 한다.

expr list에 여러 type들이 오는 경우에는 [결과 타입 조합 규칙](#08f567244d3c0586)에 따라 result type이 결정된다.

COALESCE는 CASE를 사용하여 동일하게 표현할 수 있다.

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

<a id="b6e53c6eb8be1a36"></a>
#### 사용 예

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

<a id="537e3c54efdacfea"></a>
### CONCAT

<a id="5f6afe3c29caca89"></a>
#### 구문

```
CONCAT( str1, str2, ... )
```

<a id="84e4cf38d6687924"></a>
#### 설명

\|| ( CONCATENATE )의 alias 이다.  
CONCAT 함수의 argument로써 2 ~ 254 개까지 설정할 수 있다.  
자세한 내용은 [|| (CONCATENATE)](#d94be4d95c59affd), [CONCATENATE](#0d6daaed8ec3a38c)를 참조한다.

<a id="2294446c1c9f55b5"></a>
#### 사용 예

```
gSQL> SELECT CONCAT( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="0d6daaed8ec3a38c"></a>
### CONCATENATE

<a id="3c91705affefbedd"></a>
#### 구문

```
CONCATENATE( str1, str2, ... )
```

<a id="acea7913a3bf665c"></a>
#### 설명

\|| ( CONCATENATE ) 의 alias 이다.  
CONCATENATE 함수의 argument로 2 ~ 254 개까지 설정할 수 있다.  
자세한 내용은 [CONCAT](#537e3c54efdacfea), [|| (CONCATENATE)](#d94be4d95c59affd) 를 참조한다.

<a id="535cf29548c84135"></a>
#### 사용 예

```
gSQL> SELECT CONCATENATE( 'DATA', 'BASE' ) AS RESULT FROM DUAL;
RESULT  
--------
DATABASE
1 row selected.
```

<a id="ba8ec59c0d585e05"></a>
### COS

<a id="1540eed86360dfcb"></a>
#### 구문

```
COS(num)
```

<a id="83f14f83df56f04d"></a>
#### 설명

num 의 COSINE 값을 반환한다.  
인자값 num이 NULL이면 결과값도 NULL이다.

<a id="4e7ee1c0559b1684"></a>
#### 사용 예

```
gSQL> SELECT COS( 0 ) FROM DUAL;
COS( 0 )
--------
       1
1 row selected.
```

<a id="29ee6c5035a97c3e"></a>
### COT

<a id="2b0e84defac82112"></a>
#### 구문

```
COT(num)
```

<a id="4567a0d2358bd18b"></a>
#### 설명

num의 COTANGENT 값을 반환한다.  

인자값 num이 NULL이면 결과값도 NULL이다.

<a id="e702a0a2e152d754"></a>
#### 사용 예

```
gSQL> SELECT COT( 1 ) FROM DUAL;
        COT( 1 )
----------------
.642092615934331
1 row selected.
```

<a id="0a35b1f2a520837b"></a>
### COUNT

<a id="61a71918d64844cf"></a>
#### 구문

```
COUNT( [ ALL | DISTINCT ] expr )
```

<a id="29a08bff4dd466b3"></a>
#### 설명

Aggregation 함수로써 expr이 NULL 값이 아닌 row의 개수를 얻는다.

ALL을 명시한 경우, 모든 값들에 대한 aggregation을 수행한다.  
DISTINCT을 명시한 경우, 중복 제거한 값들에 대한 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

<a id="afb23a3da56527aa"></a>
#### 사용 예

```
gSQL> SELECT COUNT(c1) FROM t1;

COUNT(C1)
---------
        3

1 row selected.
```

<a id="cb884841c2d1440a"></a>
### COUNT(*)

<a id="01b8a4d483fc6123"></a>
#### 구문

```
COUNT(*)
```

<a id="2a995dc8c174475f"></a>
#### 설명

Aggregation 함수로써 row의 개수를 얻는다.  
별도의 expression을 지정하지 않으므로 값의 NULL 여부와 무관하다.

<a id="f19b09e6a7f2b1da"></a>
#### 사용 예

```
gSQL> SELECT COUNT(*) FROM t1;

COUNT(*)
--------
       4

1 row selected.
```

<a id="ee088d323b9d8981"></a>
### CURRENT_CATALOG

<a id="b2d4fab12f997d99"></a>
#### 구문

```
CURRENT_CATALOG [()]
```

<a id="62633f510a030e2b"></a>
#### 설명

catalog name (database 이름)을 얻는다.

<a id="b5fa121a55df5bf6"></a>
#### 사용 예

```
gSQL> SELECT CURRENT_CATALOG FROM dual;

CURRENT_CATALOG
---------------
TEST_DB        

1 row selected.
```

<a id="1aea3d5d1b193899"></a>
### CURRENT_DATE

<a id="19bf12f2bd18deba"></a>
#### 구문

```
CURRENT_DATE [()]
STATEMENT_DATE()
```

<a id="6815b4e8c9ef840d"></a>
#### 설명

현재 날짜 (DATE type) 값을 얻는다.

CURRENT_DATE는 SQL 표준 함수이다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• CURRENT_DATE, STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="dd44c05a1103d3f5"></a>
#### 사용 예

```
gSQL> SELECT CURRENT_DATE FROM t1;

CURRENT_DATE
------------
2013-12-12  
2013-12-12  
2013-12-12  

3 rows selected.
```

<a id="6cad995b2f20e5b2"></a>
### CURRENT_SCHEMA

<a id="4f992385d09ba028"></a>
#### 구문

```
CURRENT_SCHEMA [()]
```

<a id="21c14f0243c14ed4"></a>
#### 설명

사용자의 현재 SCHEMA를 얻는다.

<a id="1848afc64a248e58"></a>
#### 사용 예

```
gSQL> SELECT CURRENT_SCHEMA FROM dual;

CURRENT_SCHEMA
--------------
PUBLIC        

1 row selected.
```

<a id="a4e68f37761bd434"></a>
### CURRENT_TIME

<a id="d92c19ae1c28002e"></a>
#### 구문

```
CURRENT_TIME [()]
STATEMENT_TIME()
```

<a id="4fd8798a2548c465"></a>
#### 설명

Session 시간을 기준으로 현재 TIME WITH TIME ZONE type 값을 얻는다.

CURRENT_TIME은 SQL 표준 함수이다.

현재 날짜를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• CURRENT_TIME, STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="ab2d17e3cd8f6ee3"></a>
#### 사용 예

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

<a id="00166487940f1b96"></a>
### CURRENT_TIMESTAMP

<a id="3b5e531dfea6c88b"></a>
#### 구문

```
CURRENT_TIMESTAMP [()]
STATEMENT_TIMESTAMP()
```

<a id="ecfed9c40f1ca67c"></a>
#### 설명

Session 시간을 기준으로 TIMESTAMP WITH TIME ZONE type 값을 얻는다.

CURRENT_TIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• CURRENT_TIMESTAMP, STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="ceedd40ff2678ce4"></a>
#### 사용 예

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

<a id="27bffc804504302b"></a>
### CURRENT_USER

<a id="f5e17e299fe4c516"></a>
#### 구문

```
CURRENT_USER [()]
```

<a id="3d7e2b93fb3f9a2f"></a>
#### 설명

현재 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다.
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다.
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다.
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="54946c027006c50b"></a>
#### 사용 예

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

<a id="49d99dc28cf285f7"></a>
### CURRVAL

<a id="e6bfca88c9a63c1d"></a>
#### 구문

```
seq_name.CURRVAL
CURRVAL(seq_name)
```

<a id="28bb2c65a6e5838f"></a>
#### 설명

시퀀스 객체의 현재 값을 얻는다.

최소 한 번은 NEXTVAL(seq_name) 등으로 시퀀스 값을 설정해야 한다.

<a id="be123fa308fb46f9"></a>
#### 사용 예

```
gSQL> SELECT seq.CURRVAL FROM dual;

SEQ.CURRVAL
-----------
          1

1 row selected.
```

<a id="9ed828d593dc6ae0"></a>
### DATEADD

<a id="f46861100aead245"></a>
#### 구문

```
DATEADD( datepart, number, date )
```

<a id="048884be6306dfa5"></a>
#### 설명

date의 지정된 datepart에 number를 더한 값을 반환한다.

number가 소수점인 경우 반올림되지 않는다.  
date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE 타입이 올 수 있다.  
number 또는 date가 NULL인 경우에는 결과값도 NULL이다.

인자로 받은 date의 타입과 동일한 결과 타입이 반환된다.

**datepart에 사용 가능한 형식문자열**

<a id="3fd573069e4fac73"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">설명</th></tr><tr><td>YEAR</td><td>년</td></tr><tr><td>QUARTER</td><td>분기</td></tr><tr><td>MONTH</td><td>월</td></tr><tr><td>DAYOFYEAR</td><td>일</td></tr><tr><td>DAY</td><td>요일</td></tr><tr><td>WEEK</td><td>주</td></tr><tr><td>WEEKDAY</td><td>평일</td></tr><tr><td>HOUR</td><td>시</td></tr><tr><td>MINUTE</td><td>분</td></tr><tr><td>SECOND</td><td>초</td></tr><tr><td>MILLISECOND</td><td>밀리세컨드</td></tr><tr><td>MICROSECOND</td><td>마이크로세컨드</td></tr></tbody></table>

<a id="e2f8c4b784dedd46"></a>
#### 사용 예

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

<a id="084732522318d734"></a>
### DATEDIFF

<a id="9552ccc604f5bad2"></a>
#### 구문

```
DATEDIFF( datepart, startdate, enddate )
```

<a id="a6bbd6144ce4b25a"></a>
#### 설명

enddate에서 startdate를 뺀 값을 지정된 datepart로 반환한다.

startdate 또는 enddate가 NULL이면 결과값도 NULL이다.  
startdate와 enddate에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME TYPE이 올 수 있다.

결과 타입은 NUMBER이다.

**datepart에 사용 가능한 형식 문자열**

<a id="8831b73fed407c69"></a>
<table><tbody><tr><th align="center">datepart</th><th align="center">설명</th></tr><tr><td>YEAR</td><td>년</td></tr><tr><td>QUARTER</td><td>분기</td></tr><tr><td>MONTH</td><td>월</td></tr><tr><td>DAYOFYEAR</td><td>일</td></tr><tr><td>DAY</td><td>요일</td></tr><tr><td>HOUR</td><td>시</td></tr><tr><td>MINUTE</td><td>분</td></tr><tr><td>SECOND</td><td>초</td></tr><tr><td>MILLISECOND</td><td>밀리세컨트</td></tr><tr><td>MICROSECOND</td><td>마이크로세컨드</td></tr></tbody></table>

<a id="16bb7ca67594885e"></a>
#### 사용 예

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

gSQL> SELECT 
      DATEDIFF( MONTH, 
                TO_DATE( '2013-05-14', 'YYYY-MM-DD' ), 
                TO_DATE( '2014-06-15', 'YYYY-MM-DD' ) ) AS RESULT 
      FROM DUAL;
RESULT
------
    13
1 row selected.

gSQL> SELECT 
      DATEDIFF( DAY, 
                TO_DATE( '2013-05-14', 'YYYY-MM-DD' ), 
                TO_DATE( '2014-06-15', 'YYYY-MM-DD' ) ) AS RESULT 
      FROM DUAL;
RESULT
------
   397
1 row selected.
```

<a id="3b472fb1547db027"></a>
### DATE_ADD

<a id="909084bc86ab7e15"></a>
#### 구문

```
DATE_ADD( date, INTERVAL expr unit  )
```

<a id="01ef546c0d8dba5b"></a>
#### 설명

[ADDDATE](#40e97b19083d297e)( date, INTERVAL expr unit )와 동일한 함수이다.

<a id="15118179d110d19b"></a>
#### 사용 예

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

<a id="929fc4f512892cd9"></a>
### DATE_PART

<a id="6c4e7f7e068b47c5"></a>
#### 구문

```
DATE_PART( field, datetime )
```

<a id="4e9e126380b2067f"></a>
#### 설명

DATE_PART는 EXTRACT 함수와 결과값이 같은 함수로써 입력한 datetime 타입에서 지정된 field를 찾아 반환한다.

인자 field에는 문자 literal만 올 수 있으며, YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, TIMEZONE_HOUR, TIMEZONE_MINUTE를 문자 literal로 지정할 수 있다.  
인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.

field가 datetime의 범위에 있지 않는 경우 에러를 반환한다.  
또한, DATE 타입인 경우에는 field에 YEAR, MONTH, DAY 만 올 수 있고, 그 외에는 에러를 반환한다.  

반환되는 타입은 NUMBER이다.

자세한 내용은 [EXTRACT](#b923e09ee076c491)를 참조한다.

<a id="9ba657a2c7c6653e"></a>
#### 사용 예

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

<a id="97c7ea5f728b56de"></a>
### DECODE

<a id="ce51d81574197623"></a>
#### 구문

```
DECODE( expr, comparison_expr1, result1
           [, comparison_expr2, result2
            , ...
            , comparison_exprN, resultN ]
           [, default ] )
```

<a id="177cc547a1e07bfe"></a>
#### 설명

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

<a id="128c96eae73504e3"></a>
#### 사용 예

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

<a id="85e1bac58377785e"></a>
### DEGREES

<a id="eb2b28d98e04c771"></a>
#### 구문

```
DEGREES( radians )
```

<a id="28acb19f5b9ccc34"></a>
#### 설명

라디안 단위로 표시된 각도 radians를 도 단위로 변환한 값을 반환한다.

<a id="e9a0647a210273ab"></a>
#### 사용 예

```
gSQL> SELECT DEGREES( PI() ) AS RESULT FROM DUAL;
RESULT
------
   180
1 row selected.
```

<a id="b58f7f38ee675bcf"></a>
### DIGEST

<a id="6dffe5474fe0d404"></a>
#### 구문

```
DIGEST( data, type )
```

<a id="eca779721680d671"></a>
#### 설명

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

<a id="8bc031b3181f1044"></a>
#### 사용 예

```
gSQL> SELECT HEX( DIGEST( 'my password', 'SHA256' ) ) AS RESULT FROM DUAL;

RESULT                                                          
----------------------------------------------------------------
BB14292D91C6D0920A5536BB41F3A50F66351B7B9D94C804DFCE8A96CA1051F2

1 row selected.
```

<a id="9de591ebbe891f3b"></a>
### DUMP

<a id="01603c1743f77512"></a>
#### 구문

```
DUMP( expr )
```

<a id="01f3120632d350d3"></a>
#### 설명

DUMP 함수는 expr의 내부 표현정보를 반환한다.  
내부 표현정보는 데이터 타입, 길이 (byte length), 데이터 정보로 보여준다.

expr에는 모든 타입이 올 수 있으며, 반환되는 타입은 CHARACTER VARYING이다.

<a id="cf7a3d8ff183afe8"></a>
#### 사용 예

```
gSQL> SELECT DUMP( 'DUMP' ) AS RESULT FROM DUAL;
RESULT                           
---------------------------------
Type=CHAR Len=4 : Str=68,85,77,80
1 row selected.
```

<a id="13398c36be01a534"></a>
### EXP

<a id="9bf2537ca6558430"></a>
#### 구문

```
EXP( num )
```

<a id="57d38545dc36f45f"></a>
#### 설명

EXP 함수는 e (자연로그 베이스)의 num의 제곱값을 반환한다.

<a id="2964dbf033b91d63"></a>
#### 사용 예

```
gSQL> SELECT EXP( 1 ) AS RESULT FROM DUAL;
          RESULT
----------------
2.71828182845905
1 row selected.
```

<a id="b923e09ee076c491"></a>
### EXTRACT

<a id="f7794575b8d25df9"></a>
#### 구문

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

<a id="58fcde41b07e7f5f"></a>
#### 설명

EXTRACT는 입력한 datetime 타입에서 지정된 field를 찾아 반환한다.

인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.

field가 datetime의 범위에 있지 않는 경우에는 에러를 반환한다.  
또, DATE 타입인 경우에는 field에 YEAR, MONTH, DAY만 올 수 있고, 그 외의 경우에는 에러를 반환한다.  
반환되는 타입은 NUMBER이다.

EXTRACT 함수의 결과는 [DATE_PART](#929fc4f512892cd9)와 동일하다.

<a id="373101b0fbf7bef1"></a>
#### 사용 예

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

<a id="8de7e8bc51eaefa0"></a>
### FACTORIAL

<a id="bff027dd20d3febb"></a>
#### 구문

```
FACTORIAL( num )
```

<a id="80e15c7b7139d418"></a>
#### 설명

FACTORIAL 함수는 1 ~ num 까지의 연속된 자연수를 차례로 곱한 값을 반환한다.

<a id="f74990fa1ab271b8"></a>
#### 사용 예

```
gSQL> SELECT FACTORIAL( 5 ) AS RESULT FROM DUAL;
RESULT
------
   120
1 row selected.
```

<a id="d6b3abc03cb13652"></a>
### FLOOR

<a id="d3a22504fe3a0e28"></a>
#### 구문

```
FLOOR( num )
```

<a id="ca932196d634164c"></a>
#### 설명

FLOOR 함수는 num 보다 크지 않은 가장 큰 정수를 반환한다.

<a id="62117813f7b678a7"></a>
#### 사용 예

```
gSQL> SELECT FLOOR(42.8) AS RESULT1, FLOOR(-42.8) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
     42     -43
1 row selected.
```

<a id="ea0b9a178af37c8d"></a>
### FROM_BASE64

<a id="331e7ce9608779b2"></a>
#### 구문

```
FROM_BASE64( str )
```

<a id="478c2818ce449e69"></a>
#### 설명

FROM_BASE64는 base64 인코딩으로 변환된 문자를 입력 받아 디코딩된 binary string을 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 BINARY VARYING 또는 BINARY LONG VARYING과 같은 BINARY 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 base64 문자 범위에 속하지 않는 문자가 포함되면, 에러를 반환한다.  
디코딩 할 때 str의 newline, carriage return, tab, space는 무시된다.

자세한 내용은 [TO_BASE64](#ce1f3ac6f7c95caa)를 참조한다.

<a id="14dff912e559cb2c"></a>
#### 사용 예

```
gSQL> SELECT FROM_BASE64( TO_BASE64( 'abc' ) ),
             FROM_BASE64( TO_BASE64( 'abcd' ) ) 
        FROM DUAL;
FROM_BASE64( TO_BASE64( 'abc' ) ) FROM_BASE64( TO_BASE64( 'abcd' ) )
--------------------------------- ----------------------------------
616263                            61626364                          
1 row selected.
```

<a id="308c44d267e0ca91"></a>
### GREATEST

<a id="c8f46410e898bfa9"></a>
#### 구문

```
GREATEST( expr1 [, expr2, ... exprn ] )
```

<a id="b70d9a4dc27ed788"></a>
#### 설명

GREATEST 함수는 인자로 받은 expr들 중에 가장 큰 값을 반환한다.

인자로 받은 expr들 중 하나라도 NULL인 경우, 결과값은 NULL이다.

결과 타입은 expr1 (첫 번째 expr)의 데이터 타입이다.  
expr1 (첫 번째 expr)의 데이터 타입이 숫자형인 경우와 문자형인 경우는 각각 expr1, ..., exprN의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, ..., exprN에 모두 CHAR타입이 기술된 경우, 모든  expr은 VARCHAR 타입으로 비교되고, 결과 타입은 VARCHAR 타입으로 결정된다.

<a id="5be04db79c86c3c4"></a>
#### 사용 예

```
gSQL> SELECT GREATEST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
   200
1 row selected.
```

<a id="7688a79d8466821e"></a>
### HEX

<a id="7450d46742aced1e"></a>
#### 구문

```
HEX( str )
```

<a id="2df37c2fc16904b5"></a>
#### 설명

인자 str을 16진수 문자로 반환한다.  
인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입 또는 문자 타입으로 변환될 수 있는 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.  
결과 타입은 CHARACTER VARYING 또는 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.

HEX 함수의 인자로 숫자타입이 오는 경우에는 에러를 반환한다.  
10진수 숫자를 16진수로 변환하고자 하는 경우에는  'X' number format을 이용한 TO_CHAR() 함수를 사용할 수 있다.  
예: TO_CHAR( 255, 'XX' )

자세한 내용은 [UNHEX](#0560e47a7d18fb05)를 참조한다.

<a id="a90ca11424b97604"></a>
#### 사용 예

```
gSQL> SELECT HEX( 'abc' ) FROM DUAL;
HEX( 'abc' )
------------
616263      
1 row selected.
```

<a id="c71953d88af8f408"></a>
### INITCAP

<a id="7ad4f414a907fa9f"></a>
#### 구문

```
INITCAP( str )
```

<a id="cd1922460804a766"></a>
#### 설명

INITCAP 함수는 주어진 문자열 str의 각 단어들의 첫 번째 문자를 대문자로 변환하고 첫 번째 문자 이후의 문자를 소문자로 변환하여 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.

문자열의 각 단어는 white space, 알파벳 또는 숫자가 아닌 문자로 구분한다.  
str이 NULL이면 결과값도 NULL이다.

인자로 받는 str의 타입과 동일한 타입이 반환된다.

<a id="fd8ba6392df7a9e9"></a>
#### 사용 예

```
gSQL> SELECT INITCAP( 'hi GLIESE' ) AS RESULT FROM DUAL;
RESULT   
---------
Hi Gliese
1 row selected.
```

<a id="1a84fa5265b76ee2"></a>
### INSTR

<a id="ccd9f182ee2e2ee8"></a>
#### 구문

```
INSTR( str, substr [, position [, occurrence ] ] )
```

<a id="cda181a1019c750d"></a>
#### 설명

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

<a id="35a4dd2b65a33360"></a>
#### 사용 예

```
gSQL> SELECT INSTR( 'INSTR( STR, SUBSTR )', 'SUB' ) AS RESULT1,
             INSTR( 'INSTR( STR, SUBSTR )', 'SUB', 5 ) AS RESULT2
        FROM DUAL;
RESULT1 RESULT2
------- -------
     13      13
1 row selected.

gSQL> SELECT INSTR( 'INSTR( STR, SUBSTR )', 'STR', 6, 2 ) AS RESULT1,
             INSTR( 'INSTR( STR, SUBSTR )', 'STR', -6, 2 ) AS RESULT2
      FROM DUAL;
RESULT1 RESULT2
------- -------
     16       3
1 row selected.
```

<a id="2571b0035c21570b"></a>
### LAST_DAY

<a id="889d6fe494a17298"></a>
#### 구문

```
LAST_DAY( date )
```

<a id="98d1516e9329dc2d"></a>
#### 설명

LAST_DAY 함수는 date에 포함된 월의 마지막 날짜를 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
반환되는 타입은 인자 date의 타입에 상관없이 항상 DATE이다.

<a id="c4841865890ea1cb"></a>
#### 사용 예

```
gSQL> SELECT 
      LAST_DAY( TO_DATE( '2012-07-10', 'YYYY-MM-DD' ) ) AS RESULT FROM DUAL;
RESULT    
----------
2012-07-31
1 row selected.
```

<a id="762ea15e9c2071ae"></a>
### LAST_IDENTITY_VALUE

<a id="edc68d071088ef94"></a>
#### 구문

```
LAST_IDENTITY_VALUE()
```

<a id="1ce3c0fc5a7d22e8"></a>
#### 설명

현재 session에서 identity column을 위해 자동으로 생성한 최근 값으로써 결과 타입은 NATIVE_BIGINT 이다.

자동으로 생성한 값이 없을 경우 null을 반환한다.

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

INSERT 할 때 생성된 identity column 값을 얻으려면 다음과 같이 [INSERT INTO name RETURNING .. INTO](16-sql-references.md#c1f0fbbf948ca76c) 구문을 사용한다.

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

<a id="5f546ff0a70c269e"></a>
#### 사용 예

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

<a id="350d1d2339344e99"></a>
### LEAST

<a id="98ecba1c68cf99e7"></a>
#### 구문

```
LEAST( expr1 [, expr2, ... exprn ] )
```

<a id="228449bb99cdbcc1"></a>
#### 설명

LEAST 함수는 인자로 받은 expr들 중에 가장 작은 값을 반환한다.

인자로 받은 expr들 중 하나라도 NULL인 경우, 결과값은 NULL이다.

결과 타입은 expr1 (첫 번째 expr)의 데이터 타입에 따라 결정된다.  
expr1 (첫 번째 expr)의 데이터 타입이 숫자형인 경우와 문자형인 경우에는 각각 expr1, ..., exprN의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, ..., exprN에 모두 CHAR 타입이 기술된 경우, 모든 expr은 VARCHAR 타입으로 비교되고, 결과 타입은 VARCHAR 타입이 된다.

<a id="49363284a96fab11"></a>
#### 사용 예

```
gSQL> SELECT LEAST( 100, 0, 200, 150, 1 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="21689d44ab60ac4e"></a>
### LENGTH

<a id="9ad92fafa5c09f4f"></a>
#### 구문

```
LENGTH( str )
```

<a id="61f1465a78b4572e"></a>
#### 설명

[CHAR_LENGTH](#41c3cbeb846d0e80)의 alias 이다.

<a id="17e636ace1086b79"></a>
#### 사용 예

Multi byte character set: (예: UTF8)

```
gSQL> SELECT LENGTH( 'αβ-SUMMER' ) AS RESULT FROM DUAL;
     RESULT   
     ---------------
              9
    1 row selected.
```

<a id="11bae4ba0aa6d32d"></a>
### LENGTHB

<a id="a673b25cda761683"></a>
#### 구문

```
LENGTHB( str )
```

<a id="96cdcfd1a4352536"></a>
#### 설명

OCTET_LENGTH의 alias 이다.  
자세한 내용은 [OCTET_LENGTH](#35c754cbe369df47), [BYTE_LENGTH](#43f8c447a8165c4d)를 참조한다.

<a id="0ee837f26118fd9a"></a>
#### 사용 예

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

<a id="34b5e5cab0360f64"></a>
### LN

<a id="398cc0976a9e1bd3"></a>
#### 구문

```
LN( num )
```

<a id="208087eee8649e12"></a>
#### 설명

LN 함수는 num의 자연 로그 값을 반환하는 함수이다.  
num은 0보다 큰 값이어야 한다.

<a id="c4e5d0f2e2e82c20"></a>
#### 사용 예

```
gSQL> SELECT LN( 2.71828182845905 ) AS RESULT FROM DUAL;
RESULT
------
     1
1 row selected.
```

<a id="14d2f9de457d10b2"></a>
### LOCALTIME

<a id="cc7ac2f5cc0d9d51"></a>
#### 구문

```
LOCALTIME [()]
STATEMENT_LOCALTIME()
```

<a id="9625031ff7a02284"></a>
#### 설명

Session 시간을 기준으로 현재 TIME WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• LOCALTIME, STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="8090767f1d2ac86f"></a>
#### 사용 예

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

<a id="18927e9f41bda3e1"></a>
### LOCALTIMESTAMP

<a id="92d6863ce8c64959"></a>
#### 구문

```
LOCALTIMESTAMP [()]
STATEMENT_LOCALTIMESTAMP()
```

<a id="19fa6aad08103eff"></a>
#### 설명

Session 시간을 기준으로 현재 TIMESTAMP WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 간에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• LOCALTIMESTAMP, STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="8b2743afba7fe4d9"></a>
#### 사용 예

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

<a id="457ddcee848c8a71"></a>
### LOCAL_GROUP_ID

<a id="d0d70c3160ff9c9b"></a>
#### 구문

```
LOCAL_GROUP_ID()
```

<a id="4fc5afe5d8ead92c"></a>
#### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster group ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="1ed4a52c9ca15693"></a>
#### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_GROUP_ID() FROM DUAL;

LOCAL_GROUP_ID()
----------------
               1

1 row selected.
```

<a id="1f5e1f1b6f329930"></a>
### LOCAL_GROUP_NAME

<a id="ff0da41bdaef5df1"></a>
#### 구문

```
LOCAL_GROUP_NAME()
```

<a id="ad2ae460cf73161c"></a>
#### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster group name을 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="f72efd2573df6bdd"></a>
#### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_GROUP_NAME() FROM DUAL;

LOCAL_GROUP_NAME()
------------------
G1                

1 row selected.
```

<a id="2f1ea2310dddb573"></a>
### LOCAL_MEMBER_ID

<a id="aed7a49f6419ff90"></a>
#### 구문

```
LOCAL_MEMBER_ID()
```

<a id="2d0d8ff8f880e740"></a>
#### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster member ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="c276ebacb84b1c8c"></a>
#### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_MEMBER_ID() FROM DUAL;

LOCAL_MEMBER_ID()
-----------------
                1

1 row selected.
```

<a id="1e154505cd6ba647"></a>
### LOCAL_MEMBER_NAME

<a id="b7077de49972e716"></a>
#### 구문

```
LOCAL_MEMBER_NAME()
```

<a id="eb6af8150ebf9f77"></a>
#### 설명

사용자 질의를 받아 처리하는 server에 대한 cluster member name을 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="3837c18677efe492"></a>
#### 사용 예

모든 row가 같은 값을 갖는다.

```
gSQL> SELECT LOCAL_MEMBER_NAME() FROM DUAL;

LOCAL_MEMBER_NAME()
-------------------
G1N1               

1 row selected.
```

<a id="0e732f9da532f7af"></a>
### LOG

<a id="e3497d7c9ae8e45f"></a>
#### 구문

```
LOG( num2 )
LOG( num1, num2 )
```

<a id="0a1adc9e5fa788f1"></a>
#### 설명

LOG 함수는 밑이 num1인 num2의 로그값을 반환한다.  
num1이 생략된 경우에는 밑이 10으로 계산된 값이 반환된다.

num1은 1과 0이 아닌 양수이어야 하고, num2는 양수이어야 한다.

<a id="4087f713840d64dd"></a>
#### 사용 예

```
gSQL> SELECT LOG( 100 ) AS RESULT1, LOG( 4, 16 ) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      2       2
1 row selected.
```

<a id="abaf386db4467942"></a>
### LOGON_USER

<a id="4fc791b6049f819f"></a>
#### 구문

```
LOGON_USER()
```

<a id="75a138b1017a5c5a"></a>
#### 설명

로그인 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다.
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경가능하다.
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다.
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="7947ffd6e65da839"></a>
#### 사용 예

```
% gsql test test

gSQL> SELECT LOGON_USER() AS result FROM DUAL;

RESULT
------
TEST  

1 row selected.
```

<a id="89dc33b14c803934"></a>
### LOWER

<a id="b68d1bb9c8f42e4e"></a>
#### 구문

```
LOWER( str )
```

<a id="07de6afd55926560"></a>
#### 설명

LOWER 함수는 str의 소문자를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.  
str이 NULL이면 결과값도 NULL이다.

인자 str과 동일한 타입이 반환된다.

<a id="59f7af84f8e0bccc"></a>
#### 사용 예

```
gSQL> SELECT LOWER( 'SPRING' ) AS RESULT FROM DUAL;
RESULT
------
spring
1 row selected.
```

<a id="c4bfc9126f6b9094"></a>
### LPAD

<a id="5c561f8dae5d2ab7"></a>
#### 구문

```
LPAD( str, length, [, fill] )
```

<a id="2291443a7ae0d78b"></a>
#### 설명

LPAD 함수는 string의 길이가 length가 될 때까지 str의 왼쪽에 문자열 fill을 추가한 값을 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

인자 length에는 숫자 타입이 올 수 있다.

length는 문자의 개수를 의미하며, 최대 범위는 결과 타입의 최대 PRECISION이다.  
fill이 생략된 경우, 공백 문자가 추가된다.  
str이 length보다 길이가 긴 경우에는 str을 length만큼 잘라서 반환한다.  
str, length, fill이 하나라도 NULL이면 결과값도 NULL이며, length가 0 또는 음수인 경우에도 결과값은 NULL이다.

결과 타입은 다음 표와 같다.

**LPAD의 결과 타입**

<a id="4e989cdeac81e6a5"></a>
| 인자 str의 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="a08e94f0742a1e13"></a>
#### 사용 예

```
gSQL> SELECT LPAD( 'aa', 5, 'b' ) AS RESULT FROM DUAL;
RESULT
------
bbbaa 
1 row selected.
```

<a id="4246822993541770"></a>
### LTRIM

<a id="6f242a22d6927c4e"></a>
#### 구문

```
LTRIM( trim_source [, trim_character ] )
```

<a id="13fee32e77021208"></a>
#### 설명

LTRIM 함수는 trim_source에서 trim_character를 왼쪽 방향에서 비교하여 일치하는 문자가 없을 때까지 제거한 결과를 반환한다.

인자 trim_character와 trim_source에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

trim_character, trim_source 중 하나라도 NULL이면, 결과값은 NULL이다.  
trim_character가 생략된 경우에는 기본적으로 single blank space (' ')가 지정된다.

결과 타입은 다음과 같다.

**LTRIM의 결과 타입**

<a id="3621f19667849414"></a>
| trim_source, trim_character 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="2ddafa3193f2c7f0"></a>
#### 사용 예

```
gSQL> SELECT LTRIM( '_____LTRIM', '_' ) AS RESULT FROM DUAL;
RESULT
------
LTRIM 
1 row selected.
```

<a id="634a03278cea58cf"></a>
### MAX

<a id="43b11e33815bdf3c"></a>
#### 구문

```
MAX( [ ALL | DISTINCT ] expr )
```

<a id="20089721f376f890"></a>
#### 설명

Aggregation 함수로써 row들의 expr 중 최대값을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복을 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

MAX는 ALL과 DISTINCT에 영향을 받지 않고 동일한 결과를 낸다.

<a id="788b2c39db0b7659"></a>
#### 사용 예

```
gSQL> SELECT MAX(c1) FROM t1;

MAX(C1)
-------
      3

1 row selected.
```

<a id="3e3749fffb97164e"></a>
### MIN

<a id="9b0d93b4936286b9"></a>
#### 구문

```
MIN( [ ALL | DISTINCT ] expr )
```

<a id="b9a050bec18d074f"></a>
#### 설명

Aggregation 함수로써 row들의 expr 중 최소값을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

MIN은 ALL과 DISTINCT에 영향을 받지 않고 동일한 결과를 낸다.

<a id="077aaa95a0e4b5d7"></a>
#### 사용 예

```
gSQL> SELECT MIN(c1) FROM t1;

MIN(C1)
-------
      1

1 row selected.
```

<a id="dde0d487094d72e3"></a>
### MOD

<a id="a59a4c771642f439"></a>
#### 구문

```
MOD( num1, num2 )
```

<a id="b8112724df4b8aae"></a>
#### 설명

MOD는 num1을 num2로 나눈 나머지를 반환한다.  

인자 num1, num2에는 숫자타입이 올 수 있다.  

num2가 0이면 에러를 반환한다.

<a id="3dff999bbde96def"></a>
#### 사용 예

```
gSQL> SELECT MOD(5, 4) AS RESULT1, MOD(-5, 4) AS RESULT2 FROM DUAL;
RESULT1 RESULT2
------- -------
      1      -1
1 row selected.
```

<a id="08319e67af5037d1"></a>
### MONTHS_BETWEEN

<a id="eb15f5ea9a38970f"></a>
#### 구문

```
MONTHS_BETWEEN( date1, date2 )
```

<a id="5a5af98a3b811b37"></a>
#### 설명

MONTHS_BETWEEN은 date2와 date1 사이의 일수를 31로 나눈 개월 수를 반환한다.

date1 또는 date2가 NULL이면 결과도 NULL이다.  
인자 date1, date2에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.

결과 타입은 NUMBER 이다.

> date1과 date2 모두에 동일한 날짜가 포함되어 있거나 (예: 2014-01-15 와 2014-02-15) 월의 마지막 날짜가 포함되어 있는 경우 (예: 2014-08-31와 2014-09-30), 타임스탬프 구간 (있는 경우)의 일치 여부와 상관없이 정수 결과를 반환한다.

<a id="5f46f5830985825d"></a>
#### 사용 예

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

<a id="e9a0e531f3740a16"></a>
### NEXT_DAY

<a id="fc6f6da6d6f86b8d"></a>
#### 구문

```
NEXT_DAY( date, day )
```

<a id="ac63d2d5202e5048"></a>
#### 설명

인자로 주어진 date (날짜)를 지나 처음으로 도래하는 day (요일)의 날짜를 구한다.

두 번째 인자 day에는 day를 지칭하는 스트링 또는 숫자가 올 수 있다.  
• 스트링:  SUNDAY ~ SATURDAY  또는 SUN ~ SAT  
• 숫자:  1 (sunday) ~ 7 (saturday)

반환되는 타입은 date의 입력 타입에 상관없이 항상 DATE 타입이다.  
결과값의 시분초는 입력 인자 date의 시분초를 동일하게 반환한다.

<a id="503806c2bf367942"></a>
#### 사용 예

```
gSQL> SELECT NEXT_DAY( TO_DATE( '2010-05-01', 'YYYY-MM-DD' ),
                       'SUNDAY' ) AS RESULT1 
        FROM DUAL;

RESULT1   
----------
2010-05-02

gSQL> SELECT NEXT_DAY( TO_DATE( '2010-05-01', 'YYYY-MM-DD' ),
                       'SUN' ) AS RESULT1 
        FROM DUAL;

RESULT1   
----------
2010-05-02

gSQL> SELECT NEXT_DAY( TO_DATE( '2010-05-01', 'YYYY-MM-DD' ),
                       1 ) AS RESULT1 
        FROM DUAL;

RESULT1   
----------
2010-05-02

gSQL> SELECT TO_CHAR( NEXT_DAY( TO_DATE( '2010-05-01', 'YYYY-MM-DD' ),
                                'SUNDAY' ),
                      'YYYY-MM-DD HH24:MI:SS' ) AS RESULT2 
        FROM DUAL;

RESULT2            
-------------------
2010-05-02 00:00:00
```

<a id="70c21c39c64fbe45"></a>
### NEXTVAL

<a id="9cecae3b64c46f83"></a>
#### 구문

```
seq_name.NEXTVAL
NEXTVAL( seq_name )
NEXT VALUE FOR seq_name
```

<a id="485b199ca2fb106a"></a>
#### 설명

시퀀스 객체의 다음 값을 얻는다.

<a id="1f4ebd8fea07450c"></a>
#### 사용 예

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

<a id="4d135921ffce1c85"></a>
### NULLIF

<a id="1744bc4efb30ff85"></a>
#### 구문

```
NULLIF( expr1, expr2 )
```

<a id="aeb5365b5e4b4312"></a>
#### 설명

expr1과 expr2가 같으면 null을 반환하고, 같지 않으면 첫 번째 인자인 expr1을 반환한다.

expr1과 expr2의 타입이 다를 경우, [Result Type Combination 규칙](#08f567244d3c0586)에 따라 result type이 결정된다.

NULLIF는 CASE를 사용하여 동일하게 표현할 수 있다.

- NULLIF( expr1, expr2 )

```
CASE WHEN expr1 = expr2 THEN NULL 
       ELSE expr1 
  END
```

<a id="bf18d1dd59e7b9fe"></a>
#### 사용 예

```
gSQL> SELECT NULLIF( 'SUN', 'SUN' ) AS RESULT1, 
             NULLIF( 'SUN', 'MOON' ) AS RESULT2 
       FROM DUAL;
RESULT1 RESULT2
------- -------
null    SUN    
1 row selected.
```

<a id="9ac19cfef4356d97"></a>
### NVL

<a id="84d514cea85bf195"></a>
#### 구문

```
NVL( expr1, expr2 )
```

<a id="cb529fb3cd24394a"></a>
#### 설명

expr1이 null이 아니면 expr1을 반환하고, expr1이 null이면 expr2를 반환한다.

결과 타입은 expr1의 데이터 타입에 따라 결정된다.  
expr1에 NULL이 기술된 경우에는 expr2의 타입에 따라 결과 타입이 결정된다.  
expr1의 데이터 타입이 숫자형 타입인 경우와 문자형 타입인 경우는 각각 expr1, expr2의 범위를 포함할 수 있는 타입으로 결정된다.  
expr1, expr2의 데이터 타입이 모두 CHAR 타입인 경우, 결과 타입은 VARCHAR 로 결정된다.

<a id="d7178baae43c1437"></a>
#### 사용 예

```
gSQL> SELECT I1, NVL( I1, 0 ) FROM T1;
  I1 NVL( I1, 0 )
---- ------------
   1            1
null            0
2 rows selected.
```

<a id="58bdec34e2320a7a"></a>
### NVL2

<a id="0f8c1776d8c7c967"></a>
#### 구문

```
NVL2( expr1, expr2, expr3 )
```

<a id="7e489bb4bde31a97"></a>
#### 설명

expr1이 null이 아니면 expr2를 반환하고, expr1이 null이면 expr3을 반환한다.

결과 타입은 expr2의 데이터 타입에 따라 결정된다.  
expr2에 NULL이 기술된 경우에는 expr3의 타입에 따라 결과 타입이 결정된다.  
expr2의 데이터 타입이 숫자형인 경우와 문자형인 경우에는 각각 expr2, expr3의 범위를 포함할 수 있는 타입으로 결정된다.  
expr2, expr3의 데이터 타입이 모두 CHAR 타입인 경우, 결과 타입은 VARCHAR가 된다.

<a id="c2fcbe115877aa5e"></a>
#### 사용 예

```
gSQL> SELECT I1, NVL2( I1, I1 * 1000, 0 ) FROM T1;
  I1 NVL2( I1, I1 * 1000, 0 )
---- ------------------------
   1                     1000
null                        0
2 rows selected.
```

<a id="35c754cbe369df47"></a>
### OCTET_LENGTH

<a id="9f2dce486b76e285"></a>
#### 구문

```
OCTET_LENGTH( str )  

BYTE_LENGTH( str )     

LENGTHB( str )
```

<a id="8576e230120262bb"></a>
#### 설명

OCTECT_LENGTH는 str의 바이트 수를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

str의 타입이 CHARACTER면 공백문자도 계산에 포함된다.  
str이 NULL이면 결과값도 NULL이다.

OCTET_LENGTH의 alias로는 [BYTE_LENGTH](#43f8c447a8165c4d)와 [LENGTHB](#11bae4ba0aa6d32d) 함수가 있다.

<a id="a197f3d719b6ab37"></a>
#### 사용 예

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

<a id="9432eacfe6e24942"></a>
### OVERLAY

<a id="998474e38d93060c"></a>
#### 구문

```
OVERLAY( str1 PLACING str2 FROM start_position  [ FOR string_length ] )
```

<a id="d33d25ce1a024ab9"></a>
#### 설명

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

자세한 내용은 [SUBSTRING](#5247eb0b134895cf)을 참조한다.

결과 타입은 다음 표와 같다.

**OVERLAY의 결과 타입**

<a id="c94f37e7f8a2dfe5"></a>
| str1, str2 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="5e41b82343e39c5d"></a>
#### 사용 예

```
gSQL> SELECT 
      OVERLAY( 'RESULT_OF_XXX_FUNC' PLACING 'OVERLAY' FROM 11 FOR 3 ) 
      AS RESULT 
      FROM DUAL;
RESULT                
----------------------
RESULT_OF_OVERLAY_FUNC
1 row selected.
```

<a id="46619b3749dcc372"></a>
### PI

<a id="4e1ec6d26bb612a5"></a>
#### 구문

```
PI()
```

<a id="8f316145e968b569"></a>
#### 설명

PI는 "π" constant를 반환한다.

<a id="7f7496ebbbd9b4ee"></a>
#### 사용 예

```
gSQL> SELECT PI() AS RESULT FROM DUAL;
              RESULT
--------------------
3.141592653589793E+0
1 row selected.
```

<a id="62366ed6216df66f"></a>
### POSITION

<a id="18afa1731b579adf"></a>
#### 구문

```
POSITION( str1 IN str2 )
```

<a id="bf526124e05efc41"></a>
#### 설명

POSITION 함수는 str2에서 첫 번째 str1을 찾아 그 위치를 반환하는 함수이다.

str1과 str2에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

str2에서 str1을 찾을 수 없는 경우, 리턴값 0이 반환된다.  
str2에서 str1을 찾은 경우, 1을 시작으로 그 찾은 위치를 반환한다.  
반환되는 위치값은 CHARACTER 단위로 계산된 값이다. (byte 단위가 아님)  
str1 또는 str2가 NULL이면, 반환되는 값도 NULL 이다.

<a id="1bce87391d827dd5"></a>
#### 사용 예

```
gSQL> SELECT POSITION( 'CHAR' IN 'LONG CHAR 2000' ) AS RESULT FROM DUAL;
RESULT
------
     6
1 row selected.
```

<a id="363f0d0ac0cc9ad1"></a>
### POWER

<a id="0d74f7fc043cd5d8"></a>
#### 구문

```
POWER( num1, num2 )
```

<a id="e87ed2efaa46ba7c"></a>
#### 설명

POWER 함수는 num1에 num2를 제곱한 값을 반환한다.

인수 num1과 num2에는 숫자 타입이 올 수 있다.  

num1이 음수라면 num2는 정수여야 한다.  
num1 또는 num2의 값이 NULL이면, 결과값도 NULL이다.

<a id="8d4a7c36f0877d3f"></a>
#### 사용 예

```
gSQL> SELECT POWER( 2, 3 ) AS RESULT FROM DUAL;
RESULT
------
     8
1 row selected.
```

<a id="6d1605316e480090"></a>
### RADIANS

<a id="e6706c43df66371a"></a>
#### 구문

```
RADIANS( degrees )
```

<a id="bb7fca09a747670c"></a>
#### 설명

RADIANS 함수는 degrees의 라디안을 반환한다.  

인자 degrees에는 숫자 타입이 올 수 있다.

<a id="af34842a499df49f"></a>
#### 사용 예

```
gSQL> SELECT RADIANS( 180 ) AS RESULT FROM DUAL;
          RESULT
----------------
3.14159265358979
1 row selected.
```

<a id="c27692dda69a29bc"></a>
### RANDOM

<a id="c5da7f20a9121b07"></a>
#### 구문

```
RANDOM( min, max )
```

<a id="2569b89d3d1b467d"></a>
#### 설명

RANDOM은 min 이상 max 이하의 random 값을 반환한다.  

인자 min, max에는 숫자 타입이 올 수 있다.

<a id="1880c0e22a854307"></a>
#### 사용 예

```
gSQL> SELECT RANDOM( 1, 100 ) AS RESULT FROM DUAL;
          RESULT
----------------
34.1870528003201
1 row selected.
```

<a id="7488f433adb0d426"></a>
### REPEAT

<a id="8d087106c68bff6c"></a>
#### 구문

```
REPEAT( str, num )
```

<a id="1cda03a1a731f4ed"></a>
#### 설명

REPEAT 함수는 num에 지정된 수만큼 str을 반복한 string을 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARCATER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

인자 num에는 숫자 타입이 올 수 있다.

str 또는 num 중의 하나라도 NULL이면, 결과값도 NULL이다.  
num의 값이 0 또는 음수인 경우에도 결과값은 NULL이다.

결과 타입은 다음 표와 같다.

**REPEAT의 결과 타입**

<a id="3103aef44a7612f0"></a>
| str 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="391013299bc44444"></a>
#### 사용 예

```
gSQL> SELECT REPEAT( 'ab', 3 ) AS RESULT FROM DUAL;
RESULT
------
ababab
1 row selected.
```

<a id="9b50e4bde9c8edd2"></a>
### REPLACE

<a id="cf021276df52a58c"></a>
#### 구문

```
REPLACE( str, from, to )
```

<a id="6b1492bc8d96fefc"></a>
#### 설명

REPLACE는 str string 내의 모든 from string을 to string으로 치환하여 반환한다.

인자 str, from, to에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str 값이 NULL인 경우, 결과값은 NULL이다.  
from 값이 NULL인 경우, str 값을 변환하지 않고 반환한다.  
to 값이 생략되었거나 NULL인 경우, str에서 from을 제거한 값이 반환된다.

결과 타입은 다음 표와 같다.

**REPLACE의 결과 타입**

<a id="4ccdca697f80fccf"></a>
| str 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="2ba3ca9567bff1b3"></a>
#### 사용 예

```
gSQL> SELECT REPLACE( 'HI GLIESE', 'HI', 'HELLO' ) AS RESULT FROM DUAL;
RESULT      
------------
HELLO GLIESE
1 row selected.
```

<a id="1809a812fddd9afb"></a>
### REVERSE

<a id="03b78b02438c5913"></a>
#### 구문

```
REVERSE( str )
```

<a id="debca2693d054f0d"></a>
#### 설명

REVERSE는 str의 문자를 역순으로 반환한다.

인자로는 character string 타입 또는 binary string 타입으로 변환될 수 있는 타입이 올 수 있으며  
character string 타입은 해당 문자 단위로, binary string 타입은 byte 단위로 수행된다.

str이 NULL일 경우 NULL을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**REVERSE 인자와 결과 타입**

<a id="c75fa7ffc4f4f8d6"></a>
| str | 결과 타입 |
| --- | --- |
| CHAR | CHAR |
| VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY | BINARY |
| VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="12b24b6ef3f47951"></a>
#### 사용 예

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

<a id="090988a74daf0bc0"></a>
### ROUND( number )

<a id="d5cc4878aedc64ac"></a>
#### 구문

```
ROUND( num [, scale ] )
```

<a id="6e8d8a48dba9f614"></a>
#### 설명

ROUND는 scale을 기준으로 num을 반올림한 값을 반환한다.

인자 num, scale에는 숫자 타입이 올 수 있다.

scale이 생략된 경우, scale은 0이 되어 ROUND( num, 0 )과 같이 수행된다.  
scale이 양수인 경우 소수점 오른쪽 자리수를 기준으로 반올림되고, scale이 음수인 경우 소수점 왼쪽 자리수를 기준으로 반올림된다.

<a id="d3d0a0bbe5b64c3a"></a>
#### 사용 예

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

<a id="edea2f2b54ee312d"></a>
### ROUND( date )

<a id="f448601594248f44"></a>
#### 구문

```
ROUND( date [ , fmt ] )
```

<a id="35cc3be37c3ba4d0"></a>
#### 설명

ROUND( date ) 함수는 date를 지정된 fmt 단위로 반올림한 값을 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
결과 타입은 인자로 받은 date 타입과 관계없이 항상 DATE 타입이다.

fmt가 생략되었을 경우의 기본값은 DAY 이며, 사용 가능한 형식문자열은 다음 표와 같다.

**fmt에 사용 가능한 형식문자열**

<a id="d9a43895435ad5a4"></a>
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

<a id="6991f99261f03aa1"></a>
#### 사용 예

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

<a id="ca9d8df7718213ca"></a>
### ROWID_GRID_BLOCK_ID

<a id="350cd98435deb5e6"></a>
#### 구문

```
ROWID_GRID_BLOCK_ID( rowid )
```

<a id="7bb38e26e8a78813"></a>
#### 설명

GRID block ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="8f6374210cec9a01"></a>
#### 사용 예

```
gSQL> SELECT C1, ROWID_GRID_BLOCK_ID( ROWID ) FROM T1;
C1 ROWID_GRID_BLOCK_ID( ROWID )
-- ----------------------------
 1                           52
 2                           52
 3                           52

3 rows selected.
```

<a id="cca6fe193cecd8cf"></a>
### ROWID_GRID_BLOCK_SEQ

<a id="1274531682ff5b78"></a>
#### 구문

```
ROWID_GRID_BLOCK_SEQ( rowid )
```

<a id="41a54caa0107b0ae"></a>
#### 설명

GRID block sequence를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="973bb3034d02d93a"></a>
#### 사용 예

```
gSQL> SELECT C1, ROWID_GRID_BLOCK_SEQ( ROWID ) FROM T1;
C1 ROWID_GRID_BLOCK_SEQ( ROWID )
-- -----------------------------
 1                        747465
 2                        747466
 3                        747467

3 rows selected.
```

<a id="3ec899ecfee01175"></a>
### ROWID_MEMBER_ID

<a id="3d51c1791a517902"></a>
#### 구문

```
ROWID_MEMBER_ID( rowid )
```

<a id="c11a5cee2e44cc59"></a>
#### 설명

Member ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="886ea416a39babe2"></a>
#### 사용 예

```
gSQL> SELECT C1, ROWID_MEMBER_ID( ROWID ) FROM T1;
C1 ROWID_MEMBER_ID( ROWID )
-- ------------------------
 1                        1
 2                        1
 3                        1

3 rows selected.
```

<a id="5c38946c0a3c4e2e"></a>
### ROWID_OBJECT_ID

<a id="f9727904aec51a64"></a>
#### 구문

```
ROWID_OBJECT_ID( rowid )
```

<a id="2fe287dc30da5b27"></a>
#### 설명

Object ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="0c89e24df72e8875"></a>
#### 사용 예

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

<a id="3c290dc2da7759f2"></a>
### ROWID_PAGE_ID

<a id="b6df81db99e1de8b"></a>
#### 구문

```
ROWID_PAGE_ID( rowid )
```

<a id="c1ecc4d86921d746"></a>
#### 설명

Page ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="b42e7a8f70ef8335"></a>
#### 사용 예

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

<a id="f84a300892c983d0"></a>
### ROWID_ROW_NUMBER

<a id="cd3c131d5160d09a"></a>
#### 구문

```
ROWID_ROW_NUMBER( rowid )
```

<a id="331458bbdf2660fb"></a>
#### 설명

Row number를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="377ddcfe73c7bb83"></a>
#### 사용 예

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

<a id="384d999841bafdb0"></a>
### ROWID_SHARD_ID

<a id="9a061ac252405453"></a>
#### 구문

```
ROWID_SHARD_ID( rowid )
```

<a id="c316e93961e5dcbe"></a>
#### 설명

Shard ID를 반환하는 함수이다.

> Cluster system에서 유효한 정보이다.

<a id="9b83a20cda662f6c"></a>
#### 사용 예

```
gSQL> SELECT C1, ROWID_SHARD_ID( ROWID ) FROM T1;
C1 ROWID_SHARD_ID( ROWID )
-- -----------------------
 1                       0
 2                       1
 3                       2

3 rows selected.
```

<a id="1b4522ef522e9d6f"></a>
### ROWID_TABLESPACE_ID

<a id="db4165f2b7910069"></a>
#### 구문

```
ROWID_TABLESPACE_ID( rowid )
```

<a id="bc88721d3838f05a"></a>
#### 설명

Tablespace ID를 반환하는 함수이다.

> Cluster system에서 유효하지 않은 정보이다.

<a id="7654780f8c544d20"></a>
#### 사용 예

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

<a id="f113e3c31c86a705"></a>
### ROWNUM

<a id="bc57c26c60a539ff"></a>
#### 구문

```
ROWNUM
```

<a id="2c03b4e2aa508148"></a>
#### 설명

WHERE 조건을 만족하는 row에 1부터 순차적으로 번호를 부여한다.

Oracle과의 호환성을 위해 WHERE 절에 ROWNUM 사용을 허용한다.

그러나 질의 결과 개수를 제한하려면 다음과 같이 SQL 표준의 [offset limit clause](16-sql-references.md#37f82ae17691b17d)를 사용할 것을 권장한다.

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

<a id="20a128056f0df59d"></a>
#### 사용 예

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

<a id="af49a5a736f0bf17"></a>
### RPAD

<a id="490552528ed1b660"></a>
#### 구문

```
RPAD( str, length, [, fill] )
```

<a id="4580598c7d60f9a2"></a>
#### 설명

RPAD 함수는 string의 길이가 length가 될 때까지 str의 오른쪽에 문자열 fill을 추가한 값을 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

인자 length에는 숫자 타입이 올 수 있다.

length는 문자의 개수를 의미하며 최대 범위는 결과 타입의 최대 PRECISION이다.  
fill이 생략된 경우, 공백 문자가 추가된다.  
str이 length보다 길이가 긴 경우에는 str을 length만큼 잘라서 반환한다.  
str, length, fill 중 하나라도 NULL이면 결과값도 NULL이며, length가 0 또는 음수인 경우에도 결과값은 NULL이다.

결과 타입은 다음 표와 같다.

**RPAD의 결과 타입**

<a id="140472798f2db0c3"></a>
| 인자 str의 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="f92ec99b0f6ad701"></a>
#### 사용 예

```
gSQL> SELECT RPAD( 'aa', 5, 'b' ) AS RESULT FROM DUAL;
RESULT
------
aabbb 
1 row selected.
```

<a id="a2e95277d0b9612a"></a>
### RTRIM

<a id="67c5ba86aa95e812"></a>
#### 구문

```
RTRIM( trim_source [, trim_character ] )
```

<a id="1c86639d4c396503"></a>
#### 설명

RTRIM 함수는 trim_source에서 trim_character를 오른쪽 방향에서 비교하여 일치하는 문자가 없을 때까지 제거한 결과를 반환한다.

인자 trim_character와 trim_source에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.

trim_character, trim_source 중 하나라도 NULL이면, 결과값은 NULL이다.  
trim_character가 생략된 경우에는 기본적으로 single blank space (' ')가 지정된다.

결과 타입은 다음과 같다.

**RTRIM의 결과 타입**

<a id="73fead4acab776e9"></a>
| trim_source, trim_character 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="9ec92976e4fddeba"></a>
#### 사용 예

```
gSQL> SELECT RTRIM( 'RTRIM_____', '_' ) AS RESULT FROM DUAL;
RESULT
------
RTRIM 
1 row selected.
```

<a id="748ef2ed123142fa"></a>
### SESSION_ID

<a id="aa910d5236265a3b"></a>
#### 구문

```
SESSION_ID()
```

<a id="c7880e1e8badda6d"></a>
#### 설명

현재 session의 ID를 얻는다.

<a id="3d78f09119b221b3"></a>
#### 사용 예

```
gSQL> SELECT SESSION_ID() FROM dual;

SESSION_ID()
------------
           4

1 row selected.
```

<a id="e6f850d5b5ac0e5f"></a>
### SESSION_SERIAL

<a id="6d398be2aba19022"></a>
#### 구문

```
SESSION_SERIAL()
```

<a id="8639990ab8e4b263"></a>
#### 설명

현재 session의 serial 번호를 얻는다.

<a id="e13dbbeb6188b524"></a>
#### 사용 예

```
gSQL> SELECT SESSION_SERIAL() FROM dual;

SESSION_SERIAL()
----------------
              16

1 row selected.
```

<a id="e67b1f1bb30429be"></a>
### SESSION_USER

<a id="9b4a083158615618"></a>
#### 구문

```
SESSION_USER[()]
```

<a id="f7ce085ef9bcb12f"></a>
#### 설명

세션 사용자를 반환한다.

사용자 정보는 다음과 같은 세 가지 형태로 관리된다.

- Logon user: login을 실행한 user로서 connection을 닫을 때까지 유지된다. 
- Session user: 최초 logon user와 동일하지만 SET SESSION AUTHORIZATION 구문을 이용해 변경할 수 있다. 
- Current user: 일반적으로 session user와 동일하지만 PSM, view 등을 사용할 때 접근 제어등을 위해 시스템 내부적으로 잠시 변경된다. 
    - Session user와 current user는 unix system의 real user와 effective user의 차이와 유사한 개념이다.

<a id="959f2c917c385d64"></a>
#### 사용 예

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

<a id="8492bcca66b4d195"></a>
### SHARD_GROUP_ID

<a id="a1bd733cce27411b"></a>
#### 구문

```
SHARD_GROUP_ID( table_name, shard_key_value [, ... ] )
```

<a id="bee6e29e2352e36d"></a>
#### 설명

SHARD_GROUP_ID 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard를 관리하는 group ID를 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 NATIVE_BIGINT이다.

> Cluster system에서 유효한 정보이다.

<a id="9c1a313b1fb4d01b"></a>
#### 사용 예

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

<a id="5a2f2ed73ac81eef"></a>
### SHARD_GROUP_NAME

<a id="dc4483afe35e52db"></a>
#### 구문

```
SHARD_GROUP_NAME( table_name, shard_key_value [, ... ] )
```

<a id="d4f6641e97c2b750"></a>
#### 설명

SHARD_GROUP_NAME 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard를 관리하는 group NAME을 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 VARCHAR이다.

> Cluster system에서 유효한 정보이다.

<a id="42063ce8347181cc"></a>
#### 사용 예

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

<a id="701f3a9ae9065f21"></a>
### SHARD_ID

<a id="744a63381a736dcf"></a>
#### 구문

```
SHARD_ID( table_name, shard_key_value [, ... ] )
```

<a id="9f1e53898e2b36ad"></a>
#### 설명

SHARD_ID 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard에 대한 ID를 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 NATIVE_BIGINT이다.

> Cluster system에서 유효한 정보이다.

<a id="831fa6fac1ec91b0"></a>
#### 사용 예

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

<a id="2684c938c39d754e"></a>
### SHARD_NAME

<a id="33b31ca20c738587"></a>
#### 구문

```
SHARD_NAME( table_name, shard_key_value [, ... ] )
```

<a id="e91c3ba22c624b82"></a>
#### 설명

SHARD_NAME 함수는 table_name에 shard strategy가 정의된 경우, shard_key_value 값을 저장할 수 있는 shard에 대한 NAME을 반환한다.

입력 인자 table_name은 identifier로 기술하여야 하며 table_name에 해당하는 객체가 base table이 아니거나 shard strategy가 정의되지 않은 경우, 에러가 발생한다.

입력 인자 shard_key_value는 table_name에 정의된 shard strategy의 shard key column 순으로 나열되어야 한다. shard_key_value 개수와 shard key column 개수가 일치하지 않을 경우, 에러가 발생한다.

결과 타입은 VARCHAR이다.

> Cluster system에서 유효한 정보이다.

<a id="a7654ba896175345"></a>
#### 사용 예

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

<a id="657c1b8a74a4923b"></a>
### SHIFT_LEFT

<a id="49a7f30e24eab18c"></a>
#### 구문

```
SHIFT_LEFT( num, cnt )
```

<a id="fe61c0b2639f96ac"></a>
#### 설명

SHIFT_LEFT 함수는 num을 cnt 비트만큼 왼쪽으로 이동시킨 값을 반환한다.

입력 인자 num, cnt에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환하면 소수점은 TRUNCATE 된다.

연산 시 cnt는 6 bit로 마스킹하여 6 bit 범위 내의 값으로 처리한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="ca81f9e46313aceb"></a>
#### 사용 예

```
gSQL> SELECT SHIFT_LEFT( 7, 3 ) AS RESULT FROM DUAL;
RESULT
------
    56
1 row selected.
```

<a id="ef522f94a2be0e12"></a>
### SHIFT_RIGHT

<a id="87e1586afdd15de6"></a>
#### 구문

```
SHIFT_RIGHT( num, cnt )
```

<a id="6f3a8bbad4e0c5d5"></a>
#### 설명

SHIFT_RIGHT 함수는 num을 cnt 비트만큼 오른쪽으로 이동시킨 값을 반환한다.

입력 인자 num, cnt에는 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT 또는 NATIVE_BIGINT로 변환될 수 있는 타입이 올 수 있다.  
NATIVE_BIGINT 타입으로 변환하면 소수점은 TRUNCATE 된다.

연산 시 cnt는 6 bit로 마스킹하여 6 bit 범위내의 값으로 처리한다.

결과 타입은 NATIVE_BIGINT이다.

<a id="a6b25ab4ffe413f6"></a>
#### 사용 예

```
gSQL> SELECT SHIFT_RIGHT( 56, 3 ) AS RESULT FROM DUAL;
RESULT
------
     7
1 row selected.
```

<a id="f3f4dc33b835cfb4"></a>
### SIGN

<a id="97a231b42e69c46e"></a>
#### 구문

```
SIGN( num )
```

<a id="3c27a39cd21f1d1f"></a>
#### 설명

SIGN 함수는 num의 부호를 반환한다.

인자 num에는 숫자타입이 올 수 있다.

반환값은 다음과 같다.  

• num < 0 이면 -1  
• num = 0 이면 0  
• num > 0 이면 1

<a id="bd014a2e1d5a198e"></a>
#### 사용 예

```
gSQL> SELECT SIGN(-10) AS RESULT1, 
             SIGN(0) AS RESULT2, 
             SIGN(10) AS RESULT3 FROM DUAL;
RESULT1 RESULT2 RESULT3
------- ------- -------
     -1       0       1
1 row selected.
```

<a id="b10923b221cf674f"></a>
### SIN

<a id="087d5fa3b4180b47"></a>
#### 구문

```
SIN( num )
```

<a id="0ef4a63b3e724d2f"></a>
#### 설명

SIN 함수는 num의 sine 값을 반환한다.

<a id="bf692bcf6b814b1b"></a>
#### 사용 예

```
gSQL> SELECT SIN( 0 ) AS RESULT FROM DUAL;
RESULT
------
     0
1 row selected.
```

<a id="3f92ba4885716086"></a>
### SPLIT_PART

<a id="3e7f8f31f7275c53"></a>
#### 구문

```
SPLIT_PART( string, delimiter, field )
```

<a id="3dc6aa51ca525e57"></a>
#### 설명

SPLIT_PART 함수는 string 내에서 delimiter로 지정된 문자를 구분자로 하여 field의 문자열을 반환한다.

인자 string, delimiter에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

인자 field에는 숫자 타입이 올 수 있다.

string, delimiter, field 중에 하나라도 NULL인 경우에는 결과값도 NULL이다.  
field에는 1 이상의 숫자값만 올 수 있고, 0 또는 음수일 경우에는 에러를 반환한다.

결과 타입은 다음 표와 같다.

**SPLIT_PART의 결과 타입**

<a id="e99830ab966765c5"></a>
| string 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="0c8b3d4540e04cec"></a>
#### 사용 예

```
gSQL> SELECT SPLIT_PART( 'AB;CD;EF;GH', ';', 3  ) AS RESULT FROM DUAL;
RESULT
------
EF    
1 row selected.
```

<a id="f3eeafb892d1e370"></a>
### SQRT

<a id="6a13b9141dbca5c2"></a>
#### 구문

```
SQRT( num )
```

<a id="398ad1eff63a8387"></a>
#### 설명

SQRT 함수는 num의 제곱근을 반환한다.

인자 num에는 숫자 타입이 올 수 있는데 음수가 아닌 0 이상의 값이어야 한다.

<a id="fdf8ff1a3dfaa1ed"></a>
#### 사용 예

```
gSQL> SELECT SQRT( 9 ) AS RESULT FROM DUAL;
RESULT
------
     3
1 row selected.
```

<a id="23b9e7a0262409a5"></a>
### STATEMENT_DATE

<a id="f70258ef2dafb667"></a>
#### 구문

```
STATEMENT_DATE()
CURRENT_DATE [()]
```

<a id="d04271a5e2087ce1"></a>
#### 설명

현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="1ee0fb9b3efba950"></a>
#### 사용 예

```
gSQL> SELECT STATEMENT_DATE() AS result FROM t1;

RESULT    
----------
2013-12-12
2013-12-12
2013-12-12

3 rows selected.
```

<a id="699791b88fd6ad60"></a>
### STATEMENT_LOCALTIME

<a id="8fc915b9def90f02"></a>
#### 구문

```
STATEMENT_LOCALTIME()
LOCALTIME [()]
```

<a id="1d963a2224fe7470"></a>
#### 설명

Session 시간을 기준으로 현재 TIME WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="47f5d6c9544e0c7b"></a>
#### 사용 예

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

<a id="d5718be94dde3972"></a>
### STATEMENT_LOCALTIMESTAMP

<a id="93cf8512b4bf7f27"></a>
#### 구문

```
STATEMENT_LOCALTIMESTAMP()
LOCALTIMESTAMP [()]
```

<a id="daec5fee9dc9e997"></a>
#### 설명

Session 시간을 기준으로 현재 TIMESTAMP WITHOUT TIME ZONE type 값을 얻는다.

LOCALTIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="f7e764acabe3357c"></a>
#### 사용 예

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

<a id="5c8d77b5856a285b"></a>
### STATEMENT_TIME

<a id="7ac1604316245db4"></a>
#### 구문

```
STATEMENT_TIME()
CURRENT_TIME [()]
```

<a id="76afb9e2dfaf6369"></a>
#### 설명

TIME ZONE이 있는 현재 TIME (TIME WITH TIME ZONE type) 값을 얻는다.

CURRENT_TIME은 SQL 표준 함수이다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="755a472b7dbb1ee6"></a>
#### 사용 예

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

<a id="442e0c52fd4e267e"></a>
### STATEMENT_TIMESTAMP

<a id="ef46b2e57375ab62"></a>
#### 구문

```
STATEMENT_TIMESTAMP()
CURRENT_TIMESTAMP [()]
```

<a id="963ad56b05771649"></a>
#### 설명

TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

CURRENT_TIMESTAMP는 SQL 표준 함수이다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="ba529faa9484998b"></a>
#### 사용 예

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

<a id="57d62b93fb6c220b"></a>
### STATEMENT_VIEW_SCN

<a id="ffe2f2585c01ff3d"></a>
#### 구문

```
STATEMENT_VIEW_SCN()
```

<a id="fa6779e9f352a209"></a>
#### 설명

현재 STATEMENT의 VIEW SCN을 얻는다.

<a id="7cfe90a8609d2ee9"></a>
#### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN() FROM dual;

STATEMENT_VIEW_SCN()
--------------------
17697.658.17880     

1 row selected.
```

<a id="6e86a825de9e5ca8"></a>
### STATEMENT_VIEW_SCN_DCN

<a id="f94ee7db0d9271ac"></a>
#### 구문

```
STATEMENT_VIEW_SCN_DCN()
```

<a id="d5cbba84745ad002"></a>
#### 설명

현재 STATEMENT의 VIEW SCN의 Domain Change Number (DCN) 값을 얻는다.

<a id="b760131fc75441ef"></a>
#### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_DCN() FROM dual;

STATEMENT_VIEW_SCN_DCN()
------------------------
                     658

1 row selected.
```

<a id="2c5e15daa97a831a"></a>
### STATEMENT_VIEW_SCN_GCN

<a id="8a4381348844a22a"></a>
#### 구문

```
STATEMENT_VIEW_SCN_GCN()
```

<a id="93e3a8bad511adce"></a>
#### 설명

현재 STATEMENT의 VIEW SCN의 Global Change Number (GCN) 값을 얻는다.

<a id="8cac230b162b16c9"></a>
#### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_GCN() FROM dual;

STATEMENT_VIEW_SCN_GCN()
------------------------
                   17697

1 row selected.
```

<a id="5b0a2b47021a0265"></a>
### STATEMENT_VIEW_SCN_LCN

<a id="9fe15bbcbbbc7bef"></a>
#### 구문

```
STATEMENT_VIEW_SCN_LCN()
```

<a id="55be66af00103514"></a>
#### 설명

현재 STATEMENT의 VIEW SCN의 Local Change Number (LCN) 값을 얻는다.

<a id="a80ec627da0c5796"></a>
#### 사용 예

```
gSQL> SELECT STATEMENT_VIEW_SCN_LCN() FROM dual;

STATEMENT_VIEW_SCN_LCN()
------------------------
                   17880

1 row selected.
```

<a id="55362e40aae95d6a"></a>
### STDDEV

<a id="3e80c366a88ae3ab"></a>
#### 구문

```
STDDEV( [ ALL | DISTINCT ] expr )
```

<a id="d46ca6aeef11ada4"></a>
#### 설명

Aggregation 함수로써 expr set의 표준편차 (standard deviation)를 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 수행하고, DISTINCT를 명시한 경우 중복을 제거한 값들에 대해 수행한다. 둘 다 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

NULL 값을 제외하고 DISTINCT로 중복을 제거한 후의 expr set의 개수가 한 개일 경우, [VARIANCE](#051de20384a5e1c8)와 같이 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV 인자와 결과 타입**

<a id="a6fee2b297a3ddc8"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

GOLDILOCKS는 다음과 같이 표준편차를 계산한다.  

• expr set의 개수가 1이면 0을 반환한다.  
• expr set의 개수가 1보다 크면 [STDDEV_SAMP( expr )](#3cc8ea60b60a3c12) 값을 반환한다.

> 표준편차는 분산의 양의 제곱근으로써 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV 함수는 [VARIANCE](#051de20384a5e1c8) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV( [ ALL ] expr )  
>  = SQRT( VARIANCE( [ ALL ] expr ) )  
>   
> STDDEV( DISTINCT expr )  
>  = SQRT( VARIANCE( DISTINCT expr ) )

<a id="1c26487928fe3355"></a>
#### 사용 예

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

<a id="6402c3dcd4e4fe05"></a>
### STDDEV_POP

<a id="40e350a34951d4aa"></a>
#### 구문

```
STDDEV_POP( expr )
```

<a id="dae5224baa975b58"></a>
#### 설명

Aggregation 함수로써 expr set의 모 표준편차 (population standard deviation)를 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV_POP의 인자와 결과 타입**

<a id="004f2510ed1c7f8e"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 표준편차는 모 분산의 양의 제곱근으로써 모 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV_POP 함수는 [VAR_POP](#46e177e0aaffbb82) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV_POP( expr )  
>  = SQRT( VAR_POP( expr ) )

<a id="4714d2b7d2f3bc5d"></a>
#### 사용 예

```
gSQL> SELECT STDDEV_POP(c1) FROM t1;

 STDDEV_POP(C1)
---------------
10.283968105746

1 row selected.
```

<a id="3cc8ea60b60a3c12"></a>
### STDDEV_SAMP

<a id="06dca185b73d8fcb"></a>
#### 구문

```
STDDEV_SAMP( expr )
```

<a id="3b521e728c3d7be0"></a>
#### 설명

Aggregation 함수로써 expr set의 표본 표준편차 (sample standard deviation)를 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 NULL값을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**STDDEV_SAMP의 인자와 결과 타입**

<a id="095514df6dc5db34"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 표본 표준편차는 표본 분산의 양의 제곱근으로써 표본 분산에 루트를 씌워서 계산한다.  
> 즉, STDDEV_SAMP 함수는 [VAR_SAMP](#345e88314b92a36d) 함수에 루트를 씌운 것과 같다.  
>   
> STDDEV_SAMP( expr )  
>  = SQRT( VAR_SAMP( expr ) )

<a id="8c18d841dda5fac9"></a>
#### 사용 예

```
gSQL> SELECT STDDEV_SAMP(c1) FROM t1;

 STDDEV_SAMP(C1)
----------------
11.4978258814438

1 row selected.
```

<a id="8f078bc6cefab9f8"></a>
### SUBSTR

<a id="8f1fb842035110fc"></a>
#### 구문

```
SUBSTR( str FROM start_position [ FOR string_length ] )
SUBSTR( str, start_position [ , string_length ] )
```

<a id="49649b44991cc2d8"></a>
#### 설명

[SUBSTRING](#5247eb0b134895cf)의 alias 이다.

<a id="eca33f138215e65b"></a>
#### 사용 예

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

<a id="ea687e1f8622d7d1"></a>
### SUBSTRB

<a id="a4aa2f9e1b32fe0d"></a>
#### 구문

```
SUBSTRB( str, start_position [ , string_length ] )
```

<a id="f972acd4ed22ca87"></a>
#### 설명

SUBSTRB 함수는 str에 대해 start_position으로부터 string_length 범위의 문자를 추출하여 반환한다.

SUBSTRB 함수는 start_position과 string_length가 byte 단위로 계산된다는 점 외에는 [SUBSTRING](#5247eb0b134895cf) 함수와 동일하다.

<a id="c739084399488769"></a>
#### 사용 예

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

<a id="5247eb0b134895cf"></a>
### SUBSTRING

<a id="1c34e3fc2f68ec32"></a>
#### 구문

```
SUBSTRING( str FROM start_position [ FOR string_length ] )  
SUBSTRING( str, start_position [ , string_length ] )
```

<a id="ab65dc8c0fb74ec4"></a>
#### 설명

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
자세한 내용은 [SUBSTR](#8f078bc6cefab9f8)과 [SUBSTRB](#ea687e1f8622d7d1)를 참조한다.

결과 타입은 다음 표와 같다.

**SUBSTRING의 결과 타입**

<a id="d59349f6c74f829f"></a>
| str | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="0778e058835e4ab9"></a>
#### 사용 예

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

<a id="1a0c9e6b27cddbc2"></a>
### SUM

<a id="982a73932f51a6fb"></a>
#### 구문

```
SUM( [ ALL | DISTINCT ] expr )
```

<a id="4551e503453822cf"></a>
#### 설명

Aggregation 함수로써 expr 값들의 합을 얻는다.

ALL을 명시한 경우, 모든 값들에 대해 aggregation을 수행한다.  
DISTINCT를 명시한 경우, 중복을 제거한 값들에 대해 aggregation을 수행한다.  
ALL이나 DISTINCT를 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

<a id="56234218d92a6ee8"></a>
#### 사용 예

```
gSQL> SELECT SUM(c1) FROM t1;

SUM(C1)
-------
      6

1 row selected.
```

<a id="bb00ec3be51cce3a"></a>
### SYSDATE

<a id="a131ab719d620b24"></a>
#### 구문

```
SYSDATE
```

<a id="76ade5a4a3a7577b"></a>
#### 설명

Database server가 위치하는 OS 시간을 기준으로 현재의 DATE type 값을 얻는다.

<a id="9045bb6ca7e7f586"></a>
#### 사용 예

```
gSQL> SELECT SYSDATE FROM t1;

SYSDATE   
----------
2013-12-12
2013-12-12
2013-12-12

3 rows selected.
```

<a id="2aa7a9deb171ee13"></a>
### SYS_EXTRACT_UTC

<a id="c591ca5c7ba75f05"></a>
#### 구문

```
SYS_EXTRACT_UTC( datetime_with_timezone )
```

<a id="68c8b7884811447f"></a>
#### 설명

SYS_EXTRACT_UTC는 UTC (Coordinated Universal Time—formerly Greenwich Mean Time) 값을 반환한다.  
timezone이 명시되지 않은 경우, session time zone으로 계산된다.

입력 인자에는 time, time with time zone, timestamp, timestamp with time zone 타입이 올 수 있다.  
결과 타입은 time 또는 timestamp 타입이다.

<a id="7c82d0920ff1ce0b"></a>
#### 사용 예

```
gSQL> SELECT 
      SYS_EXTRACT_UTC( 
          TO_TIMESTAMP_TZ( '2017-05-25 21:13:32.123456 +09:00',
                           'YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM') 
          ) AS RESULT 
      FROM DUAL;
RESULT                    
--------------------------
2017-05-25 12:13:32.123456
1 row selected.
```

<a id="8082a71cab46274b"></a>
### SYSTIME

<a id="d7c7aef9129446a2"></a>
#### 구문

```
SYSTIME
```

<a id="b56ced0a2e81a6c0"></a>
#### 설명

Database server가 위치하는 OS 시간을 기준으로 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

<a id="2cbcc3d25c69b7b6"></a>
#### 사용 예

```
gSQL> SELECT SYSTIME FROM t1;

SYSTIME               
----------------------
16:30:46.954941 +09:00
16:30:46.954941 +09:00
16:30:46.954941 +09:00

3 rows selected.
```

<a id="21db95ba7e8f73c4"></a>
### SYSTIMESTAMP

<a id="054c9219fc6ffdcc"></a>
#### 구문

```
SYSTIMESTAMP
```

<a id="f390188b8d8284a3"></a>
#### 설명

Database server가 위치하는 OS 시간을 기준으로 TIME ZONE이 있는 현재 TIMESTAMP WITH TIME ZONE type 값을 얻는다.

<a id="3f1bf5274564c60a"></a>
#### 사용 예

```
gSQL> SELECT SYSTIMESTAMP FROM t1;

SYSTIMESTAMP                     
---------------------------------
2013-12-12 16:37:34.432241 +09:00
2013-12-12 16:37:34.432241 +09:00
2013-12-12 16:37:34.432241 +09:00

3 rows selected.
```

<a id="851194d4a59fc92d"></a>
### TAN

<a id="4ecc0efbdfd855d6"></a>
#### 구문

```
TAN( num )
```

<a id="f79026f6d7bb1fc4"></a>
#### 설명

TAN 함수는 num의 tangent 값을 라디안 단위로 반환한다.

<a id="1bf9eddbed751bc6"></a>
#### 사용 예

```
gSQL> SELECT TAN( 1 ) AS RESULT FROM DUAL;
         RESULT
---------------
1.5574077246549
1 row selected.
```

<a id="ce1f3ac6f7c95caa"></a>
### TO_BASE64

<a id="eb6b4a31f6a6c85a"></a>
#### 구문

```
TO_BASE64( str )
```

<a id="422c9b20c8d36ba5"></a>
#### 설명

TO_BASE64는 str을 base64 인코딩으로 변환한 문자를 반환한다.  
인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입 또는 문자 타입으로 변환될 수 있는 타입과 BINARY, BINARY VARYING, BINARY LONG VARYING과 같은 BINARY 문자 타입이 올 수 있다.  
결과 타입은 CHARACTER VARYING 또는 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.

Base64 인코딩은 8 비트    바이너리 데이터를 ascii 영역으로 구성된 64개의 문자로 표현한다.  
64개의 문자는 A~Z, a~z, 0~9, +, / 로 구성된다.

6 bit를 하나의 문자로 표현하며, 세 개의 문자 (24 bit)를 하나의 단위로 네 개의 문자로 표현한다.  
인코딩 된 문자가 네 개의 문자를 채우지 못하면 나머지는 '=' 로 채운다.  
인코딩 된 문자가 76개를 넘으면 newline이 추가되어 여러 라인으로 나누어진다.

Base64 인코딩 된 문자의 디코딩은 FROM_BASE64() 함수를 이용한다.  
Base64를 디코딩 할 때는 newline, carriage return, tab, space가 무시된다.

자세한 내용은 [FROM_BASE64](#ea0b9a178af37c8d)를 참조한다.

<a id="0a805e8eb969a257"></a>
#### 사용 예

```
gSQL> SELECT TO_BASE64( 'abc' ), TO_BASE64( 'abcd' ) FROM DUAL;

TO_BASE64( 'abc' ) TO_BASE64( 'abcd' )
------------------ -------------------
YWJj               YWJjZA==           
1 row selected.
```

<a id="1aa9ef481e07ad64"></a>
### TO_CHAR( datetime )

<a id="0874a40e6008ed44"></a>
#### 구문

```
TO_CHAR( datetime [, fmt ] )
```

<a id="1155aaea021013f7"></a>
#### 설명

TO_CHAR( datetime ) 함수는 datetime을 명시된 fmt 형식의 문자열로 변환하여 반환한다.

인자 datetime에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE, TIME, TIME WITH TIME ZONE, INTERVAL 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

fmt가 생략된 경우, 다음과 같은 default format 형식을 따른다.  
• DATE: [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#39cb46c447575199)  
• TIMESTAMP: [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#db86968fe3d06d6e)  
• TIMESTAMP WITH TIME ZONE: [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#3356e96838139b8a)  
• TIME: [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#2524063f770de1b8)  
• TIME WITH TIME ZONE: [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#838ff7f06a1cc0ac)

인자 datetime이 INTERVAL 타입인 경우, fmt와 무관하게 string으로 변환하여 반환한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](#6c90db97831852f6)을 참조한다.

결과 타입은 CHARACTER VARYING 이다.

<a id="05a47249e388452f"></a>
#### 사용 예

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

<a id="d0f1dcb76f6a4884"></a>
### TO_CHAR( number )

<a id="718ca4a296333229"></a>
#### 구문

```
TO_CHAR( number [, fmt ] )
```

<a id="5241d955ca4d868e"></a>
#### 설명

TO_CHAR( number ) 함수는 number를 명시된 fmt 형식의 문자열로 변환하여 반환한다.

인자 number에는 숫자 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, 모든 유효 숫자를 문자열로 변환하여 반환한다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](#5f09922ffd9417b0)을 참조한다.

결과 타입은 CHARACTER VARYING 이다.

<a id="6782ae27c0a89e9f"></a>
#### 사용 예

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

<a id="45c8ee60f5aa8084"></a>
### TO_DATE

<a id="44ef3817d3d7e663"></a>
#### 구문

```
TO_DATE( str [, fmt ] )
```

<a id="e86cb78c0e8d5561"></a>
#### 설명

TO_DATE 함수는 명시된 fmt 형식의 문자열 str을 DATE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_DATE_FORMAT은 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](#6c90db97831852f6)을 참조한다.  
자세한 내용은 [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#39cb46c447575199)을 참조한다.

결과 타입은 DATE 이다.

<a id="7ffd8984c20218aa"></a>
#### 사용 예

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

<a id="e2adb0785ea15c2a"></a>
### TO_NATIVE_DOUBLE

<a id="f37928d9bcd5693e"></a>
#### 구문

```
TO_NATIVE_DOUBLE( str [, fmt ] )
```

<a id="4c9d619b5f2eaf85"></a>
#### 설명

TO_NATIVE_DOUBLE 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_DOUBLE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](#5f09922ffd9417b0)을 참조한다.

결과 타입은 NATIVE_DOUBLE이다.

<a id="c0eae8aa4d2964bc"></a>
#### 사용 예

```
gSQL> SELECT TO_NATIVE_DOUBLE( '123.45' ) AS RESULT1, 
             TO_NATIVE_DOUBLE( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
1 row selected.
```

<a id="9227dcb27754ec3b"></a>
### TO_NATIVE_REAL

<a id="119256002bf21052"></a>
#### 구문

```
TO_NATIVE_REAL( str [, fmt ] )
```

<a id="6e2b304f255bd779"></a>
#### 설명

TO_NATIVE_REAL 함수는 명시된 fmt 형식의 문자열 str을 NATIVE_REAL 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면, 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](#5f09922ffd9417b0)을 참조한다.

결과 타입은 NATIVE_REAL이다.

<a id="27922b1031ce4932"></a>
#### 사용 예

```
gSQL> SELECT TO_NATIVE_REAL( '123.45' ) AS RESULT1, 
             TO_NATIVE_REAL( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
```

<a id="391976f1ebfbe1b4"></a>
### TO_NUMBER

<a id="d40bf8fb3032e1f5"></a>
#### 구문

```
TO_NUMBER( str [, fmt] )
```

<a id="b090293082aec6d7"></a>
#### 설명

TO_NUMBER 함수는 명시된 fmt 형식의 문자열 str을 NUMBER 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

str과 fmt 중 하나라도 NULL이면 결과값도 NULL이다.  
fmt에 지정할 수 있는 문자열은 [Number Format 문자열](#5f09922ffd9417b0)을 참조한다.

결과 타입은 NUMBER이다.

<a id="29a8acb757765289"></a>
#### 사용 예

```
gSQL> SELECT TO_NUMBER( '123.45' ) AS RESULT1, 
             TO_NUMBER( '+123.45', 'S999.99' ) AS RESULT2 
        FROM DUAL;
RESULT1 RESULT2
------- -------
 123.45  123.45
1 row selected.
```

<a id="c6462fe8a092223a"></a>
### TO_TIME

<a id="dec3951a7d4ec590"></a>
#### 구문

```
TO_TIME( str [, fmt ] )
```

<a id="294405238a057027"></a>
#### 설명

TO_TIME 함수는 명시된 fmt 형식의 문자열 str을 TIME 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIME_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](#6c90db97831852f6)을 참조한다.  
자세한 내용은 [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#2524063f770de1b8)을 참조한다.

결과 타입은 TIME 이다.

<a id="4948c1acd3bcc717"></a>
#### 사용 예

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

<a id="ae27f0b15daa7110"></a>
### TO_TIME_TZ

<a id="c9c5f051fea27277"></a>
#### 구문

```
TO_TIME_TZ( str [, fmt ] )
```

<a id="b925fec0bf9df402"></a>
#### 설명

TO_TIME_WITH_TIME_ZONE의 alias이다.  
자세한 내용은 [TO_TIME_WITH_TIME_ZONE](#132b267c45037442)과 [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#838ff7f06a1cc0ac)을 참조한다.

<a id="e6c7ed28d089ec9d"></a>
#### 사용 예

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

<a id="132b267c45037442"></a>
### TO_TIME_WITH_TIME_ZONE

<a id="ef1abadf1f2e29b2"></a>
#### 구문

```
TO_TIME_WITH_TIME_ZONE( str [, fmt ] )
TO_TIME_TZ( str [, fmt ] )
```

<a id="42c090ae20a224cb"></a>
#### 설명

TO_TIME_WITH_TIME_ZONE 함수는 명시된 fmt 형식의 문자열 str을 TIME WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIME_WITH_TIME_ZONE_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](#6c90db97831852f6)을 참조한다.  
자세한 내용은 [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#838ff7f06a1cc0ac)을 참조한다.

TO_TIME_WITH_TIME_ZONE의 alias로는 [TO_TIME_TZ](#ae27f0b15daa7110) 함수가 있다.

결과 타입은 TIME WITH TIME ZONE 이다.

<a id="a3b80765b3057028"></a>
#### 사용 예

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

<a id="e11d27a423dbc46c"></a>
### TO_TIMESTAMP

<a id="602e6ecc79af684e"></a>
#### 구문

```
TO_TIMESTAMP( str [, fmt ] )
```

<a id="57505473c3207bbe"></a>
#### 설명

TO_TIMESTAMP 함수는 명시된 fmt 형식의 문자열 str을 TIMESTAMP 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIMESTAMP_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](#6c90db97831852f6)을 참조한다.  
자세한 내용은 [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#db86968fe3d06d6e)을 참조한다.

결과 타입은 TIMESTAMP 이다.

<a id="0a9187381b40de4a"></a>
#### 사용 예

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

<a id="1dde6cb4411f3cf2"></a>
### TO_TIMESTAMP_TZ

<a id="692146f76e676a65"></a>
#### 구문

```
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="52a30a483937702d"></a>
#### 설명

TO_TIMESTAMP_WITH_TIME_ZONE의 alias이다.  
자세한 내용은 [TO_TIMESTAMP_WITH_TIME_ZONE](#deb069ec65b335a1)과 [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#3356e96838139b8a)을 참조한다.

<a id="3f76e2a192dbb0b6"></a>
#### 사용 예

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

<a id="deb069ec65b335a1"></a>
### TO_TIMESTAMP_WITH_TIME_ZONE

<a id="c6dd61410884bd07"></a>
#### 구문

```
TO_TIMESTAMP_WITH_TIME_ZONE( str [, fmt ] )
TO_TIMESTAMP_TZ( str [, fmt ] )
```

<a id="ad00ccf1e578c3aa"></a>
#### 설명

TO_TIMESTAMP_WITH_TIME_ZONE 함수는 명시된 fmt 형식의 문자열 str을 TIMESTAMP WITH TIME ZONE 타입으로 변환하여 반환한다.

인자 str과 fmt에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.  
fmt가 생략된 경우, NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT이 default format 형식이 되고, 이 경우 str은 default format 형식의 문자열이어야 한다.

fmt에 지정할 수 있는 문자열은 [Datetime Format 문자열](#6c90db97831852f6)을 참조한다.  
자세한 내용은 [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#3356e96838139b8a)을 참조한다.

TO_TIMESTAMP_WITH_TIME_ZONE의 alias로는 [TO_TIMESTAMP_TZ](#1dde6cb4411f3cf2) 함수가 있다.

결과 타입은 TIMESTAMP WITH TIME ZONE 이다.

<a id="167e3ee46edd93f0"></a>
#### 사용 예

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

<a id="e76700903a4afd0e"></a>
### TRANSACTION_DATE

<a id="e3d66bbeed520c55"></a>
#### 구문

```
TRANSACTION_DATE()
```

<a id="a2762ae44837356e"></a>
#### 설명

Session 시간을 기준으로 현재 날짜 (DATE type) 값을 얻는다.

현재 날짜를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_DATE(): 트랜잭션 내의 모든 날짜값이 동일하다.  
• STATEMENT_DATE(): 하나의 SQL 문장 내에서 모든 날짜 값이 동일하다.  
• CLOCK_DATE(): 함수가 호출될 때마다 현재 날짜 값을 얻는다.

<a id="20e2826846d88585"></a>
#### 사용 예

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

<a id="efa6df2210cc3700"></a>
### TRANSACTION_LOCALTIME

<a id="12eea457f5d208b8"></a>
#### 구문

```
TRANSACTION_LOCALTIME()
```

<a id="b182f92d7442d93f"></a>
#### 설명

Session 시간을 기준으로 TIME ZONE이 없는 현재 시간 (TIME WITHOUT TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_LOCALTIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_LOCALTIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="f2f54210cc193f52"></a>
#### 사용 예

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

<a id="86b48c062353324f"></a>
### TRANSACTION_LOCALTIMESTAMP

<a id="7a2194e7e379466a"></a>
#### 구문

```
TRANSACTION_LOCALTIMESTAMP()
```

<a id="b41f53d8c16bd19e"></a>
#### 설명

Session 시간을 기준으로 TIME ZONE이 없는 현재 TIMESTAMP (TIMESTAMP WITHOUT TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_LOCALTIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_LOCALTIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_LOCALTIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="8bd1a37e1e51d950"></a>
#### 사용 예

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

<a id="6ad4881bb7dd2346"></a>
### TRANSACTION_TIME

<a id="0190bc9bea937d08"></a>
#### 구문

```
TRANSACTION_TIME()
```

<a id="6d283a5828f1d81c"></a>
#### 설명

Session 시간을 기준으로 TIME ZONE이 있는 현재 시간 (TIME WITH TIME ZONE type) 값을 얻는다.

현재 시간을 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIME(): 트랜잭션 내의 모든 시간값이 동일하다.  
• STATEMENT_TIME(): 하나의 SQL 문장 내에서 모든 시간값이 동일하다.  
• CLOCK_TIME(): 함수가 호출될 때마다 현재 시간값을 얻는다.

<a id="ddfc8cbb8fd8f348"></a>
#### 사용 예

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

<a id="9ee4d12b971d35ad"></a>
### TRANSACTION_TIMESTAMP

<a id="a1a87b66eed9179e"></a>
#### 구문

```
TRANSACTION_TIMESTAMP()
```

<a id="eaccaf2dfd0fe547"></a>
#### 설명

Session 시간을 기준으로 TIME ZONE이 있는 현재 TIMESTAMP (TIMESTAMP WITH TIME ZONE type) 값을 얻는다.

현재 TIMESTAMP를 얻는 함수들 사이에는 다음과 같은 차이가 있다.  

• TRANSACTION_TIMESTAMP(): 트랜잭션 내의 모든 TIMESTAMP 값이 동일하다.  
• STATEMENT_TIMESTAMP(): 하나의 SQL 문장 내에서 모든 TIMESTAMP 값이 동일하다.  
• CLOCK_TIMESTAMP(): 함수가 호출될 때마다 현재 TIMESTAMP 값을 얻는다.

<a id="658b2009fc33465a"></a>
#### 사용 예

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

<a id="e452183b84993ce5"></a>
### TRANSLATE

<a id="8e187b0e067b3f73"></a>
#### 구문

```
TRANSLATE( string, from, to )
```

<a id="fed5a41c9818f840"></a>
#### 설명

TRANSLATE 함수는 string에서 from의 문자와 일치하는 모든 문자를 그에 대응하는 to 문자로 치환하여 반환한다.

인자 string, from, to에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

string, from, to 중의 하나라도 NULL이면 결과값도 NULL이다.

string에 from의 문자와 일치하지 않는 문자는 치환되지 않는다.  
string에 from의 문자와 일치하는 문자는 그에 대응하는 to 문자로 치환된다.  
from 문자의 개수가 to 문자의 개수보다 많은 경우, to 문자와 대응되지 않는 from 문자들은 string에서 제거된 후 반환된다.  
from에 동일한 문자가 여러 번 쓰인 경우, 첫 번째 매핑된 문자로 치환된다.

결과 타입은 다음 표와 같다.

**TRANSLATE의 결과 타입**

<a id="cf8c89d1874a764a"></a>
| string 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |

<a id="75e0673e1632163e"></a>
#### 사용 예

```
gSQL> SELECT TRANSLATE( '12345', '15', 'FL'  ) AS RESULT FROM DUAL;
RESULT
------
F234L 
1 row selected.

gSQL> SELECT TRANSLATE( 'ABC12345', 'ABC12345', 'XYZ' ) AS RESULT FROM DUAL;
RESULT
------
XYZ   
1 row selected.

gSQL> SELECT TRANSLATE( 'ABC12345ABC', 'ABCABCABC', 'XYZ^&*xyz' ) AS RESULT 
      FROM DUAL;
RESULT     
-----------
XYZ12345XYZ
1 row selected.
```

<a id="be03adba17d469ce"></a>
### TRIM

<a id="d3b621b6c8282256"></a>
#### 구문

```
TRIM([ [ LEADING | TRAILING | BOTH ]  [trim_character] FROM ] trim_source)
```

<a id="f2e6eaad9386dc3b"></a>
#### 설명

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

<a id="5d42c618099b0d6f"></a>
| trim_character, trim_source 타입 | 결과 타입 |
| --- | --- |
| CHAR 또는 VARCHAR | VARCHAR |
| LONG VARCHAR | LONG VARCHAR |
| BINARY 또는 VARBINARY | VARBINARY |
| LONG VARBINARY | LONG VARBINARY |

<a id="414830486c427ac1"></a>
#### 사용 예

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

<a id="0fd60f39b2b5cced"></a>
### TRUNC( number )

<a id="30c92d515595e162"></a>
#### 구문

```
TRUNC( num [ , scale ] )
```

<a id="c422f5b63d07032d"></a>
#### 설명

TRUNC( number ) 함수는 scale 기준으로 num을 버림한 값을 반환한다.

인자 num과 scale에는 숫자 타입이 올 수 있다.

scale이 생략된 경우, scale은 0이 되어 TRUNC( num, 0 )일 때와 같이 실행된다.  
scale이 양수인 경우, 소수점 오른쪽 자리수를 기준으로 버림한다.  
scale이 음수인 경우, 소수점 왼쪽 자리수를 기준으로 버림한다.

<a id="3656c8b3cd32d9bc"></a>
#### 사용 예

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

<a id="fdc711ac10bb1cb4"></a>
### TRUNC( date )

<a id="6364afaee5348b0b"></a>
#### 구문

```
TRUNC( date [ , fmt ] )
```

<a id="d5feb6544641b452"></a>
#### 설명

TRUNC( date ) 함수는 date를 지정된 fmt 단위로 버림한 값을 반환한다.

인자 date에는 DATE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 타입이 올 수 있다.  
인자 fmt에는 CHARACTER, CHARACTER VARYING과 같은 CHARACTER 문자 타입이 올 수 있다.

결과 타입은 인자로 받은 date 타입과 관계없이 항상 DATE 타입이다.

fmt가 생략되었을 경우의 기본값은 DAY이며, 사용 가능한 형식문자열은 다음 표와 같다.

**fmt에 사용 가능한 형식문자열**

<a id="5c3eddf090c85367"></a>
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

<a id="55a0b096d22c8931"></a>
#### 사용 예

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

<a id="78a88a74025eccc4"></a>
### UPPER

<a id="9b3d11dcf4224c37"></a>
#### 구문

```
UPPER( str )
```

<a id="42e6a4f3b9a51bdc"></a>
#### 설명

UPPER 함수는 str의 대문자를 반환한다.

인자 str에는 CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.  
str이 NULL이면 결과값도 NULL이다.

반환되는 타입은 인자 str과 동일한 타입이다.

<a id="77b55ae0092868ff"></a>
#### 사용 예

```
gSQL> SELECT UPPER( 'spring' ) AS RESULT FROM DUAL;
RESULT
------
SPRING
1 row selected.
```

<a id="0560e47a7d18fb05"></a>
### UNHEX

<a id="159d0190f56145ac"></a>
#### 구문

```
UNHEX( str )
```

<a id="b575b0ca97902506"></a>
#### 설명

인자 str은 16진수 문자이며, 이를 각 byte로 표현하여 binary string으로 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 BINARY VARYING이나 BINARY LONG VARYING과 같은 BINARY 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 16진수 범위에 속하지 않는 문자가 포함되면 에러를 반환한다.

자세한 내용은 [HEX](#7688a79d8466821e)를 참조한다.

<a id="75bd643698b4bc4e"></a>
#### 사용 예

```
gSQL> SELECT UNHEX( HEX( 'abc' ) ) FROM DUAL;
UNHEX( HEX( 'abc' ) )
---------------------
616263               
1 row selected.
```

<a id="c038868bcd7f08a6"></a>
### UNHEX_TO_CHARSTR

<a id="ffcce233d646564e"></a>
#### 구문

```
UNHEX_TO_CHARSTR( str )
```

<a id="fa7f4128d37f63bc"></a>
#### 설명

인자 str은 16진수 문자이며 이를 각 byte로 표현하여 character string으로 반환한다.

입력 인자에는 CHARACTER VARYING, CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이 올 수 있고, 결과 타입은 CHARACTER VARYING이나 CHARACTER LONG VARYING과 같은 CHARACTER 문자 타입이다.

str이 NULL이면 결과값도 NULL이다.  
str에 16진수 범위에 속하지 않는 문자가 포함되면 에러를 반환한다.

인자 str가 어떤 데이터의 16진수 문자표현인지 알 수 없으므로 character string으로 반환할 때 현재 적용할 수 있는 character set을 적용하여 결과값을 반환한다.  
현재 적용할 수 있는 character set에 포함되지 않는 경우, 에러를 반환한다.

자세한 내용은 [HEX](#7688a79d8466821e)와  [UNHEX](#0560e47a7d18fb05) 를 참조한다.

<a id="97b5673d34f1552b"></a>
#### 사용 예

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

<a id="871d8b18f427df1f"></a>
### USER_ID

<a id="30256e09117dea41"></a>
#### 구문

```
USER_ID ()
```

<a id="d6cc6793cc290a2d"></a>
#### 설명

현재 사용자의 number ID를 얻는다.

> Cluster system에서는 접속한 server에 따라 다른 값을 가질 수 있다.  
> 현재 사용자의 이름을 얻는 [CURRENT_USER](#27bffc804504302b) 함수 사용을 권장한다.

<a id="3c0d2f3e31636040"></a>
#### 사용 예

```
% gsql test test

gSQL> SELECT USER_ID() FROM dual;

USER_ID()
---------
        6

1 row selected.
```

<a id="74278a9a376a7dc9"></a>
### UUID

<a id="e2def6fa49536d37"></a>
#### 구문

```
UUID()
```

<a id="3e195e9a935f9770"></a>
#### 설명

UUID 함수는 전역고유식별자 (Universal Unique Identifier) 를 생성하여 반환한다.  
반환되는 타입은 VARBINARY 이며 내부적으로 16 바이트로 구성된다.

<a id="84e58dc235d4b70f"></a>
#### 사용 예

```
gSQL> SELECT HEX( UUID() ) FROM DUAL;
HEX( UUID() )                   
--------------------------------
E6F0A5C2387511E8B95259E479C2FD50
1 row selected.
```

<a id="46e177e0aaffbb82"></a>
### VAR_POP

<a id="b2e52bb6784a60c8"></a>
#### 구문

```
VAR_POP( expr )
```

<a id="95b540c48357f2fe"></a>
#### 설명

Aggregation 함수로써 expr set의 모 분산 (population variance)을 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**VAR_POP 인자와 결과 타입**

<a id="a30f06e3ac1d3f5a"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 분산은 모 집단 (전체)의 분산이며 분산은 편차 제곱의 평균이다. 즉, 데이터의 각 값에서 모 평균 (전체의 평균)을 빼고 제곱해서 모두 더한 뒤 모 집단의 데이터 개수로 나눈다.  
> 이는 각 관찰값들이 평균으로부터 얼마나 많이 퍼져있는지 파악하는데 사용된다.

자세한 내용은 [STDDEV_POP](#6402c3dcd4e4fe05) 을 참조한다.

<a id="464583db507725eb"></a>
#### 사용 예

```
gSQL> SELECT VAR_POP(c1) FROM t1;

VAR_POP(C1)
-----------
     105.76

1 row selected.
```

<a id="345e88314b92a36d"></a>
### VAR_SAMP

<a id="5d73e925d5f8ecb0"></a>
#### 구문

```
VAR_SAMP( expr )
```

<a id="2609f740d34af1e9"></a>
#### 설명

Aggregation 함수로써 expr set의 표본 분산 (sample variance )을 얻는다.  
NULL 값을 제외한 expr set의 개수가 한 개일 때 NULL값을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**VAR_SAMP 인자와 결과 타입**

<a id="8151d24dc05dc0ed"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> 모 집단 (전체)을 다루는 모 분산과 달리, 표본 분산은 추출한 표본으로 평균과 편차를 다룬다. 즉, 데이터의 각 값에서 표본의 평균을 빼고 제곱해서 모두 더한 뒤, 표본 집단의 데이터 개수 - 1로 나눈다.  
> 이는 모 집단의 분산을 추정하는 데 사용된다.

자세한 내용은 [STDDEV_SAMP](#3cc8ea60b60a3c12) 을 참조한다.

<a id="e3368a7c2c5c4f90"></a>
#### 사용 예

```
gSQL> SELECT VAR_SAMP(c1) FROM t1;

VAR_SAMP(C1)
------------
       132.2

1 row selected.
```

<a id="051de20384a5e1c8"></a>
### VARIANCE

<a id="93e94c407ae29643"></a>
#### 구문

```
VARIANCE( [ ALL | DISTINCT ] expr )
```

<a id="990020432118481b"></a>
#### 설명

Aggregation 함수로써 expr set의 분산 (variance)을 얻는다.

ALL을 명시한 경우 모든 값들에 대해 수행하고, DISTINCT를 명시한 경우 중복을 제거한 값들에 대해 수행한다. 둘 다 명시하지 않은 경우, ALL을 명시한 것과 동일하게 처리한다.

NULL 값을 제외하고 DISTINCT로 중복을 제거한 후의 expr set의 개수가 한 개일 경우, 0을 반환한다.

인자와 결과 타입은 다음 표와 같다.

**VARIANCE 인자와 결과 타입**

<a id="5493cb1d7741d738"></a>
| expr | 결과 타입 |
| --- | --- |
| NATIVE_INTEGER 계열 * NATIVE_SMALLINT * NATIVE_INTEGER * NATIVE_BIGINT | NATIVE_DOUBLE |
| NUMBER | NUMBER |
| NATIVE_DOUBLE 계열 * NATIVE_REAL * NATIVE_DOUBLE | NATIVE_DOUBLE |

> GOLDILOCKS는 분산을 다음과 같이 계산한다.
> 
> - expr set의 개수가 1이면 0을 반환한다.
> - expr set의 개수가 1보다 크면 [VAR_SAMP( expr )](#345e88314b92a36d) 값을 반환한다.
> 

자세한 내용은 [STDDEV](#55362e40aae95d6a) 를 참조한다.

<a id="5969008a4d965d78"></a>
#### 사용 예

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

<a id="de2cfe412d1f521d"></a>
### VERSION

<a id="750e2bf30a2522bb"></a>
#### 구문

```
VERSION()
```

<a id="a0e586aca90315a4"></a>
#### 설명

제품의 version string을 얻는다.

<a id="c2ce99cda7d0e72b"></a>
#### 사용 예

```
gSQL> SELECT VERSION() FROM dual;

VERSION()                            
-------------------------------------
Release Name.X.X.X revision(XXXXX)

1 row selected.
```

<a id="9e69b4d3f99f6473"></a>
### WIDTH_BUCKET

<a id="f62e64576b20c6e2"></a>
#### 구문

```
WIDTH_BUCKET( num, min, max, cnt )
```

<a id="6f551b70658a09fc"></a>
#### 설명

WIDTH_BUCKET 함수는 명시된 min, max 범위에서 cnt와 동일한 넓이를 갖는 구간을 생성하고, num이 속하는 구간의 위치를 반환한다.

인자 num, min, max, cnt에는 숫자 타입이 올 수 있다.

min, max는 구간에 대한 범위를 의미하며, min, max 값이 같은 경우에는 에러를 반환한다.  
cnt는 구간 개수를 의미하고 양의 정수이어야 하며 0 이거나 음수인 경우에는 에러를 반환한다.  
구간의 위치에는 1부터 시작하는 번호가 부여된다.

num, min, max, cnt 중 하나라도 NULL인 경우, 결과값도 NULL이다.

<a id="cb8d733b1deaadcc"></a>
#### 사용 예

```
gSQL> SELECT WIDTH_BUCKET( 5, 1, 20, 5 ) AS RESULT FROM DUAL;
RESULT
------
     2
1 row selected.
```

---

[← 10. Server Property](../part-02-administration-manual/10-server-property.md) · [전체 목차](../README.md) · [12. SQL Languages →](12-sql-languages.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
