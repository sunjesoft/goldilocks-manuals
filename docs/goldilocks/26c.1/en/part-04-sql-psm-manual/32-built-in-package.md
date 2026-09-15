<a id="ce28a4e2e4ab76a6"></a>

# 32. Built-in Package

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/ce28a4e2e4ab76a6)  
> Tag: `26c.1_0_tag`

[← 31. PSM SQL References](31-psm-sql-references.md) · [Table of contents](../README.md) · [33. Database Connection →](../part-05-developer-manual/33-database-connection.md)

<a id="ac6c00fe81320dc4"></a>
## DBMS_LOCK Package

<a id="15eb7e94f3ee7e90"></a>
### Execution

Execute DBMS_LOCK.sql as follows to use DBMS_LOCK package.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_LOCK.sql
```

<a id="02ee3da55be56b7d"></a>
### Package Routines

<a id="14d105b7e4fd4ad5"></a>
#### SLEEP Procedure

It is a procedure which pauses the session for the specified time.

<a id="aafa5b849f535246"></a>
##### Procedure Definition

```
PROCEDURE SLEEP( seconds IN NATIVE_INTEGER )
```

<a id="34af297ce85b31b5"></a>
##### Parameters

**SLEEP Procedure Parameters**

<a id="d38b631bb4e4e77f"></a>
| Parameter | Description |
| --- | --- |
| seconds | It is the time of pausing a session. (Seconds)  The value of seconds should be 0 or bigger. |

<a id="47731896a279d678"></a>
##### Example

```
gSQL> DECLARE
  V1 VARCHAR(20);
BEGIN
  SELECT TO_CHAR( SYSTIME, 'HH24:MI:SS' ) INTO V1 FROM DUAL;
  DBMS_OUTPUT.PUT_LINE( 'CURRENT TIME = ' || V1 );
  DBMS_LOCK.SLEEP( 3 );
  DBMS_OUTPUT.PUT_LINE( 'DBMS_LOCK.SLEEP( 3 ) ');
  SELECT TO_CHAR( SYSTIME, 'HH24:MI:SS' ) INTO V1 FROM DUAL;
  DBMS_OUTPUT.PUT_LINE( 'CURRENT TIME = ' || V1 );
END;
/
CURRENT TIME = 11:53:09
DBMS_LOCK.SLEEP( 3 ) 
CURRENT TIME = 11:53:12
Anonymous PL block executed.
```

<a id="6f9299d4fb99d36c"></a>
## DBMS_OUTPUT Package

<a id="2ab2d133f122d2e3"></a>
### Execution

Execute DBMS_OUTPUT.sql as follows to use DBMS_OUTPUT Package.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_OUTPUT.sql
```

<a id="3b3538d850346cac"></a>
### Package Routines

<a id="1f009213051dc6d5"></a>
#### DISABLE Procedure

It disables the message logging feature.  
All previously logged messages are disposed.

<a id="356adf93a179dd67"></a>
##### Procedure Definition

```
PROCEDURE DISABLE
```

<a id="dc3fdba8bd823a54"></a>
##### Example

```
gSQL> BEGIN
  DBMS_OUTPUT.DISABLE;
  DBMS_OUTPUT.PUT_LINE( 'DBMS_OUTPUT() Message' );
END;
/
Anonymous PL block executed.
```

<a id="63eb316360196b38"></a>
#### ENABLE Procedure

It is a procedure which enables the message logging feature with a given buffer size.  
If it is already enabled, all messages are disposed and a new buffer is created.

<a id="9e7f0915cb879d1b"></a>
##### Procedure Definition

```
PROCEDURE ENABLE( buffer_size IN NATIVE_INTEGER := 20000 )
```

<a id="00d1ebe5b4e510a6"></a>
##### Parameters

**ENABLE Procedure Parameters**

<a id="dffc7d0fe744a943"></a>
| Parameter | Description |
| --- | --- |
| buffer_size | It is a buffer size and the default size is 20000 bytes. If buffer_size is not specified or is NULL, then the buffer size is 20000 bytes. |

<a id="a8fc1d12d349a729"></a>
##### Example

```
gSQL> BEGIN
  DBMS_OUTPUT.ENABLE;  
  DBMS_OUTPUT.PUT_LINE( 'DBMS_OUTPUT() Message' );
END;
/
DBMS_OUTPUT() Message
Anonymous PL block executed.
```

