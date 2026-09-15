<a id="8174ffb49e90200d"></a>

# 32. Built-in Package

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/8174ffb49e90200d)  
> 태그: `26c.1_0_tag`

[← 31. PSM SQL References](31-psm-sql-references.md) · [전체 목차](../README.md) · [33. Database Connection →](../part-05-developer-manual/33-database-connection.md)

<a id="1546c808087ed586"></a>
## DBMS_LOCK Package

<a id="b929396909289bf4"></a>
### 실행

DBMS_LOCK Package를 사용하기 위해서는 다음과 같이 DBMS_LOCK.sql을 실행해야 한다.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_LOCK.sql
```

<a id="e857e80640349ee8"></a>
### Package Routines

<a id="03944b1dbb2617fa"></a>
#### SLEEP Procedure

지정된 시간 동안 세션을 일시 중지하는 Procedure이다.

<a id="33ed44b81304bf21"></a>
##### Procedure Definition

```
PROCEDURE SLEEP( seconds IN NATIVE_INTEGER )
```

<a id="7d99915fcc32deda"></a>
##### Parameters

**SLEEP Procedure Parameters**

<a id="b46bdcafd6b5f3f5"></a>
| Parameter | 설명 |
| --- | --- |
| seconds | 세션을 일시 중단하는 시간 (초)이다. seconds 값은 0 이상이어야 한다. |

<a id="a3f623b161879c26"></a>
##### 사용 예

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

<a id="0db42e81688817a5"></a>
## DBMS_OUTPUT Package

<a id="911456c8c107d659"></a>
### 실행

DBMS_OUTPUT Package를 사용하기 위해서는 다음과 같이 DBMS_OUTPUT.sql을 실행해야 한다.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_OUTPUT.sql
```

<a id="d0083f7460b6a696"></a>
### Package Routines

<a id="b0eab453359938dc"></a>
#### DISABLE Procedure

메시지 로깅 기능을 비활성화 한다.  
기존에 로깅된 모든 메시지는 버려진다.

<a id="9cf3300404785469"></a>
##### Procedure Definition

```
PROCEDURE DISABLE
```

<a id="ee5e54374f8310bf"></a>
##### 사용 예

```
gSQL> BEGIN
  DBMS_OUTPUT.DISABLE;
  DBMS_OUTPUT.PUT_LINE( 'DBMS_OUTPUT() Message' );
END;
/
Anonymous PL block executed.
```

<a id="6f897be4aed9ca68"></a>
#### ENABLE Procedure

주어진 버퍼 크기로 메시지 로깅 기능을 활성화하는 Procedure이다.  
기존에 활성화 되어 있으면 모든 메시지를 버리고 새로 버퍼를 생성한다.

<a id="06ca7855c9bb4e97"></a>
##### Procedure Definition

```
PROCEDURE ENABLE( buffer_size IN NATIVE_INTEGER := 20000 )
```

<a id="62af7c7417f114aa"></a>
##### Parameters

**ENABLE Procedure Parameters**

<a id="3f8e1acdbf3fd74e"></a>
| Parameter | 설명 |
| --- | --- |
| buffer_size | 버퍼 크기를 나타내며 기본 크기는 20000 바이트이다. buffer_size를 명시하지 않거나 NULL이면 buffer 크기는 20000 바이트이다. |

<a id="6d8a8cad75074578"></a>
##### 사용 예

```
gSQL> BEGIN
  DBMS_OUTPUT.ENABLE;  
  DBMS_OUTPUT.PUT_LINE( 'DBMS_OUTPUT() Message' );
END;
/
DBMS_OUTPUT() Message
Anonymous PL block executed.
```

<a id="0da516cd380b276d"></a>
#### GET_LINE Procedure

버퍼에 저장된 메시지들 중에 아직 읽지 않은 가장 오래된 메시지 라인 한 줄을 반환한다.

<a id="dc7997eedcd3dcb8"></a>
##### Procedure Definition

```
PROCEDURE GET_LINE( line OUT VARCHAR(4000),
                    status OUT NATIVE_INTEGER )
```

<a id="046884800aede342"></a>
##### Parameters

**GET_LINE Procedure Parameters**

<a id="2715eee4fdcfded1"></a>
| Parameter | 설명 |
| --- | --- |
| line | 개행 문자를 제외한 1줄을 buffer에서 읽어 반환한다. |
| status | 메시지를 존재하면 0을 반환하고, 없으면 1을 반환한다. |

<a id="67dcaf6f63622326"></a>
##### 사용 예

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

<a id="a4072c0c58643cef"></a>
#### NEW_LINE Procedure

개행 문자를 버퍼에 저장한다.

<a id="9ee06bffd322f2fe"></a>
##### Procedure Definition

```
PROCEDURE NEW_LINE
```

<a id="8c088d87ffff0d8d"></a>
##### 사용 예

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

<a id="13bdb5c843480668"></a>
#### PUT Procedure

주어진 expression으로 만들어진 메시지를 버퍼에 저장한다.

<a id="e497a0e6912bfd1a"></a>
##### Procedure Definition

