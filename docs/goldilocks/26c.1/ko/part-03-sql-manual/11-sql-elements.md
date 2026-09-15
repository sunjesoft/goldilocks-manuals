<a id="975c1b77cd4ca4ab"></a>

# 11. SQL Elements

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/975c1b77cd4ca4ab)  
> 태그: `26c.1_0_tag`

[← 10. Server Property](../part-02-administration-manual/10-server-property.md) · [전체 목차](../README.md) · [12. SQL Languages →](12-sql-languages.md)

<a id="cad29e144b15be2b"></a>
## Syntax Elements

<a id="a6538337c848447e"></a>
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

<a id="a98c21f632f44409"></a>
### Literals

Literals는 null이 아닌 값을 기술한 것이다.

<a id="e23e696c5e79d03a"></a>
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

<a id="3cdcddacbae484ec"></a>
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

<a id="368bf7b464f88d0a"></a>
#### Datetime Literals

Datetime literals는 날짜/ 시간 타입에 대한 literals를 작성하는 형식이다. Datetime value는 string literal을 사용하여 지정하거나 TO_* 함수(TO_DATE 등)를 이용해 character 또는 numeric value를 변환하여 지정할 수도 있다.

날짜/시간 타입에는 DATE, TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 이 있다.

<a id="56878eee497b5256"></a>
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