<a id="f24f941b8e732cea"></a>
#### GET_LINE Procedure

It returns a oldest message line which has not been read among the messages stored in the buffer.

<a id="a4e910e22fbf5f63"></a>
##### Procedure Definition

```
PROCEDURE GET_LINE( line OUT VARCHAR(4000),
                    status OUT NATIVE_INTEGER )
```

<a id="00dd53176a8aaa6e"></a>
##### Parameters

**GET_LINE Procedure Parameters**

<a id="d1afdbdbd4b82ad6"></a>
| Parameter | Description |
| --- | --- |
| line | It reads a line excluding newline character from a buffer, and returns it. |
| status | If the message exists, then it returns 0. If it does not exist, then it returns 1. |

<a id="ed83b11d6c739c4f"></a>
##### Example

```
gSQL> var msg VARCHAR(100);
gSQL> var status INTEGER;
gSQL> BEGIN
  DBMS_OUTPUT.PUT_LINE( 'DBMS_OUTPUT() Message' );
  DBMS_OUTPUT.GET_LINE( :msg, :status );
END;
/
Anonymous PL block executed.

gSQL> \print msg

MSG                   
----------------------
DBMS_OUTPUT() Message

gSQL> \print status

STATUS
------
     0
```

<a id="274a2600a6f2ace7"></a>
#### NEW_LINE Procedure

It stores a newline character in the buffer.

<a id="ada3b969e773915f"></a>
##### Procedure Definition

```
PROCEDURE NEW_LINE
```

<a id="b81b330f6a2c7fbc"></a>
##### Example

```
gSQL> BEGIN
  DBMS_OUTPUT.PUT( 'DBMS_OUTPUT()' );
  DBMS_OUTPUT.PUT( ' Message' );
  DBMS_OUTPUT.NEW_LINE;
END;
/
DBMS_OUTPUT() Message
Anonymous PL block executed.
```

<a id="c8d4a49680f0841b"></a>
#### PUT Procedure

It stores the message which is created with the given expression in the buffer.

<a id="4c557c6383ee1c63"></a>
##### Procedure Definition

```
PROCEDURE PUT( item IN VARCHAR(4000) )
```

<a id="e46d806a9949ea30"></a>
##### Parameters

**PUT Procedure Parameters**

<a id="07d34a67c0003e38"></a>
| Parameter | Description |
| --- | --- |
| item | It is an expression to be stored in the buffer without a newline character. |

<a id="f5a2e8ae265e7060"></a>
##### Example

```
gSQL> var msg VARCHAR(100);
gSQL> var status INTEGER;
gSQL> BEGIN
  DBMS_OUTPUT.PUT( 'DBMS_OUTPUT()' );
  DBMS_OUTPUT.PUT( ' Message' );
  DBMS_OUTPUT.NEW_LINE;
  DBMS_OUTPUT.GET_LINE( :msg, :status );
END;
/
Anonymous PL block executed.

gSQL> \print msg

MSG                  
---------------------
DBMS_OUTPUT() Message

gSQL> \print status

STATUS
------
     0
```

<a id="4b7c394938006a16"></a>
#### PUT_LINE Procedure

It adds the last newline character to the message created with the given expression, and stores it in the buffer.

<a id="796df58de4cddf2c"></a>
##### Procedure Definition

```
PROCEDURE PUT_LINE( item IN VARCHAR(4000) )
```

<a id="e134dac32ac77c28"></a>
##### Parameters

**PUT_LINE Procedure Parameters**

<a id="eb0a978a9d0bef9c"></a>
| Parameter | Description |
| --- | --- |
| item | It is an expression to be stored in the buffer including a newline character. |

<a id="b88f44dcd1d1e48e"></a>
##### Example

```
gSQL> BEGIN
  DBMS_OUTPUT.PUT_LINE( 'DBMS_OUTPUT()' );
  DBMS_OUTPUT.PUT_LINE( ' Message' );
END;
/
DBMS_OUTPUT()
 Message
Anonymous PL block executed.
```

<a id="2428abdeb58e9991"></a>
#### SET_LOG Procedure

It is simultaneously output on the file in the given path when logging the message.

<a id="cad84b38bf50e418"></a>
##### Procedure Definition

```
PROCEDURE SET_LOG( file_path IN VARCHAR(4000), 
                   permission IN NATIVE_INTEGER := 600 )
```