```
PROCEDURE PUT( item IN VARCHAR(4000) )
```

<a id="1d759d8bd8341d5f"></a>
##### Parameters

**PUT Procedure Parameters**

<a id="da170e23180ccaac"></a>
| Parameter | 설명 |
| --- | --- |
| item | 개행 문자 없이 buffer에 저장할 expression 이다. |

<a id="3509a2ec04c24d77"></a>
##### 사용 예

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

<a id="c494268a5e3c7abd"></a>
#### PUT_LINE Procedure

주어진 expression으로 만들어진 메시지에 마지막 개행 문자를 추가하여 버퍼에 저장한다.

<a id="727a8795ed68da82"></a>
##### Procedure Definition

```
PROCEDURE PUT_LINE( item IN VARCHAR(4000) )
```

<a id="0e81a3b2c5d56c6a"></a>
##### Parameters

**PUT_LINE Procedure Parameters**

<a id="a3d93ac62e064f63"></a>
| Parameter | 설명 |
| --- | --- |
| item | 개행 문자를 포함하여 buffer에 저장할 expression 이다. |

<a id="ae7d689042b247b8"></a>
##### 사용 예

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

<a id="eacbd7b5ff2d6914"></a>
#### SET_LOG Procedure

메시지를 로깅할 때 주어진 경로에 있는 파일에도 동시에 출력한다.

<a id="a68d00260d76a766"></a>
##### Procedure Definition

```
PROCEDURE SET_LOG( file_path IN VARCHAR(4000), 
                   permission IN NATIVE_INTEGER := 600 )
```

<a id="fd7f2c0fa166b667"></a>
##### Parameters

**SET_LOG Procedure Parameters**

<a id="0aaae5a3ed5a90ef"></a>
| Parameter | 설명 |
| --- | --- |
| file_path | 메시지를 로깅할 파일의 경로이다. 파일의 경로가 상대 경로이면 &lt;SYSTEM_LOGGER_DIR&gt; 프로퍼티에 해당하는 디렉토리 아래에서 대상 파일을 찾는다. |
| permission | 기본 권한은 600이다. file의 권한을 지정한다. |

<a id="ea75b1c6cff9a55f"></a>
##### 사용 예

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

<a id="6a3fdd4a1042b7a7"></a>
## DBMS_SQL Package

<a id="7b3e0b217d6986fe"></a>
### 실행

DBMS_SQL Package를 사용하기 위해서는 다음과 같이 DBMS_SQL.sql을 실행해야 한다.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_SQL.sql
```

<a id="ac8ad7fd5e0adc1e"></a>
### Package Routines

<a id="17bc366c75907fe9"></a>
#### RETURN_RESULT Procedure

ref cursor를 통해 실행된 질의 결과를 클라이언트 어플리케이션에 반환한다.

<a id="eeb33b6fee41842a"></a>
##### Procedure Definition

```
PROCEDURE RETURN_RESULT( rc IN SYS_REFCURSOR )
```

<a id="7053127b0707eea5"></a>
##### Parameters

**RETURN_RESULT Procedure Parameters**

<a id="3cfaadc3c12be73b"></a>
| Parameter | 설명 |
| --- | --- |
| rc | 질의 결과를 위한 reference cursor 이다. |

<a id="4aa821870946ebe7"></a>
##### 사용 예

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

<a id="8018ec8fa790dad4"></a>
## DBMS_STANDARD Package

<a id="6e240f13a0e62feb"></a>
### 실행

DBMS_STANDARD Package를 사용하기 위해서는 다음과 같이 DBMS_STANDARD.sql을 실행해야 한다.

```
% gsql sys gliese --as sysdba --import $GOLDILOCKS_HOME/admin/packages/DBMS_STANDARD.sql
```

<a id="785146b5734d9cc6"></a>
### Package Routines

<a id="302dd861e432bac0"></a>
#### RAISE_APPLICATION_ERROR Procedure

임의의 사용자 exception을 발생시킨다.

<a id="853d7530778b302f"></a>
##### Procedure Definition

```
PROCEDURE RAISE_APPLICATION_ERROR( error_code    IN NATIVE_INTEGER,
                                   error_message IN VARCHAR(4000),
                                   stack_flag    IN BOOLEAN := FALSE )
```

<a id="ed2d011b2f944a43"></a>
##### Parameters

**RAISE_APPLICATION_ERROR Procedure Parameters**

<a id="5f5cc7ddeb976c24"></a>
| Parameter | 설명 |
| --- | --- |
| error_code | 사용자가 지정한 임의의 에러 코드이다. -20000 ~ -20999 사이의 값만 허용한다. |
| error_message | 사용자가 지정한 에러 코드에 해당하는 에러 메시지이다. |
| stack_flag | 기본값은 FALSE이다. parameter가 TRUE이면 기존 에러 스택에 에러를 쌓고, FALSE이면 기존의 에러를 대체한다. |

<a id="550187dcad43e0f4"></a>
##### 사용 예

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

[← 31. PSM SQL References](31-psm-sql-references.md) · [전체 목차](../README.md) · [33. Database Connection →](../part-05-developer-manual/33-database-connection.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