자세한 내용은 [TO_DATE](17-built-in-function-references.md#e1ae1f9cb408151d), [Datetime Format 문자열](#95e37f19cf8bd6a2), [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#09118aefc816172d)을 참조한다.

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

<a id="6a2cd49edd91d392"></a>
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

자세한 내용은 [TO_TIME](17-built-in-function-references.md#91b2febb7ce81d9c), [Datetime Format 문자열](#95e37f19cf8bd6a2), [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#d78680ceba6107a9)을 참조한다.

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

<a id="c6cfdbd6c9172fa1"></a>
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

자세한 내용은 [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#a9f9c02ecbf276e7), [Datetime Format 문자열](#95e37f19cf8bd6a2), [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#d8ed241efdbfc8ee)을 참조한다.

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

<a id="a94a20f552d8aca6"></a>
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

자세한 내용은 [TO_TIMESTAMP](17-built-in-function-references.md#48f2f9c2be120650), [Datetime Format 문자열](#95e37f19cf8bd6a2), [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#b83b0daa42003bc4)을 참조한다.

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

<a id="e2a086cf463c9217"></a>
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

자세한 내용은 [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#667ef9b2a77a0436), [Datetime Format 문자열](#95e37f19cf8bd6a2),  [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#8cf319a54a7fec34)을 참조한다.

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

<a id="dae2fb81bd7a9e09"></a>
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

자세한 내용은 [INTERVAL](16-built-in-data-type-references.md#566a59cfb0f9f3e6), [INTERVAL * TO * 에서 두 번째 이후 field의 precision과 값의 범위](16-built-in-data-type-references.md#33e046fc808fce90), [NUMTOYMINTERVAL](17-built-in-function-references.md#b5c581181c57d3ff) , [NUMTODSINTERVAL](17-built-in-function-references.md#ec0c8757a80dc2bb)을 참조한다.

<a id="2c58febfc9e2d9ea"></a>
#### Interval literals의 사용 예

다음은 interval literals를 사용하는 예들이다.

<a id="046309104b8000de"></a>
##### Interval YEAR

다음은 interval YEAR literals를 사용하는 예이다.

<a id="73d7edd6d9b11380"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'YEAR INTERVAL'01-00'YEAR | 1 year | +01-00 |
| INTERVAL'100'YEAR | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100'YEAR(3) | 100 year | +100-00 |
| INTERVAL'+999999'YEAR(6) | 999999 year | +999999-00 |
| INTERVAL'-999999'YEAR(6) | -(999999 year) | -999999-00 |

<a id="3381a2741a2d7be9"></a>
##### Interval MONTH

다음은 interval MONTH literals를 사용하는 예이다.

<a id="3dd72d579411483a"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'MONTH INTERVAL'00-01'MONTH | 1 month | +00-01 |
| INTERVAL'100'MONTH | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100'MONTH(3) | 8 year 4 month | +008-04 |
| INTERVAL'+999999'MONTH(6) | 83333 year 3 month | +083333-03 |
| INTERVAL'-999999'MONTH(6) | -(83333 year 3 month) | -083333-03 |

<a id="94832cf5e520edbe"></a>
##### Interval YEAR TO MONTH

다음은 interval YEAR TO MONTH literals를 사용하는 예이다.

<a id="fa4709319ff88f58"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1-06'YEAR TO MONTH | 1 year 6 month | +01-06 |
| INTERVAL'1-12'YEAR TO MONTH | Month value가 11을 초과하여 에러가 반환된다. | - |
| INTERVAL'100-11'YEAR TO MONTH | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100-11'YEAR(3) TO MONTH | 100 year 11 month | +100-11 |
| INTERVAL'+999999-11'YEAR(6) TO MONTH | 999999 year 11 month | +999999-11 |
| INTERVAL'-999999-11'YEAR(6) TO MONTH | -(999999 year 11 month) | -999999-11 |

<a id="a6c87ed1b3aa06fb"></a>
##### Interval DAY

다음은 interval DAY literals를 사용하는 예이다.

<a id="e2ef1090c62a065f"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'DAY INTERVAL'01 00:00:00'DAY | 1 day | +01 00:00:00 |
| INTERVAL'100'DAY | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100'DAY(3) | 100 day | +100 00:00:00 |
| INTERVAL'+999999'DAY(6) | 999999 day | +999999 00:00:00 |
| INTERVAL'-999999'DAY(6) | -(999999 day) | -999999 00:00:00 |

<a id="b6e9172de6c1b1ed"></a>
##### Interval HOUR

다음은 interval HOUR literals를 사용하는 예이다.

<a id="042b904d2af03cef"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'HOUR INTERVAL'00 01:00:00'HOUR | 1 hour | +00 01:00:00 |
| INTERVAL'1000'HOUR(3) | Leading precision 3을 초과하여 에러가 반환된다. | - |
| INTERVAL'1000'HOUR(4) | 41 day 16 hour | +0041 16:00:00 |
| INTERVAL'+999999'HOUR(6) | 41666 day 15 hour | +041666 15:00:00 |
| INTERVAL'-999999'HOUR(6) | -(41666 day 15 hour) | -041666 15:00:00 |

<a id="1e87ea9341247c62"></a>
##### Interval MINUTE

다음은 interval MINUTE literals를 사용하는 예이다.

<a id="500c126773c72547"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'MINUTE INTERVAL'00 00:01:00'MINUTE | 1 minute | +00 00:01:00 |
| INTERVAL'12345'MINUTE(4) | Leading precision 4를 초과하여 에러가 반환된다. | - |
| INTERVAL'12345'MINUTE(5) | 8 day 13 hour 45 minute | +00008 13:45:00 |
| INTERVAL'+999999'MINUTE(6) | 694 day 10 hour 39 minute | +000694 10:39:00 |
| INTERVAL'-999999'MINUTE(6) | -(694 day 10 hour 39 minute) | -000694 10:39:00 |

<a id="a9cb7a7fe65c880e"></a>
##### Interval SECOND

다음은 interval SECOND literals를 사용하는 예이다.

<a id="89b9f1107800453b"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1'SECOND INTERVAL'00 00:00:01.000000'SECOND | 1 second | +00 00:00:01.000000 |
| INTERVAL'100'SECOND | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'99.9999999'SECOND INTERVAL'99.9999999'SECOND(2,6) | Fractional seconds가 반올림되어 100 second가 되므로 leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'99.9999999'SECOND(3) | 1 minute 40 second | +000 00:01:40.000000 |
| INTERVAL'29.506167'SECOND(2, 2) | 29.51 second | +00 00:00:29.51 |
| INTERVAL'999999.999999'SECOND(6,6) | 11day 13 hour 46 minute 39.999999 second | +000011 13:46:39.999999 |
| INTERVAL'-999999.999999'SECOND(6,6) | -( 11day 13 hour 46 minute 39.999999 second) | -000011 13:46:39.999999 |

<a id="526043a6f6c797f7"></a>
##### Interval DAY TO HOUR

다음은 interval DAY TO HOUR literals를 사용하는 예이다.

<a id="2cd6b0c46d612785"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1 23'DAY TO HOUR INTERVAL'01 23:00:00'DAY TO HOUR | 1 day 23 hour | +01 23:00:00 |
| INTERVAL'1 24'DAY TO HOUR | Hour value가 23을 초과한 invalid 값으로써 에러를 반환한다. | - |
| INTERVAL'100 23'DAY TO HOUR | Leading precision 2를 초과하여 에러를 반환한다. | - |
| INTERVAL'100 23'DAY(3) TO HOUR | 100 day 23 hour | +100 23:00:00 |
| INTERVAL'+999999 23'DAY(6) TO HOUR | 999999 day 23 hour | +999999 23:00:00 |
| INTERVAL'-999999 23'DAY(6) TO HOUR | -(999999 day 23 hour) | -999999 23:00:00 |
| INTERVAL'-999999 +23'DAY(6) TO HOUR | 부호지정 오류로 인한 에러이다. | - |

<a id="19f806d3e05e05f8"></a>
##### Interval DAY TO MINUTE

다음은 interval DAY TO MINUTE literals를 사용하는 예이다.

<a id="61137c726b6cb4f1"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'1 23:59'DAY TO MINUTE INTERVAL'01 23:59:00'DAY TO MINUTE | 1 day 23 hour 59 second | +01 23:59:00 |
| INTERVAL'1 24:59'DAY TO MINUTE | Hour value가 23을 초과한 invalid 값으로써 에러가 반환된다. | - |
| INTERVAL'1 23:60'DAY TO MINUTE | Minute value가 59를 초과한 invalid 값으로써 에러가 반환된다. | - |
| INTERVAL'100 23:59'DAY TO MINUTE | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100 23:59'DAY(3) TO MINUTE | 100 day 23 hour 59 minute | +100 23:59:00 |
| INTERVAL'+999999 23:59'DAY(6) TO MINUTE | 999999 day 23 hour 59 minute | +999999 23:59:00 |
| INTERVAL'-999999 23:59'DAY(6) TO MINUTE | -(999999 day 23 hour 59 minute) | -999999 23:59:00 |

<a id="96f10367af7dd2b5"></a>
##### Interval DAY TO SECOND

다음은 interval DAY TO SECOND literals를 사용하는 예이다.

<a id="c80d70ed1f7b52da"></a>
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

<a id="4fe4cdadf7e40d71"></a>
##### Interval HOUR TO MINUTE

다음은 interval HOUR TO MINUTE literals를 사용하는 예이다.

<a id="ebe7f49d8dac7df0"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL'23:59'HOUR TO MINUTE INTERVAL'00 23:59:00'HOUR TO MINUTE | 23 hour 59 minute | +00 23:59:00 |
| INTERVAL'23:60'HOUR TO MINUTE | Minute value가 59를 초과하여 에러가 반환된다. | - |
| INTERVAL'100:59'HOUR TO MINUTE | Leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL'100:59'HOUR(3) TO MINUTE | 4 day 4 hour 59 minute | +004 04:59:00 |
| INTERVAL'+999999:59'HOUR(6) TO MINUTE | 41666 day 15 hour 59 minute | +041666 15:59:00 |
| INTERVAL'-999999:59'HOUR(6) TO MINUTE | -(41666 day 15 hour 59 minute) | -041666 15:59:00 |

<a id="016da5c1f2011d4d"></a>
##### Interval HOUR TO SECOND

다음은 interval HOUR TO SECOND literals를 사용하는 예이다.

<a id="60bfe3304ccefc0f"></a>
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

<a id="3cf160ac6b9b9dac"></a>
##### Interval MINUTE TO SECOND

다음은 interval MINUTE TO SECOND literals를 사용하는 예이다.

<a id="73a0d02eadd55b5e"></a>
| 예 | 설명 | Display string |
| --- | --- | --- |
| INTERVAL '15:23.123456'MINUTE TO SECOND INTERVAL '00 00:15:23.123456'MINUTE TO SECOND | 15 minute 23.123456 second | +00 00:15:23.123456 |
| INTERVAL '15:60.123456'MINUTE TO SECOND | Second value가 59를 초과하여 에러가 반환된다. | - |
| INTERVAL '99:59.999999'MINUTE TO SECOND(2) | Fractional seconds가 반올림되어 100 minute가 되므로 leading precision 2를 초과하여 에러가 반환된다. | - |
| INTERVAL '99:59.999999'MINUTE(3) TO SECOND(2) | 1 hour 40 minute | +000 01:40:00.00 |
| INTERVAL '+999999:59.999999'MINUTE(6) TO SECOND(6) | 694 day 10 hour 39 minute 59.999999 second | +000694 10:39:59.999999 |
| INTERVAL '-999999:59.999999'MINUTE(6) TO SECOND(6) | -(694 day 10 hour 39 minute 59.999999 second) | -000694 10:39:59.999999 |

<a id="8538e7aa0e372c44"></a>
### Null Value

Null value는 알 수 없는 값 또는 정의되지 않은 값이다. 모든 data type 값이 null value가 될 수 있다.   
Boolean type의 unknown 값은 null value로 대체되어 표현된다.  
Null value는 keyword로 정의되어 있으며 대소문자 구분없이 사용한다.

다음은 null value를 기술하는 예이다.

```
NULL
Null
```

<a id="0c0fe841b325908b"></a>
### Comments

<a id="659451acb5e02019"></a>
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

<a id="e93e5fb2553aee34"></a>
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

<a id="3f40effdddf471b7"></a>
#### Hint Comments

Hint comments는 /*+로 시작하고, */로 끝나는 comment 이다. Hint comments는 multiple line comments와 비슷하지만 시작 기호에 +가 더 있다는 점이 다르다. Hint comments에서 시작기호의 *와 + 사이에 공백이 존재하면 multiple line comments로 처리되는 것에 주의한다.

Hint comments는 다른 comment들과 달리 사용 가능한 위치가 SELECT 키워드의 바로 다음으로 지정되어 있다. Hint comments에는 사용자가 GOLDILOCKS의 optimizer에게 처리 방법 등을 지정하는 내용이 기술되어 있는데 자세한 내용은 [SQL Hint](15-sql-tuning.md#54d9bce5449eb296)를 참조한다.

다음은 hint comments를 사용하는 예이다.

```
gSQL> SELECT /*+ FULL(T1) */ * FROM T1;

I1        I2        I3        I4        I5       
--------- --------- --------- --------- ---------
column i1 column i2 column i3 column i4 column i5

1 row selected.
```

<a id="534a380cb99f453d"></a>
### SQL Reserved Words and Keywords

<a id="c04cd1a93f48cd58"></a>
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

다음은 GOLDILOCKS SQL reserved words인데 * 표시한 것은 SQL standard에서 명시한 reserved words이다. 해당 리스트는 [V$RESERVED_WORDS](../part-02-administration-manual/9-database-information.md#ebd95a0e07bb165b) view를 통해 검색할 수 있다.

ABSOLUTE  
ACCESS  
ADMINISTRATION  
ALL *  
ALLOCATE *  
ALTER *  
ANALYZE         
AND *  
ANTI            
ANY *  
ARE *  
AS *  
ASYMMETRIC *  
AT *  
AUDIT           
AUTHORIZATION *  
BEGIN *  
BETWEEN *  
BOTH *  
BY *  
CALL *  
CASE *  
CHECK *  
CLOSE *  
CLUSTER              
CLUSTER_GROUP_ID     
CLUSTER_GROUP_NAME   
CLUSTER_MEMBER_ID    
CLUSTER_MEMBER_NAME  
CLUSTER_SHARD_ID     
COLUMN *  
COMMENT  
COMMIT *  
CONNECT *  
CONNECT_BY_ISCYCLE   
CONNECT_BY_ISLEAF    
CONNECT_BY_ROOT      
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
DISCONNECT *  
DISTINCT *  
DROP *  
ELSE *  
EMPTY         
END *  
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
INDEX         
INDICATOR *  
INNER *  
INOUT *  
INSERT *  
INTERSECT *  
INTO *  
IS *  
JOIN *  
LAST  
LATERAL         
LEADING *  
LEFT *  
LEVEL           
LIKE *  
LIMIT  
LOCAL *  
LOCALTIME *  
LOCALTIMESTAMP *  
LOCAL_OFFLINE   
LOCK            
MATCH *  
MEMBER *  
MERGE *  
MINUS  
NATURAL *  
NEW *  
NEXT  
NOAUDIT         
NONE            
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
OVER              
PACKAGE           
PHYSICAL_PAGE_ID  
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
ROWNUM           
ROWS *  
ROW_NUMBER *  
SAVEPOINT *  
SELECT *  
SEMI             
SESSION_USER *  
SET *  
SHARDING_HANDLE  
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
SYS_CONNECT_BY_PATH  
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
USAGE         
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

<a id="20b8f341233d1fe0"></a>
#### SQL Keywords

GOLDILOCKS SQL keywords는 reserved word가 아니다. 그러나 GOLDILOCKS 내부적으로 사용하는 keyword이므로 GOLDILOCKS SQL keywords를 사용할 경우 결과의 가독성이 떨어질 수 있어 사용을 권장하지 않는다.

GOLDILOCKS SQL keywords 목록은 [V$KEYWORDS](../part-02-administration-manual/9-database-information.md#439efe20f50404cf) view를 통해 검색할 수 있다.

<a id="2a6af7d320105606"></a>
### 호환성

Syntax element에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="ae58a9d1058881f7"></a>
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

<a id="0e511565dcb79955"></a>
## Data Type

<a id="a5388cb38ea88284"></a>
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

<a id="e606ca61adf8eabd"></a>
#### 십진 숫자 타입

유효 숫자의 정밀도를 나타내는 precision과 소수점의 범위를 나타내는 scale이 십진수 (decimal)를 기반으로 한다.

<a id="787283f263708d58"></a>
##### 십진 고정 소수점 타입

십진 고정 소수점 타입은 SQL에서 정의한 타입이다.

**십진 고정 소수점 타입**

<a id="0387df76119e911f"></a>
| Type | Decimal precision | Decimal scale |  |
| --- | --- | --- | --- |
| NUMBER( p ) | p | 0 | [NUMBER](16-built-in-data-type-references.md#c6ff1bfcdb167a6b) |
| NUMBER( p, s ) | p | s | [NUMBER](16-built-in-data-type-references.md#c6ff1bfcdb167a6b) |
| NUMERIC( p ) | p | 0 | [NUMERIC](16-built-in-data-type-references.md#cdae231a5b04aa57) |
| NUMERIC( p, s ) | p | s | [NUMERIC](16-built-in-data-type-references.md#cdae231a5b04aa57) |
| DECIMAL( p ) | p | 0 | [NUMERIC](16-built-in-data-type-references.md#cdae231a5b04aa57) 타입 alias |
| DECIMAL( p, s ) | p | s | [NUMERIC](16-built-in-data-type-references.md#cdae231a5b04aa57) 타입 alias |
| DEC( p ) | p | 0 | [NUMERIC](16-built-in-data-type-references.md#cdae231a5b04aa57) 타입 alias |
| DEC( p, s ) | p | s | [NUMERIC](16-built-in-data-type-references.md#cdae231a5b04aa57) 타입 alias |
| SMALLINT | 5 | 0 | [NUMBER](16-built-in-data-type-references.md#c6ff1bfcdb167a6b) 타입 alias |
| INTEGER | 10 | 0 | [NUMBER](16-built-in-data-type-references.md#c6ff1bfcdb167a6b) 타입 alias |
| BIGINT | 19 | 0 | [NUMBER](16-built-in-data-type-references.md#c6ff1bfcdb167a6b) 타입 alias |
| INT2 | 5 | 0 | [NUMBER](16-built-in-data-type-references.md#c6ff1bfcdb167a6b) 타입 alias |
| INT4 | 10 | 0 | [NUMBER](16-built-in-data-type-references.md#c6ff1bfcdb167a6b) 타입 alias |
| INT8 | 19 | 0 | [NUMBER](16-built-in-data-type-references.md#c6ff1bfcdb167a6b) 타입 alias |

<a id="f92a881003171f09"></a>
##### 십진 부동 소수점 타입

십진 부동 소수점 타입은 SQL에서 정의한 타입이다.

**십진 부동 소수점 타입**

<a id="8c67835b9d065b06"></a>
| Type | Decimal precision | Decimal scale | 참조 |
| --- | --- | --- | --- |
| NUMBER | 38 | N/A | [NUMBER](16-built-in-data-type-references.md#c6ff1bfcdb167a6b) |
| FLOAT( p ) | ceil( log<sub>10</sub> 2<sup>p</sup> ) | N/A | [FLOAT](16-built-in-data-type-references.md#52cda9688510ddb8) |
| REAL | ceil( log<sub>10</sub> 2<sup>24</sup> ) = 8 | N/A | [FLOAT](16-built-in-data-type-references.md#52cda9688510ddb8) 타입의 alias |
| DOUBLE | ceil( log<sub>10</sub> 2<sup>53</sup> ) = 16 | N/A | [FLOAT](16-built-in-data-type-references.md#52cda9688510ddb8) 타입의 alias |
| FLOAT4 | ceil( log<sub>10</sub> 2<sup>24</sup> ) = 8 | N/A | [FLOAT](16-built-in-data-type-references.md#52cda9688510ddb8) 타입의 alias |
| FLOAT8 | ceil( log<sub>10</sub> 2<sup>53</sup> ) = 16 | N/A | [FLOAT](16-built-in-data-type-references.md#52cda9688510ddb8) 타입의 alias |

<a id="58ce4a90f42d41c7"></a>
#### 이진 숫자 타입

유효 숫자의 정밀도를 나타내는 precision과 소수점의 범위를 나타내는 scale이 이진수 (binary)를 기반으로 한다.

<a id="1f28ae4f111ef1bf"></a>
##### 이진 고정 소수점 타입

이진 고정 소수점 타입은 C 언어의 signed integer 계열 타입을 참조한다.  
Sign bit를 표시하기 위해 1 bit를 사용하고 나머지 bit들은 precision을 표현하는데 사용하며 scale을 표현할 때는 bit를 사용하지 않는다.

**이진 고정 소수점 타입**

<a id="48d64815be66ce64"></a>
| Type | Binary precision | Binary scale | 참조 |
| --- | --- | --- | --- |
| NATIVE_SMALLINT | 15 | 0 | [NATIVE_SMALLINT](16-built-in-data-type-references.md#a044180afc5b8dd2) |
| NATIVE_INTEGER | 31 | 0 | [NATIVE_INTEGER](16-built-in-data-type-references.md#7c681b02bb8881b7) |
| NATIVE_BIGINT | 63 | 0 | [NATIVE_BIGINT](16-built-in-data-type-references.md#44caf5234d199c06) |

<a id="26f46811b470ef7e"></a>
##### 이진 부동 소수점 타입

이진 부동 소수점 타입은 C 언어의 float과 double 타입을 참조한다.   
Sign bit를 표시하기 위해 1 bit를 사용하고 나머지 bit들은 precision과 scale을 표현하기 위해 사용한다.

**이진 부동 소수점 타입**

<a id="30ba83f5c70e7d5e"></a>
| Type | Binary precision | Binary scale | 참조 |
| --- | --- | --- | --- |
| NATIVE_REAL | 23 | 8 | [NATIVE_REAL](16-built-in-data-type-references.md#999ec9a26801d7fc) |
| NATIVE_DOUBLE | 52 | 11 | [NATIVE_DOUBLE](16-built-in-data-type-references.md#5e9f6066e970ac2e) |

> 이진 부동 소수점 타입에 대한 precision과 scale은 OS 및 compiler의 환경에 따라 변동될 수 있다.

<a id="fb77121239da93bf"></a>
### CHARACTER STRING 타입

CHARACTER STRING 타입은 가변길이 문자열 여부와 문자열의 최대 길이에 따라 구분할 수 있다.

- 가변길이 문자열 여부에 따른 분류
    - 고정 길이 문자열
        - [CHARACTER](16-built-in-data-type-references.md#096de4cc7c228c39)
    - 가변 길이 문자열
        - [CHARACTER VARYING](16-built-in-data-type-references.md#f93f94cc03a69695), [CHARACTER LONG VARYING](16-built-in-data-type-references.md#2dec07a3232abf0a)
- 문자열의 최대 길이에 따른 분류
    - 2000 [ characters 또는 bytes ]
        - [CHARACTER](16-built-in-data-type-references.md#096de4cc7c228c39)
    - 4000 [ characters 또는 bytes ]
        - [CHARACTER VARYING](16-built-in-data-type-references.md#f93f94cc03a69695)
    - 100 megabytes
        - [CHARACTER LONG VARYING](16-built-in-data-type-references.md#2dec07a3232abf0a)

<a id="c535d51ebaa5c602"></a>
### BINARY STRING 타입

BINARY STRING 타입은 가변길이 이진 문자열 여부와 이진 문자열의 최대 길이에 따라 구분할 수 있다.

- 가변길이 이진 문자열 여부에 따른 분류
    - 고정 길이 이진 문자열
        - [BINARY](16-built-in-data-type-references.md#9fc22edda9fa4078)
    - 가변 길이 이진 문자열
        - [BINARY VARYING](16-built-in-data-type-references.md#67dd67b9ba80c5e4), [BINARY LONG VARYING](16-built-in-data-type-references.md#129c6e5a4235d3d5)
- 이진 문자열의 최대 길이 따른 분류
    - 2000 
        - [BINARY](16-built-in-data-type-references.md#9fc22edda9fa4078)
    - 4000 
        - [BINARY VARYING](16-built-in-data-type-references.md#67dd67b9ba80c5e4)
    - 100 megabytes
        - [BINARY LONG VARYING](16-built-in-data-type-references.md#129c6e5a4235d3d5)

<a id="8186ddbb4bdea94b"></a>
### 날짜/ 시간 타입

날짜/ 시간 타입은 년, 월, 일, 시, 분, 초, time zone offset을 각 타입의 표현방식에 맞게 지정한다.  
날짜/ 시간 타입에는 [DATE](16-built-in-data-type-references.md#30e7e89edce7c53b), [TIME](16-built-in-data-type-references.md#5543fbcfbecdcada), [TIMESTAMP](16-built-in-data-type-references.md#87997e1e9ab5b1a5) 타입이 있다.

<a id="f984af7dc4c30bf9"></a>
### INTERVAL 타입

INTERVAL 타입은 시간 간격을 지정한다.  
년, 월, 일, 시, 분, 초의 시간 간격을 각 타입의 표현방식에 맞게 지정한다.

[INTERVAL](16-built-in-data-type-references.md#566a59cfb0f9f3e6) 타입은 값의 표현 범위에 따라 YEAR TO MONTH 계열과 DAY TO SECOND 계열로 구분할 수 있다.

<a id="d1ce2fedce9342ad"></a>
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

자세한 내용은 [BOOLEAN](16-built-in-data-type-references.md#5dd8a936670a0b64)을 참조한다.

<a id="032f64525a92081e"></a>
### ROWID 타입

데이터베이스에 저장된 모든 레코드는 각기 다른 위치정보를 가지고 있으며, 각각의 레코드를 구분하기 위해 레코드 식별자 (ROWID)를 사용한다.

ROWID 타입은 레코드 식별자 (ROWID)를 저장 관리하기 위한 타입이다.   
ROWID pseudo column을 사용한 질의를 통해 레코드 식별자 (ROWID)를 얻을 수 있다.

자세한 내용은 [ROWID](16-built-in-data-type-references.md#20b3d19ae7ac61d4)를 참조한다.

<a id="329e88f63daf5a67"></a>
### 타입간 비교

두 타입간의 비교는 하나의 대표 타입을 기준으로 수행된다. 비교 대상 타입이 대표 타입과 다를 경우 타입 변환을 통해 비교할 수도 있다.  
[타입간 비교를 위한 대표 타입](#f025fcab1bd555ba)에서는 두 타입간의 비교를 위한 대표 타입을 정의한다.

다음 표에서는 각 대표 타입별로 비교를 위해 대상 타입들을 변환하는 것에 대해 설명한다.

- [VC 에서의 비교를 위한 타입 변환](#4f57a55c54bcb335)
- [LC 에서의 비교를 위한 타입 변환](#dc2e0759d9db9a09)
- [VB 에서의 비교를 위한 타입 변환](#98eb991936b6d98d)
- [LB 에서의 비교를 위한 타입 변환](#c8352a28b912d364)
- [NB 에서의 비교를 위한 타입 변환](#38f077e50a46c9b6)
- [ND 에서의 비교를 위한 타입 변환](#829c412928c1b23a)
- [NU 에서의 비교를 위한 타입 변환](#7b3b9ca2121beb58)
- [DA 에서의 비교를 위한 타입 변환](#983d9fe0dfa14166)
- [TI 에서의 비교를 위한 타입 변환](#a09b19774db85ad6)
- [TZ 에서의 비교를 위한 타입 변환](#025e1866f1a590be)
- [TS 에서의 비교를 위한 타입 변환](#a7024aaabd8da3dc)
- [SZ 에서의 비교를 위한 타입 변환](#59164e2d32a60920)
- [YM 에서의 비교를 위한 타입 변환](#750b1347e75f3598)
- [DS 에서의 비교를 위한 타입 변환](#31e463d91a3e8ad0)
- [BO 에서의 비교를 위한 타입 변환](#c0b1202d8c6140a4)
- [RI 에서의 비교를 위한 타입 변환](#2a768bf035aa1b55)

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

<a id="f025fcab1bd555ba"></a>
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

<a id="4f57a55c54bcb335"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | CHAR (변환 없음) |
| VARCHAR | VARCHAR (변환 없음) |

**`LC` 에서의 비교를 위한 타입 변환**

<a id="dc2e0759d9db9a09"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | CHAR (변환 없음) |
| VARCHAR | VARCHAR (변환 없음) |
| LONG VARCHAR | LONG VARCHAR (변환 없음) |

**`VB` 에서의 비교를 위한 타입 변환**

<a id="98eb991936b6d98d"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| BINARY | BINARY (변환 없음) |
| VARBINARY | VARBINARY (변환 없음) |

**`LB` 에서의 비교를 위한 타입 변환**

<a id="c8352a28b912d364"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| BINARY | BINARY (변환 없음) |
| VARBINARY | VARBINARY (변환 없음) |
| LONG VARBINARY | LONG VARBINARY (변환 없음) |

**`NB` 에서의 비교를 위한 타입 변환**

<a id="38f077e50a46c9b6"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | NATIVE_BIGINT |
| VARCHAR | NATIVE_BIGINT |
| LONG VARCHAR | NATIVE_BIGINT |
| NATIVE_SMALLINT | NATIVE_SMALLINT (변환 없음) |
| NATIVE_INTEGER | NATIVE_INTEGER (변환 없음) |
| NATIVE_BIGINT | NATIVE_BIGINT (변환 없음) |

**`ND` 에서의 비교를 위한 타입 변환**

<a id="829c412928c1b23a"></a>
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

<a id="7b3b9ca2121beb58"></a>
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

<a id="983d9fe0dfa14166"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | DATE |
| VARCHAR | DATE |
| LONG VARCHAR | DATE |
| DATE | DATE (변환 없음) |

**`TI` 에서의 비교를 위한 타입 변환**

<a id="a09b19774db85ad6"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | TIME |
| VARCHAR | TIME |
| LONG VARCHAR | TIME |
| TIME | TIME (변환 없음) |

**`TZ` 에서의 비교를 위한 타입 변환**

<a id="025e1866f1a590be"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | TIME_TZ |
| VARCHAR | TIME_TZ |
| LONG VARCHAR | TIME_TZ |
| TIME | TIME_TZ |
| TIME_TZ | TIME_TZ (변환 없음) |

**`TS` 에서의 비교를 위한 타입 변환**

<a id="a7024aaabd8da3dc"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | TIMESTAMP |
| VARCHAR | TIMESTAMP |
| LONG VARCHAR | TIMESTAMP |
| DATE | DATE (변환 없음) |
| TIMESTAMP | TIMESTAMP (변환 없음) |

**`SZ` 에서의 비교를 위한 타입 변환**

<a id="59164e2d32a60920"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | TIMESTAMP_TZ |
| VARCHAR | TIMESTAMP_TZ |
| LONG VARCHAR | TIMESTAMP_TZ |
| DATE | TIMESTAMP_TZ |
| TIMESTAMP | TIMESTAMP_TZ |
| TIMESTAMP_TZ | TIMESTAMP_TZ (변환 없음) |

**`YM` 에서의 비교를 위한 타입 변환**

<a id="750b1347e75f3598"></a>
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

<a id="31e463d91a3e8ad0"></a>
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

<a id="c0b1202d8c6140a4"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | BOOLEAN |
| VARCHAR | BOOLEAN |
| LONG VARCHAR | BOOLEAN |
| BOOLEAN | BOOLEAN (변환 없음) |

**`RI` 에서의 비교를 위한 타입 변환**

<a id="2a768bf035aa1b55"></a>
| 원본 타입 | 변환 타입 |
| --- | --- |
| CHAR | ROWID |
| VARCHAR | ROWID |
| LONG VARCHAR | ROWID |
| ROWID | ROWID (변환 없음) |

<a id="d9c1b23c9cbab71c"></a>
### 타입간 변환

타입간 변환은 내부 변환 (implicit type conversion)과 외부 변환 (explicit type conversion)으로 구분된다.

- 내부 변환 (implicit type conversion)은 select, insert, delete, update를 위한 expression, operator, function, condition 들에서 발생한다.
- 외부 변환 (explicit type conversion)은 CAST operator를 통해 이루어진다.

[타입간 변환](#89835b5bc8c8df63)에서는 한 data type에서 다른 data type으로의 변환 가능 여부를 설명한다.

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

<a id="89835b5bc8c8df63"></a>
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
        - 자세한 내용은 [Interval Literals](#dae2fb81bd7a9e09)를 참조한다.
        - 변환 타입에 정의된 precision에 의해 overflow가 발생할 수 있다.
    - 원본 타입이 NATIVE_SMALLINT, NATIVE_INTEGER, NATIVE_BIGINT, NUMBER, NUMERIC, FLOAT 타입인 경우
        - 변환 타입이 single field (YEAR, MONTH)이어야 한다.
        - 변환 타입에 정의된 precision에 의해 overflow가 발생할 수 있다.
    - 원본 타입이 INTERVAL YEAR TO MONTH 계열 타입인 경우
        - 변환 타입에 정의된 precision에 의해 overflow가 발생할 수 있다.

- INTERVAL DAY TO SECOND 계열 타입으로의 변환
    - 원본 타입이 CHARACTER STRING 타입인 경우
        - day-time interval literal 형식에 맞지 않는 문자열이 오는 경우 에러가 발생한다.
        - 자세한 내용은 [Interval Literals](#dae2fb81bd7a9e09)를 참조한다.
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

<a id="9e7de21e8a975434"></a>
### 타입간 조합

<a id="95c14735bd0e9969"></a>
#### 타입간 조합이 필요한 경우

CASE 연산자, 집합 연산자 ([set operator](20-sql-references-h-z.md#8fd806f5930143e4))는 다수의 expression을 연산 결과로 가진다.  
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
    - 집합 연산자 ([set operator](20-sql-references-h-z.md#8fd806f5930143e4))
    - CASE 연산자 
        - [CASE Expression](#2633f85220fe5028)
        - [COALESCE](17-built-in-function-references.md#04470874956922ee)
        - [NULLIF](17-built-in-function-references.md#5c39f8c5b46c9f0c)

<a id="e881713e04641bea"></a>
#### 결과 타입 조합 규칙

각 expression의 data type은 조합 가능한 동일한 계열의 타입이어야 한다.

- 결과 타입 조합 규칙이 적용되는 예
    - 집합 연산자 ([set operator](20-sql-references-h-z.md#8fd806f5930143e4))
    - CASE 연산자 
        - [CASE Expression](#2633f85220fe5028)
        - [COALESCE](17-built-in-function-references.md#04470874956922ee)
        - [NULLIF](17-built-in-function-references.md#5c39f8c5b46c9f0c)

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

<a id="2cf8897ed2903856"></a>
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
- 자세한 내용은 [타입간 비교](#329e88f63daf5a67)를 참조한다.

<a id="c54a7611f50a3a40"></a>
### 호환성

Data type에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="526bd5fa08164e2b"></a>
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

<a id="eb1bb584b1499788"></a>
## Format 문자열

Format 문자열은 숫자 타입이나 날짜/ 시간 타입을 문자열로 변환하거나 문자열을 숫자 타입이나 날짜/ 시간 타입으로 변환하기 위한 형식을 정의한 문자열이다.

- 숫자 타입이나 날짜/시간 타입을 문자열로 변환할 때 다음과 같은 형식으로 문자열을 표현한다.
    - [TO_CHAR( number )](17-built-in-function-references.md#69fde4657a756aff), [TO_CHAR( datetime )](17-built-in-function-references.md#49e380b1da61d32b)
    - 숫자 타입: TO_CHAR( 1234.56, 'S9,999.99' ) → '+1,234.56'
    - 날짜/ 시간 타입: TO_CHAR( SYSDATE, 'YYYY-MM-DD' ) → '2012-07-15'
- 문자열을 숫자 타입이나 날짜/ 시간 타입으로 변환할 때 다음과 같은 형식으로 문자열을 표현한다.
**[ TO_NATIVE_SMALLINT](17-built-in-function-references.md#802fe8044515d1c9), [TO_NATIVE_INTEGER](17-built-in-function-references.md#f4ea0087d7690777), [TO_NATIVE_BIGINT](17-built-in-function-references.md#860aa4f498a985ca)
    - [TO_NUMBER](17-built-in-function-references.md#5b93653f4677d64c), [TO_NATIVE_REAL](17-built-in-function-references.md#9c39d911dce66749), [TO_NATIVE_DOUBLE](17-built-in-function-references.md#b6f99a7754f9a09a)
    - [TO_DATE](17-built-in-function-references.md#e1ae1f9cb408151d)
    - [TO_TIMESTAMP](17-built-in-function-references.md#48f2f9c2be120650), [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#667ef9b2a77a0436)
    - [TO_TIME](17-built-in-function-references.md#91b2febb7ce81d9c), [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#a9f9c02ecbf276e7)
    - 숫자 타입: TO_NUMBER( '+1,234.56', 'S9,999.99' ) → NUMBER TYPE
    - 날짜/ 시간 타입: TO_DATE( '2012-07-15', 'YYYY-MM-DD' ) → DATE TYPE

Format 문자열은 다음과 같은 타입으로 구분된다.  
• 숫자 타입: [Number Format 문자열](#36aa4bb1bae7fc27)  
• 날짜/ 시간 타입: [Datetime Format 문자열](#95e37f19cf8bd6a2)

<a id="36aa4bb1bae7fc27"></a>
### Number Format 문자열

Number format 문자열은 숫자 타입을 문자열로 변환하거나 문자열을 숫자 타입으로 변환하기 위한 형식을 정의한 문자열이다.

Number format 문자열은 [TO_CHAR( number )](17-built-in-function-references.md#69fde4657a756aff), [TO_NATIVE_SMALLINT](17-built-in-function-references.md#802fe8044515d1c9), [TO_NATIVE_INTEGER](17-built-in-function-references.md#f4ea0087d7690777), [TO_NATIVE_BIGINT](17-built-in-function-references.md#860aa4f498a985ca), [TO_NUMBER](17-built-in-function-references.md#5b93653f4677d64c), [TO_NATIVE_REAL](17-built-in-function-references.md#9c39d911dce66749), [TO_NATIVE_DOUBLE](17-built-in-function-references.md#b6f99a7754f9a09a) 함수의 인자로 사용된다.

Number format 문자열에는 표현하고자 하는 형식에 따라 여러 개의 format element를 지정할 수 있다.

모든 number format element는 그 형식에 맞게 반올림하여 적용한다.  
변환하고자 하는 value의 소수점 이전 digit 개수가 format 문자열에 지정된 숫자의 자리수보다 큰 경우, '#' 문자로 대체된다.  
MI, S, PR의 부호를 표현하는 format element를 지정하지 않은 경우, 음수는 숫자 앞에 '-' 부호를 양수는 공백을 반환하는 방식으로 부호를 표현한다.

**Number format elements**

<a id="c03c92aa4ef522fb"></a>
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
| S | S9999 9999S | 양수인 경우 숫자 앞에 '+' 부호를 음수인 경우 '-' 부호를 반환한다. (S9999)  양수인 경우 숫자 끝에 '+' 부호를 음수인 경우 '-' 부호를 반환한다. (9999S) Format 문자열의 맨 처음 또는 맨 마지막에만 지정할 수 있다. MI, PR과 함께 지정할 수 없다. |
| V | 999V99 | V format element 뒤에 오는 9의 digit 개수가 n일 때, value에 10<sup>n</sup> 을 곱한 값을 반환한다.  소수점(.)과 함께 지정할 수 없다. TO_NUMBER 함수에는 사용할 수 없다. |
| X | XXXX xxxx | 지정된 X digit 수에 맞게 공백과 16 진수를 반환한다. 정수값을 16 진수로 반환한다. (정수가 아닌 경우 반올림하여 정수값을 만든다.) XXXX는 16 진수 대문자를 xxxx는 16 진수 소문자를 반환한다. 변환된 16 진수 digit 개수가 명시된 X의 개수보다 작은 경우, 차이나는 부분을 공백으로 채워 반환한다. 0과 양의 정수만 처리하고, 음수인 경우 '#' 문자로 대체된다. Format element 0 및 FM과만 함께 지정할 수 있으며, 다른 format element와는 함께 지정할 수 없다. |
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

<a id="95e37f19cf8bd6a2"></a>
### Datetime Format 문자열

Datetime format 문자열은 날짜/ 시간 타입을 문자열로 변환하거나 문자열을 날짜/ 시간 타입으로 변환하기 위한 형식을 정의한 문자열이다.

Datetime format 문자열은 [TO_CHAR( datetime )](17-built-in-function-references.md#49e380b1da61d32b), [TO_DATE](17-built-in-function-references.md#e1ae1f9cb408151d), [TO_TIMESTAMP](17-built-in-function-references.md#48f2f9c2be120650), [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#667ef9b2a77a0436), [TO_TIME](17-built-in-function-references.md#91b2febb7ce81d9c), [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#a9f9c02ecbf276e7) 함수의 인자로 사용된다.

날짜/ 시간 타입의 경우, format 문자열을 지정하지 않으면 default 값으로 처리되는데, 각 타입의 default 값은 session property인 NLS_*_FORMAT에 지정된 값이다.

- DATE: [NLS_DATE_FORMAT](../part-02-administration-manual/10-server-property.md#09118aefc816172d)
- TIMESTAMP: [NLS_TIMESTAMP_FORMAT](../part-02-administration-manual/10-server-property.md#b83b0daa42003bc4)
- TIMESTAMP WITH TIME ZONE: [NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#8cf319a54a7fec34)
- TIME: [NLS_TIME_FORMAT](../part-02-administration-manual/10-server-property.md#d78680ceba6107a9)
- TIME WITH TIME ZONE: [NLS_TIME_WITH_TIME_ZONE_FORMAT](../part-02-administration-manual/10-server-property.md#d8ed241efdbfc8ee)

NLS_*_FORMAT 값들은 [ALTER SESSION SET property_name](18-sql-references-a-b.md#2a4ad434eedabea8) 구문으로 변경할 수 있다.

Datetime format 문자열에는 표현하고자 하는 형식에 따라 여러 개의 format element를 지정할 수 있다.

**Datetime format elements**

<a id="4f511204de6f8227"></a>
<table><thead><tr><th align="center" valign="middle">Format<br>element</th><th align="center" valign="middle">TO_*<br>datetime<br>사용여부</th><th align="center" valign="middle">설명</th></tr></thead><tbody><tr><td valign="middle">-<br>/<br>,<br>.<br>;<br>:<br>"text"<br>특수문자</td><td valign="middle">Y</td><td valign="middle">지정된 위치에 format element의 문자를 반환한다.</td></tr><tr><td valign="middle">AD<br>A.D.</td><td valign="middle">Y</td><td valign="middle">서기</td></tr><tr><td valign="middle">AM<br>A.M.</td><td valign="middle">Y</td><td valign="middle">오전</td></tr><tr><td valign="middle">BC<br>B.C.</td><td valign="middle">Y</td><td valign="middle">기원전</td></tr><tr><td valign="middle">CC</td><td valign="middle">N</td><td valign="middle">세기<br>네 자리 연도 중 마지막 두 자리가 01 ~ 99 이면 처음 두 자리에 1을 더한 값을 반환한다. (예: 2005년도일 경우 21)<br>네 자리 연도 중 마지막 두 자리가 00 이면 처음 두 자리 값이 반환된다. (예: 2000년도일 경우 20)</td></tr><tr><td valign="middle">D</td><td valign="middle">Y</td><td valign="middle">일주일 중 몇 번째 날인지를 반환한다. (1 ~ 7)<br>일요일 (1) ~ 토요일 (7)</td></tr><tr><td valign="middle">DAY<br>Day<br>day</td><td valign="middle">Y</td><td valign="middle">요일을 반환한다. ( 예: SUNDAY )<br><ul><li>DAY: 모두 대문자로 반환한다.</li><li>Day: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>day: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">DD</td><td valign="middle">Y</td><td valign="middle">달의 몇 번째 날인지를 반환한다. (1 ~ 31)</td></tr><tr><td valign="middle">DDD</td><td valign="middle">Y</td><td valign="middle">연도의 몇 번째 날인지를 반환한다. (1 ~ 366)</td></tr><tr><td valign="middle">DY<br>Dy<br>dy</td><td valign="middle">Y</td><td valign="middle">요일의 약어를 반환한다. (예: SUN)<br><ul><li>DY: 모두 대문자로 반환한다.</li><li>Dy: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>dy: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">FF[1..6]</td><td valign="middle">Y</td><td valign="middle">Fractional seconds를 FF 이후에 지정한 숫자 (1 ~ 6)의 개수만큼 반환한다.<br>숫자를 지정하지 않은 경우, 기본값은 6이다. (FF는 FF6과 같다.)<br>Fractional seconds의 digit 개수가 FF 이후에 지정한 숫자보다 많으면 버림처리된다.<br>Fractional seconds의 digit 개수가 FF 이후에 지정한 숫자보다 적으면 지정된 숫자에 맞추어 0이 추가된다.<br>DATE 타입에서는 사용할 수 없다.</td></tr><tr><td valign="middle">HH<br>HH12</td><td valign="middle">Y</td><td valign="middle">시간 (1 ~ 12)</td></tr><tr><td valign="middle">HH24</td><td valign="middle">Y</td><td valign="middle">시간 (0 ~ 23)</td></tr><tr><td valign="middle">IW</td><td align="left" valign="middle">N</td><td valign="middle">ISO 8601 표준에 정의된 calendar week (1 ~ 52주 또는 1 ~ 53주)로 지정된 연도의 첫 번째 목요일이 있는 주가 첫 번째 주가 된다.<br><ul><li>Calendar week는 monday부터 시작한다.</li><li>First calendar week는 1월 4일을 포함한다.</li><li>First calendar week는 12월 29, 30, 31을 포함할 수 있다.</li><li>Last calendar week는 1월 1, 2, 3을 포함할 수 있다.</li></ul></td></tr><tr><td valign="middle">IYYY</td><td align="left" valign="middle">N</td><td valign="middle">ISO 8601 표준에 정의된 calendar week를 수용하는 4자리 연도이다.</td></tr><tr><td valign="middle">IYY<br>IY<br>I</td><td align="left" valign="middle">N</td><td valign="middle">ISO 8601 표준에 정의된 calendar week를 수용하는 3자리 연도이다.<br>ISO 8601 표준에 정의된 calendar week를 수용하는 2자리 연도이다.<br>ISO 8601 표준에 정의된 calendar week를 수용하는 1자리 연도이다.</td></tr><tr><td valign="middle">J</td><td valign="middle">Y</td><td valign="middle">BC 4714-11-24 일부터 경과된 날짜를 반환한다.</td></tr><tr><td valign="middle">MI</td><td valign="middle">Y</td><td valign="middle">분 (0 ~ 59)</td></tr><tr><td valign="middle">MM</td><td valign="middle">Y</td><td valign="middle">월 (01 ~ 12), 1월 (01) ~ 12월 (12)</td></tr><tr><td valign="middle">MON<br>Mon<br>mon</td><td valign="middle">Y</td><td valign="middle">월의 약어 (예: JAN ) 이다.<br><ul><li>MON: 모두 대문자로 반환한다.</li><li>Mon: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>mon: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">MONTH<br>Month<br>month</td><td valign="middle">Y</td><td valign="middle">월의 이름 (예: JANUARY) 이다.<br><ul><li>MONTH: 모두 대문자로 반환한다.</li><li>Month: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>month: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">PM<br>P.M.</td><td valign="middle">Y</td><td valign="middle">오후</td></tr><tr><td valign="middle">Q</td><td valign="middle">N</td><td valign="middle">연도의 분기 (1 ~ 4) 이다.<br>1월에서 3월 (1) ~ 10월에서 12월 (4) 이다.</td></tr><tr><td valign="middle">RM<br>Rm<br>rm</td><td valign="middle">Y</td><td valign="middle">월을 로마숫자로 반환한다. (예: I)<br><ul><li>RM: 모두 대문자로 반환한다.</li><li>Rm: 첫 번째 문자만 대문자로 반환하고 그 외는 소문자로 반환한다.</li><li>rm: 모두 소문자로 반환한다.</li></ul></td></tr><tr><td valign="middle">RR</td><td valign="middle">Y</td><td valign="middle">조정된 두 자리 연도이다.<br>RR로 표현된 두 자리 연도를 네 자리 연도로 표현하는 방법은 다음과 같다.<br><ul><li>RR로 표현된 두 자리 연도가 00 ~ 49인 경우<br><ul><li>현재 연도의 마지막 두 자리가 00 ~ 50 이면,<br><ul><li>현재 연도의 처음 두 자리와 RR로 표현된 두 자리 연도</li></ul></li><li>현재 연도의 마지막 두 자리가 51 ~ 99 이면,<br><ul><li>(현재 연도의 처음 두 자리 + 1)와 RR로 표현된 두 자리 연도</li></ul></li></ul></li><li>RR로 표현된 두 자리 연도가 50 ~ 99 인 경우<br><ul><li>현재 연도의 마지막 두 자리가 00 ~ 50 이면,<br><ul><li>(현재 연도의 처음 두 자리 - 1 )와 RR로 표현된 두 자리 연도</li></ul></li><li>현재 연도의 마지막 두 자리가 51 ~ 99 이면,<br><ul><li>현재 연도의 처음 두 자리와 RR로 표현된 두 자리 연도</li></ul></li></ul></li></ul></td></tr><tr><td valign="middle">RRRR</td><td valign="middle">Y</td><td valign="middle">조정된 네 자리 연도이다.<br>네 자리 또는 두 자리로 입력받을 수 있다.<br>두 자리로 입력받을 경우, RR과 동일하게 처리된다.</td></tr><tr><td valign="middle">SS</td><td valign="middle">Y</td><td valign="middle">초 (0 ~ 59)</td></tr><tr><td valign="middle">SSSSS</td><td valign="middle">Y</td><td valign="middle">지난 자정을 기준으로 경과된 초 (0 ~ 86399) 이다.</td></tr><tr><td valign="middle">TZH</td><td valign="middle">Y</td><td valign="middle">Time zone hour 이다.<br>DATE, TIMESTAMP, TIME 타입에서는 사용할 수 없고, TIMESTAMP WITH TIME ZONE, TIME WITH TIME ZONE 타입에서만 사용할 수 있다.</td></tr><tr><td valign="middle">TZM</td><td valign="middle">Y</td><td valign="middle">Time zone minute 이다.<br>DATE, TIMESTAMP, TIME 타입에서는 사용할 수 없고, TIMESTAMP WITH TIME ZONE, TIME WITH TIME ZONE 타입에서만 사용할 수 있다.</td></tr><tr><td valign="middle">WW</td><td valign="middle">N</td><td valign="middle">연도의 몇 번째 주 (1 ~ 53) 인지를 반환한다.<br>첫 번째 주 1은 1월 1일부터 7일까지이다.</td></tr><tr><td valign="middle">W</td><td valign="middle">N</td><td valign="middle">월의 몇 번째 주 (1 ~ 5)인지 반환한다.<br>첫 번째 주 1은 월의 1일부터 7일까지이다.</td></tr><tr><td valign="middle">Y,YYY</td><td valign="middle">Y</td><td valign="middle">Comma가 포함된 Y,YYY 형식의 연도를 반환한다.</td></tr><tr><td valign="middle">YYYY<br>SYYYY</td><td valign="middle">Y</td><td valign="middle">네자리 연도이다.<br>SYYYY는 연도의 부호를 표기한다.<br><ul><li>BC인 경우 '-'로 , AD인 경우 ' ' 로 표기된다.</li></ul></td></tr><tr><td valign="middle">YYY<br>YY<br>Y</td><td valign="middle">Y</td><td valign="middle"><ul><li>YYY: 현재 연도의 마지막 3자리 연도이다.</li><li>YY: 현재 연도의 마지막 2자리 연도이다.</li><li>Y: 현재 연도의 마지막 1자리 연도이다.</li></ul></td></tr></tbody></table>

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
  • TO_CHAR( TO_DATE( '2000-01-01', 'SYYYY-MM-DD' ), 'SYYYY' )
    ==> ' 2000'

* YYY  • TO_CHAR( TO_DATE( '012-07-15', 'YYY-MM-DD' ), 'YYY' )
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

<a id="26c6918438c54a30"></a>
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
• [Null Value](#8538e7aa0e372c44)  
• [Literals](#a98c21f632f44409)  
• [Pseudo Columns](#d11a00f1d7c6a919)  
• [Operators](#d299c729efc89f6f)  
• [Functions](#7657a2aeb9898162)

<a id="1ca64bf2a25ba919"></a>
### Boolean Value Expression

<a id="48c6c97b05562a10"></a>
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

<a id="7e18749d2f309dbc"></a>
#### 설명

&lt;boolean value expression&gt;은 boolean value를 기술한다. Boolean value를 갖는 &lt;boolean primary&gt;는 &lt;column&gt;과 &lt;condition&gt;, &lt;boolean predicand&gt;가 있다. &lt;column&gt;의 경우 BOOLEAN type으로 선언되어야 하고 CAST를 이용하여 boolean value를 반환할 수도 있다.

&lt;boolean value expression&gt;은 AND나 OR, NOT 등과 같은 논리 연산자와 함께 사용할 수 있으며 boolean value만의 연산자인 IS, IS NOT을 지원한다.

&lt;boolean test&gt;에 기술된 IS, IS NOT 연산자는 &lt;boolean primary&gt;에 기술된 boolean value가 &lt;truth value&gt;인 TRUE, FALSE, UNKNOWN 중 하나와 일치하는지 여부를 판단한다.

자세한 내용은 [Conditions](#15df5544af4a1a35)를 참조한다.

<a id="1417e623d63b30be"></a>
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

<a id="2633f85220fe5028"></a>
### CASE Expression

<a id="1d277003c3e6bfb2"></a>
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

<a id="0739ce691c59503d"></a>
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

THEN 또는 ELSE 절의 result에 여러 type이 오는 경우, [결과 타입 조합 규칙](#e881713e04641bea)에 따라 result type을 결정한다.

자세한 내용은 다음을 참조한다.  
• [COALESCE](17-built-in-function-references.md#04470874956922ee)  
• [NULLIF](17-built-in-function-references.md#5c39f8c5b46c9f0c)

<a id="29843e6d391adc21"></a>
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

<a id="3efabbd964b67a26"></a>
### CAST specification

<a id="9d41250e632bbe44"></a>
#### 구문

```
CAST( expression AS data_type )
```

<a id="5e208c9ec17de732"></a>
#### 설명

CAST는 expression의 데이터 타입을 지정된 data_type의 데이터 타입으로 변환한다.

<a id="78273bcbaa506a12"></a>
#### 사용 예

```
gSQL> SELECT CAST( '1-2' AS INTERVAL YEAR TO MONTH ) AS RESULT FROM DUAL;  
RESULT
------
+01-02
1 row selected.
```

<a id="f8d781cc1f437dc9"></a>
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

<a id="fec51269bcb9cc7a"></a>
### 호환성

Expression에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="2eb132cdb3a86a96"></a>
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
| T121 | WITH (excluding RECURSIVE) in query expression | O |
| T581 | Regular expression substring function | X |

<a id="d11a00f1d7c6a919"></a>
## Pseudo Columns

Pseudo column은 function과 유사하지만, pseudo column을 수행할 때 row 단위로 매번 다른 값을 반환할 수 있다는 점에서 table의 column과도 유사하다.

**지원되는 pseudo column**

<a id="0756a2e153edfe99"></a>
<table><tbody><tr><th align="center">이름</th><th align="center">설명</th><th align="center">참고</th></tr><tr><td align="left" valign="middle">CURRVAL</td><td align="left" valign="middle">Sequence와 관련있는 pseudo column이다.</td><td align="left" valign="middle"><a href="17-built-in-function-references.md#2bee070f9c29bf65">CURRVAL</a></td></tr><tr><td align="left" valign="middle">NEXTVAL</td><td align="left" valign="middle">Sequence와 관련있는 pseudo column이다.</td><td align="left" valign="middle"><a href="17-built-in-function-references.md#608a9268f6f53c18">NEXTVAL</a></td></tr><tr><td align="left" valign="middle">ROWNUM</td><td align="left" valign="middle">조건을 만족하는 row의 번호이다.</td><td align="left" valign="middle"><a href="17-built-in-function-references.md#3cb51993ddf55ab0">ROWNUM</a></td></tr><tr><td align="left" valign="middle">ROWID</td><td align="left" valign="middle">데이터베이스 내의 레코드 식별자를 반환한다.</td><td align="left" valign="middle"><a href="#d32d53d2575416a5">ROWID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_GROUP_ID</td><td align="left" valign="middle">레코드가 저장된 group의 식별자를 반환한다.</td><td align="left" valign="middle"><a href="#13198547de13bca1">CLUSTER_GROUP_ID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_MEMBER_ID</td><td align="left" valign="middle">레코드가 저장된 member의 식별자를 반환한다.</td><td align="left" valign="middle"><a href="#444b1c344fa44f89">CLUSTER_MEMBER_ID Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_GROUP_NAME</td><td align="left" valign="middle">레코드가 저장된 group의 이름을 반환한다.</td><td align="left" valign="middle"><a href="#65ee967b590044af">CLUSTER_GROUP_NAME Pseudo Column</a></td></tr><tr><td align="left" valign="middle">CLUSTER_MEMBER_NAME</td><td align="left" valign="middle">레코드가 저장된 member의 이름을 반환한다.</td><td align="left" valign="middle"><a href="#ca58b94136f72354">CLUSTER_MEMBER_NAME Pseudo Column</a></td></tr><tr><td valign="middle">CLUSTER_SHARD_ID</td><td valign="middle">레코드가 저장된 shard의 식별자를 반환한다.</td><td valign="middle"><a href="#1927c9ea85226403">CLUSTER_SHARD_ID Pseudo Column</a></td></tr></tbody></table>

<a id="d32d53d2575416a5"></a>
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

자세한 내용은 [ROWID](16-built-in-data-type-references.md#20b3d19ae7ac61d4), [ROWID-related Functions](#249d20f3917a7eae)를 참조한다.

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

<a id="13198547de13bca1"></a>
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

<a id="444b1c344fa44f89"></a>
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

<a id="65ee967b590044af"></a>
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

<a id="ca58b94136f72354"></a>
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

<a id="1927c9ea85226403"></a>
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

<a id="8359b3865395fec5"></a>
### 호환성

Pseudo column에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="58a33438392cc8b2"></a>
<table><tbody><tr><th align="center">&nbsp;Feature ID</th><th align="center">&nbsp;설명</th><th align="center">&nbsp;지원 여부</th></tr><tr><td align="left">T176</td><td align="left">Sequence generator support</td><td align="center">O</td></tr><tr><td align="left">T177</td><td align="left">&nbsp;Sequence generator support: simple restart option</td><td align="center">O</td></tr></tbody></table>

<a id="d299c729efc89f6f"></a>
## Operators

Operator는 구문상에서 하나 이상의 특정 기호 또는 keyword로 표현되며, 하나 이상의 argument들을 가지고 기능을 수행한다.

Operator에는 다음과 같이 다양한 형태가 있다.  
• Arithmetic operator  
• Concatenation operator  
• Set operator

<a id="b1a8ea64fa264070"></a>
### Arithmetic Operator

<a id="6db73376f6d13fcb"></a>
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

<a id="a58c20a65bd4d376"></a>
#### 설명

Arithmetic operator는 숫자형, 날짜/ 시간, INTERVAL 타입의 산술 연산을 수행한다.

Arithmetic operator의 우선순위는 다음과 같다.

1. [+ (POSITIVE)](17-built-in-function-references.md#bd714b8df1748510), [- (NEGATIVE)](17-built-in-function-references.md#fd8f2f96027d5c69)
2. [* (MULTIPLICATION)](17-built-in-function-references.md#8d66ed492522d26e), [/ (DIVISION)](17-built-in-function-references.md#296a41984f9582a0)
3. [+ (ADDITION)](17-built-in-function-references.md#393f2bd7ac2ec7a5), [- (SUBTRACTION)](17-built-in-function-references.md#ef4eebc1388b8004)

<a id="017011718ed24cdd"></a>
### Concatenation Operator

<a id="80a8a83008f95117"></a>
#### 구문

```
<concatenation operator> ::=
        <expression> || <expression>
```

<a id="8a58b445b2c9b7a9"></a>
#### 설명

Concatenation operator는 CHARACTER STRING 타입이나 BINARY STRING 타입의 value 사이를 연결한 문자열을 반환한다.  
자세한 내용은 [|| (CONCATENATE)](17-built-in-function-references.md#30b41dd69ad4319b), [CONCATENATE](17-built-in-function-references.md#f86aa5c3d97dc300)를 참조한다.

<a id="2b63450df16dd248"></a>
### Set Operator

<a id="3cd6dbcbb3ed6a37"></a>
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

<a id="86941872344ff63f"></a>
#### 설명

[set operator](20-sql-references-h-z.md#8fd806f5930143e4)는 부질의 (subquery) 결과들에 대한 집합 (set) 연산을 수행한다.

INTERSECT ALL/ DISTINCT는 다른 set operator 보다 우선한다.

**Set operators**

<a id="31d03d0583ecca0c"></a>
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

<a id="0d2d6f185ee15bae"></a>
### 호환성

Operator에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="aefd9eae1a58d4ba"></a>
<table><tbody><tr><th align="center">Feature ID</th><th align="center">설명</th><th align="center">지원 여부</th></tr><tr><td align="left" valign="middle">E011-04</td><td align="left" valign="middle">Arithmetic operators</td><td align="center" valign="middle">O</td></tr><tr><td valign="middle">E021-07</td><td valign="middle">Character concatenation</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-01</td><td align="left" valign="middle">UNION DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-02</td><td align="left" valign="middle">UNION ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-03</td><td align="left" valign="middle">EXCEPT DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-05</td><td align="left" valign="middle">Columns combined via table operators need not have exactly the same data type</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">E071-06</td><td align="left" valign="middle">Table operators in subqueries</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F041-08</td><td align="left" valign="middle">All comparison operators are supported (rather than just =)</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F303</td><td align="left" valign="middle">INTERSECT DISTINCT table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F305</td><td align="left" valign="middle">INTERSECT ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F304</td><td align="left" valign="middle">EXCEPT ALL table operator</td><td align="center" valign="middle">O</td></tr><tr><td align="left" valign="middle">F846</td><td align="left" valign="middle">Octet support in regular expression operators</td><td align="center" valign="middle">X</td></tr><tr><td align="left" valign="middle">J571</td><td align="left" valign="middle">NEW operator</td><td align="center" valign="middle">X</td></tr></tbody></table>

<a id="7657a2aeb9898162"></a>
## Functions

Operator와 기능상으로는 유사하지만, function은 이름 뒤에 괄호를 사용하여 argument들을 명시한다.   
Function은 0개 이상의 argument를 포함할 수 있다.

Function 형태는 다음과 같이 구분된다.  
• Single row function  
• Aggregate function

<a id="2014a347fc85178f"></a>
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
- Statistics information function

<a id="78abaeb07312de17"></a>
#### Numeric Functions

Numeric function은 숫자형 값을 입력받아 숫자형 결과를 반환하는 function이다.

Numeric function의 종류는 다음과 같다.

- [ABS](17-built-in-function-references.md#49e1ba0580f64e62)
- [ACOS](17-built-in-function-references.md#af8eaec1ed5ab4c0)
- [ASIN](17-built-in-function-references.md#fc3b02e1549e5dab)
- [ATAN](17-built-in-function-references.md#31056f39ac4ea50f)
- [ATAN2](17-built-in-function-references.md#afe54e7ea18a7c26)
- [BITAND](17-built-in-function-references.md#0fe01d5c696eb761) 
- [BITNOT](17-built-in-function-references.md#b7e603a350a417a7)
- [BITOR](17-built-in-function-references.md#d1d1fc67acccbf08)
- [BITXOR](17-built-in-function-references.md#f2d55a750c989c84)
- [CBRT](17-built-in-function-references.md#b61e9231dbfbd8fc)
- [CEIL](17-built-in-function-references.md#fb759ce74d51cda7)
- [COS](17-built-in-function-references.md#550b8141a8dabe36) 
- [COT](17-built-in-function-references.md#23f1271a3371704b)
- [DEGREES](17-built-in-function-references.md#17a832a9787fdb0e)
- [EXP](17-built-in-function-references.md#652cd3b0ced6bc32)
- [FACTORIAL](17-built-in-function-references.md#96e098f688ced383)
- [FLOOR](17-built-in-function-references.md#37b8b2a8227612bc) 
- [LN](17-built-in-function-references.md#1af3c5c68fbbc382)
- [LOG](17-built-in-function-references.md#ab56736fb79f42fc)
- [MOD](17-built-in-function-references.md#b6614f54ea98c663) 
- [PI](17-built-in-function-references.md#ef00931fa68bd858)
- [POWER](17-built-in-function-references.md#490f1f0ac5cc3ec9)
- [RADIANS](17-built-in-function-references.md#20f440225faf5f03)
- [RANDOM](17-built-in-function-references.md#ebddf91f17ff9c2d)
- [ROUND( number )](17-built-in-function-references.md#d84fc397d10c7016)
- [SHARD_ID](17-built-in-function-references.md#f9b439ced7819257)
- [SHIFT_LEFT](17-built-in-function-references.md#2126c43ce8408f3a)
- [SHIFT_RIGHT](17-built-in-function-references.md#c3159c8b187b7228)
- [SIGN](17-built-in-function-references.md#4f30e22deda50e48)
- [SIN](17-built-in-function-references.md#347ea90359f89d0e)
- [SQRT](17-built-in-function-references.md#f0c1c8a3477d6d6f)
- [TAN](17-built-in-function-references.md#b8421f4ba9b9b484)
- [TRUNC( number )](17-built-in-function-references.md#c9dc8637f4717039)
- [WIDTH_BUCKET](17-built-in-function-references.md#3ca6f7a7fdf7ba43)

<a id="0003a48ea3f7f062"></a>
#### Character String Functions Returning Character Values

Character string functions returning character values는 CHARACTER STRING형 값을 입력받아 CHARACTER STRING형 결과를 반환하는 function이다.

Character string functions returning character value의 종류는 다음과 같다.

- [CHR](17-built-in-function-references.md#465c03a9b42080cd)
- [CONCAT](17-built-in-function-references.md#9242750a22d6bb53)
- [CONCATENATE](17-built-in-function-references.md#f86aa5c3d97dc300)
- [INITCAP](17-built-in-function-references.md#405c8f5a4181712d)
- [LOWER](17-built-in-function-references.md#03c55163b33ff21c)
- [LPAD](17-built-in-function-references.md#57c2aeb569da8a55)
- [LTRIM](17-built-in-function-references.md#c1673b54eb0d99bd)
- [OVERLAY](17-built-in-function-references.md#f9762257927cdd90)
- [REGEXP_REPLACE](17-built-in-function-references.md#cbbf5abf3bd78123)
- [REGEXP_SUBSTR](17-built-in-function-references.md#cefe81f21ed82b68)
- [REPEAT](17-built-in-function-references.md#1f821bcbb4581842) 
- [REPLACE](17-built-in-function-references.md#7cbb3ba7fc25e00f)
- [REVERSE](17-built-in-function-references.md#c6f1ca3690636f48)
- [RPAD](17-built-in-function-references.md#103a6121afa30d89)
- [RTRIM](17-built-in-function-references.md#6209e4959fd4b648)
- [SPLIT_PART](17-built-in-function-references.md#e5c09988e44a0ee4)
- [SUBSTR](17-built-in-function-references.md#dd65acd21add6abf)
- [SUBSTRB](17-built-in-function-references.md#1816902f3ae32864)
- [TRANSLATE](17-built-in-function-references.md#2cfe96c173495d9a)
- [TRIM](17-built-in-function-references.md#06cfed983d14eaf0)
- [UPPER](17-built-in-function-references.md#f76fb8f8d18ecc4d)

<a id="0c0e35ea9c0fbec6"></a>
#### Character String Functions Returning Number Values

Character string functions returning number value는 CHARACTER STRING형 값을 입력받아 숫자형 결과를 반환하는 function이다.

Character string functions returning number value의 종류는 다음과 같다.

- [ASCII](17-built-in-function-references.md#9f1ebbc3fa98c148)
- [BIT_LENGTH](17-built-in-function-references.md#ae4da9b7765fd53d)
- [BYTE_LENGTH](17-built-in-function-references.md#2e9fab2319460d39)
- [CHAR_LENGTH](17-built-in-function-references.md#419a706c1c7cf97a)
- [INSTR](17-built-in-function-references.md#95f0d155a49249e9)
- [LENGTH](17-built-in-function-references.md#05398af639dccbdf)
- [LENGTHB](17-built-in-function-references.md#601cb51b0994464d)
- [OCTET_LENGTH](17-built-in-function-references.md#ebe17e037d8d8ea6)
- [POSITION](17-built-in-function-references.md#8ea4feaa9605d463)
- [REGEXP_COUNT](17-built-in-function-references.md#5a9c61acf90fd5c1)
- [REGEXP_INSTR](17-built-in-function-references.md#3a5d8345b833199f)

<a id="5088723c94ef9ea8"></a>
#### Datetime Functions

Datetime function은 DATE/ TIME/ TIMESTAMP/ INTERVAL 형 값을 입력받아 DATE/ TIME/ TIMESTAMP/ INTERVAL형 결과를 반환하는 function이다.

Datetime function의 종류는 다음과 같다.

- [ADDDATE](17-built-in-function-references.md#697ea8afd9a5c84e)
- [ADDTIME](17-built-in-function-references.md#ae8af9cb0c29ff45)
- [ADD_MONTHS](17-built-in-function-references.md#2875ddd3ff069dd3)
- [DATEADD](17-built-in-function-references.md#64772be178cb6dad)
- [DATEDIFF](17-built-in-function-references.md#2166fdf4962b7a1d)
- [DATE_ADD](17-built-in-function-references.md#93f2a2ab0fe05576)
- [DATE_PART](17-built-in-function-references.md#052dff56ca55ff3f)
- [EXTRACT](17-built-in-function-references.md#c3ddc90dd21782b7) 
- [FROM_TZ](17-built-in-function-references.md#b8e235f519cbbf4f)
- [LAST_DAY](17-built-in-function-references.md#54b97cb12add7e5f)
- [MONTHS_BETWEEN](17-built-in-function-references.md#d1392f141e83ac3a)

<a id="c17415d95c858d93"></a>
#### General Comparison Functions

General comparison function은 value 집합에 대한 최소값 또는 최대값을 구하는 function이다.

General comparison function의 종류는 다음과 같다.

- [GREATEST](17-built-in-function-references.md#2c4f5032fdd3a378)
- [LEAST](17-built-in-function-references.md#72380c9a67173fb9)

<a id="68961017da2f76ac"></a>
#### Conversion Functions

Conversion function은 특정 data type으로의 값을 설정하는 function이다.

Conversion function 종류는 다음과 같다.

- [NUMTODSINTERVAL](17-built-in-function-references.md#ec0c8757a80dc2bb)
- [NUMTOYMINTERVAL](17-built-in-function-references.md#b5c581181c57d3ff)
- [TO_CHAR( datetime )](17-built-in-function-references.md#49e380b1da61d32b)
- [TO_CHAR( number )](17-built-in-function-references.md#69fde4657a756aff)
- [TO_DATE](17-built-in-function-references.md#e1ae1f9cb408151d)
- [TO_NATIVE_BIGINT](17-built-in-function-references.md#860aa4f498a985ca)
- [TO_NATIVE_DOUBLE](17-built-in-function-references.md#b6f99a7754f9a09a)
- [TO_NATIVE_INTEGER](17-built-in-function-references.md#f4ea0087d7690777)
- [TO_NATIVE_REAL](17-built-in-function-references.md#9c39d911dce66749)
- [TO_NATIVE_SMALLINT](17-built-in-function-references.md#802fe8044515d1c9)
- [TO_NUMBER](17-built-in-function-references.md#5b93653f4677d64c)
- [TO_TIME](17-built-in-function-references.md#91b2febb7ce81d9c)
- [TO_TIME_TZ](17-built-in-function-references.md#09815ff744a36043)
- [TO_TIME_WITH_TIME_ZONE](17-built-in-function-references.md#a9f9c02ecbf276e7)
- [TO_TIMESTAMP](17-built-in-function-references.md#48f2f9c2be120650)
- [TO_TIMESTAMP_TZ](17-built-in-function-references.md#06416af7336d7daf)
- [TO_TIMESTAMP_WITH_TIME_ZONE](17-built-in-function-references.md#667ef9b2a77a0436)

<a id="4f77b386118750ec"></a>
#### Conditional Functions

Conditional function은 조건에 따라 특정값을 결과로 반환하는 function이다.

Conditional function의 종류는 다음과 같다.

- [CASE2](17-built-in-function-references.md#57df539807682278)
- [DECODE](17-built-in-function-references.md#c951d8e927911955)

<a id="5618c8a863aa72d3"></a>
#### NULL-related Functions

NULL-related function은 입력값이 NULL값인지 여부에 따라 특정값을 결과로 반환하는 function이다.

NULL-related function의 종류는 다음과 같다.

- [COALESCE](17-built-in-function-references.md#04470874956922ee)
- [NULLIF](17-built-in-function-references.md#5c39f8c5b46c9f0c)
- [NVL](17-built-in-function-references.md#00a4fa9fc6ce087b)
- [NVL2](17-built-in-function-references.md#efc7c9afd4e32b88)

<a id="249d20f3917a7eae"></a>
#### ROWID-related Functions

ROWID-related function은 ROWID에 대한 정보를 얻기 위한 function이다.

ROWID-related function의 종류는 다음과 같다.

- Standalone에서 유효한 function
    - [ROWID_OBJECT_ID](17-built-in-function-references.md#4ee48c1d18ede954)
    - [ROWID_TABLESPACE_ID](17-built-in-function-references.md#275b71b4fbb14ee1)
    - [ROWID_PAGE_ID](17-built-in-function-references.md#6cc0447e41b24c0b)
    - [ROWID_ROW_NUMBER](17-built-in-function-references.md#5906bacda936fa19)

- Cluster에서 유효한 function
    - [ROWID_GRID_BLOCK_ID](17-built-in-function-references.md#6bb3f3b9e9c6f50e)
    - [ROWID_GRID_BLOCK_SEQ](17-built-in-function-references.md#cd8883c9cf87b7f3)
    - [ROWID_MEMBER_ID](17-built-in-function-references.md#7acaab2066b99338)
    - [ROWID_SHARD_ID](17-built-in-function-references.md#140ec83744716830)

<a id="9da7f0061aa0f33c"></a>
#### Encryption Functions

Encryption function은 주어진 plain text를 특정 알고리즘으로 encrypt/ decrypt 하거나 hash한 결과값을 반환하는 function이다.

Encryption function의 종류는 다음과 같다.

- [DIGEST](17-built-in-function-references.md#f38a99e71e7b4e26)
- [HASH32](17-built-in-function-references.md#3b5f99df99c16049)

<a id="a260fa2f0fb1638c"></a>
#### System Information Functions

System information function은 session과 system에 대한 정보를 얻기 위한 function이다.

System information function의 종류는 다음과 같다.

- [CLOCK_DATE](17-built-in-function-references.md#8d4aa10dcf8c0deb)
- [CLOCK_LOCALTIME](17-built-in-function-references.md#a1e867d976dcf8d3)
- [CLOCK_LOCALTIMESTAMP](17-built-in-function-references.md#c99ee0e195480e4a)
- [CURRENT_CATALOG](17-built-in-function-references.md#91d13fe4a6f153de)
- [CURRENT_DATE](17-built-in-function-references.md#072b484139124e1d)
- [CURRENT_ROLE](17-built-in-function-references.md#84f3b85ed9383e58)
- [CURRENT_SCHEMA](17-built-in-function-references.md#4d350b96f9d2a1a4)
- [CURRENT_TIME](17-built-in-function-references.md#b857364923db6e01)
- [CURRENT_TIMESTAMP](17-built-in-function-references.md#168559e424362489)
- [CURRENT_USER](17-built-in-function-references.md#b74ed317d4b03cd1)
- [LAST_IDENTITY_VALUE](17-built-in-function-references.md#0a4be64485ed5393)
- [LOCAL_MEMBER_POSITION](17-built-in-function-references.md#afd5f1462dcfbc60)
- [LOCALTIME](17-built-in-function-references.md#29a1e06e2f61c0cf)
- [LOCALTIMESTAMP](17-built-in-function-references.md#b90cd72f5e69bd64)
- [LOGON_USER](17-built-in-function-references.md#4b8d5f7b599da219)
- [SESSION_ID](17-built-in-function-references.md#f57af3ac6abb0112)
- [SESSION_SERIAL](17-built-in-function-references.md#fe0cf26aca2f050a)
- [SESSION_USER](17-built-in-function-references.md#e576d54163cde37e)
- [SESSIONTIMEZONE](17-built-in-function-references.md#3c731030f2080f50)
- [STATEMENT_DATE](17-built-in-function-references.md#bcca3fc8f6bc7136)
- [STATEMENT_LOCALTIME](17-built-in-function-references.md#0494f700ca96575f)
- [STATEMENT_LOCALTIMESTAMP](17-built-in-function-references.md#65aa4ab1672611f0)
- [STATEMENT_TIME](17-built-in-function-references.md#4602661083943637)
- [STATEMENT_TIMESTAMP](17-built-in-function-references.md#e4324e327ac60b19)
- [STATEMENT_VIEW_SCN](17-built-in-function-references.md#75d041f10dddde72)
- [SYSDATE](17-built-in-function-references.md#082d06d73d6c99a7)
- [SYSTIME](17-built-in-function-references.md#2fe60c11f4576cb8)
- [SYSTIMESTAMP](17-built-in-function-references.md#85bb49d3d48c5c50)
- [TRANSACTION_DATE](17-built-in-function-references.md#9b10ec80b2a03980)
- [TRANSACTION_LOCALTIME](17-built-in-function-references.md#4a034746c1090f4f)
- [TRANSACTION_LOCALTIMESTAMP](17-built-in-function-references.md#ff99817aedcfa218)
- [TRANSACTION_TIME](17-built-in-function-references.md#9ca27a5be131a69d)
- [TRANSACTION_TIMESTAMP](17-built-in-function-references.md#3b4cff9a30424ac1)
- [USER_ID](17-built-in-function-references.md#1021d52d545afbb0)
- [VERSION](17-built-in-function-references.md#de255a4e725990b5)

<a id="fffe0009d4c9c8e7"></a>
#### Statistics Information function

Statistics information function은 object에 대한 정보를 조회하는 function 이다.

Statistics information function의 종류는 다음과 같다.

- [TABLE_PHYSICAL_STATS](17-built-in-function-references.md#b6629b53c0b75cd5)
- [INDEX_PHYSICAL_STATS](17-built-in-function-references.md#8ecc511dde1fe96e)
- [GSI_PHYSICAL_STATS](17-built-in-function-references.md#07153d77d1b51d4a)

<a id="67ffc000313e5858"></a>
### Aggregate Function

Aggregate function은 여러 row에 대해 하나의 결과 row를 생성하는 function이다.

Aggregation function의 종류는 다음과 같다.

- [COUNT](17-built-in-function-references.md#afd0d6dd3d81826b)
- [COUNT(*)](17-built-in-function-references.md#9ba48f32b5d0883b)
- [SUM](17-built-in-function-references.md#ec30d624521e1798)
- [AVG](17-built-in-function-references.md#1a081b007cc42414)
- [MIN](17-built-in-function-references.md#e9ae230f46525210)
- [MAX](17-built-in-function-references.md#314460f16bf53fb9)
- [STDDEV](17-built-in-function-references.md#f0420e3d95a59bdb)
- [STDDEV_POP](17-built-in-function-references.md#0a4728846b8e14ba)
- [STDDEV_SAMP](17-built-in-function-references.md#76f1f4a01a39aaf0)
- [VAR_POP](17-built-in-function-references.md#3c837bf115b1008a)
- [VAR_SAMP](17-built-in-function-references.md#dc962b0b48f04aed)
- [VARIANCE](17-built-in-function-references.md#ab8b6a136b382960)
- [APPROX_COUNT_DISTINCT](17-built-in-function-references.md#4bd83f1213792549)

<a id="87f34e385804bc26"></a>
### Window Function

정의된 레코드 범위에 대한 function의 결과를 반환하는 함수이다.

정의된 레코드 범위를 window 라고 하며, OVER &lt;window name or specification&gt;에 수행 범위를 정의한다.

Window에 대한 자세한 내용은 [window clause](20-sql-references-h-z.md#f9eea6d4ba5feccc)를 참조한다.

그룹 내 각각의 레코드는 window (정의된 레코드 범위)에 대해 window function을 수행한 결과를 갖는다. 따라서 window function은 aggregate function과 달리 각 그룹에 대해 여러 개의 레코드를 반환한다.

Window function은 select list와 order by clause에 기술할 수 있다.

Window function의 종류는 다음과 같다.

- [AVG() OVER](17-built-in-function-references.md#f7ea4f1a7c386ef9)
- [CORR() OVER](17-built-in-function-references.md#f6965ab879be69b9)
- [COUNT() OVER](17-built-in-function-references.md#582dda281cd4fe2f)
- [COUNT(*) OVER](17-built-in-function-references.md#df6e1de4166a2f4e)
- [COVAR_POP() OVER](17-built-in-function-references.md#8531f86ea30bc50f)
- [COVAR_SAMP() OVER](17-built-in-function-references.md#220b7c02b596f959)
- [CUME_DIST() OVER](17-built-in-function-references.md#46ea2ec9c3721407)
- [DENSE_RANK() OVER](17-built-in-function-references.md#d3e8703b5b1b8331)
- [FIRST() OVER](17-built-in-function-references.md#4981ab75e0efea25)
- [FIRST_VALUE() OVER](17-built-in-function-references.md#84e97a097c1ee6bf)
- [LAG() OVER](17-built-in-function-references.md#4918b9387a19231b)
- [LAST() OVER](17-built-in-function-references.md#76b6d58617b4030b)
- [LAST_VALUE() OVER](17-built-in-function-references.md#1b557a326f8bb6ae)
- [LEAD() OVER](17-built-in-function-references.md#724d528c51441dae)
- [LISTAGG() OVER](17-built-in-function-references.md#102baf39aaaf238c)
- [MAX() OVER](17-built-in-function-references.md#f24a16652f711f98)
- [MEDIAN() OVER](17-built-in-function-references.md#6e2d4738fd4f25a5)
- [MIN() OVER](17-built-in-function-references.md#ba035b5b6ae776da)
- [NTH_VALUE() OVER](17-built-in-function-references.md#97b8815e3ed2ffbc)
- [NTILE() OVER](17-built-in-function-references.md#f11c1348046c4464)
- [PERCENT_RANK() OVER](17-built-in-function-references.md#1da4d29d25993dd6)
- [PERCENTILE_CONT() OVER](17-built-in-function-references.md#f8428bd33ea54be9)
- [PERCENTILE_DISC() OVER](17-built-in-function-references.md#52c5c48f4b031ee4)
- [RANK() OVER](17-built-in-function-references.md#f22ac34b9aeabc5b)
- [RATIO_TO_REPORT() OVER](17-built-in-function-references.md#8b7fe6b51af90fef)
- [REGR_AVGX() OVER](17-built-in-function-references.md#dc239c13bc818a97)
- [REGR_AVGY() OVER](17-built-in-function-references.md#0dbeeb562321f811)
- [REGR_COUNT() OVER](17-built-in-function-references.md#bc3457333732e609)
- [REGR_INTERCEPT() OVER](17-built-in-function-references.md#af3a190d5ff8ba06)
- [REGR_R2() OVER](17-built-in-function-references.md#f2419709daefb084)
- [REGR_SLOPE() OVER](17-built-in-function-references.md#55b6ea15f8a2d849)
- [REGR_SXX() OVER](17-built-in-function-references.md#0ed25bd5b207eb09)
- [REGR_SXY() OVER](17-built-in-function-references.md#467c0e80a94fbf4e)
- [REGR_SYY() OVER](17-built-in-function-references.md#ab7060c3d6b62f26)
- [ROW_NUMBER() OVER](17-built-in-function-references.md#09243273d0b502c2)
- [STDDEV() OVER](17-built-in-function-references.md#39c1758ce4105113)
- [STDDEV_POP() OVER](17-built-in-function-references.md#01c0463a3aebd337)
- [STDDEV_SAMP() OVER](17-built-in-function-references.md#2438c9326be21907)
- [STRING_AGG() OVER](17-built-in-function-references.md#15ac63821b70703c)
- [SUM() OVER](17-built-in-function-references.md#1a83ad57ee5a8705)
- [VAR_POP() OVER](17-built-in-function-references.md#99f8aaa14ba889ca)
- [VAR_SAMP() OVER](17-built-in-function-references.md#c444a0ff2efb2aae)
- [VARIANCE() OVER](17-built-in-function-references.md#75eb00197e439b14)

<a id="8fbab1f0a7f7f89e"></a>
### 호환성

Function에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="bff795e420bb46db"></a>
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
| F441 | Extended set function support | O |
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
| T321-01 | User-defined functions with no overloading | O |
| T326 | Table functions | X |
| T341 | Overloading of SQL-invoked functions and SQL-invoked procedures | X |
| T433 | Multiargument GROUPING function | X |
| T441 | ABS and MOD functions | O |
| T571 | Array-returning external SQL-invoked functions | X |
| T572 | Multiset-returning external SQL-invoked functions | X |
| T581 | Regular expression substring function | X |
| T614 | NTILE function | O |
| T615 | LEAD and LAG functions | O |
| T616 | Null treatment option for LEAD and LAG functions | O |
| T617 | FIRST_VALUE and LAST_VALUE functions | O |
| T618 | NTH_VALUE function | O |
| T619 | Nested window functions | X |
| T621 | Enhanced numeric functions | O |

<a id="15df5544af4a1a35"></a>
## Conditions

<a id="33f578a3c5b3646f"></a>
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
• Distinct condition

**Condition 우선순위**

<a id="9f97f10e06a5ac64"></a>
| 우선순위 | Condition 종류 |
| --- | --- |
| 1 | 조건절에 쓰여진 연산자들 |
| 2 | =, !=, &lt;, &gt;, &lt;=, &gt;= |
| 3 | IS [NOT] NULL, [NOT] BETWEEN,  [NOT] IN,  LIKE, EXISTS, IS [NOT] DISTINCT FROM |
| 4 | NOT |
| 5 | AND |
| 6 | OR |

<a id="3d9a2600ca60016c"></a>
### Comparison Conditions

양쪽 조건을 비교하여 TRUE, FALSE, UNKNOWN 값의 boolean 타입을 반환한다.

**Comparison condition**

<a id="d60db4bf18db4d09"></a>
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

자세한 내용은 [타입간 비교](#329e88f63daf5a67)를 참조한다.

<a id="e0f4bffb7baaa315"></a>
#### &lt; Simple Comparison Conditions &gt;

<a id="130010ab6661cd3f"></a>
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

자세한 내용은 [Scalar Subquery Expression](#f8d781cc1f437dc9)을 참조한다.

<a id="144e6b9bf7d33c4f"></a>
##### 설명

comparison_operator 양쪽에 expr_list 또는 subquery가 오는 경우, 비교되는 expr의 개수 또는 subquery target의 개수는 동일해야 한다.  
Subquery가 오는 경우, 결과 레코드는 한 건이어야 한다.

<a id="0a682d893c8f3c52"></a>
##### 사용 예

**Simple comparison condition의 예**

<a id="1ce26054cfabced7"></a>
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

<a id="8566e597aacfba36"></a>
#### &lt; Group Comparison Conditions &gt;

<a id="1e0ed403b84398b9"></a>
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

자세한 내용은 [Scalar Subquery Expression](#f8d781cc1f437dc9)을 참조한다.

<a id="ee8a4b6710b75cb5"></a>
##### 설명

comparison_operator 양쪽에 expr_list 또는 subquery가 오는 경우, 비교되는 expr의 개수 또는 subquery target의 개수는 동일해야 한다.  
comparison_operator 왼쪽에 subquery가 오는 경우, 결과 레코드는 한 건이어야 한다.  
comparison_operator 오른쪽에 subquery가 오는 경우, 결과 레코드는 여러 건일 수 있다.

<a id="506acbd77af752ed"></a>
##### 사용 예

<a id="e9ca918def4be976"></a>
<table class="table column_count_2"><caption>Group comparison condition의 예</caption><thead><tr><th class="to_center"><div>Condition</div></th><th class="to_center"><div>결과</div></th></tr></thead><tbody><tr><td class="to_left"><div>1 =any ( 1, 2, 3, 4, 5 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>1 =any ( 1, 2, null, 4, 5 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>1 =any ( 2, null, 4, 5 )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td class="to_left"><div>1 =any ( 100, 2, 3, 4, 5 )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td class="to_left"><div>1 =all ( 1, +1, 1E+0 )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>1 =all ( 1, +1, 1E+0, null )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td class="to_left"><div>1 =all ( 1, 2, 3, 4, 5 )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =any ( ( 0, 1 ), ( 1, 2 ), ( 3, 4 ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =any ( ( 0, 1 ), ( 1, 2 ), ( null, null ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =any ( ( 0, 1 ), ( 2, 3 ), ( 3, 4 ) )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =all ( ( 1, 2 ), ( +1, +2 ), ( 1E+0, 2E+0 ) )</div></td><td class="to_left"><div>TRUE</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =all ( ( 1, 2 ), ( +1, +2 ), ( null, null ) )</div></td><td class="to_left"><div>NULL</div></td></tr><tr><td class="to_left"><div>( 1, 2 ) =all ( ( 0, 1 ), ( 2, 3 ), ( 3, 4 ) )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><th class="to_left" colspan="2"><div>comparison_operator 오른쪽 subquery의 결과 레코드가 0인 경우</div></th></tr><tr><td class="to_left"><div>( 'X' ) =any ( select dummy from dual where dummy = 'Y' )</div></td><td class="to_left"><div>FALSE</div></td></tr><tr><td class="to_left"><div>( 'X' ) =all ( select dummy from dual where dummy = 'Y' )</div></td><td class="to_left"><div>TRUE</div></td></tr></tbody></table>

<a id="43b74e22686ea598"></a>
### Logical Conditions

Logical condition으로는 AND, OR, NOT이 있다.

<a id="a09e5a67cfb052f9"></a>
#### AND

<a id="03ae66ab5dfcc119"></a>
##### 구문

```
<boolean value expression> AND <boolean value expression>
```

<a id="12008f72a3024ba9"></a>
##### 설명

**AND boolean operator의 truth table**

<a id="f33799131b70749f"></a>
| AND | True | False | Unknown |
| --- | --- | --- | --- |
| True | True | False | Unknown |
| False | False | False | False |
| Unknown | Unknown | False | Unknown |

<a id="1cee0ed303db3b6d"></a>
#### OR

<a id="cac4205de69ce2f8"></a>
##### 구문

```
<boolean value expression> OR <boolean value expression>
```

<a id="d2106205c10fd091"></a>
##### 설명

**OR boolean operator의 truth table**

<a id="ffb6c068f6e7f3fa"></a>
| OR | True | False | Unknown |
| --- | --- | --- | --- |
| True | True | True | True |
| False | True | False | Unknown |
| Unknown | True | Unknown | Unknown |

<a id="789fde33e82f3b21"></a>
#### NOT

<a id="911f0eee1030668a"></a>
##### 구문

```
NOT <boolean value expression>
```

<a id="0f0b357b8cbabcd8"></a>
##### 설명

**NOT boolean operator의 truth table**

<a id="880dd846a8836ddc"></a>
| expr | NOT |
| --- | --- |
| True | False |
| False | True |
| Unknown | Unknown |

<a id="6f8b46d483534778"></a>
### Null Condition

<a id="7393ebff27a9e347"></a>
#### 구문

```
<expr> IS [NOT] NULL
```

<a id="29164d5486540c2f"></a>
#### 설명

expr의 결과가 NULL 값인지 여부를 검사한다.

**Is Null 조건의 결과표**

<a id="a2e1007eee4fb403"></a>
| expr | IS NULL | IS NOT NULL |
| --- | --- | --- |
| NULL | True | False |
| NOT NULL | False | True |

<a id="71cbcde8703ec76b"></a>
### Compound Condition

여러 조건들이 결합되어 만들어진 조건식이다.

```
compound_condition ::=
        ( condition )
      | NOT condition
      | condition < AND | OR > condition
```

<a id="8f5140ead7f7d8de"></a>
### Pattern-matching Conditions

<a id="2a77e99e87ade08b"></a>
#### LIKE Condition

<a id="eb4401fecf89f5cd"></a>
##### 구문

```
like_condition ::=
        string [NOT] LIKE pattern [ ESCAPE escape_character ]
```

<a id="90cd41733aedc551"></a>
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

pattern에 포함된 '_' 또는 '%'를 문자로 비교하고자 하는 경우, ESCAPE 절을 사용한다.  
escape_character를 지정하고, 지정된 escape_character를 pattern의 '_' 또는 '%' 앞에 기술한다.

<a id="f9e11da95b9f11d5"></a>
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

<a id="bd7439f58b8d5d07"></a>
#### REGEXP_LIKE Condition

<a id="27b705d8ee903d72"></a>
##### 구문

```
regexp_like_condition ::=
        REGEXP_LIKE ( source_string, pattern[, match_param ] )
```

<a id="077eb6b31eff688b"></a>
##### 설명

source_string 이 지정된 pattern 과 match 되는지 검사한다.

*source_string*  
검색 대상 문자 표현식으로, CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있다.

*pattern*  
regular expression (정규 표현식)으로, CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입 또는 문자 타입으로 변환될 수 있는 타입이 올 수 있다.  
512 byte까지 기술할 수 있다.  
pattern 에서 지정할 수 있는 operator는 [Regular Expression](#909ce869a4298578) 을 참조한다.

*match_param*  
function 의 기본 matching 수행 동작을 변경할 수 있는 문자 표현식으로, CHARACTER, CHARACTER VARYING, CHARACTER LONG VARYING과 같은 문자 타입이 올 수 있다.

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

<a id="75c823ea7e1ee26c"></a>
##### 사용 예

```
gSQL> 
SELECT web_street_name FROM web_site;
WEB_STREET_NAME
---------------
Dogwood Sunset 
7th            
2nd 3rd        
Hill 5th       
Cedar North    
5 rows selected.

gSQL> 
SELECT *
  FROM web_site
 WHERE REGEXP_LIKE( web_street_name, '[[:digit:]]th$' );
WEB_STREET_NAME
---------------
7th            
Hill 5th       
2 rows selected.
```

<a id="884089b2ad210a53"></a>
### BETWEEN Condition

<a id="1fa2ad6a9f7ce4bc"></a>
#### 구문

```
<between condition> ::=
   <expr1> [ NOT ] BETWEEN [ ASYMMETRIC | SYMMETRIC ] <expr2> AND <expr3>
```

<a id="922f2f2a828193c1"></a>
#### 설명

expr1이 expr2와 expr3 범위 내의 조건인지 검사한다.

ASYMMETRIC이나 SYMMETRIC이 생략된 경우, default는 ASYMMETRIC 이다.  
expr1, expr2, expr3의 data type이 다른 경우, conversion이 수행된다.  
자세한 내용은 [타입간 비교](#329e88f63daf5a67), [타입간 변환](#d9c1b23c9cbab71c)을 참조한다.

**Between 구문 동치**

<a id="6e8ee6743c5e9aef"></a>
| A | B |
| --- | --- |
| X BETWEEN ASYMMETRIC Y AND Z | X BETWEEN Y AND Z |
| X BETWEEN Y AND Z | X >= Y AND X <= Z |
| X NOT BETWEEN Y AND Z | NOT( X BETWEEN Y AND Z ) |
| X BETWEEN SYMMETRIC Y AND Z | ((X BETWEEN Y AND Z) OR (X BETWEEN Z AND Y) |
| X NOT BETWEEN SYMMETRIC Y AND Z | NOT( X BETWEEN SYMMETRIC Y AND Z ) |

<a id="3dac00359dd7c8d8"></a>
#### 사용 예

<a id="5e698a0d16ca2249"></a>
<table class="table column_count_3"><caption>Between 구문의 예</caption><thead><tr><th class="to_center" colspan="2"><div>Condition</div></th><th class="to_center"><div>결과</div></th></tr></thead><tbody><tr><td class="to_middle" rowspan="3"><div>BETWEEN [ ASYMMETRIC ]</div></td><td><div>3 BETWEEN 1 AND 5</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr><tr><td><div>NULL BETWEEN 1 AND 5
3 BETWEEN NULL AND 5
3 BETWEEN 1 AND NULL</div></td><td class="to_left to_middle"><div>NULL</div></td></tr><tr><td><div>3 BETWEEN 5 AND 1</div></td><td class="to_left to_middle"><div>FALSE</div></td></tr><tr><td class="to_middle" rowspan="3"><div>BETWEEN SYMMETRIC</div></td><td><div>3 BETWEEN SYMMETRIC 1 AND 5</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr><tr><td><div>NULL BETWEEN SYMMETRIC 1 AND 5
3 BETWEEN SYMMETRIC NULL AND 5
3 BETWEEN SYMMETRIC 1 AND NULL</div></td><td class="to_left to_middle"><div>NULL</div></td></tr><tr><td><div>3 BETWEEN SYMMETRIC 5 AND 1</div></td><td class="to_left to_middle"><div>TRUE</div></td></tr></tbody></table>

<a id="4e40c3ef8ad89ceb"></a>
### IN Condition

<a id="294e621fed4d78a1"></a>
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

<a id="510282205226d18b"></a>
#### 설명

IN condition은 =ANY와 동일한 결과를 반환한다.  
NOT IN condition은 !=ALL과 동일한 결과를 반환한다.

자세한 내용은 [Comparison Conditions](#3d9a2600ca60016c)를 참조한다.

<a id="463613b29b7dce69"></a>
#### 사용 예

**IN condition의 예**

<a id="95dec0f129c98b5e"></a>
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

<a id="711b9309d75ef91c"></a>
### EXISTS Condition

<a id="179487fe295ac9ed"></a>
#### 구문

```
exists_conditions ::= 
        EXISTS ( subquery )
```

<a id="00bfd41215d53bb9"></a>
#### 설명

Subquery의 결과 레코드 존재 유무를 검사한다.   
Subquery의 결과 레코드가 존재하면 TRUE를 반환하고, 결과 레코드가 존재하지 않으면 FALSE를 반환한다.

<a id="3e809d5a75af5315"></a>
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

<a id="d7076301923c524c"></a>
### DISTINCT Condition

<a id="806f50889a1a80e5"></a>
#### 구문

```
distinct_conditions ::= 
        <expr> IS [NOT] DISTINCT FROM <expr>
      | ( <expr_list> ) IS [NOT] DISTINCT FROM ( <expr_list> )
```

<a id="e2cdc4d8e0874353"></a>
#### 설명

Distinct condition의 피연산자는 서로 비교 가능한 타입이어야 한다.  
피연산자로 &lt;expr_list&gt;가 오는 경우, 같은 position의 데이터가 비교 대상이 된다.

Distinct condition의 피연산자로 모두 not null value가 오는 경우,  
is distinct from 은 not equal(!=) 과 같고   
is not distinct from 은 eqaul(=) 과 같은 결과를 반환한다.

Distinct condition은 NULL value를 unknown이 아닌 일반 데이터로 처리한다는 점이 다른 비교 연산자와의 차이점이다.

- IS DISTINCT FROM
    - 피연산자 모두 NULL인 경우
        - NULL is distinct from NULL => FALSE
    - 피연산자 중 하나가 NULL인 경우
        - NULL is distinct from 1 => TRUE
        - 1 is distinct from NULL => TRUE
    - 피연산자 모두 not NULL인 경우
        - 1 is distinct from 1 => FALSE
        - 1 is distinct from 2 => TRUE
    - 피연산자로 &lt;expr_list&gt;가 오는 경우
        - ( 1, 2, 3 ) is distinct from ( 1, 2, 3 ) => FALSE
        - ( 1, 2, 3 ) is distinct from ( 1, 3, 3 ) => TRUE
        - ( 1, 2, 3 ) is distinct from ( 4, 5, 6 ) => TRUE

- IS NOT DISTINCT FROM
    - 피연산자 모두 NULL인 경우
        - NULL is not distinct from NULL => TRUE
    - 피연산자 중 하나가 NULL인 경우
        - NULL is not distinct from 1 => FALSE
        - 1 is not distinct from NULL => FALSE
    - 피연산자 모두 not NULL인 경우
        - 1 is not distinct from 1 => TRUE
        - 1 is not distinct from 2 => FALSE
    - 피연산자로 &lt;expr_list&gt;가 오는 경우
        - ( 1, 2, 3 ) is not distinct from ( 1, 2, 3 ) => TRUE
        - ( 1, 2, 3 ) is not distinct from ( 1, 3, 3 ) => FALSE
        - ( 1, 2, 3 ) is not distinct from ( 4, 5, 6 ) => FALSE

<a id="29d5a555addf4759"></a>
#### 사용 예

```
* IS DISTINCT FROM

gSQL>
SELECT i1,
       i2,
       i1 IS DISTINCT FROM i2 AS IsDistinct
  FROM t1; 

  I1   I2 ISDISTINCT
---- ---- ----------
   1 null TRUE      
   1    1 FALSE     
   1    2 TRUE      
null null FALSE     
null    1 TRUE      
null    2 TRUE      

6 rows selected.

gSQL>
SELECT i1,
       i2,
       i3,
       ( I1, I2, I3 ) IS DISTINCT FROM ( 1, 1, 1 ) AS RESULT 
  FROM t1;

  I1   I2   I3 RESULT
---- ---- ---- ------
   1    1    1 FALSE 
   2 null    3 TRUE  
null null null TRUE  

3 rows selected.


* IS NOT DISTINCT FROM

gSQL>
SELECT i1,
       i2,
       i1 IS NOT DISTINCT FROM i2 AS IsNotDistinct 
  FROM t1; 

  I1   I2 ISNOTDISTINCT
---- ---- -------------
   1 null FALSE        
   1    1 TRUE         
   1    2 FALSE        
null null TRUE         
null    1 FALSE        
null    2 FALSE        

6 rows selected.

gSQL> 
SELECT i1,
       i2,
       i3,
       ( I1, I2, I3 ) IS NOT DISTINCT FROM ( 1, 1, 1 ) AS RESULT
 FROM t1;

  I1   I2   I3 RESULT
---- ---- ---- ------
   1    1    1 TRUE  
   2 null    3 FALSE 
null null null FALSE 

3 rows selected.
```

<a id="f391b428241fb120"></a>
### 호환성

Condition에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="20f575d4dd2f4cbb"></a>
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
| T501 | Enhanced EXISTS predicate | O |
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

<a id="909ce869a4298578"></a>
## Regular Expression

Regular Expression 은 메타문자 (operators)와 문자 리터럴을 사용하여 검색 패턴을 지정한다.

```
July (fourth|4(th)?)
```

- 메타문자 (operator)
    - (), |, ?
- 문자리터럴
    - July, fourth, 4, th
- 일치하는 문자열
    - July fourth
    - July 4th
    - July 4

<a id="e4a5084588b0c387"></a>
### Regular Expressions

- [REGEXP_LIKE Condition](#bd7439f58b8d5d07)
- [REGEXP_COUNT](17-built-in-function-references.md#5a9c61acf90fd5c1)
- [REGEXP_INSTR](17-built-in-function-references.md#3a5d8345b833199f)
- [REGEXP_REPLACE](17-built-in-function-references.md#cbbf5abf3bd78123)
- [REGEXP_SUBSTR](17-built-in-function-references.md#cefe81f21ed82b68)

<a id="6c5d9938302fa9a3"></a>
### Regular Expression Matching Options

Regular Expression matching 수행 동작을 지정하는 option의 종류는 다음과 같다.

- i
- c
- n
- m
- x

```
* i : case-insensitive matching

gSQL>
SELECT REGEXP_COUNT( 'Superscript digits', 's', 1, 'i' ) AS RESULT
  FROM dual;
RESULT
------
     3
1 row selected.
```

```
* c : case-sensitive matching

gSQL> 
SELECT REGEXP_COUNT( 'Superscript digits', 's', 1, 'c' ) AS RESULT
  FROM dual;
RESULT
------
     2
1 row selected.
```

```
* n : Dot operator(.) 가 newline character 와의 match 허용

gSQL> 
SELECT * FROM t1;
C1               
-----------------
matching options:
i, c, n, m, x    
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, ':.+', 1, 1, 'n' ) AS RESULT
  FROM t1;
RESULT       
-------------
:            
i, c, n, m, x
1 row selected.
```

```
* m : 문자열 내부의 newline character를 행을 종료하는 multiline mode 로 지정

gSQL> 
SELECT * FROM t1;
C1               
-----------------
matching options:
i, c, n, m, x    
1 row selected.

gSQL> 
SELECT REGEXP_COUNT( c1, '^.+', 1, 'm' ) AS RESULT
  FROM t1;
RESULT
------
     2
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, '^.+', 1, 1, 'm' ) AS RESULT1,
       REGEXP_SUBSTR( c1, '^.+', 1, 2, 'm' ) AS RESULT2
  FROM t1;
RESULT1           RESULT2      
----------------- -------------
matching options: i, c, n, m, x
1 row selected.
```

```
* x : regular expression 내의 whitespace 를 무시한다.

gSQL> 
SELECT REGEXP_SUBSTR('MATCHING', 'M A T C H I N G', 1, 1, 'x') AS RESULT
  FROM dual;
RESULT  
--------
MATCHING
1 row selected.
```

<a id="9085d17c2eb9fcb1"></a>
### Regular Expression Operators

Operator 는 데이터베이스 문자셋의 데이터를 처리하고, 멀티바이트 문자도 일치 항목에 포함한다.

**Regular Expression Operators**

<a id="3adc3edcb6126838"></a>
<table><thead><tr><th align="center">Operator</th><th align="center">설명</th></tr></thead><tbody><tr><td valign="middle">\</td><td valign="middle">escape character<br>\ 다음 문자를 문자 literal 로 다룬다.<br><ul><li>operator 를 문자로 검색할 수 있다.<br><ul><li>예: \+ ( + 를 문자로 검색한다. )</li><li>예: \\ ( \ 를 문자로 검색한다. )</li></ul></li></ul></td></tr><tr><td valign="middle">.</td><td valign="middle">하나의 문자와 match 된다.</td></tr><tr><td valign="middle">*</td><td valign="middle">0 개 이상 ( zero or more ) match 된다. (greedy)</td></tr><tr><td valign="middle">+</td><td valign="middle">하나 이상 ( one or more ) match 된다. (greedy)</td></tr><tr><td valign="middle">?</td><td valign="middle">0 또는 1 개 ( zero or one ) match 된다. (greedy)</td></tr><tr><td valign="middle">|</td><td valign="middle">Alternation: 여러식 중 하나와 match 된다.</td></tr><tr><td valign="middle">^</td><td valign="middle"><ul><li>Default mode: 문자열의 시작과 match 된다.<br><ul><li>예: abc\ndef 는 정규표현식 ^. 에 a 가 match 된다.</li></ul></li><li>Multi line mode ( matching option 'm' ): 문자열 내 모든 행의 시작과 match 된다.<br><ul><li>예: abc\ndef 는 정규표현식 ^. 에 a, d 가 match 된다.</li></ul></li></ul></td></tr><tr><td valign="middle">$</td><td valign="middle"><ul><li>Default mode: 문자열의 끝 또는 문자열 끝의 \n 바로 앞 문자와 match 된다.<br><ul><li>예: abc\ndef, abc\ndef\n 은 정규표현식 .$ 에 모두 f 가 match 된다.</li></ul></li><li>Multi line mode ( matching option 'm' ): 문자열내 모든 행의 끝과 match 된다.<br><ul><li>예: abc\ndef 는 정규표현식 .$ 에 c, f 가 match 된다.</li></ul></li></ul></td></tr><tr><td valign="middle">[ ]</td><td valign="middle">[ ] 내의 문자리스트들 중 하나와 match 된다.<br><ul><li>[ ] 내 문자리스트에는 single character, - (range), [: :] (character class) 을 나열할 수 있다.<br><ul><li>예: REGEXP_SUBSTR( 'aB9', '[aA-Z[:digit:]]*' ) ==&gt; aB9</li></ul></li><li>- (range) 에 기술된 문자는 unicode 의 binary code 로 비교된다.</li><li>- (range), [: :] (character class) 을 제외하고 모두 literal 로 해석한다.</li><li>] (right bracket) 문자를 문자리스트에 포함하고자 하는 경우, 문자리스트의 첫번째로 기술한다.<br><ul><li>예: REGEXP_SUBSTR( ']', '[]Bracket]' ) ==&gt; ]</li></ul></li><li>- ( hyphen ) 문자를 문자리스트에 포함하고자 하는 경우, 문자리스트의 첫번째 또는 마지막에 기술한다.<br><ul><li>예: REGEXP_SUBSTR( '-', '[-Bracket]' ) ==&gt; -</li><li>예: REGEXP_SUBSTR( '-', '[Bracket-]' ) ==&gt; -</li></ul></li></ul></td></tr><tr><td valign="middle">[^ ]</td><td valign="middle">[ ] 내의 문자리스트들에 존재하지 않는 문자와 match 된다.<br><ul><li>[ ] 내 문자리스트에는 single character, - (range), [: :] (character class) 을 나열할 수 있다.<br><ul><li>예: REGEXP_SUBSTR( 'aB9', '[^aA-Z[:digit:]]*' ) ==&gt; NULL</li></ul></li><li>- (range) 에 기술된 문자는 unicode 의 binary code 로 비교된다.</li><li>- (range), [: :] (character class) 를 제외하고 모두 literal 로 해석한다.</li><li>] (right bracket) 문자를 문자리스트에 포함하고자 하는 경우, ^ 다음에 기술한다.<br><ul><li>예: REGEXP_SUBSTR( ']', '[^]Bracket]' ) ==&gt; NULL</li></ul></li><li>- ( hyphen ) 문자를 문자리스트에 포함하고자 하는 경우, ^ 다음에 기술하거나, 문자리스트 마지막에 기술한다.<br><ul><li>예: REGEXP_SUBSTR( '-', '[^-Bracket]' ) ==&gt; NULL</li><li>예: REGEXP_SUBSTR( '-', '[^Bracket-]' ) ==&gt; NULL</li></ul></li></ul></td></tr><tr><td valign="middle">( )</td><td valign="middle">( ) 안의 expression 을 하나의 subexpression 그룹으로 다룬다.<br>subexpression 은 subexpression 에 포함될 수 있다.<br>subexpression의 여는 괄호 '(' 를 시작으로 왼쪽에서 오른쪽으로 subexpression 을 count 한다.<br><ul><li>(abc)((12(345))67(89))<br><ul><li>1: abc</li><li>2: 123456789</li><li>3: 12345</li><li>4: 345</li><li>5: 89</li></ul></li></ul></td></tr><tr><td valign="middle">{m}</td><td valign="middle">m 번 match 된다.</td></tr><tr><td valign="middle">{m,}</td><td valign="middle">최소 m 번 이상 match 된다. (greedy)</td></tr><tr><td valign="middle">{m,n}</td><td valign="middle">최소 m 번 이상 최대 n 번까지 match 된다. (greedy)</td></tr><tr><td valign="middle">\n</td><td valign="middle">Back Reference<br>Back Reference 이전에 정의된 n 번째 subexpression 과 match 된다.<br>n 은 1 ~ 9 까지의 정수이다.<br>Back Reference 는 각 subexpression 의 여는 괄호 '(' 를 시작으로 왼쪽에서 오른쪽으로 subexpression 을 count 한다.</td></tr><tr><td valign="middle">[: :]</td><td valign="middle">character class 에 속하는 문자와 match 된다.<br><ul><li>[:alnum:] : 알파벳과 숫자</li><li>[:alpha:] : 알파벳</li><li>[:blank:] : 공백과 탭</li><li>[:cntrl:] : 제어문자</li><li>[:digit:] : 숫자</li><li>[:graph:] : space 를 제외한 printable characters</li><li>[:lower:] : 소문자</li><li>[:print:] : space 를 포함한 printable characters</li><li>[:punct:] : 특수문자</li><li>[:space:] : white space</li><li>[:upper:] : 대문자</li><li>[:xdigit:] : 16 진수 숫자</li></ul></td></tr><tr><td valign="middle">\d</td><td valign="middle">digit character 와 match 된다.<br>[[:digit:]] 과 동일하다.</td></tr><tr><td valign="middle">\D</td><td valign="middle">digit character 가 아닌 문자와 match 된다.<br>[^[:digit:]] 과 동일하다.</td></tr><tr><td valign="middle">\w</td><td valign="middle">alphanumeric, underscore 문자와 match 된다.<br>[[:alnum:]_] 와 동일하다.</td></tr><tr><td valign="middle">\W</td><td valign="middle">word character 가 아닌 문자와 match 된다.<br>[^[:alnum:]_] 와 동일하다.</td></tr><tr><td valign="middle">\s</td><td valign="middle">whitespace character 와 match 된다.<br>[[:space:]] 와 동일하다.</td></tr><tr><td valign="middle">\S</td><td valign="middle">whitespace character 가 아닌 문자와 match 된다.<br>[^[:space:]] 와 동일하다.</td></tr><tr><td valign="middle">\A</td><td valign="middle">문자열의 시작과 match 된다.</td></tr><tr><td valign="middle">\Z</td><td valign="middle">문자열의 끝 또는 문자열 끝의 \n 바로 앞 문자와 match 된다.<br>예: abc\ndef, abc\ndef\n 은 정규표현식 .\Z 에 모두 f 가 match 된다.</td></tr><tr><td valign="middle">\z</td><td valign="middle">문자열의 끝과 match 된다.</td></tr><tr><td valign="middle">*?</td><td valign="middle">0 번이상 ( zero or more ) match 된다. (nongreedy)</td></tr><tr><td valign="middle">+?</td><td valign="middle">1 번이상 ( one or more ) match 된다. (nongreedy)</td></tr><tr><td valign="middle">??</td><td valign="middle">0 또는 1 번 ( zero or one ) match 된다. (nongreedy)</td></tr><tr><td valign="middle">{m}?</td><td valign="middle">m 번 match 된다. (nongreedy)</td></tr><tr><td valign="middle">{m,}?</td><td valign="middle">최소 m 번 이상 match 된다. (nongreedy)</td></tr><tr><td valign="middle">{m,n}?</td><td valign="middle">최소 m 번 이상 최대 n 번 이하로 match 된다. (nongreedy)</td></tr></tbody></table>

- greedy
    - 가능한 가장 많이 패턴에 match 되는 항목을 찾는다.
- nongreedy
    - 가능한 가장 적게 패턴에 match 되는 항목을 찾는다.

```
### 예:

gSQL> 
SELECT REGEXP_SUBSTR( 'axxxbxbxb', 'a\w+b' ) AS RES_GREEDY,
       REGEXP_SUBSTR( 'axxxbxbxb', 'a\w+?b' ) AS RES_NON_GREEDY
  FROM dual;
RES_GREEDY RES_NON_GREEDY
---------- --------------
axxxbxbxb  axxxb         
1 row selected.
```

다음은 각각의 regular expression operator를 사용한 예이다.

```
• \

gSQL> 
SELECT REGEXP_SUBSTR( '(a)\1', '\(a\)\\1' ) AS RESULT FROM dual;
RESULT
------
(a)\1 
1 row selected.
```

```
•.

gSQL> SELECT REGEXP_SUBSTR( 'abcde', 'a...e' ) AS RESULT FROM dual;
RESULT
------
abcde 
1 row selected.
```

```
• *, +, ?

gSQL> 
SELECT REGEXP_SUBSTR( 'ab', 'ax*b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axb', 'ax*b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxb', 'ax*b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
ab      axb     axxxb  
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'ab', 'ax+b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axb', 'ax+b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxb', 'ax+b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
null    axb     axxxb  
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'ab', 'ax?b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axb', 'ax?b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxb', 'ax?b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
ab      axb     null   
1 row selected.
```

```
• |

gSQL> 
SELECT REGEXP_SUBSTR( 'Regexp', '(R|r)egexp' ) AS RESULT1,
       REGEXP_SUBSTR( 'regexp', '(R|r)egexp' ) AS RESULT2
 FROM dual;
RESULT1 RESULT2
------- -------
Regexp  regexp 
1 row selected.
```

```
• ^, $

gSQL> 
SELECT * FROM t1;
C1             
---------------
Line1 : aaa xy1
Line2 : bbb xy2
Line3 : ccc xy3
1 row selected.

gSQL> 
SELECT REGEXP_COUNT( c1, '^Line[[:digit:]]' ) AS RESULT_DEFAULT_MODE,
       REGEXP_COUNT( c1, '^Line[[:digit:]]', 1, 'm' ) AS RESULT_MULTILINE_MODE
  FROM t1;
RESULT_DEFAULT_MODE RESULT_MULTILINE_MODE
------------------- ---------------------
                  1                     3
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, '^Line[[:digit:]]', 1 ) AS RES_DEFAULT,
       REGEXP_SUBSTR( c1, '^Line[[:digit:]]', 1, 1, 'm' ) AS RES_MULTILINE_1,
       REGEXP_SUBSTR( c1, '^Line[[:digit:]]', 1, 2, 'm' ) AS RES_MULTILINE_2,
       REGEXP_SUBSTR( c1, '^Line[[:digit:]]', 1, 3, 'm' ) AS RES_MULTILINE_3
  FROM t1;
RES_DEFAULT RES_MULTILINE_1 RES_MULTILINE_2 RES_MULTILINE_3
----------- --------------- --------------- ---------------
Line1       Line1           Line2           Line3          
1 row selected.


gSQL> 
SELECT REGEXP_COUNT( c1, 'xy[[:digit:]]$' ) AS RESULT_DEFAULT_MODE,
       REGEXP_COUNT( c1, 'xy[[:digit:]]$', 1, 'm' ) AS RESULT_MULTILINE_MODE
  FROM t1;
RESULT_DEFAULT_MODE RESULT_MULTILINE_MODE
------------------- ---------------------
                  1                     3
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, 'xy[[:digit:]]$', 1 ) AS RES_DEFAULT,
       REGEXP_SUBSTR( c1, 'xy[[:digit:]]$', 1, 1, 'm' ) AS RES_MULTILINE_1,
       REGEXP_SUBSTR( c1, 'xy[[:digit:]]$', 1, 2, 'm' ) AS RES_MULTILINE_2,
       REGEXP_SUBSTR( c1, 'xy[[:digit:]]$', 1, 3, 'm' ) AS RES_MULTILINE_3
  FROM t1;
RES_DEFAULT RES_MULTILINE_1 RES_MULTILINE_2 RES_MULTILINE_3
----------- --------------- --------------- ---------------
xy3         xy1             xy2             xy3            
1 row selected.
```

```
• [ ], [^ ]

gSQL> 
SELECT REGEXP_SUBSTR( 'a', '[abc]' ) AS RESULT1,
       REGEXP_SUBSTR( 'A', '[A-Z]' ) AS RESULT2,
       REGEXP_SUBSTR( '1', '[[:digit:]]' ) AS RESULT3,
       REGEXP_SUBSTR( 'abAB12', '[abcA-Z[:digit:]]+' ) AS RESULT
  FROM dual;
RESULT1 RESULT2 RESULT3 RESULT
------- ------- ------- ------
a       A       1       abAB12
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'x', '[^abc]' ) AS RESULT1,
       REGEXP_SUBSTR( 'y', '[^A-Z]' ) AS RESULT2,
       REGEXP_SUBSTR( 'z', '[^[:digit:]]' ) AS RESULT3,
       REGEXP_SUBSTR( 'xyz', '[^abcA-Z[:digit:]]+' ) AS RESULT
  FROM dual;
RESULT1 RESULT2 RESULT3 RESULT
------- ------- ------- ------
x       y       z       xyz   
1 row selected.
```

```
• ( ), \n

gSQL> 
SELECT REGEXP_SUBSTR( 'abcbcabc', 'a(bc)\1a\1' ) AS RESULT1,
       REGEXP_SUBSTR( 'abcbcabc', '(a)(b)(c)\2\3\1\2\3' ) AS RESULT2,
       REGEXP_SUBSTR( 'abcbcabc', '(a(bc))\2\1' ) AS RESULT3
 FROM dual;
RESULT1  RESULT2  RESULT3 
-------- -------- --------
abcbcabc abcbcabc abcbcabc
1 row selected.
```

```
• {m}, {m,}, {m,n}

gSQL> 
SELECT REGEXP_SUBSTR( 'axxb', 'ax{3}b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxb', 'ax{3}b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxxxb', 'ax{3}b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
null    axxxb   null   
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'axxb', 'ax{3,}b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxb', 'ax{3,}b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxxxb', 'ax{3,}b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
null    axxxb   axxxxxb
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'axxb', 'ax{3,5}b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxb', 'ax{3,5}b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxxxb', 'ax{3,5}b' ) AS RESULT3,
       REGEXP_SUBSTR( 'axxxxxxxb', 'ax{3,5}b' ) AS RESULT4
  FROM dual;
RESULT1 RESULT2 RESULT3 RESULT4
------- ------- ------- -------
null    axxxb   axxxxxb null   
1 row selected.
```

```
• [: :]

gSQL> 
SELECT REGEXP_SUBSTR( 'abc123', '[[:alnum:]]+' ) AS RESULT1,
       REGEXP_SUBSTR( 'abc', '[[:alpha:]]+' ) AS RESULT2,
       REGEXP_SUBSTR( '123', '[[:digit:]]+' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
abc123  abc     123    
1 row selected.
```

```
• \d, \D, \w, \W, \s, \S

gSQL> 
SELECT REGEXP_SUBSTR( '123', '\d+' ) AS RESULT1,
       REGEXP_SUBSTR( 'abc', '\D+' ) AS RESULT2
  FROM dual;
RESULT1 RESULT2
------- -------
123     abc    
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'A_B_C', '\w+' ) AS RESULT1,
       REGEXP_SUBSTR( '+ @', '\W+' ) AS RESULT2
  FROM dual;
RESULT1 RESULT2
------- -------
A_B_C   + @    
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'a   d', 'a\s+d' ) AS RESULT1,
       REGEXP_SUBSTR( 'abc d', '\S+' ) AS RESULT2
  FROM dual;
RESULT1 RESULT2
------- -------
a   d   abc    
1 row selected.
```

```
• \A

gSQL> 
select * from t1;
C1             
---------------
Line1 : aaa xy1
Line2 : bbb xy2
Line3 : ccc xy3
1 row selected.

gSQL> 
SELECT REGEXP_COUNT( c1, '\ALine[[:digit:]]' ) AS RESULT_DEFAULT_MODE,
       REGEXP_COUNT( c1, '\ALine[[:digit:]]', 1, 'm' ) AS RESULT_MULTILINE_MODE
  FROM t1;
RESULT_DEFAULT_MODE RESULT_MULTILINE_MODE
------------------- ---------------------
                  1                     1
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, '\ALine[[:digit:]]' ) AS RESULT_DEFAULT_MODE,
       REGEXP_SUBSTR( c1, '\ALine[[:digit:]]', 1, 1, 'm' ) AS RESULT_MULTILINE_MODE
  FROM t1;
RESULT_DEFAULT_MODE RESULT_MULTILINE_MODE
------------------- ---------------------
Line1               Line1                
1 row selected.
```

```
• \Z

gSQL> 
SELECT c1 FROM t1;
C1 
---
abc    <-- 첫번째 레코드 abc\ndef 
def
abc    <-- 두번째 레코드 abc\ndef\n
def
   
2 rows selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, '.\Z' ) AS REGEXP_SUBSTR_RES 
  FROM t1;
REGEXP_SUBSTR_RES
-----------------
f                
f                
2 rows selected.
```

```
• \z

gSQL> 
SELECT * FROM t1;
C1             
---------------
Line1 : aaa xy1
Line2 : bbb xy2
Line3 : ccc xy3
1 row selected.

gSQL> 
SELECT REGEXP_COUNT( c1, '\w+\d\z' ) AS RESULT_DEFAULT_MODE,
       REGEXP_COUNT( c1, '\w+\d\z', 1, 'm' ) AS RESULT_MULTILINE_MODE
  FROM t1;
RESULT_DEFAULT_MODE RESULT_MULTILINE_MODE
------------------- ---------------------
                  1                     1
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( c1, '\w+\d\z' ) AS RESULT_DEFAULT_MODE,
       REGEXP_SUBSTR( c1, '\w+\d\z', 1, 1, 'm' ) AS RESULT_MULTILINE_MODE
  FROM t1;
RESULT_DEFAULT_MODE RESULT_MULTILINE_MODE
------------------- ---------------------
xy3                 xy3                  
1 row selected.
```

```
• *?, +?, ??

gSQL> 
SELECT REGEXP_SUBSTR( 'ab', 'a\w*?b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxbxb', 'a\w*?b' ) AS RESULT2
  FROM dual;
RESULT1 RESULT2
------- -------
ab      axxxb  
1 row selected.


gSQL> 
SELECT REGEXP_SUBSTR( 'ab', 'a\w+?b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxbxb', 'a\w+?b' ) AS RESULT2
  FROM dual;
RESULT1 RESULT2
------- -------
null    axxxb  
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'ab', 'a\w??b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axbxb', 'a\w??b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxbxb', 'a\w?b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
ab      axb     null   
1 row selected.
```

```
• {n}?, {n,}?, {n,m}?

gSQL> 
SELECT REGEXP_SUBSTR( 'abxb', 'a\w{3}?b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxbxbxb', 'a\w{3}?b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxxxbxbxb', 'a\w{3}?b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
null    axxxb   null   
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'abxb', 'a\w{3,}?b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxbxb', 'a\w{3,}?b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxxxbxbxb', 'a\w{3,}?b' ) AS RESULT3
  FROM dual;
RESULT1 RESULT2 RESULT3
------- ------- -------
null    axxxb   axxxxxb
1 row selected.

gSQL> 
SELECT REGEXP_SUBSTR( 'abxb', 'a\w{3,5}?b' ) AS RESULT1,
       REGEXP_SUBSTR( 'axxxbxb', 'a\w{3,5}?b' ) AS RESULT2,
       REGEXP_SUBSTR( 'axxxxxbxbxb', 'a\w{3,5}?b' ) AS RESULT3,
       REGEXP_SUBSTR( 'axxxxxxxbxbxb', 'a\w{3,5}?b' ) AS RESULT4
  FROM dual;
RESULT1 RESULT2 RESULT3 RESULT4
------- ------- ------- -------
null    axxxb   axxxxxb null   
1 row selected.
```

<a id="d0188a14aead086d"></a>
## JSON String Constructor

JSON string constructor는 SQL expression을 인자로 받아 JSON 형식의 문자열을 생성하는 함수이다.

JSON string constructor는 다음과 같이 구분된다.  
• JSON value constructor  
• JSON aggregate constructor  
• JSON window constructor

<a id="afe1f87a6eb6381f"></a>
### JSON String Constructor

<a id="7386aeb6dcfeb30a"></a>
#### JSON value Constructor

JSON value constructor는 매 row 마다 하나의 JSON 문자열 row를 생성하는 single row function이다.

JSON value constructor의 종류는 다음과 같다.

- [JSON_ARRAY](17-built-in-function-references.md#de97ba0a4d32a2af)
- [JSON_OBJECT](17-built-in-function-references.md#8cd5e69d1f7d5ba9)

<a id="900d89639c906cbd"></a>
#### JSON aggregate Constructor

JSON aggregate constructor는 결과를 집계하여 하나의 JSON 문자열 row를 생성하는 aggregate function이다.

JSON aggregate constructor의 종류는 다음과 같다.

- [JSON_ARRAYAGG](17-built-in-function-references.md#6a1307addaa8d032)
- [JSON_OBJECTAGG](17-built-in-function-references.md#f2ed9f8209629cd7)

<a id="d5d22ac6b5b0da15"></a>
#### JSON window Constructor

JSON window constructor는 OVER 절을 이용하여 정의된 레코드 범위에 대한 JSON 문자열을 생성하는 window 함수이다.

window 내 그룹에 따라 결과 row의 수가 결정된다는 점에서 aggregate function과 차이가 있다.

JSON window constructor의 종류는 다음과 같다.

- [JSON_ARRAYAGG() OVER](17-built-in-function-references.md#677ae68f770b3e92)
- [JSON_OBJECTAGG() OVER](17-built-in-function-references.md#4b6cac5f93cac0c0)

<a id="5deaadddbd962867"></a>
### JSON 문자열

JSON 문자열에는 JSON object 문자열과 JSON array 문자열, 두 가지 유형이 있다.

<a id="31bef42f6c0fd5e8"></a>
#### JSON Object 문자열

JSON object 문자열은 연속된 key-value 쌍을 중괄호로 묶는 방식으로 구성되는데, 이 때 key는 SQL 문자열이어야 한다.

```
{ key : value }
{ key : value, key : value, ... }
```

JSON object 문자열을 결과로 도출하는 함수는 다음 세 가지 함수이다.

- [JSON_OBJECT](17-built-in-function-references.md#8cd5e69d1f7d5ba9)
- [JSON_OBJECTAGG](17-built-in-function-references.md#f2ed9f8209629cd7)
- [JSON_OBJECTAGG() OVER](17-built-in-function-references.md#4b6cac5f93cac0c0)

<a id="3f0d2e35d4fdc782"></a>
#### JSON Array 문자열

JSON array 문자열은 연속된 value를 대괄호로 묶는 방식으로 구성되어 있다.

```
[ value ]
[ value, value, ... ]
```

JSON array 문자열을 결과로 도출하는 함수는 다음 세 가지 함수이다.

- [JSON_ARRAY](17-built-in-function-references.md#de97ba0a4d32a2af)
- [JSON_ARRAYAGG](17-built-in-function-references.md#6a1307addaa8d032)
- [JSON_ARRAYAGG() OVER](17-built-in-function-references.md#677ae68f770b3e92)

<a id="6f43e90101daa4ab"></a>
### JSON Structural Characters

JSON string을 구성하는 character에는 여섯 가지 종류가 있다.

<a id="e89e833f7a2a0856"></a>
| JSON structural character | 설명 |
| --- | --- |
| [ | JSON array 문자열을 시작할 때 사용하는 대괄호이다. |
| ] | JSON array 문자열을 닫을 때 사용하는 대괄호이다. |
| { | JSON object 문자열을 시작할 때 사용하는 중괄호이다. |
| } | JSON object 문자열을 닫을 때 사용하는 중괄호이다. |
| : | key를 구분하는 문자이다. |
| , | value를 구분하는 문자이다. |

이 문자들은 앞뒤 공백을 허용한다.

<a id="4e4d428a809878fe"></a>
### JSON Escape Characters

JSON 문자열 내에서 escape 되는 문자는 다음과 같다.

<a id="dd3b45d93b74c0be"></a>
| 문자 | escape 형태 | 설명 |
| --- | --- | --- |
| " | \" | quotation mark |
| \ | \\ | back slash |
| CHR(8) | \b | backspace |
| CHR(12) | \f | form feed |
| CHR(10) | \n | new line feed |
| CHR(19) | \r | carriage return |
| CHR(9) | \t | tab |

다음은 문자가 escape 되는 예이다.

```
gSQL> SELECT JSON_OBJECT( 'quote' VALUE '"',
                          'backslash' VALUE '\',
                          'backspace' VALUE CHR(8),
                          'formfeed' VALUE CHR(12),
                          'newline' VALUE CHR(10),
                          'carriage_return' VALUE CHR(13),
                          'tab' VALUE CHR(9) ) AS escaped_json
       FROM dual;

ESCAPED_JSON                                                                    
-------------------------------------------------------------------------
{"quote":"\"","backslash":"\\","backspace":"\b","formfeed":"\f","newline":"\n","carriage_return":"\r","tab":"\t"}                                   

1 row selected.
```

다음은 escape 되지 않은 문자열과 escape 된 문자열을 비교하는 예이다.

```
--# escape 되지 않은 결과
SELECT * FROM sample_table;

ID STRING_DATA             
-- ------------------------
 1 simple string           
 2 This is first sentence. 
   This is second sentence.
 3 He said, "Hello".       

3 rows selected.


--# escape 된 결과
SELECT JSON_OBJECT( 'ID'    VALUE id,
                    'DATA'  VALUE string_data ) AS json_string
  FROM sample_table;

JSON_STRING                                                        
-------------------------------------------------------------------
{"ID":1,"DATA":"simple string"}                                    
{"ID":2,"DATA":"This is first sentence.\nThis is second sentence."}
{"ID":3,"DATA":"He said, \"Hello\"."}                              

3 rows selected.
```

<a id="64334c03f1fa7288"></a>
### JSON Result Control Options

<a id="80e8f502383fbf61"></a>
#### JSON Constructor Null Clause

JSON string constructor의 인자 value가 null 일 때 출력되는 결과를 제어할 수 있다.

```
<JSON constructor null clause> ::=
    NULL ON NULL
  | ABSENT ON NULL
  | EMPTY STRING ON NULL
```

<a id="05eda104e71d4aed"></a>
##### NULL ON NULL

Value가 null 인 경우, JSON string null을 출력한다.

```
gSQL> SELECT JSON_OBJECT( name VALUE balances NULL ON NULL ) AS res_json_object
        FROM accounts;

RES_JSON_OBJECT
---------------
{"Alice":50000}
{"Bob":null}   
{"Chris":1000} 

3 rows selected.

gSQL> SELECT JSON_ARRAY( name, balances NULL ON NULL ) AS res_json_array
        FROM accounts;

RES_JSON_ARRAY 
---------------
["Alice",50000]
["Bob",null]   
["Chris",1000] 

3 rows selected.
```

<a id="98a9084da910cd37"></a>
##### ABSENT ON NULL

Value가 null 인 경우, 이를 무시하고 아무것도 출력하지 않는다.

```
gSQL> SELECT JSON_OBJECT( name VALUE balances ABSENT ON NULL ) AS res_json_object
        FROM accounts;

RES_JSON_OBJECT
---------------
{"Alice":50000}
{}             
{"Chris":1000} 

3 rows selected.

gSQL> SELECT JSON_ARRAY( name, balances ABSENT ON NULL ) AS res_json_array
        FROM accounts; 

RES_JSON_ARRAY 
---------------
["Alice",50000]
["Bob"]        
["Chris",1000] 

3 rows selected.
```

<a id="d6c89d99ecbb115e"></a>
##### EMPTY STRING ON NULL

Value가 null 인 경우, empty string ("")을 출력한다.

```
gSQL> SELECT JSON_OBJECT( name VALUE balances EMPTY STRING ON NULL ) AS res_json_object
        FROM accounts;

RES_JSON_OBJECT
---------------
{"Alice":50000}
{"Bob":""}     
{"Chris":1000} 

3 rows selected.

gSQL> SELECT JSON_ARRAY( name, balances EMPTY STRING ON NULL ) AS res_json_array
        FROM accounts;

RES_JSON_ARRAY 
---------------
["Alice",50000]
["Bob",""]     
["Chris",1000] 

3 rows selected.
```

<a id="2bce9d5d0bac743d"></a>
#### JSON Key Uniqueness Constraint

JSON object key field의 중복 허용 여부를 설정할 수 있다.

```
<JSON key uniqueness constraint> ::=
    WITH UNIQUE [ KEYS ]
  | WITHOUT UNIQUE [ KEYS ]
```

<a id="36df593f97798ace"></a>
##### WITH UNIQUE [ KEYS ]

하나의 JSON object 내에서 key가 중복될 수 없다. 만약 중복된 경우에는 에러를 반환한다.

```
CREATE TABLE t1 ( key1 VARCHAR(3), data1 VARCHAR(3) );
INSERT INTO t1 VALUES ( 'K1', 'D1' );
INSERT INTO t1 VALUES ( 'K2', 'D2' );
INSERT INTO t1 VALUES ( 'K1', 'D3' );
COMMIT;

gSQL> SELECT JSON_OBJECTAGG( key1 VALUE data1 WITH UNIQUE KEYS ) AS result 
        FROM t1;

ERR-42000(13065): duplicate key names 'K1' in JSON object
```

<a id="76dcd2d5605f05a8"></a>
##### WITHOUT UNIQUE [ KEYS ]

하나의 JSON object 내에서 중복된 key를 허용한다.

```
gSQL> SELECT JSON_OBJECTAGG( key1 VALUE data1 WITHOUT UNIQUE KEYS ) AS result
      FROM t1;

RESULT                         
-------------------------------
{"K1":"D1","K2":"D2","K1":"D3"}

1 row selected.
```

<a id="90516a21bfc51e9b"></a>
#### JSON Array Aggregate Order By Clause

ORDER BY 절에 지정된 sort specification list의 순서에 따라 value를 정렬한 후 JSON_ARRAYAGG 결과를 생성한다.

```
<JSON array aggregate order by clause> ::=
    ORDER BY <sort specification list>

<sort specification list> ::=
    <sort specification> [ { <comma> <sort specification> }... ]

<sort specification> ::=
    <sort key> [ <ordering specification> ] [ <null ordering> ]

<sort key> ::=
    <value expression>

<ordering specification> ::=
      ASC
    | DESC

<null ordering> ::=
      NULLS FIRST
    | NULLS LAST
```

다음은 JSON array aggregate order by clause를 사용하여 JSON array value를 정렬하는 예이다.

```
CREATE TABLE t1 ( c1 int );
INSERT INTO t1 VALUES (3),(1),(null),(2);

gSQL> SELECT JSON_ARRAYAGG( c1 ) AS res_json_sort
       FROM t1;

RES_JSON_SORT
-------------
[3,1,2]     

gSQL> SELECT JSON_ARRAYAGG( c1 ORDER BY c1 ) AS res_json_sort
       FROM t1;

RES_JSON_SORT
-------------
[1,2,3]
```

- &lt;ordering specification&gt;
    - 정렬 순서를 지정한다.
        - ASC: 오름차순으로 정렬한다.
        - DESC: 내림차순으로 정렬한다.
    - 지정하지 않으면 기본값은 ASC 이다.

```
gSQL> SELECT JSON_ARRAYAGG( c1 ORDER BY c1 ASC ) AS res_json_sort
        FROM t1;

RES_JSON_SORT
-------------
[1,2,3]                            

1 row selected.

gSQL> SELECT JSON_ARRAYAGG( c1 ORDER BY c1 DESC ) AS res_json_sort
        FROM t1;

RES_JSON_SORT
-------------
[3,2,1]                             

1 row selected.
```

- &lt;null ordering&gt;
    - NULL 값과 NULL이 아닌 값의 정렬 순서를 지정한다.
        - NULLS FIRST: NULL 값을 먼저 정렬한다.
        - NULLS LAST: NULL 값을 나중에 정렬한다.
    - 지정하지 않으면 기본값은 NULLS LAST 이다.

```
gSQL> SELECT JSON_ARRAYAGG( c1 ORDER BY c1 NULL ON NULL ) AS res_json_sort
        FROM t1;

RES_JSON_SORT
-------------
[1,2,3,null]                                

1 row selected.

gSQL> SELECT JSON_ARRAYAGG( c1 ORDER BY c1 NULLS FIRST NULL ON NULL ) AS res_json_sort
        FROM t1;

RES_JSON_SORT
-------------
[null,1,2,3]                                            

1 row selected.

gSQL> SELECT JSON_ARRAYAGG( c1 ORDER BY c1 NULLS LAST NULL ON NULL ) AS res_json_sort
        FROM t1;

RES_JSON_SORT
-------------
[1,2,3,null]                                           

1 row selected.
```

<a id="d8ec54a70fd9d3a7"></a>
#### JSON Output Clause

JSON string constructor로 생성된 문자열의 결과 타입과 출력 형식을 제어할 수 있다.

```
<JSON output clause> ::=
    RETURNING <string data type> [PRETTY]

<string data type> ::=
    CHAR(n)
  | VARCHAR(n)
  | LONG VARCHAR
```

- 결과 문자열의 data type을 지정할 수 있다.
    - Data type은 character string type 중 하나로 지정할 수 있다.

- PRETTY 옵션을 적용하여 출력 형식을 변경할 수 있다.

다음은 JSON output clause를 명시하여 결과 data type를 지정하는 예이다.

```
gSQL> SELECT JSON_OBJECT( name VALUE balances RETURNING VARCHAR(100) ) AS res_json_object
        FROM accounts;

RES_JSON_OBJECT
---------------
{"Alice":50000}
{"Bob":null}   
{"Chris":1000} 

3 rows selected.
```

위 예시에 PRETTY 옵션을 적용한 결과는 다음과 같다.

```
gSQL> SELECT JSON_OBJECT( name VALUE balances RETURNING VARCHAR(100) PRETTY ) AS res_json_object
        FROM accounts;

RES_JSON_OBJECT  
-----------------
{                
    "Alice":50000
}                
{                
    "Bob":null   
}                
{                
    "Chris":1000 
}                

3 rows selected.
```

<a id="7ae7ca1fd68e4fab"></a>
### JSON 문자열 출력 형식

JSON string constructor가 생성하는 문자열은 인자 expression의 SQL data type에 따라 다음과 같이 출력된다.

<a id="7243045179fc6fa6"></a>
| expression의 SQL data type | 결과 출력 형식 |
| --- | --- |
| 숫자 | Numeric |
| Boolean | Boolean |
| Character String | String |
| Binary String | String |
| 날짜/시간 | String |
| Interval | String |

- 결과 출력 형식이 string 일 경우, expression의 시작과 끝에 쌍따옴표 (")를 포함하여 출력한다.

각 인자 expression의 SQL data type에 따른 결과 JSON 문자열의 출력 형식은 다음과 같다.

<a id="612d107a6a67c84b"></a>
#### 숫자

숫자 타입은 numeric에서 표현 가능한 모든 유효숫자를 표현할 수 있다.

```
gSQL> SELECT JSON_OBJECT( 'k_num' VALUE 100 ) AS result
        FROM dual;

RESULT       
-------------
{"k_num":100}

1 row selected.

gSQL> SELECT JSON_ARRAY( 100 ) AS result
        FROM dual;

RESULT
------
[100] 

1 row selected.
```

<a id="4516b4251621616e"></a>
#### Boolean

```
gSQL> SELECT JSON_OBJECT( 'k_boolean' VALUE true ) AS result
        FROM dual;

RESULT            
------------------
{"k_boolean":true}

1 row selected.

gSQL> SELECT JSON_ARRAY( true ) AS result
        FROM dual;

RESULT
------
[true]

1 row selected.
```

<a id="af4d683a00af4f39"></a>
#### Character String

```
gSQL> SELECT JSON_OBJECT( 'k_char' VALUE 'hello' ) AS result
        FROM dual;

RESULT            
------------------
{"k_char":"hello"}

1 row selected.

gSQL> SELECT JSON_ARRAY( 'hello' ) AS result
        FROM dual; 

RESULT   
---------
["hello"]

1 row selected.
```

<a id="3eebd76a90b00063"></a>
#### Binary String

Binary string은 16진수 문자열로 표현된다.

```
gSQL> SELECT JSON_OBJECT( 'k_binary' VALUE X'0011FF' ) AS result
        FROM dual;

RESULT               
---------------------
{"k_binary":"0011FF"}

1 row selected.

gSQL> SELECT JSON_ARRAY( X'0011FF' ) AS result
        FROM dual; 

RESULT    
----------
["0011FF"]

1 row selected.
```

<a id="b2fe2b7a95a4eef3"></a>
#### 날짜/ 시간

<a id="bc0803f283584de2"></a>
##### 날짜

날짜 타입은 'YYYY-MM-DDTHH:MM:SS' 형식으로 출력된다.

- 'T'는 날짜와 시간을 구분하는 문자이다.

```
gSQL> SELECT JSON_OBJECT( 'k_date' VALUE DATE '2025-05-05' ) AS result
        FROM dual;

RESULT                          
--------------------------------
{"k_date":"2025-05-05T00:00:00"}

1 row selected.

gSQL> SELECT JSON_ARRAY( DATE '2025-05-05' ) AS result
        FROM dual;

RESULT                 
-----------------------
["2025-05-05T00:00:00"]

1 row selected.
```

<a id="89e535635a4ecbe1"></a>
##### 시간

시간 타입은 'HH:MM:SS.FF6' 형식으로 출력된다.

- 필요에 따라 'HH:MM:SS.FF6±TZH:TZM' 형식으로 타임존을 표시한다.

```
gSQL> SELECT JSON_OBJECT( 'k_time' VALUE TIME '15:30:59.999999' ) AS result
        FROM dual;

RESULT                      
----------------------------
{"k_time":"15:30:59.999999"}

1 row selected.

gSQL> SELECT JSON_ARRAY( TIME'15:30:59.999999' ) AS result
        FROM dual; 

RESULT             
-------------------
["15:30:59.999999"]

1 row selected.
```

<a id="9d1dc419627a6914"></a>
##### Timestamp

Timestamp 타입은 'YYYY-MM-DDTHH:MM:SS.FF6' 형식으로 출력된다.

- 'T'는 날짜와 시간을 구분하는 문자이다.
- 필요에 따라 'YYYY-MM-DDTHH:MM:SS.FF6±TZH:TZM' 형식으로 타임존을 표시한다.

```
gSQL> SELECT JSON_OBJECT( 'k_timestamp' VALUE TIMESTAMP '2025-05-05 12:30:45 +09:00' ) AS result
        FROM dual;

RESULT                                            
--------------------------------------------------
{"k_timestamp":"2025-05-05T12:30:45.000000+09:00"}

1 row selected.

gSQL> SELECT JSON_ARRAY( TIMESTAMP '2025-05-05 12:30:45 +09:00' ) AS result
        FROM dual;

RESULT                              
------------------------------------
["2025-05-05T12:30:45.000000+09:00"]

1 row selected.
```

<a id="ab6bafde7a14d7ad"></a>
#### Interval

Interval 타입은 ISO 8601에 정의된 duration format으로 표현된다.

<a id="0d5a11b256b606bc"></a>
##### Interval Year to Month

Interval Year to Month 타입은 'P[n]Y[n]M' 구조로 출력된다.

- 'P'는 기간 (period)을 나타내는 접두사이다.
- 'Y' (year), 'M' (month)은 날짜 기반 기간을 나타내는 단위이며, 값이 0인 항목은 생략된다.
    - 예: 'P1Y' (1년), 'P3M' (3개월), 'P1Y2M' (1년 2개월)
- 모든 값이 0일 경우, 기본값은 '"P0Y"'로 출력된다.

```
gSQL> SELECT JSON_OBJECT( 'k_int_ytom' VALUE INTERVAL '3-6' YEAR TO MONTH ) AS result
        FROM dual; 

RESULT                
----------------------
{"k_int_ytom":"P3Y6M"}

1 row selected.

gSQL> SELECT JSON_ARRAY( INTERVAL '3-6' YEAR TO MONTH ) AS result
        FROM dual; 

RESULT   
---------
["P3Y6M"]

1 row selected.

gSQL> SELECT JSON_OBJECT( 'k_int_ytom' VALUE INTERVAL '0-6' YEAR TO MONTH ) AS result
        FROM dual; 

RESULT              
--------------------
{"k_int_ytom":"P6M"}

1 row selected.

gSQL> SELECT JSON_ARRAY( INTERVAL '0-6' YEAR TO MONTH ) AS result
        FROM dual; 

RESULT 
-------
["P6M"]

1 row selected.

gSQL> SELECT JSON_OBJECT( 'k_int_ytom' VALUE INTERVAL '0-0' YEAR TO MONTH ) AS result
        FROM dual;

RESULT              
--------------------
{"k_int_ytom":"P0Y"}

1 row selected.

gSQL> SELECT JSON_ARRAY( INTERVAL '0-0' YEAR TO MONTH ) AS result
        FROM dual; 

RESULT 
-------
["P0Y"]

1 row selected.
```

<a id="6f6dc56803ee7242"></a>
##### Interval Day to Second

Interval Day to Second 타입은 'P[n]DT[n]H[n]M[n]S' 구조로 출력된다.

- 'P'는 기간 (period)을 나타내는 접두사이다.
- 'D' (day)는 날짜 기반 기간을 나타내는 단위이다.
- 'T'는 날짜 기반 기간과 시간 기반 기간을 구분하는 문자이다.
- 'H' (hour), 'M' (minute), 'S' (second)는 시간 기반 기간을 나타내는 단위이다.
- 필요에 따라 소수점 이하 초를 포함할 수 있으며, 소수점 이하 초는 6자리로 고정되어 있다.
    - 예: 'P1DT2H30M15.123000S' (1일 2시간 30분 15.123초)
- 값이 0인 항목은 생략할 수 있다.
    - 예: 'P2DT3H' (2일 3시간), 'PT45M' (45분)
- 모든 값이 0일 경우, 기본값은 '"P0D"'로 출력된다.

```
gSQL> SELECT JSON_OBJECT( 'k_int_dtos' VALUE INTERVAL '1 2:30:15.123' DAY TO SECOND ) AS result
        FROM dual;

RESULT                              
------------------------------------
{"k_int_dtos":"P1DT2H30M15.123000S"}

1 row selected.


gSQL> SELECT JSON_ARRAY( INTERVAL '1 2:30:15.123' DAY TO SECOND ) AS result
        FROM dual;

RESULT                 
-----------------------
["P1DT2H30M15.123000S"]

1 row selected.

gSQL> SELECT JSON_OBJECT( 'k_int_dtos' VALUE INTERVAL '0 00:30:00' DAY TO SECOND ) AS result
        FROM dual;

RESULT                
----------------------
{"k_int_dtos":"PT30M"}

1 row selected.

gSQL> SELECT JSON_ARRAY( INTERVAL '0 00:30:00' DAY TO SECOND ) AS result
        FROM dual;

RESULT   
---------
["PT30M"]

1 row selected.

gSQL> SELECT JSON_OBJECT( 'k_int_dtos' VALUE INTERVAL '0 00:00:00' DAY TO SECOND ) AS result
        FROM dual;

RESULT              
--------------------
{"k_int_dtos":"P0D"}

1 row selected.

gSQL> SELECT JSON_ARRAY( INTERVAL '0 00:00:00' DAY TO SECOND ) AS result
        FROM dual;

RESULT 
-------
["P0D"]

1 row selected.
```

<a id="b92246d82719ed44"></a>
### 호환성

JSON string constructor에 대한 SQL 표준 호환성은 다음과 같다.

**SQL 표준 호환성**

<a id="aba52577a3832fb1"></a>
| Feature ID | 설명 | 지원 여부 |
| --- | --- | --- |
| T811 | Basic SQL/JSON constructor functions | O |
| T812 | SQL/JSON: JSON_OBJECTAGG | O |
| T813 | SQL/JSON: JSON_ARRAYAGG with ORDER BY | O |
| T814 | Colon in JSON_OBJECT or JSON_OBJECTAGG | O |
| T830 | Enforcing unique keys in SQL/JSON constructor functions | O |

---

[← 10. Server Property](../part-02-administration-manual/10-server-property.md) · [전체 목차](../README.md) · [12. SQL Languages →](12-sql-languages.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
