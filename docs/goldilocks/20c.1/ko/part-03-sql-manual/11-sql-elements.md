<a id="be38a337a989c54c"></a>

# 11. SQL Elements

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/be38a337a989c54c)  
> 태그: `20c.1_30_tag`

[← 10. Server Property](../part-02-administration-manual/10-server-property.md) · [전체 목차](../README.md) · [12. SQL Languages →](12-sql-languages.md)

<a id="6b79f992ad045736"></a>
## Syntax Elements

<a id="bf797922265f9c61"></a>
### Identifiers

Identifier는 ordinary identifier와 delimited identifier로 나뉜다.  
Ordinary identifier는 문자 또는 문자와 숫자로 구성된 identifier로써 내부적으로 모든 문자를 대문자로 치환하여 사용한다. 따라서 대소문자를 구분하지 않는다.

다음은 ordinary identifier의 예이다.

```
GOLDILOCKS
GoldiLocks
```

Delimited identifier는 double quote (")를 시작과 끝에 기술한 문자 또는 문자와 숫자로 구성된 identifier로써 내부적으로 해당 문자를 모두 기술한 그대로 사용한다. 따라서 delimited identifier를 사용할 경우 대소문자를 구분한다.

다음은 delimited identifier의 예이다.

```
"GOLDILOCKS"
"GoldiLocks"
```

<a id="7922fb336863cf09"></a>
### Literals

Literals는 null이 아닌 값을 기술한 것이다.

<a id="c339f15239126a53"></a>
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

<a id="f9391621ee983a7e"></a>
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

<a id="617ba58a2c8c397c"></a>
#### Datetime Literals

Datetime literals는 날짜/ 시간 타입에 대한 literals를 작성하는 형식이다. Datetime value는 string literal을 사용해서 지정하거나 TO_* 함수(TO_DATE 등)를 이용해 character 또는 numeric value를 변환하여 지정할 수도 있다.

날짜/시간 타입에는 DATE, TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 이 있다.

<a id="90d5f064040cb8b2"></a>
##### Date Literals

Date literals는 DATE'string literal' 또는 TO_DATE(string_literal [, format])의 형태로 작성할 수 있다.

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
- Date value들을 시분초를 제외하고 년월일값만 비교하려면 TRUNC 함수를 이용해서 시분초값을 자정으로 설정해야 한다.

자세한 내용은 [TO_DATE](17-built-in-function-references.md#df568ff4577a76a5), [Datetime Format 문자열](#33b8ffdce1d3bfd9), [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#ec78df636da07fb6)을 참조한다.

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

<a id="2dc127512065d64c"></a>
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

자세한 내용은 [TO_TIME](17-built-in-function-references.md#acb02dbbdf32b2dd), [Datetime Format 문자열](#33b8ffdce1d3bfd9), [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#1793ce4c56053b95)을 참조한다.

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

<a id="a28cad8d72e5222f"></a>
##### Time with time zone Literals

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

자세한 내용은 [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#2bc444fb42cdd6a2), [Datetime Format 문자열](#33b8ffdce1d3bfd9), [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#0a90eef2149e893a)을 참조한다.

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

<a id="c92f2a650490cc5b"></a>
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

자세한 내용은 [TO_TIMESTAMP](17-built-in-function-references.md#9b24efe199e4c67b), [Datetime Format 문자열](#33b8ffdce1d3bfd9), [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#15c05b1b42192d13)을 참조한다.

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

<a id="7e152e3049a66f04"></a>
##### Timestamp with time zone Literals

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

자세한 내용은 [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#f50291e3f07ed587), [Datetime Format 문자열](#33b8ffdce1d3bfd9),  [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#7dad2bb0bce4c28d)을 참조한다.

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

<a id="114c959a7fc72d5d"></a>
#### Interval Literals

Interval literals는 시간의 간격을 지정한다.

Interval은 크게 두 가지로 분류되며 다음과 같이 표현한다.

- Year-month INTERVAL values
    - YEAR와 MONTH를 포함한다.
    - Display string 표현: 'year-month'
    - INTERVAL 'string literal' YEAR[leading precision] TO MONTH 또는 NUMTOYMINTERVAL( num, interval_indicator ) 형태로 작성할 수 있다.
- Day-time INTERVAL values
    - DAY, HOUR, MINUTE, SECOND (fractional seconds 포함)를 포함한다.
    - Display string 표현: 'day hour:minute:second.fractional_seconds'
    - INTERVAL 'string literal' DAY[leading precision] TO SECOND[fractional seconds precision] 또는 NUMTODSINTERVAL( num, interval_indicator ) 형태로 작성할 수 있다.
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
• 해당 field의 자리수로써 2 ~ 6까지 지정할 수 있으며, 지정하지 않을 경우의 기본값은 2이다.  
• Leading field 값이 leading precision 값을 초과하면 에러를 반환한다.

Fractional seconds precision  
• Fractional seconds의 자리수로써 0 ~ 6까지 지정할 수 있으며, 지정하지 않을 경우의 기본값은 6이다.  
• Fractional second field 값이 fractional seconds precision 값을 초과하면 반올림된다.

자세한 내용은 [INTERVAL](16-built-in-data-type-references.md#0ccce32eeb813195), [INTERVAL * TO * 에서 두 번째 이후 field의 precision과 값의 범위](16-built-in-data-type-references.md#0dd5a4e65d5e78fc), [NUMTOYMINTERVAL](17-built-in-function-references.md#403c620fa29a8d5a), [NUMTODSINTERVAL](17-built-in-function-references.md#d37de1ba15fe628b)을 참조한다.

<a id="c8c62c6fb43b65ac"></a>
#### Interval literals의 사용 예

다음은 interval literals를 사용하는 예들이다.

<a id="5390f7982e4db530"></a>
##### Interval YEAR

다음은 interval YEAR literals를 사용하는 예이다.

<a id="ba893dcc07752224"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'YEAR INTERVAL'01-00'YEAR | 1 year | +01-00 |
| INTERVAL'100'YEAR | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100'YEAR(3) | 100 year | +100-00 |
| INTERVAL'+999999'YEAR(6) | 999999 year | +999999-00 |
| INTERVAL'-999999'YEAR(6) | -(999999 year) | -999999-00 |

<a id="54d61e7c5907ad90"></a>
##### Interval MONTH

다음은 interval MONTH literals를 사용하는 예이다.

<a id="16333ea8eb58b82a"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'MONTH INTERVAL'00-01'MONTH | 1 month | +00-01 |
| INTERVAL'100'MONTH | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100'MONTH(3) | 8 year 4 month | +008-04 |
| INTERVAL'+999999'MONTH(6) | 83333 year 3 month | +083333-03 |
| INTERVAL'-999999'MONTH(6) | -(83333 year 3 month) | -083333-03 |

<a id="fc2017ffa4a4d9e3"></a>
##### Interval YEAR TO MONTH

다음은 interval YEAR TO MONTH literals를 사용하는 예이다.

<a id="be4f971c32ef0644"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1-06'YEAR TO MONTH | 1 year 6 month | +01-06 |
| INTERVAL'1-12'YEAR TO MONTH | Month value가 11을 초과하여 에러가 반환된다. | - |
| INTERVAL'100-11'YEAR TO MONTH | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100-11'YEAR(3) TO MONTH | 100 year 11 month | +100-11 |
| INTERVAL'+999999-11'YEAR(6) TO MONTH | 999999 year 11 month | +999999-11 |
| INTERVAL'-999999-11'YEAR(6) TO MONTH | -(999999 year 11 month) | -999999-11 |

<a id="dcdeb1df813be2fe"></a>
##### Interval DAY

다음은 interval DAY literals를 사용하는 예이다.

<a id="31c2854ba88f99fd"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'DAY INTERVAL'01 00:00:00'DAY | 1 day | +01 00:00:00 |
| INTERVAL'100'DAY | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100'DAY(3) | 100 day | +100 00:00:00 |
| INTERVAL'+999999'DAY(6) | 999999 day | +999999 00:00:00 |
| INTERVAL'-999999'DAY(6) | -(999999 day) | -999999 00:00:00 |

<a id="b03c37226948cce8"></a>
##### Interval HOUR

다음은 interval HOUR literals를 사용하는 예이다.

<a id="c4efe6a383fdec94"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'HOUR INTERVAL'00 01:00:00'HOUR | 1 hour | +00 01:00:00 |
| INTERVAL'1000'HOUR(3) | Leading precision 3을 초과하여 에러가 반환된다. | - |
| INTERVAL'1000'HOUR(4) | 41 day 16 hour | +0041 16:00:00 |
| INTERVAL'+999999'HOUR(6) | 41666 day 15 hour | +041666 15:00:00 |
| INTERVAL'-999999'HOUR(6) | -(41666 day 15 hour) | -041666 15:00:00 |

<a id="c9e336386c2b311a"></a>
##### Interval MINUTE

다음은 interval MINUTE literals를 사용하는 예이다.

<a id="8bf90613b6e73f8d"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'MINUTE INTERVAL'00 00:01:00'MINUTE | 1 minute | +00 00:01:00 |
| INTERVAL'12345'MINUTE(4) | Leading precision 4를 초과하여 에러가 반환된다. | - |
| INTERVAL'12345'MINUTE(5) | 8 day 13 hour 45 minute | +00008 13:45:00 |
| INTERVAL'+999999'MINUTE(6) | 694 day 10 hour 39 minute | +000694 10:39:00 |
| INTERVAL'-999999'MINUTE(6) | -(694 day 10 hour 39 minute) | -000694 10:39:00 |

<a id="ade846f553b7c195"></a>
##### Interval SECOND

다음은 interval SECOND literals를 사용하는 예이다.

<a id="98b92b29f6092279"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'SECOND INTERVAL'00 00:00:01.000000'SECOND | 1 second | +00 00:00:01.000000 |
| INTERVAL'100'SECOND | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'99.9999999'SECOND INTERVAL'99.9999999'SECOND(2,6) | Fractional seconds가 반올림되어 100 second가 되므로 leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'99.9999999'SECOND(3) | 1 minute 40 second | +000 00:01:40.000000 |
| INTERVAL'29.506167'SECOND(2, 2) | 29.51 second | +00 00:00:29.51 |
| INTERVAL'999999.999999'SECOND(6,6) | 11day 13 hour 46 minute 39.999999 second | +000011 13:46:39.999999 |
| INTERVAL'-999999.999999'SECOND(6,6) | -( 11day 13 hour 46 minute 39.999999 second) | -000011 13:46:39.999999 |

<a id="d33e77f28d40de27"></a>
##### Interval DAY TO HOUR

다음은 interval DAY TO HOUR literals를 사용하는 예이다.

<a id="b402cac871f332eb"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1 23'DAY TO HOUR INTERVAL'01 23:00:00'DAY TO HOUR | 1 day 23 hour | +01 23:00:00 |
| INTERVAL'1 24'DAY TO HOUR | Hour value가 23을 초과한 invalid 값으로써 에러를 반환한다. | - |
| INTERVAL'100 23'DAY TO HOUR | Leading precision 2를 초과하여 에러를 반환한다. | - |
| INTERVAL'100 23'DAY(3) TO HOUR | 100 day 23 hour | +100 23:00:00 |
| INTERVAL'+999999 23'DAY(6) TO HOUR | 999999 day 23 hour | +999999 23:00:00 |
| INTERVAL'-999999 23'DAY(6) TO HOUR | -(999999 day 23 hour) | -999999 23:00:00 |
| INTERVAL'-999999 +23'DAY(6) TO HOUR | 부호지정 오류로 인한 에러이다. | - |

<a id="bcdaf9a63a1c3bc7"></a>
##### Interval DAY TO MINUTE

다음은 interval DAY TO MINUTE literals를 사용하는 예이다.

<a id="ee873a7892f9e3e7"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1 23:59'DAY TO MINUTE INTERVAL'01 23:59:00'DAY TO MINUTE | 1 day 23 hour 59 second | +01 23:59:00 |
| INTERVAL'1 24:59'DAY TO MINUTE | Hour value가 23을 초과한 invalid 값으로써 에러가 반환된다. | - |
| INTERVAL'1 23:60'DAY TO MINUTE | Minute value가 59를 초과한 invalid 값으로써 에러가 반환된다. | - |
| INTERVAL'100 23:59'DAY TO MINUTE | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100 23:59'DAY(3) TO MINUTE | 100 day 23 hour 59 minute | +100 23:59:00 |
| INTERVAL'+999999 23:59'DAY(6) TO MINUTE | 999999 day 23 hour 59 minute | +999999 23:59:00 |
| INTERVAL'-999999 23:59'DAY(6) TO MINUTE | -(999999 day 23 hour 59 minute) | -999999 23:59:00 |

<a id="1fb3fd859ccd4cac"></a>
##### Interval DAY TO SECOND

다음은 interval DAY TO SECOND literals를 사용하는 예이다.

<a id="7ade34ddd5996496"></a>
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

<a id="b084c7772a587c56"></a>
##### Interval HOUR TO MINUTE

다음은 interval HOUR TO MINUTE literals를 사용하는 예이다.

<a id="cd961e1f744380c0"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'23:59'HOUR TO MINUTE INTERVAL'00 23:59:00'HOUR TO MINUTE | 23 hour 59 minute | +00 23:59:00 |
| INTERVAL'23:60'HOUR TO MINUTE | Minute value가 59를 초과하여 에러가 반환된다. | - |
| INTERVAL'100:59'HOUR TO MINUTE | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100:59'HOUR(3) TO MINUTE | 4 day 4 hour 59 minute | +004 04:59:00 |
| INTERVAL'+999999:59'HOUR(6) TO MINUTE | 41666 day 15 hour 59 minute | +041666 15:59:00 |
| INTERVAL'-999999:59'HOUR(6) TO MINUTE | -(41666 day 15 hour 59 minute) | -041666 15:59:00 |

<a id="ac6eeca4537b05be"></a>
##### Interval HOUR TO SECOND

다음은 interval HOUR TO SECOND literals를 사용하는 예이다.

<a id="897a89f48cda581b"></a>
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

<a id="80b0ec3d3877d60b"></a>
##### Interval MINUTE TO SECOND

다음은 interval MINUTE TO SECOND literals를 사용하는 예이다.

<a id="0447111b0993a859"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL '15:23.123456'MINUTE TO SECOND INTERVAL '00 00:15:23.123456'MINUTE TO SECOND | 15 minute 23.123456 second | +00 00:15:23.123456 |
| INTERVAL '15:60.123456'MINUTE TO SECOND | Second value가 59를 초과하여 에러가 반환된다. | - |
| INTERVAL '99:59.999999'MINUTE TO SECOND(2) | Fractional seconds가 반올림되어 100 minute가 되므로 leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL '99:59.999999'MINUTE(3) TO SECOND(2) | 1 hour 40 minute | +000 01:40:00.00 |
| INTERVAL '+999999:59.999999'MINUTE(6) TO SECOND(6) | 694 day 10 hour 39 minute 59.999999 second | +000694 10:39:59.999999 |
| INTERVAL '-999999:59.999999'MINUTE(6) TO SECOND(6) | -(694 day 10 hour 39 minute 59.999999 second) | -000694 10:39:59.999999 |

<a id="791a504e407d6262"></a>
### Null Value

Null value는 알 수 없는 값 또는 정의되지 않은 값이다. 모든 data type 값이 null value가 될 수 있다.   
Boolean type의 unknown 값은 null value로 대체되어 표현된다.  
Null value는 keyword로 정의되어 있으며 대소문자 구분없이 사용한다.

다음은 null value를 기술하는 예이다.

```
NULL
Null
```

<a id="2f026740093827c1"></a>
### Comments

<a id="387e3c8cc1a6a19d"></a>
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

<a id="adec39c0ab55add5"></a>
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

<a id="6ef172db083bb28e"></a>
#### Hint Comments

Hint comments는 /*+로 시작하고, */로 끝나는 comment 이다. Hint comments는 multiple line comments와 비슷하지만 시작 기호에 +가 더 있다는 점이 다르다. Hint comments에서 시작기호의 *와 + 사이에 공백이 존재하면 multiple line comments로 처리되는 것에 주의한다.

Hint comments는 다른 comment들과 달리 사용 가능한 위치가 SELECT 키워드의 바로 다음으로 지정되어 있다. Hint comments에는 사용자가 GOLDILOCKS의 optimizer에게 처리 방법 등을 지정하는 내용이 기술되어 있는데 자세한 내용은 [hint clause](18-sql-references.md#18aca4d715cae99a)를 참조한다.

다음은 hint comments를 사용하는 예이다.

```
gSQL> SELECT /*+ FULL(T1) */ * FROM T1;

I1        I2        I3        I4        I5       
--------- --------- --------- --------- ---------
column i1 column i2 column i3 column i4 column i5

1 row selected.
```

<a id="e9b431c0093f5f82"></a>
### SQL Reserved Words and Keywords

<a id="a62a0c178ef0b7e5"></a>
#### SQL Reserved Words

GOLDILOCKS에는 SQL reserved words로 지정된 reserved word가 있으며, 해당 SQL reserved words 들은 해당 사용 위치가 아닌 곳에서 사용할 수 없다.

SQL reserved words 를 double quote (") 를 이용하여 identifier 로 사용할 수 있으나, 이 경우 가독성이 떨어지므로 다음과 같이 사용하는 것은 권장하지 않는다.

```
gSQL> CREATE TABLE "SELECT" ( "FROM" INTEGER );

Table created.

gSQL> INSERT INTO "SELECT" ( "FROM" ) VALUES ( 1 );

1 row created.

gSQL> SELECT "FROM" FROM "SELECT";

FROM
----
   1

1 row selected.
```

다음은 GOLDILOCKS SQL reserved words인데 * 표시한 것은 SQL standard에서 명시한 reserved words이다. 해당 리스트는 [V$RESERVED_WORDS](../part-02-administration-manual/9-database-information.md#29264fc27574029b) view를 통해 검색할 수 있다.

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

<a id="cafe08095bff229c"></a>
#### SQL Keywords

GOLDILOCKS SQL keywords는 reserved word가 아니다. 그러나 GOLDILOCKS 내부적으로 사용하는 keyword이므로 GOLDILOCKS SQL keywords를 사용할 경우 결과의 가독성이 떨어질 수 있어 사용을 권장하지 않는다.

GOLDILOCKS SQL keywords 목록은 [V$KEYWORDS](../part-02-administration-manual/9-database-information.md#3b0adc773fc9d49d) view를 통해 검색할 수 있다.

<a id="f83232ad25c08476"></a>
### 호환성

Syntax element에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="0b4e252dea050afb"></a>
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

<a id="2ec7b2e6f23b520c"></a>
## Data Type

<a id="cd884c03908152b2"></a>
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
        - 타입 예: FLOAT(precision), NATIVE_DOUBLE

<a id="4245915c69776a33"></a>
#### 십진 숫자 타입

유효 숫자의 정밀도를 나타내는 precision과 소수점의 범위를 나타내는 scale이 십진수 (decimal)를 기반으로 한다.

<a id="ec02ff4f3fcdd6c8"></a>
##### 십진 고정 소수점 타입

십진 고정 소수점 타입은 SQL에서 정의한 타입이다.

**십진 고정 소수점 타입**

<a id="ec8d1fd7368b45b1"></a>
| Type | Decimal precision | Decimal scale |  |
| --- | --- | --- | --- |
| NUMBER( p ) | p | 0 | [NUMBER](16-built-in-data-type-references.md#d4da0b52871ed864) |
| NUMBER( p, s ) | p | s | [NUMBER](16-built-in-data-type-references.md#d4da0b52871ed864) |
| NUMERIC( p ) | p | 0 | [NUMERIC](16-built-in-data-type-references.md#262a9c1980fc868d) |
| NUMERIC( p, s ) | p | s | [NUMERIC](16-built-in-data-type-references.md#262a9c1980fc868d) |
| DECIMAL( p ) | p | 0 | [NUMERIC](16-built-in-data-type-references.md#262a9c1980fc868d) 타입의 alias |
| DECIMAL( p, s ) | p | s | [NUMERIC](16-built-in-data-type-references.md#262a9c1980fc868d) 타입의 alias |
| DEC( p ) | p | 0 | [NUMERIC](16-built-in-data-type-references.md#262a9c1980fc868d) 타입의 alias |
| DEC( p, s ) | p | s | [NUMERIC](16-built-in-data-type-references.md#262a9c1980fc868d) 타입의 alias |
| SMALLINT | 5 | 0 | [NUMBER](16-built-in-data-type-references.md#d4da0b52871ed864) 타입의 alias |
| INTEGER | 10 | 0 | [NUMBER](16-built-in-data-type-references.md#d4da0b52871ed864) 타입의 alias |
| BIGINT | 19 | 0 | [NUMBER](16-built-in-data-type-references.md#d4da0b52871ed864) 타입의 alias |
| INT2 | 5 | 0 | [NUMBER](16-built-in-data-type-references.md#d4da0b52871ed864) 타입의 alias |
| INT4 | 10 | 0 | [NUMBER](16-built-in-data-type-references.md#d4da0b52871ed864) 타입의 alias |
| INT8 | 19 | 0 | [NUMBER](16-built-in-data-type-references.md#d4da0b52871ed864) 타입의 alias |

<a id="5d3ab029494f4296"></a>
##### 십진 부동 소수점 타입

십진 부동 소수점 타입은 SQL에서 정의한 타입이다.

**십진 부동 소수점 타입**

<a id="861cf5e7c6777eeb"></a>
| Type | Decimal precision | Decimal scale | 참조 |
| --- | --- | --- | --- |
| NUMBER | 38 | N/A | [NUMBER](16-built-in-data-type-references.md#d4da0b52871ed864) |
| FLOAT( p ) | ceil( log<sub>10</sub> 2<sup>p</sup> ) | N/A | [FLOAT](16-built-in-data-type-references.md#c47f4a3b4efb2143) |
| REAL | ceil( log<sub>10</sub> 2<sup>24</sup> ) = 8 | N/A | [FLOAT](16-built-in-data-type-references.md#c47f4a3b4efb2143) 타입의 alias |
| DOUBLE | ceil( log<sub>10</sub> 2<sup>53</sup> ) = 16 | N/A | [FLOAT](16-built-in-data-type-references.md#c47f4a3b4efb2143) 타입의 alias |
| FLOAT4 | ceil( log<sub>10</sub> 2<sup>24</sup> ) = 8 | N/A | [FLOAT](16-built-in-data-type-references.md#c47f4a3b4efb2143) 타입의 alias |
| FLOAT8 | ceil( log<sub>10</sub> 2<sup>53</sup> ) = 16 | N/A | [FLOAT](16-built-in-data-type-references.md#c47f4a3b4efb2143) 타입의 alias |

<a id="f259ce1ec57cda2d"></a>
#### 이진 숫자 타입

유효 숫자의 정밀도를 나타내는 precision과 소수점의 범위를 나타내는 scale이 이진수 (binary)를 기반으로 한다.

<a id="fd5674ffe6530b33"></a>
##### 이진 고정 소수점 타입

이진 고정 소수점 타입은 C 언어의 signed integer 계열 타입을 참조한다.  
Sign bit를 표시하기 위해 1 bit를 사용하고 나머지 bit들은 precision을 표현하는데 사용하며 scale을 표현할 때는 bit를 사용하지 않는다.

**이진 고정 소수점 타입**

<a id="040c740412651588"></a>
| Type | Binary precision | Binary scale | 참조 |
| --- | --- | --- | --- |
| NATIVE_SMALLINT | 15 | 0 | [NATIVE_SMALLINT](16-built-in-data-type-references.md#b716ee44eeaa792e) |
| NATIVE_INTEGER | 31 | 0 | [NATIVE_INTEGER](16-built-in-data-type-references.md#0dbe4f5b1e200b00) |
| NATIVE_BIGINT | 63 | 0 | [NATIVE_BIGINT](16-built-in-data-type-references.md#7b26f305ddff254c) |

<a id="4a580466441b90ec"></a>
##### 이진 부동 소수점 타입

이진 부동 소수점 타입은 C 언어의 float과 double 타입을 참조한다.   
Sign bit를 표시하기 위해 1 bit를 사용하고 나머지 bit들은 precision과 scale을 표현하기 위해 사용한다.

**이진 부동 소수점 타입**

<a id="0801113590cd0149"></a>
| Type | Binary precision | Binary scale | 참조 |
| --- | --- | --- | --- |
| NATIVE_REAL | 23 | 8 | [NATIVE_REAL](16-built-in-data-type-references.md#08b92e33b3b9ead9) |
| NATIVE_DOUBLE | 52 | 11 | [NATIVE_DOUBLE](16-built-in-data-type-references.md#191fed243eebfee2) |

> 이진 부동 소수점 타입에 대한 precision과 scale은 OS 및 compiler의 환경에 따라 변동될 수 있다.

<a id="bb07f9901fe50c72"></a>
### CHARACTER STRING 타입

CHARACTER STRING 타입은 가변길이 문자열 여부와 문자열의 최대 길이에 따라 구분할 수 있다.

- 가변길이 문자열 여부에 따른 분류
    - 고정 길이 문자열
        - [CHARACTER](16-built-in-data-type-references.md#aeb676a21f399a39)
    - 가변 길이 문자열
        - [CHARACTER VARYING](16-built-in-data-type-references.md#6e53a7ffeb6fb35f), [CHARACTER LONG VARYING](16-built-in-data-type-references.md#08664b5282cf54a9)
- 문자열의 최대 길이에 따른 분류
    - 2000 [ characters 또는 bytes ]
        - [CHARACTER](16-built-in-data-type-references.md#aeb676a21f399a39)
    - 4000 [ characters 또는 bytes ]
        - [CHARACTER VARYING](16-built-in-data-type-references.md#6e53a7ffeb6fb35f)
    - 100 megabytes
        - [CHARACTER LONG VARYING](16-built-in-data-type-references.md#08664b5282cf54a9)

<a id="674ef5ca7e47fb3a"></a>
### BINARY STRING 타입

BINARY STRING 타입은 가변길이 이진 문자열 여부와 이진 문자열의 최대 길이에 따라 구분할 수 있다.

- 가변길이 이진 문자열 여부에 따른 분류
    - 고정 길이 이진 문자열
        - [BINARY](16-built-in-data-type-references.md#16d517e125730db5)
    - 가변 길이 이진 문자열
        - [BINARY VARYING](16-built-in-data-type-references.md#c9c575a219d3ec4e), [BINARY LONG VARYING](16-built-in-data-type-references.md#a1bffd61af7e5ea4)
- 이진 문자열의 최대 길이 따른 분류
    - 2000 
        - [BINARY](16-built-in-data-type-references.md#16d517e125730db5)
    - 4000 
        - [BINARY VARYING](16-built-in-data-type-references.md#c9c575a219d3ec4e)
    - 100 megabytes
        - [BINARY LONG VARYING](16-built-in-data-type-references.md#a1bffd61af7e5ea4)

<a id="84771af713e15d70"></a>
### 날짜/ 시간 타입

날짜/ 시간 타입은 년, 월, 일, 시, 분, 초, time zone offset을 각 타입의 표현방식에 맞게 지정한다.  
날짜/ 시간 타입에는 [DATE](16-built-in-data-type-references.md#9b5c806f4902fa9b), [TIME](16-built-in-data-type-references.md#0b85028d443c04e4), [TIMESTAMP](16-built-in-data-type-references.md#c4ae3ac3856a9ee0) 타입이 있다.

<a id="60e8b4f6948367dc"></a>
### INTERVAL 타입

INTERVAL 타입은 시간 간격을 지정한다.  
년, 월, 일, 시, 분, 초의 시간 간격을 각 타입의 표현방식에 맞게 지정한다.

[INTERVAL](16-built-in-data-type-references.md#0ccce32eeb813195) 타입은 값의 표현 범위에 따라 YEAR TO MONTH 계열과 DAY TO SECOND 계열로 구분할 수 있다.

<a id="59cc8f2d779a16e6"></a>
### BOOLEAN 타입

Boolean 타입은 TRUE, FALSE, UNKNOWN의 truth 값을 저장하며 UNKNOWN일 경우 null 값으로 표현한다. Condition으로 사용된 모든 expression들은 boolean 값을 반환하며, boolean type으로 정의된 column 또는 value는 condition으로 사용할 수 있다.

Boolean 타입으로 저장될 수 있는 literal은 다음과 같다.

- TRUE 값
    - Keyword: TRUE
    - 문자: 't', 'true' , 'y', 'yes' , 'on' ,'1'
- FALSE 값
    - Keyword: FALSE
    - 문자: 'f', 'false', 'n', 'no', 'off', '0'
- UNKNOWN 값
    - Keyword: UNKNOWN, NULL

자세한 내용은 [BOOLEAN](16-built-in-data-type-references.md#4fbcc0ac3db99021)을 참조한다.

<a id="9bbecdd88f33a6a9"></a>
### ROWID 타입

데이터베이스에 저장된 모든 레코드는 각기 다른 위치정보를 가지고 있으며, 각각의 레코드를 구분하기 위해 레코드 식별자 (ROWID)를 사용한다.

ROWID 타입은 레코드 식별자 (ROWID)를 저장 관리하기 위한 타입이다.   
ROWID pseudo column을 사용한 질의를 통해 레코드 식별자 (ROWID)를 얻을 수 있다.

자세한 내용은 [ROWID](16-built-in-data-type-references.md#4b6cf4f36148607d)를 참조한다.

<a id="9824da3e073b48e9"></a>
### 타입간 비교

두 타입간의 비교는 하나의 대표 타입을 기준으로 수행된다. 비교 대상 타입이 대표 타입과 다를 경우 타입 변환을 통해 비교할 수도 있다.  
[타입간 비교를 위한 대표 타입](#aaecc9679b40524f)에서는 두 타입간의 비교를 위한 대표 타입을 정의한다.

다음 표에서는 각 대표 타입별로 비교를 위해 대상 타입들을 변환하는 것에 대해 설명한다.

- [VC 에서의 비교를 위한 타입 변환](#f7d06de0e25623be)
- [LC 에서의 비교를 위한 타입 변환](#6ad146c8675247a5)
- [VB 에서의 비교를 위한 타입 변환](#f2e4e7811a4a7b57)
- [LB 에서의 비교를 위한 타입 변환](#6b45396f32d3d21b)
- [NB 에서의 비교를 위한 타입 변환](#edf991feb12a5dff)
- [ND 에서의 비교를 위한 타입 변환](#ec7d0ece1143763e)
- [NU 에서의 비교를 위한 타입 변환](#b7c26758a0794dd3)
- [DA 에서의 비교를 위한 타입 변환](#0d72b978d0c91e88)
- [TI 에서의 비교를 위한 타입 변환](#086b89ccb4e1dd08)
- [TZ 에서의 비교를 위한 타입 변환](#c5057b2863da639c)
- [TS 에서의 비교를 위한 타입 변환](#08bfbb3c2f57c3ba)
- [SZ 에서의 비교를 위한 타입 변환](#f0a1a6f84ca4e1b8)
- [YM 에서의 비교를 위한 타입 변환](#0918017f5c39ea9e)
- [DS 에서의 비교를 위한 타입 변환](#462d83bcdc712e6c)
- [BO 에서의 비교를 위한 타입 변환](#13d531b8420e71c1)
- [RI 에서의 비교를 위한 타입 변환](#964fe3714a6a14e8)

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

<a id="aaecc9679b40524f"></a>
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

<a id="f7d06de0e25623be"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | CHAR (변환 없음) |
| VARCHAR | VARCHAR (변환 없음) |

**`LC` 에서의 비교를 위한 타입 변환**

<a id="6ad146c8675247a5"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | CHAR (변환 없음) |
| VARCHAR | VARCHAR (변환 없음) |
| LONG VARCHAR | LONG VARCHAR (변환 없음) |

**`VB` 에서의 비교를 위한 타입 변환**

<a id="f2e4e7811a4a7b57"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| BINARY | BINARY (변환 없음) |
| VARBINARY | VARBINARY (변환 없음) |

**`LB` 에서의 비교를 위한 타입 변환**

<a id="6b45396f32d3d21b"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| BINARY | BINARY (변환 없음) |
| VARBINARY | VARBINARY (변환 없음) |
| LONG VARBINARY | LONG VARBINARY (변환 없음) |

**`NB` 에서의 비교를 위한 타입 변환**

<a id="edf991feb12a5dff"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | NATIVE_BIGINT |
| VARCHAR | NATIVE_BIGINT |
| LONG VARCHAR | NATIVE_BIGINT |
| NATIVE_SMALLINT | NATIVE_SMALLINT (변환 없음) |
| NATIVE_INTEGER | NATIVE_INTEGER (변환 없음) |
| NATIVE_BIGINT | NATIVE_BIGINT (변환 없음) |

**`ND` 에서의 비교를 위한 타입 변환**

<a id="ec7d0ece1143763e"></a>
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

<a id="b7c26758a0794dd3"></a>
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

<a id="0d72b978d0c91e88"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | DATE |
| VARCHAR | DATE |
| LONG VARCHAR | DATE |
| DATE | DATE (변환 없음) |

**`TI` 에서의 비교를 위한 타입 변환**

<a id="086b89ccb4e1dd08"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | TIME |
| VARCHAR | TIME |
| LONG VARCHAR | TIME |
| TIME | TIME (변환 없음) |

**`TZ` 에서의 비교를 위한 타입 변환**

<a id="c5057b2863da639c"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | TIME_TZ |
| VARCHAR | TIME_TZ |
| LONG VARCHAR | TIME_TZ |
| TIME | TIME_TZ |
| TIME_TZ | TIME_TZ (변환 없음) |

**`TS` 에서의 비교를 위한 타입 변환**

<a id="08bfbb3c2f57c3ba"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | TIMESTAMP |
| VARCHAR | TIMESTAMP |
| LONG VARCHAR | TIMESTAMP |
| DATE | DATE (변환 없음) |
| TIMESTAMP | TIMESTAMP (변환 없음) |

**`SZ` 에서의 비교를 위한 타입 변환**

<a id="f0a1a6f84ca4e1b8"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | TIMESTAMP_TZ |
| VARCHAR | TIMESTAMP_TZ |
| LONG VARCHAR | TIMESTAMP_TZ |
| DATE | TIMESTAMP_TZ |
| TIMESTAMP | TIMESTAMP_TZ |
| TIMESTAMP_TZ | TIMESTAMP_TZ (변환 없음) |

**`YM` 에서의 비교를 위한 타입 변환**

<a id="0918017f5c39ea9e"></a>
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

<a id="462d83bcdc712e6c"></a>
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

<a id="13d531b8420e71c1"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | BOOLEAN |
| VARCHAR | BOOLEAN |
| LONG VARCHAR | BOOLEAN |
| BOOLEAN | BOOLEAN (변환 없음) |

**`RI` 에서의 비교를 위한 타입 변환**

<a id="964fe3714a6a14e8"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | ROWID |
| VARCHAR | ROWID |
| LONG VARCHAR | ROWID |
| ROWID | ROWID (변환 없음) |

<a id="07646aa9949781c3"></a>
### 타입간 변환

타입간 변환은 내부 변환 (implicit type conversion)과 외부 변환 (explicit type conversion)으로 구분된다.

- 내부 변환 (implicit type conversion)은 select, insert, delete, update를 위한 expression, operator, function, condition 들에서 발생한다.
- 외부 변환 (explicit type conversion)은 CAST operator를 통해 이루어진다.

[타입간 변환](#41afdd00fc7000a0)에서는 한 data type에서 다른 data type으로의 변환 가능 여부를 설명한다.

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

<a id="41afdd00fc7000a0"></a>
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
    - 원본 타입이 숫자형 타입, 날짜/ 시간 타입, INTERVAL 타입, BOOLEAN 타입, ROWID 타입인 경우
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
        - 자세한 내용은 [Interval Literals](#114c959a7fc72d5d)를 참조한다.
        - 변환 타입에 정의된 precision에 의해 overflow가 발생할 수 있다.
    - 원본 타입이 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, NUMBER, NUMERIC, FLOAT 타입인 경우
        - 변환 타입이 single field (YEAR, MONTH)이어야 한다.
        - 변환 타입에 정의된 precision에 의해 overflow가 발생할 수 있다.
    - 원본 타입이 INTERVAL YEAR TO MONTH 계열 타입인 경우
        - 변환 타입에 정의된 precision에 의해 overflow가 발생할 수 있다.

- INTERVAL DAY TO SECOND 계열 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - day-time interval literal 형식에 맞지 않는 문자열이 오는 경우 에러가 발생한다.
        - 자세한 내용은 [Interval Literals](#114c959a7fc72d5d)를 참조한다.
        - 변환 타입에 정의된 precision에 의해 overflow가 발생하거나 반올림될 수 있다.
    - 원본 타입이 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, NUMBER, NUMERIC, FLOAT 타입인 경우
        - 변환 타입이 single field (DAY, HOUR, MINUTE, SECOND)이어야 한다.
        - 변환 타입에 정의된 precision에 의해 overflow가 발생하거나 반올림될 수 있다.
    - 원본 타입이 INTERVAL DAY TO SECOND 계열 타입인 경우
        - 변환 타입에 정의된 precision에 의해 overflow가 발생하거나 반올림될 수 있다.

- BOOLEAN 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - 대소문자 구분없이 문자열이 "TRUE" 또는 "FALSE"인 경우에 변환할 수 있다. (앞뒤에 공백이 있는 경우에도 변환 가능)
    - 원본 타입이 BOOLEAN 타입인 경우
        - 에러가 발생하지 않는다.

- ROWID 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - ROWID format 형식에 맞지 않는 문자열이 오는 경우 에러가 발생한다.
    - 원본 타입이 ROWID 타입인 경우
        - 에러가 발생하지 않는다.

<a id="f6fdfb2d45144ef8"></a>
### 타입간 조합

<a id="593e2935fff4231f"></a>
#### 타입간 조합이 필요한 경우

CASE 연산자, 집합 연산자 ([set operator](18-sql-references.md#72ceb9751f3faad0))는 다수의 expression을 연산 결과로 가진다.  
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
    - 집합 연산자 ([set operator](18-sql-references.md#72ceb9751f3faad0))
    - CASE 연산자 
        - [CASE Expression](#bb49538a9d9c8016)
        - [COALESCE](17-built-in-function-references.md#aeb25577697c2128)
        - [NULLIF](17-built-in-function-references.md#1a0eb6819456e426)

<a id="933953bbf127dad3"></a>
#### 결과 타입 조합 규칙

각 expression의 data type은 조합 가능한 동일한 계열의 타입이어야 한다.

- 결과 타입 조합 규칙이 적용되는 예
    - 집합 연산자 ([set operator](18-sql-references.md#72ceb9751f3faad0))
    - CASE 연산자 
        - [CASE Expression](#bb49538a9d9c8016)
        - [COALESCE](17-built-in-function-references.md#aeb25577697c2128)
        - [NULLIF](17-built-in-function-references.md#1a0eb6819456e426)

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

<a id="0e0a1cbf5844e5fe"></a>
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
    - YEAR와 MONTH가 혼재되어 있을 경우, INTERVAL YEAR TO MONTH
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
    - TIME/ TIMESTAMP 형
        - 대상 expression 중 최대 fractional seconds precision
    - INTERVAL YEAR TO MONTH
        - 대상 expression 중 최대 leading precision
    - INTERVAL DAY TO SECOND
        - Leading precision: start field의 maximum leading precision
        - Fractional seconds precision은 maximum fractional seconds precision
- 자세한 내용은 [타입간 비교](#9824da3e073b48e9)를 참조한다.

<a id="de0010542fe8a37a"></a>
### 호환성

Data type에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="5a3696720446c64b"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| B033 | Untyped SQL-invoked function arguments | X |
| E011-01 | INTEGER and SMALLINT data types | O |
| E011-02 | REAL, DOUBLE PRECISON, and FLOAT data types | O |
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

<a id="39f8adcb6d9e9327"></a>
## Format 문자열

Format 문자열은 숫자 타입이나 날짜/ 시간 타입을 문자열로 변환하거나 문자열을 숫자 타입이나 날짜/ 시간 타입으로 변환하기 위한 형식을 정의한 문자열이다.

- 숫자 타입이나 날짜/시간 타입을 문자열로 변환할 때 다음과 같은 형식으로 문자열을 표현한다.
    - [TO_CHAR( number )](17-built-in-function-references.md#3b3cd1288d7889b5), [TO_CHAR( datetime )](17-built-in-function-references.md#6a95099dcd5efb32)
    - 숫자 타입: TO_CHAR( 1234.56, 'S9,999.99' ) → '+1,234.56'
    - 날짜/ 시간 타입: TO_CHAR( SYSDATE, 'YYYY-MM-DD' ) → '2012-07-15'
- 문자열을 숫자 타입이나 날짜/ 시간 타입으로 변환할 때 다음과 같은 형식으로 문자열을 표현한다.
**[ TO_NATIVE_SMALLINT](17-built-in-function-references.md#b14c8133f703798a), [TO_NATIVE_INTEGER](17-built-in-function-references.md#c2469a52fabc4b1e), [TO_NATIVE_BIGINT](17-built-in-function-references.md#b11ead8c69613a1b)
    - [TO_NUMBER](17-built-in-function-references.md#067b6a80dbba0c22), [TO_NATIVE_REAL](17-built-in-function-references.md#876e14c5cbf8499f), [TO_NATIVE_DOUBLE](17-built-in-function-references.md#f52bafc2e71c1d8c)
    - [TO_DATE](17-built-in-function-references.md#df568ff4577a76a5)
    - [TO_TIMESTAMP](17-built-in-function-references.md#9b24efe199e4c67b), [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#f50291e3f07ed587)
    - [TO_TIME](17-built-in-function-references.md#acb02dbbdf32b2dd), [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#2bc444fb42cdd6a2)
    - 숫자 타입: TO_NUMBER( '+1,234.56', 'S9,999.99' ) → NUMBER TYPE
    - 날짜/ 시간 타입: TO_DATE( '2012-07-15', 'YYYY-MM-DD' ) → DATE TYPE

Format 문자열은 다음과 같은 타입으로 구분된다.  
• 숫자 타입: [Number Format 문자열](#1600ba7580e6ec90)  
• 날짜/ 시간 타입: [Datetime Format 문자열](#33b8ffdce1d3bfd9)

<a id="1600ba7580e6ec90"></a>
### Number Format 문자열

Number format 문자열은 숫자 타입을 문자열로 변환하거나 문자열을 숫자 타입으로 변환하기 위한 형식을 정의한 문자열이다.

Number format 문자열은 [TO_CHAR( number )](17-built-in-function-references.md#3b3cd1288d7889b5), [TO_NATIVE_SMALLINT](17-built-in-function-references.md#b14c8133f703798a), [TO_NATIVE_INTEGER](17-built-in-function-references.md#c2469a52fabc4b1e), [TO_NATIVE_BIGINT](17-built-in-function-references.md#b11ead8c69613a1b), [TO_NUMBER](17-built-in-function-references.md#067b6a80dbba0c22), [TO_NATIVE_REAL](17-built-in-function-references.md#876e14c5cbf8499f), [TO_NATIVE_DOUBLE](17-built-in-function-references.md#f52bafc2e71c1d8c) 함수의 인자로 사용된다.

Number format 문자열에는 표현하고자 하는 형식에 따라 여러 개의 format element를 지정할 수 있다.

모든 number format element는 그 형식에 맞게 반올림하여 적용한다.  
변환하고자 하는 value의 소수점 이전 digit 개수가 format 문자열에 지정된 숫자의 자리수보다 큰 경우, '#' 문자로 대체된다.  
MI, S, PR의 부호를 표현하는 format element를 지정하지 않은 경우, 음수는 숫자 앞에 '-' 부호를 양수는 공백을 반환하는 방식으로 부호를 표현한다.

**Number format elements**

<a id="a59d8b7541a019e1"></a>
| Format  element | 예제 | 설명 |
| --- | --- | --- |
| , (comma) | 9,999 | 지정한 위치에 comma를 반환한다.  Comma를 여러 개 지정할 수 있다.  Format 문자열은 comma로 시작할 수 없고 소수점 (.) 이후에도 올 수 없다. |
| . (period) | 99.99 | 지정한 위치에 소수점 (.)을 반환한다. Format 문자열 내에서 소수점은 한 번만 지정할 수 있다. |
| $ | $9999 | 숫자 앞에 $ 기호를 반환한다. |
| 0 | 0999  9990 | 숫자 앞이나 끝에 0을 반환한다. 변환하고자 하는 value의 digit 개수가 format 문자열의 0 위치까지의 digit 개수보다 작은 경우, 차이나는 부분을 0으로 채워 반환한다. |
| 9 | 9999 | 부호와 명시된 9의 개수에 맞게 공백과 숫자를 반환한다. 변환하고자 하는 value의 digit 개수가 명시된 9의 개수보다 작은 경우, 차이나는 부분을 공백으로 채워 반환한다. 음수인 경우 숫자 앞에 '-' 부호를 양수는 공백을 반환하는 방식으로 부호를 표현한다. Format 문자열 소수점 이전의 정수부로 표현되는 값이 0인 경우, 이 0은 공백으로 반환된다. 예: TO_CHAR( 0.123, '9.999' ) → .123 예: TO_CHAR( 0, '9' ) → 0 |
| B | B9999 | 값이 0 이 되는 경우, 공백을 반환한다. |
| EEEE | 9.9EEEE | 지수 표기법으로 반환한다. Format 문자열의 맨 마지막에 오거나, S, MI, PR 앞에 올 수 있다. Comma (,)와 함께 지정할 수 없다. |
| MI | 9999MI | 음수인 경우 숫자 끝에 '-' 를 양수인 경우 공백을 반환한다. Format 문자열의 마지막에만 지정할 수 있고, S, PR과 함께 지정할 수 없다. |
| PR | 9999PR | 음수인 경우 꺽쇠 괄호 안에 숫자를 반환한다. &lt;숫자&gt; 양수인 경우 숫자 앞뒤에 공백이 반환된다. Format 문자열의 마지막에만 지정할 수 있고, S, MI와 함께 지정할 수 없다. |
| RN  rn | RN rn | 로마 숫자를 대문자로 반환한다. 로마 숫자를 소문자로 반환한다. 1 ~ 3999 사이의 숫자에서만 반환된다. FM format element 이외의 다른 format element와는 함께 지정할 수 없다. TO_NUMBER 함수에는 사용할 수 없다. |
| S | S9999 9999S | 양수인 경우 숫자 앞에 '+' 부호를 음수인 경우 '-' 부호를 반환한다. (S9999) 양수인 경우 숫자 끝에 '+' 부호를 음수인 경우 '-' 부호를 반환한다. (9999S) Format 문자열의 맨 처음 또는 맨 마지막에만 지정할 수 있다. MI, PR과 함께 지정할 수 없다. |
| V | 999V99 | V format element 뒤에 오는 9의 digit 개수가 n일 때, value에 10<sup>n</sup> 을 곱한 값을 반환한다.  소수점(.)과 함께 지정할 수 없다. TO_NUMBER 함수에는 사용할 수 없다. |
| X | XXXX xxxx | 지정된 X digit 수에 맞게 공백과 16 진수를 반환한다. 정수값을 16 진수로 반환한다. (정수가 아닌 경우 반올림하여 정수값을 만든다.) XXXX는 16 진수 대문자를 xxxx는 16 진수 소문자를 반환한다. 변환된 16 진수 digit 개수가 명시된 X의 개수보다 작은 경우, 차이나는 부분을 공백으로 채워 반환한다. 0과 양의 정수만 처리하고, 음수인 경우 '#'문자로 대체된다. Format element 0 및 FM과만 함께 지정할 수 있으며, 다른 format element와는 함께 지정할 수 없다. |
| FM | FM | 앞 뒤 공백을 제거하여 왼쪽 정렬되는 효과를 반환한다. 숫자 앞 뒤에 붙는 공백을 제거한다. 9 format element에 의해 소수점 이하에 추가된 0을 제거한다. |

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

<a id="33b8ffdce1d3bfd9"></a>
### Datetime Format 문자열

Datetime format 문자열은 날짜/ 시간 타입을 문자열로 변환하거나 문자열을 날짜/ 시간 타입으로 변환하기 위한 형식을 정의한 문자열이다.

Datetime format 문자열은 [TO_CHAR( datetime )](17-built-in-function-references.md#6a95099dcd5efb32), [TO_DATE](17-built-in-function-references.md#df568ff4577a76a5), [TO_TIMESTAMP](17-built-in-function-references.md#9b24efe199e4c67b), [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#f50291e3f07ed587), [TO_TIME](17-built-in-function-references.md#acb02dbbdf32b2dd), [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#2bc444fb42cdd6a2) 함수의 인자로 사용된다.

날짜/ 시간 타입의 경우, format 문자열을 지정하지 않으면 default 값으로 처리되는데, 각 타입의 default 값은 session property인 NLS_*_FORMAT에 지정된 값이다.

- DATE: [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#ec78df636da07fb6)
- TIMESTAMP: [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#15c05b1b42192d13)
- TIMESTAMP WITH TIME ZONE: [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#7dad2bb0bce4c28d)
- TIME: [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#1793ce4c56053b95)
- TIME WITH TIME ZONE: [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#0a90eef2149e893a)

NLS_*_FORMAT 값들은 [ALTER SESSION SET property_name](18-sql-references.md#4b18743f121b279d) 구문으로 변경할 수 있다.

Datetime format 문자열에는 표현하고자 하는 형식에 따라 여러 개의 format element를 지정할 수 있다.

**Datetime format elements**

<a id="6fba6ec594d851a6"></a>
<table><thead><tr><th align="center" valign="middle">Format<br>element</th><th align="center" valign="middle">TO_*<br>datetime<br>사용여부</th><th align="center" valign="middle">설명</th></tr></thead><tbody><tr><td valign="middle">-<br>/<br>,<br>.<br>;<br>:<br>"text"<br>특수문자</td><td valign="middle">Y</td><td valign="middle">지정된 위치에 format element의 문자를 반환한다.</td></tr><tr><td valign="middle">AD<br>A.D.</td><td valign="middle">Y</td><td valign="middle">서기</td></tr><tr><td valign="middle">AM<br>A.M.</td><td valign="middle">Y</td><td valign="middle">오전</td></tr><tr><td valign="middle">BC<br>B.C.</td><td valign="middle">Y</td><td valign="middle">기원전</td></tr><tr><td valign="middle">CC</td><td valign="middle">N</td><td valign="middle">세기<br>네 자리 연도 중 마지막 두 자리가 01 ~ 99 이면 처음 두 자리에 1을 더한 값을 반환한다. (예: 2005년도일 경우 21)<br>네 자리 연도 중 마지막 두 자리가 00 이면 처음 두 자리 값이 반환된다. (예: 2000년도일 경우 20)</td></tr><tr><td valign="middle">D</td><td valign="middle">Y</td><td valign="middle">일주일 중 몇 번째 날인지를 반환한다. (1 ~ 7)<br>일요일 (1) ~ 토요일 (7)</td></tr><tr><td valign="middle">DAY<br>Day<br>day</td><td valign="middle">Y</td><td valign="middle">요일을 반환한다. ( 예: SUNDAY )<br><ul><li>DAY: 모두 대문자로 반환한다.</li><li>Day: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>day: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">DD</td><td valign="middle">Y</td><td valign="middle">달의 몇 번째 날인지를 반환한다. (1 ~ 31)</td></tr><tr><td valign="middle">DDD</td><td valign="middle">Y</td><td valign="middle">연도의 몇 번째 날인지를 반환한다. (1 ~ 366)</td></tr><tr><td valign="middle">DY<br>Dy<br>dy</td><td valign="middle">Y</td><td valign="middle">요일의 약어를 반환한다. (예: SUN)<br><ul><li>DY: 모두 대문자로 반환한다.</li><li>Dy: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>dy: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">FF[1..6]</td><td valign="middle">Y</td><td valign="middle">Fractional seconds를 FF 이후에 지정한 숫자 (1 ~ 6)의 개수만큼 반환한다.<br>숫자를 지정하지 않은 경우, 기본값은 6이다. (FF는 FF6과 같다.)<br>Fractional seconds의 digit 개수가 FF 이후에 지정한 숫자보다 많으면 버림처리된다.<br>Fractional seconds의 digit 개수가 FF 이후에 지정한 숫자보다 적으면 지정된 숫자에 맞추어 0이 추가된다.<br>DATE 타입에서는 사용할 수 없다.</td></tr><tr><td valign="middle">HH<br>HH12</td><td valign="middle">Y</td><td valign="middle">시간 (1 ~ 12)</td></tr><tr><td valign="middle">HH24</td><td valign="middle">Y</td><td valign="middle">시간 (0 ~ 23)</td></tr><tr><td valign="middle">IW</td><td align="left" valign="middle">N</td><td valign="middle">ISO 8601 표준에 정의된 calendar week (1 ~ 52주 또는 1 ~ 53주)로 지정된 연도의 첫 번째 목요일이 있는 주가 첫 번째 주가 된다.<br><ul><li>Calendar week는 monday부터 시작한다.</li><li>First calendar week는 1월 4일을 포함한다.</li><li>First calendar week는 12월 29, 30, 31을 포함할 수 있다.</li><li>Last calendar week는 1월 1, 2, 3을 포함할 수 있다.</li></ul></td></tr><tr><td valign="middle">IYYY</td><td align="left" valign="middle">N</td><td valign="middle">ISO 8601 표준에 정의된 calendar week를 수용하는 4자리 연도이다.</td></tr><tr><td valign="middle">IYY<br>IY<br>I</td><td align="left" valign="middle">N</td><td valign="middle">ISO 8601 표준에 정의된 calendar week를 수용하는 3자리 연도이다.<br>ISO 8601 표준에 정의된 calendar week를 수용하는 2자리 연도이다.<br>ISO 8601 표준에 정의된 calendar week를 수용하는 1자리 연도이다.</td></tr><tr><td valign="middle">J</td><td valign="middle">Y</td><td valign="middle">BC 4714-11-24 일부터 경과된 날짜를 반환한다.</td></tr><tr><td valign="middle">MI</td><td valign="middle">Y</td><td valign="middle">분 (0 ~ 59)</td></tr><tr><td valign="middle">MM</td><td valign="middle">Y</td><td valign="middle">월 (01 ~ 12), 1월 (01) ~ 12월 (12)</td></tr><tr><td valign="middle">MON<br>Mon<br>mon</td><td valign="middle">Y</td><td valign="middle">월의 약어 (예: JAN ) 이다.<br><ul><li>MON: 모두 대문자로 반환한다.</li><li>Mon: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>mon: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">MONTH<br>Month<br>month</td><td valign="middle">Y</td><td valign="middle">월의 이름 (예: JANUARY) 이다.<br><ul><li>MONTH: 모두 대문자로 반환한다.</li><li>Month: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>month: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">PM<br>P.M.</td><td valign="middle">Y</td><td valign="middle">오후</td></tr><tr><td valign="middle">Q</td><td valign="middle">N</td><td valign="middle">연도의 분기 (1 ~ 4) 이다.<br>1월에서 3월 (1) ~ 10월에서 12월 (4) 이다.</td></tr><tr><td valign="middle">RM<br>Rm<br>rm</td><td valign="middle">Y</td><td valign="middle">월을 로마숫자로 반환한다. (예: I)<br><ul><li>RM: 모두 대문자로 반환한다.</li><li>Rm: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>rm: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">RR</td><td valign="middle">Y</td><td valign="middle">조정된 두 자리 연도이다.<br>RR로 표현된 두 자리 연도를 네 자리 연도로 표현하는 방법은 다음과 같다.<br><ul><li>RR로 표현된 두 자리 연도가 00 ~ 49인 경우<br><ul><li>현재 연도의 마지막 두 자리가 00 ~ 50 이면,<br><ul><li>현재 연도의 처음 두 자리와 RR로 표현된 두 자리 연도</li></ul></li><li>현재 연도의 마지막 두 자리가 51 ~ 99 이면,<br><ul><li>(현재 연도의 처음 두 자리 + 1)와 RR로 표현된 두 자리 연도</li></ul></li></ul></li><li>RR로 표현된 두 자리 연도가 50 ~ 99 인 경우<br><ul><li>현재 연도의 마지막 두 자리가 00 ~ 50 이면,<br><ul><li>(현재 연도의 처음 두 자리 - 1 )와 RR로 표현된 두 자리 연도</li></ul></li><li>현재 연도의 마지막 두 자리가 51 ~ 99 이면,<br><ul><li>현재 연도의 처음 두 자리와 RR로 표현된 두 자리 연도</li></ul></li></ul></li></ul></td></tr><tr><td valign="middle">RRRR</td><td valign="middle">Y</td><td valign="middle">조정된 네 자리 연도이다.<br>네 자리 또는 두 자리로 입력받을 수 있다.<br>두 자리로 입력받을 경우, RR과 동일하게 처리된다.</td></tr><tr><td valign="middle">SS</td><td valign="middle">Y</td><td valign="middle">초 (0 ~ 59)</td></tr><tr><td valign="middle">SSSSS</td><td valign="middle">Y</td><td valign="middle">지난 자정을 기준으로 경과된 초 (0 ~ 86399) 이다.</td></tr><tr><td valign="middle">TZH</td><td valign="middle">Y</td><td valign="middle">Time zone hour 이다.<br>DATE, TIMESTAMP, TIME 타입에서는 사용할 수 없고, TIMESTAMP WITH TIME ZONE, TIME WITH TIME ZONE 타입에서만 사용할 수 있다.</td></tr><tr><td valign="middle">TZM</td><td valign="middle">Y</td><td valign="middle">Time zone minute 이다.<br>DATE, TIMESTAMP, TIME 타입에서는 사용할 수 없고, TIMESTAMP WITH TIME ZONE, TIME WITH TIME ZONE 타입에서만 사용할 수 있다.</td></tr><tr><td valign="middle">WW</td><td valign="middle">N</td><td valign="middle">연도의 몇 번째 주 (1 ~ 53) 인지를 반환한다.<br>첫 번째 주 1은 1월 1일부터 7일까지이다.</td></tr><tr><td valign="middle">W</td><td valign="middle">N</td><td valign="middle">월의 몇 번째 주 (1 ~ 5)인지 반환한다.<br>첫 번째 주 1은 월의 1일부터 7일까지이다.</td></tr><tr><td valign="middle">Y,YYY</td><td valign="middle">Y</td><td valign="middle">Comma가 포함된 Y,YYY 형식의 연도를 반환한다.</td></tr><tr><td valign="middle">YYYY<br>SYYYY</td><td valign="middle">Y</td><td valign="middle">네자리 연도이다.<br>SYYYY는 BC 연도인 경우 '-' 부호를 반환한다.</td></tr><tr><td valign="middle">YYY<br>YY<br>Y</td><td valign="middle">Y</td><td valign="middle"><ul><li>YYY: 현재 연도의 마지막 3자리 연도이다.</li><li>YY: 현재 연도의 마지막 2자리 연도이다.</li><li>Y: 현재 연도의 마지막 1자리 연도이다.</li></ul></td></tr></tbody></table>

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

<a id="7762cb83a82d78cc"></a>
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
• [Null Value](#791a504e407d6262)  
• [Literals](#7922fb336863cf09)  
• [Pseudo Columns](#c9e59cbfd1413ab8)  
• [Operators](#e427f345f41dfd32)  
• [Functions](#104d7da3e0db0f3a)

<a id="41853988a18eb2ee"></a>
### Boolean Value Expression

<a id="99ae1fbedc746cce"></a>
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

<a id="c548be6c1145e64a"></a>
#### 설명

&lt;boolean value expression&gt;은 boolean value를 기술한다. Boolean value를 갖는 &lt;boolean primary&gt;는 &lt;column&gt;과 &lt;condition&gt;, &lt;boolean predicand&gt;가 있다. &lt;column&gt;의 경우 BOOLEAN type으로 선언되어야 하고 CAST를 이용하여 boolean value를 반환할 수도 있다.

&lt;boolean value expression&gt;은 AND나 OR, NOT 등과 같은 논리 연산자와 함께 사용할 수 있으며 boolean value만의 연산자인 IS, IS NOT을 지원한다.

&lt;boolean test&gt;에 기술된 IS, IS NOT 연산자는 &lt;boolean primary&gt;에 기술된 boolean value가 &lt;truth value&gt;인 TRUE, FALSE, UNKNOWN 중 하나와 일치하는지 여부를 판단한다.

자세한 내용은 [Conditions](#7eb55c6cc8416c9a)를 참조한다.

<a id="291d86abf887137a"></a>
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

<a id="bb49538a9d9c8016"></a>
### CASE Expression

<a id="dff2e910dd9697b7"></a>
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

<a id="4b81c65076450d71"></a>
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

THEN 또는 ELSE 절의 result에 여러 type이 오는 경우, [결과 타입 조합 규칙](#933953bbf127dad3)에 따라 result type을 결정한다.

자세한 내용은 다음을 참조한다.  
• [COALESCE](17-built-in-function-references.md#aeb25577697c2128)  
• [NULLIF](17-built-in-function-references.md#1a0eb6819456e426)

<a id="8d068cf57feaf8da"></a>
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

<a id="9ef17e393dd756a4"></a>
### CAST specification

<a id="61304e08a7f04059"></a>
#### 구문

```
CAST( expression AS data_type )
```

<a id="1fd1ffdd3bc1f55c"></a>
#### 설명

CAST는 expression의 데이터 타입을 지정된 data_type의 데이터 타입으로 변환한다.

<a id="fbe994798bee99d8"></a>
#### 사용 예

```
gSQL> SELECT CAST( '1-2' AS INTERVAL YEAR TO MONTH ) AS RESULT FROM DUAL;  
RESULT
------
+01-02
1 row selected.
```

<a id="29b8e6e51e78727e"></a>
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

<a id="38e545616722dc46"></a>
### 호환성

Expression에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="3df51e073f993334"></a>
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

<a id="c9e59cbfd1413ab8"></a>
## Pseudo Columns

Pseudo column은 function과 유사하지만, pseudo column을 수행할 때 row 단위로 매번 다른 값을 반환할 수 있다는 점에서 table의 column과도 유사하다.

**지원되는 pseudo column**

<a id="b80c30d52a976471"></a>
<table><tbody><tr><th align="center">이름</th><th align="center">설명</th><th align="center">참고</th></tr><tr><td align="left" valign="middle">CURRVAL</td><td align="left" valign="middle">Sequence와 관련있는 pseudo column이다.</td><td align="left" valign="middle"><a href="17-built-in-function-references.md#6b00b628498e23d6">CURRVAL</a></td></tr><tr><td align="left" valign="middle">NEXTVAL</td><td align="left" valign="middle">Sequence와 관련있는 pseudo column이다.</td><td align="left" valign="middle"><a href="17-built-in-function-references.md#c73afcf37cccda71">NEXTVAL</a></td></tr><tr><td align="left" valign="middle">ROWNUM</td><td align="left" valign="middle">조건을 만족하는 row의 번호이다.</td><td align="left" valign="middle"><a href="17-built-in-function-references.md#de83f2cf7fcb4fc7">ROWNUM</a></td></tr><tr><td align="left" valign="middle">ROWID</td><td align="left" valign="middle">데이터베이스 내의 레코드 식별자를 반환한다.</td><td align="left" valign="middle"><a href="#1f9e90b49995d73c">ROWID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_GROUP_ID</td><td align="left" valign="middle">레코드가 저장된 group의 식별자를 반환한다.</td><td align="left" valign="middle"><a href="#b15e27b9eeacf741">CLUSTER_GROUP_ID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_MEMBER_ID</td><td align="left" valign="middle">레코드가 저장된 member의 식별자를 반환한다.</td><td align="left" valign="middle"><a href="#b036ce578757de93">CLUSTER_MEMBER_ID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_GROUP_NAME</td><td align="left" valign="middle">레코드가 저장된 group의 이름을 반환한다.</td><td align="left" valign="middle"><a href="#094c56adf05c9575">CLUSTER_GROUP_NAME Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_MEMBER_NAME</td><td align="left" valign="middle">레코드가 저장된 member의 이름을 반환한다.</td><td align="left" valign="middle"><a href="#c56e6e33fe294e19">CLUSTER_MEMBER_NAME Pseudo Column</a></td></tr><tr><td valign="middle">CLUSTER_SHARD_ID</td><td valign="middle">레코드가 저장된 shard의 식별자를 반환한다.</td><td valign="middle"><a href="#4258be38b894e285">CLUSTER_SHARD_ID Pseudo Column</a></td></tr></tbody></table>

<a id="1f9e90b49995d73c"></a>
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

ROWID pseudo column은 SELECT만 가능하고, INSERT, UPDATE, DELETE는 할 수 없다.

자세한 내용은 [ROWID](16-built-in-data-type-references.md#4b6cf4f36148607d), [ROWID-related Functions](#91f9a8652bdd7728)를 참조한다.

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

<a id="b15e27b9eeacf741"></a>
### CLUSTER_GROUP_ID Pseudo Column

CLUSTER_GROUP_ID pseudo column은 레코드 저장된 server의 group 식별자를 반환한다.

CLUSTER_GROUP_ID pseudo column은 SELECT만 가능하고, INSERT, UPDATE, DELETE는 할 수 없다.

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

<a id="b036ce578757de93"></a>
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

<a id="094c56adf05c9575"></a>
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

<a id="c56e6e33fe294e19"></a>
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

<a id="4258be38b894e285"></a>
### CLUSTER_SHARD_ID Pseudo Column

CLUSTER_SHARD_ID pseudo column은 레코드가 저장된 shard 식별자를 반환한다.

CLUSTER_SHARD_ID pseudo column은 SELECT만 할 수 있고 INSERT, UPDATE, DELETE는 할 수 없다.

> Cluster system에서 유효한 정보이다.

다음은 CLUSTER_SHARD_ID pseudo column을 검색하는 예이다.

```
gSQL> SELECT T1.C1, T1.CLUSTER_SHARD_ID FROM T1;

C1 CLUSTER_SHARD_ID
-- ----------------
A                14
B                17
C                 4

3 rows selected.
```

<a id="3ac4e53b75afe6a0"></a>
### 호환성

Pseudo column에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="885aac052701105d"></a>
<table><tbody><tr><th align="center">&nbsp;Feature ID</th><th align="center">&nbsp;설명</th><th align="center">&nbsp;지원 여부</th></tr><tr><td align="left">T176</td><td align="left">Sequence generator support</td><td align="center">O</td></tr><tr><td align="left">T177</td><td align="left">&nbsp;Sequence generator support: simple restart option</td><td align="center">O</td></tr></tbody></table>

<a id="e427f345f41dfd32"></a>
## Operators

Operator는 구문상에서 하나 이상의 특정 기호 또는 keyword로 표현되며, 하나 이상의 argument들을 가지고 기능을 수행한다.

Operator에는 다음과 같이 다양한 형태가 있다.  
• Arithmetic operator  
• Concatenation operator  
• Set operator

<a id="2967dc66690f13e5"></a>
### Arithmetic Operator

<a id="1e37fd7bd776bdde"></a>
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

<a id="92bcca189dd81952"></a>
#### 설명

Arithmetic operator는 숫자형, 날짜/ 시간, INTERVAL 타입의 산술 연산을 수행한다.

Arithmetic operator의 우선순위는 다음과 같다.

1. [+ (POSITIVE)](17-built-in-function-references.md#f2a00d7e7ae5b96f), [- (NEGATIVE)](17-built-in-function-references.md#b3e82f0107863a21)
2. [* (MULTIPLICATION)](17-built-in-function-references.md#fad9a0fb63da9e30), [/ (DIVISION)](17-built-in-function-references.md#f812a57fc35a9de4)
3. [+ (ADDITION)](17-built-in-function-references.md#56899a78835fb201), [- (SUBTRACTION)](17-built-in-function-references.md#62a61dfa79308362)

<a id="6f78ccd3fed8e9d0"></a>
### Concatenation Operator

<a id="39e474e2db43a4ac"></a>
#### 구문

```
<concatenation operator> ::=
        <expression> || <expression>
```

<a id="e024c9beddd452e1"></a>
#### 설명

Concatenation operator는 CHARACTER STRING 타입이나 BINARY STRING 타입의 value 사이를 연결한 문자열을 반환한다.  
자세한 내용은 [|| (CONCATENATE)](17-built-in-function-references.md#e72ca95b1d94da0e), [CONCATENATE](17-built-in-function-references.md#b04073e8a9e83240)를 참조한다.

<a id="6cf2d9a90584fe2c"></a>
### Set Operator

<a id="f12e35de62c380f7"></a>
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

<a id="963f6f9d135cf81e"></a>
#### 설명

[set operator](18-sql-references.md#72ceb9751f3faad0)는 부질의 (subquery) 결과들에 대한 집합 (set) 연산을 수행한다.

INTERSECT ALL/ DISTINCT는 다른 set operator 보다 우선한다.

**Set operators**

<a id="0c97ce10cb84b7b5"></a>
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

<a id="5a4b5d1925948f10"></a>
### 호환성

Operator에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="2d7c4476d7f0c58b"></a>
<table><tbody><tr><th align="center">Feature ID</th><th align="center">설명</th><th align="center">지원 여부</th></tr><tr><td align="left" valign="middle">E011-04</td><td align="left" valign="middle">Arithmetic operators</td><td align="center" valign="middle">O</td></tr><tr><td valign="middle">E021-07</td><td valign="middle">Character concatenation</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-01</td><td align="left" valign="middle">UNION DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-02</td><td align="left" valign="middle">UNION ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-03</td><td align="left" valign="middle">EXCEPT DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-05</td><td align="left" valign="middle">Columns combined via table operators need not have exactly the same data type</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-06</td><td align="left" valign="middle">Table operators in subqueries</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F041-08</td><td align="left" valign="middle">All comparison operators are supported (rather than just =)</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F302-01</td><td align="left" valign="middle">INTERSECT DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F302-02</td><td align="left" valign="middle">INTERSECT ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F304</td><td align="left" valign="middle">EXCEPT ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F846</td><td align="left" valign="middle">Octet support in regular expression operators</td><td align="center" valign="middle">X</td></tr><tr><td align="left" valign="middle">J571</td><td align="left" valign="middle">NEW operator</td><td align="center" valign="middle">X</td></tr></tbody></table>

<a id="104d7da3e0db0f3a"></a>
## Functions

Operator와 기능상으로는 유사하지만, function은 이름 뒤에 괄호를 사용하여 argument들을 명시한다.   
Function은 0개 이상의 argument를 포함할 수 있다.

Function 형태는 다음과 같이 구분된다.  
• Single row function  
• Aggregate function

<a id="84c081a5b06e98d7"></a>
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

<a id="306d166a089533ae"></a>
#### Numeric Functions

Numeric function은 숫자형 값을 입력받아 숫자형 결과를 반환하는 function이다.

Numeric function의 종류는 다음과 같다.

- [ABS](17-built-in-function-references.md#2b6afdb6d28566b4)
- [ACOS](17-built-in-function-references.md#ecdb650a6b8661c2)
- [ASIN](17-built-in-function-references.md#4833418524efb2a8)
- [ATAN](17-built-in-function-references.md#4662c67032984a00)
- [ATAN2](17-built-in-function-references.md#aa92618acb0d4aa2)
- [BITAND](17-built-in-function-references.md#1154feda9405cb0b)
- [BITNOT](17-built-in-function-references.md#b75d190540619c02)
- [BITOR](17-built-in-function-references.md#0d276f0eef4a5adb)
- [BITXOR](17-built-in-function-references.md#34f572a6fa6e089a)
- [CBRT](17-built-in-function-references.md#d22ca9da93eeaad8)
- [CEIL](17-built-in-function-references.md#b680b186a63b3b2b)
- [COS](17-built-in-function-references.md#7ae5adee2b5ffeb4)
- [COT](17-built-in-function-references.md#52eb3609f8be03a0)
- [DEGREES](17-built-in-function-references.md#2b46e598f27f67a9)
- [EXP](17-built-in-function-references.md#bf969764a55a9f7c)
- [FACTORIAL](17-built-in-function-references.md#6ddcda3a0a6ec66b)
- [FLOOR](17-built-in-function-references.md#84a75960cb409117)
- [LN](17-built-in-function-references.md#9d359a582dbdc25c)
- [LOG](17-built-in-function-references.md#ea9a2c5eb2dd8b5e)
- [MOD](17-built-in-function-references.md#e37be12b25d1865a)
- [PI](17-built-in-function-references.md#f3d7a516fcd28b5c)
- [POWER](17-built-in-function-references.md#d03682bac268946a)
- [RADIANS](17-built-in-function-references.md#a1c5806a676b274b)
- [RANDOM](17-built-in-function-references.md#d8c373526e895389)
- [ROUND( number )](17-built-in-function-references.md#c7c9ba9e02aa45e9)
- [SHARD_ID](17-built-in-function-references.md#f5eca2e78ed397dc)
- [SHIFT_LEFT](17-built-in-function-references.md#02f9dd54b8fa5fc1)
- [SHIFT_RIGHT](17-built-in-function-references.md#b3968c38e9e8929d)
- [SIGN](17-built-in-function-references.md#842ccb40a1076da9)
- [SIN](17-built-in-function-references.md#dc26a246aa47fdb5)
- [SQRT](17-built-in-function-references.md#f43bf802d8823c6d)
- [TAN](17-built-in-function-references.md#40f8d8af2e77cecd)
- [TRUNC( number )](17-built-in-function-references.md#2e0f8d04a2200181)
- [WIDTH_BUCKET](17-built-in-function-references.md#324628402e81b43e)

<a id="e8f5809eba5241e8"></a>
#### Character String Functions Returning Character Values

Character string functions returning character values는 CHARACTER STRING형 값을 입력받아 CHARACTER STRING형 결과를 반환하는 function이다.

Character string functions returning character value의 종류는 다음과 같다.

- [CHR](17-built-in-function-references.md#019b8157cbcb19a0)
- [CONCAT](17-built-in-function-references.md#a9fb83a876b717d9)
- [CONCATENATE](17-built-in-function-references.md#b04073e8a9e83240)
- [INITCAP](17-built-in-function-references.md#d0066b9ecb068fd8)
- [LOWER](17-built-in-function-references.md#9a81a6ccdf6d2b82)
- [LPAD](17-built-in-function-references.md#0cb417d8d3ab34a0)
- [LTRIM](17-built-in-function-references.md#2ceea524cfe974a6)
- [OVERLAY](17-built-in-function-references.md#300e6c6428fb2f72)
- [REPEAT](17-built-in-function-references.md#e735b34d6307a737)
- [REPLACE](17-built-in-function-references.md#4b27ef660974af19)
- [REVERSE](17-built-in-function-references.md#2ed783c153c3ed1a)
- [RPAD](17-built-in-function-references.md#473a6134cf8242c2)
- [RTRIM](17-built-in-function-references.md#e0b41913fdb9726a)
- [SPLIT_PART](17-built-in-function-references.md#99a53f6e194ede23)
- [SUBSTR](17-built-in-function-references.md#088cbfd5cb643df6)
- [SUBSTRB](17-built-in-function-references.md#a8a6ec8a9639b059)
- [TRANSLATE](17-built-in-function-references.md#c3b99612e17ec2ce)
- [TRIM](17-built-in-function-references.md#cb54da70d0db3b75)
- [UPPER](17-built-in-function-references.md#ae6e3aa65d222bc9)

<a id="6fd88ab1246408e1"></a>
#### Character String Functions Returning Number Values

Character string functions returning number value는 CHARACTER STRING형 값을 입력받아 숫자형 결과를 반환하는 function이다.

Character string functions returning number value의 종류는 다음과 같다.

- [ASCII](17-built-in-function-references.md#56c32c5dadd6452f)
- [BIT_LENGTH](17-built-in-function-references.md#de539a00415063b3)
- [BYTE_LENGTH](17-built-in-function-references.md#75d9967da5addf6b)
- [CHAR_LENGTH](17-built-in-function-references.md#6fba33a6d3e98937)
- [INSTR](17-built-in-function-references.md#688630b899f0ad69)
- [LENGTH](17-built-in-function-references.md#45df1dbd6c5b6d9a)
- [LENGTHB](17-built-in-function-references.md#3c531ddc38355109)
- [OCTET_LENGTH](17-built-in-function-references.md#efc6be7a196cd804)
- [POSITION](17-built-in-function-references.md#24f04da084362731)

<a id="3db762de6851c73d"></a>
#### Datetime Functions

Datetime function은 DATE/ TIME/ TIMESTAMP/ INTERVAL 형 값을 입력받아 DATE/ TIME/ TIMESTAMP/ INTERVAL형 결과를 반환하는 function이다.

Datetime function의 종류는 다음과 같다.

- [ADDDATE](17-built-in-function-references.md#441090925f082310)
- [ADDTIME](17-built-in-function-references.md#ea5ffc510f0a29b9)
- [ADD_MONTHS](17-built-in-function-references.md#b4bb9ce42541b64d)
- [DATEADD](17-built-in-function-references.md#61f38c2b4d02b2ce)
- [DATEDIFF](17-built-in-function-references.md#819ababb5d9c70ac)
- [DATE_ADD](17-built-in-function-references.md#95ae0ba30c34a837)
- [DATE_PART](17-built-in-function-references.md#ea420adbc4d8a5b9)
- [EXTRACT](17-built-in-function-references.md#9426b123a329beab)
- [LAST_DAY](17-built-in-function-references.md#3b926ff5e22014e6)
- [MONTHS_BETWEEN](17-built-in-function-references.md#5d80a6a3a0b2bb51)

<a id="9531208e7392de6a"></a>
#### General Comparison Functions

General comparison function은 value 집합에 대한 최소값 또는 최대값을 구하는 function이다.

General comparison function의 종류는 다음과 같다.

- [GREATEST](17-built-in-function-references.md#8dda308b18de124f)
- [LEAST](17-built-in-function-references.md#e7e917c6a12122df)

<a id="404c041b74e88d43"></a>
#### Conversion Functions

Conversion function은 특정 data type으로의 값을 설정하는 function이다.

Conversion function 종류는 다음과 같다.

- [NUMTODSINTERVAL](17-built-in-function-references.md#d37de1ba15fe628b)
- [NUMTOYMINTERVAL](17-built-in-function-references.md#403c620fa29a8d5a)
- [TO_CHAR( datetime )](17-built-in-function-references.md#6a95099dcd5efb32)
- [TO_CHAR( number )](17-built-in-function-references.md#3b3cd1288d7889b5)
- [TO_DATE](17-built-in-function-references.md#df568ff4577a76a5)
- [TO_NATIVE_BIGINT](17-built-in-function-references.md#b11ead8c69613a1b)
- [TO_NATIVE_DOUBLE](17-built-in-function-references.md#f52bafc2e71c1d8c)
- [TO_NATIVE_INTEGER](17-built-in-function-references.md#c2469a52fabc4b1e)
- [TO_NATIVE_REAL](17-built-in-function-references.md#876e14c5cbf8499f)
- [TO_NATIVE_SMALLINT](17-built-in-function-references.md#b14c8133f703798a)
- [TO_NUMBER](17-built-in-function-references.md#067b6a80dbba0c22)
- [TO_TIME](17-built-in-function-references.md#acb02dbbdf32b2dd)
- [TO_TIME_TZ](17-built-in-function-references.md#2c8cee3ecac352ee)
- [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#2bc444fb42cdd6a2)
- [TO_TIMESTAMP](17-built-in-function-references.md#9b24efe199e4c67b)
- [TO_TIMESTAMP_TZ](17-built-in-function-references.md#ed65dccded47eca7)
- [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#f50291e3f07ed587)

<a id="631ca2b4c86e2f32"></a>
#### Conditional Functions

Conditional function은 조건에 따라 특정값을 결과로 반환하는 function이다.

Conditional function의 종류는 다음과 같다.

- [CASE2](17-built-in-function-references.md#4a7aa86c6e3377f7)
- [DECODE](17-built-in-function-references.md#05826b18bdaba90e)

<a id="9016eff8e4dde090"></a>
#### NULL-related Functions

NULL-related function은 입력값이 NULL값인지 여부에 따라 특정값을 결과로 반환하는 function이다.

NULL-related function의 종류는 다음과 같다.

- [COALESCE](17-built-in-function-references.md#aeb25577697c2128)
- [NULLIF](17-built-in-function-references.md#1a0eb6819456e426)
- [NVL](17-built-in-function-references.md#cd58b7ac439d7044)
- [NVL2](17-built-in-function-references.md#4c314d8391c02bca)

<a id="91f9a8652bdd7728"></a>
#### ROWID-related Functions

ROWID-related function은 ROWID에 대한 정보를 얻기 위한 function이다.

ROWID-related function의 종류는 다음과 같다.

- Standalone에서 유효한 function
    - [ROWID_OBJECT_ID](17-built-in-function-references.md#58e3a5bd0def5c9a)
    - [ROWID_TABLESPACE_ID](17-built-in-function-references.md#07d4c357b5fc362a)
    - [ROWID_PAGE_ID](17-built-in-function-references.md#2f604dcd124fb135)
    - [ROWID_ROW_NUMBER](17-built-in-function-references.md#7a77be578809282d)

- Cluster에서 유효한 function
    - [ROWID_GRID_BLOCK_ID](17-built-in-function-references.md#5094b18e0b5310db)
    - [ROWID_GRID_BLOCK_SEQ](17-built-in-function-references.md#88b241dbab2cf2c4)
    - [ROWID_MEMBER_ID](17-built-in-function-references.md#491cf1642b2825bb)
    - [ROWID_SHARD_ID](17-built-in-function-references.md#5449cb99e218c681)

<a id="354df4d2d617e165"></a>
#### Encryption Functions

Encryption function은 주어진 plain text를 특정 알고리즘으로 encrypt/ decrypt 하거나 hash한 결과값을 반환하는 function이다.

Encryption function에 대한 자세한 내용은 [DIGEST](17-built-in-function-references.md#e25c62592a4caee6)를 참조한다.

<a id="c3db8ab0bc8b0a99"></a>
#### System Information Functions

System information function은 session과 system에 대한 정보를 얻기 위한 function이다.

System information function의 종류는 다음과 같다.

- [CLOCK_DATE](17-built-in-function-references.md#0c40087b7a9c2a37)
- [CLOCK_LOCALTIME](17-built-in-function-references.md#8e4a2491e3df3c06)
- [CLOCK_LOCALTIMESTAMP](17-built-in-function-references.md#f8a81f1510396294)
- [CURRENT_CATALOG](17-built-in-function-references.md#ddf459a10d33119b)
- [CURRENT_DATE](17-built-in-function-references.md#ded9d6f2e7bd80f0)
- [CURRENT_SCHEMA](17-built-in-function-references.md#8c9bf7e541e58fb7)
- [CURRENT_TIME](17-built-in-function-references.md#6f0c3028f6461836)
- [CURRENT_TIMESTAMP](17-built-in-function-references.md#d8795b1505198a32)
- [CURRENT_USER](17-built-in-function-references.md#c806d6efc62f415a)
- [LAST_IDENTITY_VALUE](17-built-in-function-references.md#a6e5d3dbfa265092)
- [LOCALTIME](17-built-in-function-references.md#436222f8341b1345)
- [LOCALTIMESTAMP](17-built-in-function-references.md#4996dddc37478f57)
- [LOGON_USER](17-built-in-function-references.md#e49dffe98c9e9356)
- [SESSION_ID](17-built-in-function-references.md#1b7c0b750961d7f7)
- [SESSION_SERIAL](17-built-in-function-references.md#6940db2b4a41c5f0)
- [SESSION_USER](17-built-in-function-references.md#85daf59be974e642)
- [STATEMENT_DATE](17-built-in-function-references.md#e0db7e4b814701b9)
- [STATEMENT_LOCALTIME](17-built-in-function-references.md#1b646c7eaaf08d0a)
- [STATEMENT_LOCALTIMESTAMP](17-built-in-function-references.md#c8242dda8b1d9add)
- [STATEMENT_TIME](17-built-in-function-references.md#c1369b47f50bd366)
- [STATEMENT_TIMESTAMP](17-built-in-function-references.md#4bbe90a1d33f4975)
- [STATEMENT_VIEW_SCN](17-built-in-function-references.md#1e1bf5e3049aa0eb)
- [SYSDATE](17-built-in-function-references.md#7cd347863588d3fb)
- [SYSTIME](17-built-in-function-references.md#a5d70afe0da7d254)
- [SYSTIMESTAMP](17-built-in-function-references.md#3aab6136b131a50a)
- [TRANSACTION_DATE](17-built-in-function-references.md#0bc76aea67fa8413)
- [TRANSACTION_LOCALTIME](17-built-in-function-references.md#4563686bf922c0bd)
- [TRANSACTION_LOCALTIMESTAMP](17-built-in-function-references.md#069b770b657fc5e1)
- [TRANSACTION_TIME](17-built-in-function-references.md#0ff656b3e06e603d)
- [TRANSACTION_TIMESTAMP](17-built-in-function-references.md#dbe1c4ab1d0ac244)
- [USER_ID](17-built-in-function-references.md#ceaad10397d2ba2f)
- [VERSION](17-built-in-function-references.md#38cde8c6fcd22905)

<a id="e6da1dfbb34caaf1"></a>
### Aggregate Function

Aggregate function은 여러 row에 대해 하나의 결과 row를 생성하는 function이다.

Aggregation function의 종류는 다음과 같다.

- [COUNT](17-built-in-function-references.md#39cbfb0dcaff5e1d)
- [COUNT(*)](17-built-in-function-references.md#a13672e170033862)
- [SUM](17-built-in-function-references.md#f9aa343d3860da32)
- [AVG](17-built-in-function-references.md#508fdfccb1d4afc3)
- [MIN](17-built-in-function-references.md#df013296d65d98cb)
- [MAX](17-built-in-function-references.md#7949d0584926f17b)
- [STDDEV](17-built-in-function-references.md#710271af985cd947)
- [STDDEV_POP](17-built-in-function-references.md#9cf33dd4c3767fa7)
- [STDDEV_SAMP](17-built-in-function-references.md#5048db9c0886f2f3)
- [VAR_POP](17-built-in-function-references.md#b236ef352055656d)
- [VAR_SAMP](17-built-in-function-references.md#ceed8a819f8dd64d)
- [VARIANCE](17-built-in-function-references.md#fe7ab65e1a6c5b53)

<a id="bcc8805b943ad9c8"></a>
### 호환성

Function에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="5cf399976c0216ea"></a>
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

<a id="7eb55c6cc8416c9a"></a>
## Conditions

<a id="9340902966685757"></a>
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

<a id="6b00da26440f04de"></a>
| 우선순위 | Condition 종류 |
| --- | --- |
| 1 | 조건절에 쓰여진 연산자들 |
| 2 | =, !=, &lt;, &gt;, &lt;=, &gt;= |
| 3 | IS [NOT] NULL, [NOT] BETWEEN,  [NOT] IN,  LIKE, EXISTS |
| 4 | NOT |
| 5 | AND |
| 6 | OR |

<a id="f03abd4a5593b82a"></a>
### Comparison Conditions

양쪽 조건을 비교하여 TRUE, FALSE, UNKNOWN 값의 boolean 타입을 반환한다.

**Comparison condition**

<a id="8840ab290b4aa9e9"></a>
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

자세한 내용은 [타입간 비교](#9824da3e073b48e9)를 참조한다.

<a id="1757f7208f25b0b0"></a>
#### &lt; Simple Comparison Conditions &gt;

<a id="f0cf5cbc599486e4"></a>
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

자세한 내용은 [Scalar Subquery Expression](#29b8e6e51e78727e)을 참조한다.

<a id="83aae28a303c018a"></a>
##### 설명

comparison_operator 양쪽에 expr_list 또는 subquery가 오는 경우, 비교되는 expr의 개수 또는 subquery target의 개수는 동일해야 한다.  
Subquery가 오는 경우, 결과 레코드는 한 건이어야 한다.

<a id="c1b5d13b135f852f"></a>
##### 사용 예

**Simple comparison condition의 예**

<a id="b331cc370b37d8ba"></a>
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

<a id="37aca0585a44a543"></a>
#### &lt; Group Comparison Conditions &gt;

<a id="57bdcd190af517f4"></a>
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

자세한 내용은 [Scalar Subquery Expression](#29b8e6e51e78727e)을 참조한다.

<a id="841fafff3d0323d3"></a>
##### 설명

comparison_operator 양쪽에 expr_list 또는 subquery가 오는 경우, 비교되는 expr의 개수 또는 subquery target의 개수는 동일해야 한다.  
comparison_operator 왼쪽에 subquery가 오는 경우, 결과 레코드는 한 건이어야 한다.  
comparison_operator 오른쪽에 subquery가 오는 경우, 결과 레코드는 여러 건일 수 있다.

<a id="bcdce9008f4c0349"></a>
##### 사용 예

<a id="9c05137cb062bd40"></a>
<table class="table column_count_2"><caption>Group comparison condition의 예</caption><thead><tr><th class="to_center"><div>Condition</div></th><th class="to_center"><div>결과</div></th></tr></thead><tbody><tr><td class="to_left"><div>1 =any ( 1, 2, 3, 4, 5 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>1 =any ( 1, 2, null, 4, 5 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>1 =any ( 2, null, 4, 5 )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td class="to_left"><div>1 =any ( 100, 2, 3, 4, 5 )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td class="to_left"><div>1 =all ( 1, +1, 1E+0 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>1 =all ( 1, +1, 1E+0, null )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td class="to_left"><div>1 =all ( 1, 2, 3, 4, 5 )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =any ( ( 0, 1 ), ( 1, 2 ), ( 3, 4 ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =any ( ( 0, 1 ), ( 1, 2 ), ( null, null ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =any ( ( 0, 1 ), ( 2, 3 ), ( 3, 4 ) )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =all ( ( 1, 2 ), ( +1, +2 ), ( 1E+0, 2E+0 ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =all ( ( 1, 2 ), ( +1, +2 ), ( null, null ) )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =all ( ( 0, 1 ), ( 2, 3 ), ( 3, 4 ) )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><th class="to_left" colspan="2"><div>comparison_operator 오른쪽 subquery의 결과 레코드가 0인 경우</div></th></tr><tr><td class="to_left"><div>( 'X' ) =any ( select dummy from dual where dummy = 'Y' )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td class="to_left"><div>( 'X' ) =all ( select dummy from dual where dummy = 'Y' )</div></td><td class="to_left"><div>TRUE</div></td></tr></tbody></table>

<a id="55e5dab5bd1d973b"></a>
### Logical Conditions

Logical condition으로는 AND, OR, NOT이 있다.

<a id="ef8111815cc5a39a"></a>
#### AND

<a id="4a6f83208e20ab17"></a>
##### 구문

```
<boolean value expression> AND <boolean value expression>
```

<a id="0e630f6da1d15592"></a>
##### 설명

**AND boolean operator의 truth table**

<a id="b327452886767e19"></a>
| AND | True | False | Unknown |
| --- | --- | --- | --- |
| True | True | False | Unknown |
| False | False | False | False |
| Unknown | Unknown | False | Unknown |

<a id="41ea483f4c31cf4c"></a>
#### OR

<a id="f77b69e7b380e1dc"></a>
##### 구문

```
<boolean value expression> OR <boolean value expression>
```

<a id="944d923999af34c6"></a>
##### 설명

**OR boolean operator의 truth table**

<a id="47b829f3d9fb40d8"></a>
| OR | True | False | Unknown |
| --- | --- | --- | --- |
| True | True | True | True |
| False | True | False | Unknown |
| Unknown | True | Unknown | Unknown |

<a id="c42189207bc8257c"></a>
#### NOT

<a id="6965fc22bccfc797"></a>
##### 구문

```
NOT <boolean value expression>
```

<a id="7af8c5fcc3ffe961"></a>
##### 설명

**NOT boolean operator의 truth table**

<a id="d2558766bf272121"></a>
| expr | NOT |
| --- | --- |
| True | False |
| False | True |
| Unknown | Unknown |

<a id="f19034e61d61b788"></a>
### Null Condition

<a id="a0088f76c02212d5"></a>
#### 구문

```
<expr> IS [NOT] NULL
```

<a id="949e9c0c57090e4b"></a>
#### 설명

expr의 결과가 NULL 값인지 여부를 검사한다.

**Is Null 조건의 결과표**

<a id="a5a212638d622bdb"></a>
| expr | IS NULL | IS NOT NULL |
| --- | --- | --- |
| NULL | True | False |
| NOT NULL | False | True |

<a id="f94948e480aedc63"></a>
### Compound Condition

여러 조건들이 결합되어 만들어진 조건식이다.

```
compound_condition ::=
        ( condition )
      | NOT condition
      | condition < AND | OR > condition
```

<a id="90cd55c77f7f2a6c"></a>
### Pattern-matching Conditions

<a id="3ab5336a00f5ea8a"></a>
#### LIKE Condition

<a id="2eca2f5fae83739f"></a>
##### 구문

```
like_condition ::=
        string [NOT] LIKE pattern [ ESCAPE escape_character ]
```

<a id="68d46ee6352f12a8"></a>
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

<a id="47f294e15ca7e73a"></a>
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

<a id="e494b78f7002fa7c"></a>
### BETWEEN Condition

<a id="72e9247f408dcd91"></a>
#### 구문

```
<between condition> ::=
   <expr1> [ NOT ] BETWEEN [ ASYMMETRIC | SYMMETRIC ] <expr2> AND <expr3>
```

<a id="478e1a73351fb860"></a>
#### 설명

expr1이 expr2와 expr3 범위 내의 조건인지 검사한다.

ASYMMETRIC이나 SYMMETRIC이 생략된 경우, default는 ASYMMETRIC 이다.  
expr1, expr2, expr3의 data type이 다른 경우, conversion이 수행된다.  
자세한 내용은 [타입간 비교](#9824da3e073b48e9), [타입간 변환](#07646aa9949781c3)을 참조한다.

**Between 구문 동치**

<a id="e32f60f9472e108a"></a>
| A | B |
| --- | --- |
| X BETWEEN ASYMMETRIC Y AND Z | X BETWEEN Y AND Z |
| X BETWEEN Y AND Z | X >= Y AND X <= Z |
| X NOT BETWEEN Y AND Z | NOT( X BETWEEN Y AND Z ) |
| X BETWEEN SYMMETRIC Y AND Z | ((X BETWEEN Y AND Z) OR (X BETWEEN Z AND Y) |
| X NOT BETWEEN SYMMETRIC Y AND Z | NOT( X BETWEEN SYMMETRIC Y AND Z ) |

<a id="0b247c911fec4cc6"></a>
#### 사용 예

<a id="648f995b1b65dc35"></a>
<table class="table column_count_3"><caption>Between 구문의 예</caption><thead><tr><th class="to_center" colspan="2"><div>Condition</div></th><th class="to_center"><div>결과</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>BETWEEN [ ASYMMETRIC ]</div></td><td><div>3 BETWEEN 1 AND 5</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr><tr><td><div>NULL BETWEEN 1 AND 5
3 BETWEEN NULL AND 5
3 BETWEEN 1 AND NULL</div></td><td class="to_left to_middle"><div>NULL</div></td></tr><tr><td><div>3 BETWEEN 5 AND 1</div></td><td class="to_left to_middle"><div>FALSE</div></td></tr><tr><td class="to_middle" rowspan="3"><div>BETWEEN SYMMETRIC</div></td><td><div>3 BETWEEN SYMMETRIC 1 AND 5</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr><tr><td><div>NULL BETWEEN SYMMETRIC 1 AND 5
3 BETWEEN SYMMETRIC NULL AND 5
3 BETWEEN SYMMETRIC 1 AND NULL</div></td><td class="to_left to_middle"><div>NULL</div></td></tr><tr><td><div>3 BETWEEN SYMMETRIC 5 AND 1</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr></tbody></table>

<a id="a18f1eddc1a23880"></a>
### IN Condition

<a id="a9d582712c659423"></a>
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

<a id="e1433746b26e951d"></a>
#### 설명

IN condition은 =ANY와 동일한 결과를 반환한다.  
NOT IN condition은 !=ALL과 동일한 결과를 반환한다.

자세한 내용은 [Comparison Conditions](#f03abd4a5593b82a)를 참조한다.

<a id="d5aae757fbfbc9f0"></a>
#### 사용 예

**IN condition의 예**

<a id="52606adcace3b4fb"></a>
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

<a id="9b7fc8db846e9dfc"></a>
### EXISTS Condition

<a id="9296b7f0c24f5842"></a>
#### 구문

```
exists_conditions ::= 
        EXISTS ( subquery )
```

<a id="c0046af7ecc92b13"></a>
#### 설명

Subquery의 결과 레코드 존재 유무를 검사한다.   
Subquery의 결과 레코드가 존재하면 TRUE를 반환하고, 결과 레코드가 존재하지 않으면 FALSE를 반환한다.

<a id="d9820eb7ba36caf0"></a>
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

<a id="a08584485314993c"></a>
### 호환성

Condition에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="4d837ef702363a11"></a>
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

---

[← 10. Server Property](../part-02-administration-manual/10-server-property.md) · [전체 목차](../README.md) · [12. SQL Languages →](12-sql-languages.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
