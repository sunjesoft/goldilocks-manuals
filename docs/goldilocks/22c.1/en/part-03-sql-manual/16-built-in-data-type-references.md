<a id="a90121b2dc2d62f4"></a>

# 16. Built-in Data Type References

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/a90121b2dc2d62f4)  
> Tag: `22c.1_10_tag`

[← 15. SQL Tuning](15-sql-tuning.md) · [Table of contents](../README.md) · [17. Built-in Function References →](17-built-in-function-references.md)

<a id="a27c8bd4daa34d34"></a>
## Aliases of Built-in Data Types

- BIGINT
    - It is as same as NUMBER(19,0).
    - Refer to [NUMBER](#8b9bf393a6b71702).
- BINARY
    - Refer to [BINARY](#cdba24bfff4b3bfd).
- BINARY VARYING
    - Refer to [BINARY VARYING](#b2a630321104f6a3) .
- BINARY LONG VARYING
    - Refer to [BINARY LONG VARYING](#40f9036f7bb326d8) .
- BOOLEAN
    - Refer to [BOOLEAN](#a62b94ed1d88f602).
- CHAR
    - It is as same as CHARACTER.
    - Refer to [CHARACTER](#c2f6a601412ef1cc).
- CHARACTER
    - Refer to [CHARACTER](#c2f6a601412ef1cc).
- CHARACTER VARYING
    - Refer to [CHARACTER VARYING](#f627085c747f8be8).
- CHARACTER LONG VARYING
    - Refer to [CHARACTER LONG VARYING](#ce64f50f891e4a29).
- DATE
    - Refer to [DATE](#8689fda1b80cf3b7).
- DEC
    - It is as same as NUMERIC.
    - Refer to [NUMERIC](#8cdfb339ae3e47bf).
- DECIMAL
    - It is as same as NUMERIC.
    - Refer to [NUMERIC](#8cdfb339ae3e47bf).
- DOUBLE
    - It is as same as FLOAT(53).
    - Refer to [FLOAT](#e1bb6a1eec7496d0).
- DOUBLE PRECISION
    - It is as same as FLOAT(53).
    - Refer to [FLOAT](#e1bb6a1eec7496d0).
- FLOAT
    - Refer to [FLOAT](#e1bb6a1eec7496d0).
- FLOAT4
    - It is as same as FLOAT(24).
    - Refer to [FLOAT](#e1bb6a1eec7496d0).
- FLOAT8
    - It is as same as FLOAT(53).
    - Refer to [FLOAT](#e1bb6a1eec7496d0).
- INT
    - It is as same as NUMBER(10,0).
    - Refer to [NUMBER](#8b9bf393a6b71702).
- INT2
    - It is as same as NUMBER(5,0).
    - Refer to [NUMBER](#8b9bf393a6b71702).
- INT4
    - It is as same as NUMBER(10,0).
    - Refer to [NUMBER](#8b9bf393a6b71702).
- INT8
    - It is as same as NUMBER(19,0).
    - Refer to [NUMBER](#8b9bf393a6b71702).
- INTEGER
    - It is as same as NUMBER(10,0).
    - Refer to [NUMBER](#8b9bf393a6b71702).
- INTERVAL
    - Refer to [INTERVAL](#22fc0092f6f0fd6f).
- LONG BINARY VARYING
    - It is as same as BINARY LONG VARYING. 
    - Refer to [BINARY LONG VARYING](#40f9036f7bb326d8).
- LONG CHAR VARYING
    - It is as same as CHARACTER LONG VARYING.
    - Refer to [CHARACTER LONG VARYING](#ce64f50f891e4a29).
- LONG CHARACTER VARYING
    - It is as same as CHARACTER LONG VARYING. 
    - Refer to [CHARACTER LONG VARYING](#ce64f50f891e4a29).
- LONG VARCHAR
    - It is as same as CHARACTER LONG VARYING.
    - Refer to [CHARACTER LONG VARYING](#ce64f50f891e4a29).
- NATIVE_BIGINT
    - Refer to [NATIVE_BIGINT](#3ab4c4c4b2da694c).
- NATIVE_DOUBLE
    - Refer to [NATIVE_DOUBLE](#16b7464454d1f023).
- NATIVE_INTEGER
    - Refer to [NATIVE_INTEGER](#781670ea6f07e05f).
- NATIVE_REAL
    - Refer to [NATIVE_REAL](#00e9340516368be0).
- NATIVE_SMALLINT
    - Refer to [NATIVE_SMALLINT](#6d0effad10db44e1).
- NUMBER
    - Refer to [NUMBER](#8b9bf393a6b71702).
- NUMERIC
    - Refer to [NUMERIC](#8cdfb339ae3e47bf).
- ROWID
    - Refer to [ROWID](#15b522cf4559d114).
- SMALLINT
    - It is as same as NUMBER(5,0). 
    - Refer to [NUMBER](#8b9bf393a6b71702).
- TIME
    - Refer to [TIME](#654af5ad2c0e7412).
- TIMESTAMP
    - Refer to [TIMESTAMP](#a616b596ff859564).
- VARBINARY
    - It is as same as BINARY VARYING.
    - Refer to [BINARY VARYING](#b2a630321104f6a3).
- VARCHAR
    - It is as same as CHARACTER VARYING. 
    - Refer to [CHARACTER VARYING](#f627085c747f8be8).
- VARCHAR2
    - It is as same as CHARACTER VARYING. 
    - Refer to [CHARACTER VARYING](#f627085c747f8be8).

<a id="cdba24bfff4b3bfd"></a>
## BINARY

<a id="7c963e2d4172fee1"></a>
### Syntax

```
BINARY [ (length) ]
```

<a id="2b6bcdc0a6ee3ed8"></a>
### Syntax Rules and Parameters

- length: It is the binary string length.
    - Range: 1 ~ 2000
    - Default value: 1

<a id="336fa861642c9a70"></a>
### Description

A fixed-length binary string is stored.  
If the binary string length to be stored is shorter than the specified length,  X'00 ' is stored in the remaining part.  
• Storage size: Bytes of the length value

<a id="d9931281d4a4d725"></a>
### For More Information

Refer to the followings.

- [BINARY VARYING](#b2a630321104f6a3)
- [BINARY LONG VARYING](#40f9036f7bb326d8)

<a id="b2a630321104f6a3"></a>
## BINARY VARYING

<a id="00906d1a24a7f026"></a>
### Syntax

```
BINARY VARYING (length)
```

<a id="0c321ad31b105f5d"></a>
### Syntax Rules and Parameters

- length: It is the maximum length of binary string.
    - Range: 1 ~ 4000

<a id="22961e99bb5dbd8a"></a>
### Description

The variable-length binary string is stored.  

• Storage size: Bytes of the binary string to be stored  
• Alias names: VARBINARY

<a id="d66b90c088230595"></a>
### For More Information

Refer to the followings.

- [BINARY](#cdba24bfff4b3bfd)
- [BINARY LONG VARYING](#40f9036f7bb326d8)

<a id="40f9036f7bb326d8"></a>
## BINARY LONG VARYING

<a id="283ee43d1f8a80a4"></a>
### Syntax

```
BINARY LONG VARYING
```

<a id="b7602cb8161d0d63"></a>
### Description

The value of the long variable binary string is stored.  
• Maximum storage size: 100 megabytes  
• Storage size: Bytes of the binary string to be stored  
• Alias names: LONG BINARY VARYING, LONG VARBINARY

It can not be used as a column of the key, so there are limitations as follows.  
• It can not be used as a key column of an index.  
• It can not be used as the expression of ORDER BY clause.   
• It can not be used as the expression of GROUP BY clause.  
• It can not be used as the expression of DISTINCT clause.  
• It can not be used as the expression of UNION, INTERSECT, EXCEPT clauses.

<a id="0f5d2547290e4e89"></a>
### For More Information

Refer to the followings.

- [BINARY](#cdba24bfff4b3bfd)
- [BINARY VARYING](#b2a630321104f6a3)

<a id="a62b94ed1d88f602"></a>
## BOOLEAN

<a id="fdedbe4b0a935d9c"></a>
### Syntax

```
BOOLEAN
```

<a id="3ad9c3d4f2414999"></a>
### Description

TRUE or FALSE is stored.  
• Storage size: 1 byte.

<a id="c2f6a601412ef1cc"></a>
## CHARACTER

<a id="d4ca64ee0a86b7ea"></a>
### Syntax

```
CHARACTER [ (length [ CHARACTERS | OCTETS | CHAR | BYTE ] ) ]
```

<a id="1f7af814100b4a28"></a>
### Syntax Rules and Parameters

- length: It is the string length.
    - Range: 1 ~ 2000
    - Default value: 1

- [ CHARACTERS | OCTETS | CHAR | BYTE ]: It is unit of length.
    - CHARACTERS
        - The number of characters
        - CHAR is as same as CHARACTERS.
    - OCTETS
        - The number of bytes
        - BYTE is as same as OCTETS.
    - If omitted, the default is the property value of [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#24f01f5e333485e5) which is set when creating database.

<a id="24f19b1ddcd80b2a"></a>
### Description

A fixed-length string is stored.  
If the length of the string to be stored is shorter than the specified length, white spaces are stored in the remaining part.

- Storage size: Bytes of the length value
- Alias name: CHAR

<a id="2bfc577f8beb7688"></a>
### For More Information

Refer to the followings.

- [CHARACTER VARYING](#f627085c747f8be8)
- [CHARACTER LONG VARYING](#ce64f50f891e4a29)

<a id="f627085c747f8be8"></a>
## CHARACTER VARYING

<a id="d736a4c5e79fab57"></a>
### Syntax

```
CHARACTER VARYING ( length [ CHARACTERS | OCTETS | CHAR | BYTE ] )
```

<a id="a7b24d3279d6b469"></a>
### Syntax Rules and Parameters

- length: It is the string length.
    - Range: 1 ~ 4000

- [ CHARACTERS | OCTETS | CHAR | BYTE ]: It is unit of length.
    - CHARACTERS
        - The number of characters
        - CHAR is as same as CHARACTERS.
    - OCTETS
        - The number of bytes
        - BYTE is as same as OCTETS.
    - If omitted, the default is the property value of [CHAR_LENGTH_UNITS](../part-02-administration-manual/10-server-property.md#24f01f5e333485e5) which is set when creating database.

<a id="99561064ccf975a6"></a>
### Description

The variable-length string is stored.  

• Storage size: Bytes of the string to be stored  
• Alias names: VARCHAR, VARCHAR2

<a id="09011102fe757d25"></a>
### For More Information

Refer to the followings.

- [CHARACTER](#c2f6a601412ef1cc)
- [CHARACTER LONG VARYING](#ce64f50f891e4a29)

<a id="ce64f50f891e4a29"></a>
## CHARACTER LONG VARYING

<a id="607f8b01efbf41a8"></a>
### Syntax

```
CHARACTER LONG VARYING
```

<a id="c5c9d9a5a58e4ac1"></a>
### Description

The value of the long variable-length string is stored.  

• Maximum storage size: 100 megabytes  
• Storage size: Bytes of the string to be stored   
• Alias names: LONG CHARACTER VARYING, LONG CHAR VARYING, LONG VARCHAR

It can not be used as a column of the key, so there are limitations as follows.  

• It can not be used as a key column of an index.  
• It can not be used as the expression of ORDER BY clause.   
• It can not be used as the expression of GROUP BY clause.  
• It can not be used as the expression of DISTINCT clause.  
• It can not be used as the expression of UNION, INTERSECT, EXCEPT clauses.

<a id="ac1f0cbf0059b83f"></a>
### For More Information

Refer to the followings.

- [CHARACTER](#c2f6a601412ef1cc)
- [CHARACTER VARYING](#f627085c747f8be8)

<a id="8689fda1b80cf3b7"></a>
## DATE

<a id="8eb24a2aafdc5755"></a>
### Syntax

```
DATE
```

<a id="360d280029242dfb"></a>
### Description

It is the date type including YEAR, MONTH, DAY, HOUR, MINUTE and SECOND (excluding fractional seconds).  
• Value range: Date value between '4714-11-24 BC' and '9999-12-31 AD'   
• Storage size: 8 bytes

<a id="39c7091f1970e1a8"></a>
### For More Information

Refer to the followings.

- [Date Literals](11-sql-elements.md#b0587faae87d76d3)
- [TIME](#654af5ad2c0e7412)
- [TIMESTAMP](#a616b596ff859564)

<a id="e1bb6a1eec7496d0"></a>
## FLOAT

<a id="22a8620e14acefa9"></a>
### Syntax

```
FLOAT[ ( precision ) ]
```

<a id="bb8074b2db3d2bd2"></a>
### Syntax Rules and Parameters

- precision: It is the binary precision of significant digits.
    - Precision range: 1 ~ 126
    - Default value: 126

<a id="5f0f53a590d0d488"></a>
### Description

The floating point value with a binary precision is stored.

- Exponential range: 1E-130 ~ 1E+125
- Storage size: (number of digits in integer part + 1) / 2 + (number of digits in fractional part + 1) / 2 + 1 (exponent, sign)

It has a binary precision value unlike [NUMBER](#8b9bf393a6b71702), [NUMERIC](#8cdfb339ae3e47bf) types.

- Alias names: REAL = FLOAT(24), DOUBLE = FLOAT(53), DOUBLE PRECISION = FLOAT(53), FLOAT4 = FLOAT(24), FLOAT8 = FLOAT(53).

<a id="11dd566ca1a3afb2"></a>
### For More Information

Refer to the followings.

- [NUMBER](#8b9bf393a6b71702)
- [NUMERIC](#8cdfb339ae3e47bf)

<a id="22fc0092f6f0fd6f"></a>
## INTERVAL

<a id="bf23383b010deea9"></a>
### Syntax

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

<a id="64e86da87a2c3bfe"></a>
### Syntax Rules and Parameters

- INTERVAL YEAR [ ( leading_precision ) ]: A period of YEAR is stored.
    - leading_precision 
        - The number of digits in YEAR
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL MONTH [ ( leading_precision ) ]: A period of MONTH is stored.
    - leading_precision 
        - The number of digits in MONTH
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL YEAR [ ( leading_precision ) ] TO MONTH: A period of YEAR and MONTH is stored.
    - leading_precision
        - The number of digits in YEAR
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL DAY [ ( leading_precision ) ]: A period of DAY is stored.
    - leading_precision 
        - The number of digits in DAY
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL HOUR [ ( leading_precision ) ]: A period of HOUR is stored.
    - leading_precision 
        - The number of digits in HOUR
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL MINUTE [ ( leading_precision ) ]: A period of MINUTE is stored.
    - leading_precision 
        - The number of digits in MINUTE
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL SECOND [ ( leading_precision [ , fractional_seconds_precision ] ) ]: A period of SECOND is stored.
    - leading_precision 
        - The number of digits in SECOND
        - Value range: 2 ~ 6
        - Default value: 2
    - fractional_seconds_precision
        - The number of digits in fractional seconds
        - Value range: 0 ~ 6
        - Default value: 6

- INTERVAL DAY [ ( leading_precision ) ] TO HOUR: A period of DAY and HOUR is stored.
    - leading_precision 
        - The number of digits in DAY
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL DAY [ ( leading_precision ) ] TO MINUTE: A period of DAY, HOUR, and MINUTE is stored.
    - leading_precision 
        - The number of digits in DAY
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL DAY [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]: A period of DAY, HOUR, MINUTE, and SECOND is stored.
    - leading_precision 
        - The number of digits in DAY
        - Value range: 2 ~ 6
        - Default value: 2
    - fractional_seconds_precision
        - The number of digits in fractional seconds
        - Value range: 0 ~ 6
        - Default value: 6

- INTERVAL HOUR [ ( leading_precision ) ] TO MINUTE: A period of HOUR and MINUTE is stored.
    - leading_precision 
        - The number of digits in HOUR
        - Value range: 2 ~ 6
        - Default value: 2

- INTERVAL HOUR [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]: A period of HOUR, MINUTE and SECOND is stored.
    - leading_precision 
        - The number of digits in HOUR
        - Value range: 2 ~ 6
        - Default value: 2
    - fractional_seconds_precision
        - The number of digits in fractional seconds
        - Value range: 0 ~ 6
        - Default value: 6

- INTERVAL MINUTE [ ( leading_precision ) ] TO SECOND [ ( fractional_seconds_precision ) ]: A period of MINUTE and SECOND is stored.
    - leading_precision 
        - The number of digits in MINUTE 
        - Value range: 2 ~ 6
        - Default value: 2
    - fractional_seconds_precision
        - The number of digits in fractional seconds
        - Value range: 0 ~ 6
        - Default value: 6

<a id="3633a89edfad90b5"></a>
### Description

INTERVAL types are classified into YEAR TO MONTH family type and DAY TO SECOND family type depending on the range of value representation as follows.

- YEAR TO MONTH family type: Its storage size is 8 bytes.
    - INTERVAL YEAR
    - INTERVAL MONTH
    - INTERVAL YEAR TO MONTH

- DAY TO SECOND family type: Its storage size is 16 bytes.
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

If the number which is bigger than number of the specified digits is in the field to which the leading_precision is specified, then an error is returned.  
If the number which is bigger than number of the specified digits is in the field to which the fractional_seconds_precision is specified, it is rounded off.

**Precisions and value range of the second or later field in INTERVAL * TO ***

<a id="36ef5919e77b6362"></a>
| Field | Precision | Value range |
| --- | --- | --- |
| MONTH | 2 | 0 ~ 11 |
| HOUR | 2 | 0 ~ 23 |
| MINUTE | 2 | 0 ~ 59 |
| SECOND (interger part) | 2 | 0 ~ 59 |

<a id="2e056ed1b1be3b89"></a>
### For More Information

Refer to [Interval Literals](11-sql-elements.md#63d668408fea8219).

<a id="3ab4c4c4b2da694c"></a>
## NATIVE_BIGINT

<a id="733c15054e473c80"></a>
### Syntax

```
NATIVE_BIGINT
```

<a id="d63a8c9629c89806"></a>
### Description

Signed 8-byte integer is stored.

It is as same as long long data type of C language (8 bytes integer).

- Value range: -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807
- Storage size: 8 bytes

<a id="16b7464454d1f023"></a>
## NATIVE_DOUBLE

<a id="798cef46e0384b38"></a>
### Syntax

```
NATIVE_DOUBLE
```

<a id="5c879615ccff3a4a"></a>
### Description

Double precision floating-point number (8 bytes) is stored.

It is as same as double data type of C language.

- Exponential range: 1E-307 ~ 1E+308
- Storage size: 8 bytes

<a id="781670ea6f07e05f"></a>
## NATIVE_INTEGER

<a id="7e511dff5d8dffcd"></a>
### Syntax

```
NATIVE_INTEGER
```

<a id="e0362834c06ab79a"></a>
### Description

Signed 4 byte integer is stored.

It is as same as integer data type of C language (4 bytes).

- Value range: -2,147,483,648 ~ +2,147,483,647
- Storage size: 4 bytes

<a id="00e9340516368be0"></a>
## NATIVE_REAL

<a id="9be025f60895df01"></a>
### Syntax

```
NATIVE_REAL
```

<a id="dd50e07ab4bd2ea7"></a>
### Description

Single precision floating-point number (4 bytes) is stored.

It is as same as float data type of C language.

- Exponential range: 1E-37 ~ 1E+37
- Storage size: 4 bytes

<a id="6d0effad10db44e1"></a>
## NATIVE_SMALLINT

<a id="40fce81d953b3475"></a>
### Syntax

```
NATIVE_SMALLINT
```

<a id="04490ab1e2608966"></a>
### Description

Signed 2 byte integer is stored.

It is as same as short data type of C language.

- Value range: -32,768 ~ 32,767
- Storage size: 2 bytes

<a id="8b9bf393a6b71702"></a>
## NUMBER

<a id="f6d05fda96063c0f"></a>
### Syntax

```
NUMBER  [ ( precision [ , scale ] ) ]
```

<a id="f7e28e0c35259d5d"></a>
### Syntax Rules and Parameters

- NUMBER: A floating point number without a precision and scale is stored.
    - The range of significant digits: 38
    - Exponential range: 1E-130 ~ 1E+125
    - It is as same as FLOAT (126).

- NUMBER(precision): The integer with significant digits of precision is stored.
    - Precision range: 1 ~ 38
    - The scale value: 0
    - It has a decimal precision value unlike [FLOAT](#e1bb6a1eec7496d0) type.
    - It is as same as NUMBER(precision, 0), NUMERIC(precision, 0).

- NUMBER(precision, scale): A fixed point number with precision and scale is stored.
    - Precision range: 1 ~ 38
    - Scale range: -84 ~ 127
    - It has a decimal precision value unlike [FLOAT](#e1bb6a1eec7496d0) type.
    - It is as same as NUMERIC (precision,scale).
    - Alias names: SMALLINT = NUMBER(5,0), INTEGER = NUMBER(10,0), BIGINT = NUMBER(19,0), INT2 = NUMBER(5,0), INT4 = NUMBER(10,0), INT8 = NUMBER(19,0)

<a id="254bb8262a890fcf"></a>
### Description

NUMBER type is similar to NUMERIC type, but if both the precision and scale are omitted, NUMBER type stores the floating point number whose precision and scale are not specified.

- NUMBER without precision, scale: Floating-point number
- NUMERIC without precision, scale: The fixed point number of NUMERIC(38, 0)
- Storage size: (number of digits in integer part + 1) / 2 + (number of digits in fractional part + 1) / 2 + 1 (exponent, sign)

<a id="4b6aa3488ce7efed"></a>
### For More Information

Refer to the followings.

- [FLOAT](#e1bb6a1eec7496d0)
- [NUMERIC](#8cdfb339ae3e47bf)

<a id="8cdfb339ae3e47bf"></a>
## NUMERIC

<a id="c5ed51167923de96"></a>
### Syntax

```
NUMERIC  [ ( precision [ , scale ] ) ]
```

<a id="e31df477781fee3e"></a>
### Syntax Rules and Parameters

- precision: It is the decimal precision of significant digits.
    - precision range: 1 ~ 38
    - Default value: 38

- scale: It is the decimal point range.
    - scale range: -84 ~ 127
    - Default value: 0

<a id="d5f7746c4bae21d5"></a>
### Description

A fixed point number with precision and scale is stored.

If the precision and scale are omitted, it means as follows.

- NUMERIC = NUMERIC(38,0)
- NUMERIC(p) = NUMERIC(p,0)

NUMBER type is similar to NUMERIC type, but if both the precision and scale are omitted, NUMBER type stores the floating-point number whose precision and scale are not specified.

- NUMBER without precision, scale: Floating point number
- NUMERIC without precision, scale: Fixed point number of NUMERIC(38,0)
- Storage size: (number of digits in integer part + 1) / 2 + (number of digits in fractional part + 1) / 2 + 1 (exponent, sign)

<a id="2dddba3e17ab850d"></a>
### For More Information

Refer to the followings.

- [FLOAT](#e1bb6a1eec7496d0)
- [NUMBER](#8b9bf393a6b71702)

<a id="15b522cf4559d114"></a>
## ROWID

<a id="ae1e1503d12785c2"></a>
### Syntax

```
ROWID
```

<a id="59933f1fb8ff32d2"></a>
### Description

A record identifier (ROWID) is stored.  

A record identifier (ROWID) is the identification information of each record in database.  

When querying the ROWID pseudo column, each record identifier (ROWID) is obtained. This ROWID pseudo column has the ROWID data type information.

ROWID type consists of the followings in a stand-alone system.  
• OBJECT_ID   
• TABLESPACE_ID   
• PAGE_ID   
• OFFSET within PAGE

ROWID type consists of the followings in a cluster system.  
• GRID_BLOCK_SEQUENCE  
• GRID_BLOCK_ID  
• MEMBER_ID  
• SHARD_ID

ROWID is stored in the base 64 value, which can include A ~ Z, a ~ z, 0 ~ 9, +, /.  
Each component information of ROWID is obtained using ROWID-related functions.

• Storage size: 16 bytes

<a id="336caa373981d1cf"></a>
### For More Information

Refer to the followings.

- [ROWID Pseudo Column](11-sql-elements.md#1be00498c6fd4676)
- [ROWID-related Functions](11-sql-elements.md#6a6d19f960a479a3)

<a id="654af5ad2c0e7412"></a>
## TIME

<a id="c458f033e6707041"></a>
### Syntax

```
TIME [ ( fractional_seconds_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
```

<a id="3b69522a2d2a440c"></a>
### Syntax Rules and Parameters

- fractional_seconds_precision: It is the number of significant digits in fractional seconds.
    - fractional_seconds_precision range: 0 ~ 6
    - Default value: 6

- [ WITH TIME ZONE | WITHOUT TIME ZONE ]: It specifies whether to store TIME ZONE value.
    - WITH TIME ZONE: The time which includes time zone
    - WITHOUT TIME ZONE: The time which does not include time zone
    - Default value: WITHOUT TIME ZONE

<a id="46b0595e9d5bf9cc"></a>
### Description

The time which includes HOUR, MINUTE and SECOND is stored.

- Storage size 
    - TIME WITHOUT TIME ZONE: 8 bytes
    - TIME WITH TIME ZONE: 12 bytes

<a id="d7511e9ddf8b7d6c"></a>
### For More Information

Refer to the followings.

- [Time Literals](11-sql-elements.md#43ea460ce8516097)
- [Time with Time Zone Literals](11-sql-elements.md#a5ec0ff246fabe14)
- [DATE](#8689fda1b80cf3b7)
- [TIMESTAMP](#a616b596ff859564)

<a id="a616b596ff859564"></a>
## TIMESTAMP

<a id="14784b23c17a6880"></a>
### Syntax

```
TIMESTAMP [ ( fractional_seconds_precision ) ] [ WITH TIME ZONE | WITHOUT TIME ZONE ]
```

<a id="bdc5e2e97e59848d"></a>
### Syntax Rules and Parameters

- fractional_seconds_precision: It is the number of significant digits in the fractional seconds.
    - fractional_seconds_precision range: 0 ~ 6
    - Default value: 6

- [ WITH TIME ZONE | WITHOUT TIME ZONE ]: It specifies whether to store TIME ZONE value.
    - WITH TIME ZONE: The time which includes time zone. 
    - WITHOUT TIME ZONE: The time which does not include time zone. 
    - Default value: WITHOUT TIME ZONE

<a id="48d949b089de25e2"></a>
### Description

The time which includes YEAR, MONTH, DATE, HOUR, MINUTE and SECOND is stored.

- Storage size 
    - TIMESTAMP WITHOUT TIME ZONE: 8 bytes
    - TIMESTAMP WITH TIME ZONE: 12 bytes

<a id="d9785bf76a34ac11"></a>
### For More Information

Refer to the followings.

- [Timestamp Literals](11-sql-elements.md#2ea699144d21921e)
- [Timestamp with Time Zone Literals](11-sql-elements.md#f917d4c9493483f4)
- [DATE](#8689fda1b80cf3b7)
- [TIME](#654af5ad2c0e7412)

---

[← 15. SQL Tuning](15-sql-tuning.md) · [Table of contents](../README.md) · [17. Built-in Function References →](17-built-in-function-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