<a id="7ec2ca5b5a5a08fd"></a>
##### Parameters

**SET_LOG Procedure Parameters**

<a id="517ccd0345c1095c"></a>
| Parameter | Description |
| --- | --- |
| file_path | It is the file path where the message will be logged. If the file path is a relative path, then it looks for the target file under the directory corresponding to &lt;SYSTEM_LOGGER DIR&gt; property. |
| permission | The default permission is 600. It specifies the permission of the file. |

<a id="234340ae278aef16"></a>
##### Example

```
gSQL> BEGIN
   DBMS_OUTPUT.SET_LOG('output.log', 600);
   DBMS_OUTPUT.PUT_LINE( 'DBMS_OUTPUT() Message' );
END;
/
DBMS_OUTPUT() Message
Anonymous PL block executed.

gSQL> !cat $GOLDILOCKS_DATA/trc/output.log
DBMS_OUTPUT() Message
```

<a id="a819d824dcf50a58"></a>
## DBMS_SQL Package

<a id="f35df6360294810f"></a>
### Execution

Execute DBMS_SQL.sql as follows to use DBMS_SQL package.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_SQL.sql
```

<a id="1842e1fd05dd569e"></a>
### Package Routines

<a id="d17c9ee5dc6fbb89"></a>
#### RETURN_RESULT Procedure

It returns the query result which was executed through the ref cursor to the client application.

<a id="ebc6633eb6dd88ed"></a>
##### Procedure Definition

```
PROCEDURE RETURN_RESULT( rc IN SYS_REFCURSOR )
```

<a id="01eb9d18eace7ab6"></a>
##### Parameters

**RETURN_RESULT Procedure Parameters**

<a id="42676357cbd212f1"></a>
| Parameter | Description |
| --- | --- |
| rc | It is the reference cursor for the query result. |

<a id="2df4dd19609b41ef"></a>
##### Example

```
gSQL> DECLARE
  rc1 SYS_REFCURSOR;
BEGIN
  OPEN rc1 FOR SELECT SESSION_ID(), SESSION_SERIAL(), SESSION_USER() FROM DUAL;
  DBMS_SQL.RETURN_RESULT( rc1 );
END;
/ 
Anonymous PL block executed.

ResultSet #1

SESSION_ID() SESSION_SERIAL() SESSION_USER()
------------ ---------------- --------------
          31               13 TEST
```

<a id="4c82915a169b5813"></a>
## DBMS_STANDARD Package

<a id="65426483809569a7"></a>
### Execution

Execute DBMS_STANDARD.sql as follows to use DBMS_STANDARD package.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_STANDARD.sql
```

<a id="478d78b50f811401"></a>
### Package Routines

<a id="bccac45ce5c02864"></a>
#### RAISE_APPLICATION_ERROR Procedure

It raises an arbitrary user exception.

<a id="7c3e85de4cf71851"></a>
##### Procedure Definition

```
PROCEDURE RAISE_APPLICATION_ERROR( error_code    IN NATIVE_INTEGER,
                                   error_message IN VARCHAR(4000),
                                   stack_flag    IN BOOLEAN := FALSE )
```

<a id="366081f22345c71f"></a>
##### Parameters

**RAISE_APPLICATION_ERROR Procedure Parameters**

<a id="21d8706b416a3d42"></a>
| Parameter | Description |
| --- | --- |
| error_code | It is an arbitrary error code specified by a user. The value between -20000 ~ -20999 is allowed. |
| error_message | It is the error message corresponding the user-specified error code. |
| stack_flag | The default value is FALSE. It the parameter is TRUE, then the error is accumulated on the existing error stack. If it is FALSE, then it substitutes the existing error. |

<a id="55f8085e1f808574"></a>
##### Example

```
gSQL> DECLARE
  V1 INTEGER;
BEGIN
  V1 := 100/0;
EXCEPTION
  WHEN OTHERS THEN
    RAISE_APPLICATION_ERROR (-20000, 'custom error message', TRUE);
END;
/
ERR-2F000(20000): custom error message
ERR-22012(12122): divisor is equal to zero : 
  V1 := 100/0;
        *
ERROR at line 4:
```

---

[← 31. PSM SQL References](31-psm-sql-references.md) · [Table of contents](../README.md) · [33. Database Connection →](../part-05-developer-manual/33-database-connection.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
