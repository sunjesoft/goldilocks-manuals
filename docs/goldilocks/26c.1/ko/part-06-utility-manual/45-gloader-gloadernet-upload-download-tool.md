<a id="75c0ed6d4461d913"></a>

# 45. gloader/gloadernet (Upload/download Tool)

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/75c0ed6d4461d913)  
> 태그: `26c.1_0_tag`

[← 44. gsql/gsqlnet (Interactive SQL Tool)](44-gsql-gsqlnet-interactive-sql-tool.md) · [전체 목차](../README.md) · [46. gdump →](46-gdump.md)

<a id="feca1b18001721b0"></a>
## gloader 개요

gloader는 GOLDILOCKS 내에 존재하는 데이터를 테이블 단위로 다운로드 또는 업로드 할 수 있는 유틸리티이다.

**실행파일 구분**

<a id="3bdc2039ecf521b3"></a>
| 실행파일 이름 | 구분 |
| --- | --- |
| gloader | Direct attach (D/A) 환경에서 사용된다. |
| gloadernet | Client/ server (C/S) 환경에서 사용된다. |

<a id="d54746dd91ee6bf4"></a>
### Environment

gloader는 database와 연결되어야 하고 gloader를 사용할 때 필요한 모든 파일에 주의를 기울여야 한다.

<a id="0b4bb4ce6c7530c3"></a>
![gloader environment](../assets/images/e8dfff3dcc68f203.png)

데이터를 업로드하려면 control file과 datafile이 필요하고 업로드 결과로써 log file이 생성된다.   
데이터를 다운로드하려면 control file이 필요하고 다운로드 결과로써 datafile과 log file, bad file이 생성된다.

<a id="0d60d4242ee5ca65"></a>
#### Control File

Control file은 gloader가 동작하는데 필요한 파일로써 다음과 같은 정보를 가지고 있다. ([Control File 구문](#815b915f23d2e72e)를 참조한다.)

- Table 이름
- Schema 이름
- Row의 column 사이의 구분자
- Column 데이터의 시작과 끝을 알리는 qualifier
- Row 사이의 구분자
- Character set
- 공백 문자에 대한 trim 여부
- Where 절
- Column 지정

<a id="c38e20888366b318"></a>
#### Data File

gloader가 데이터를 업로드 할 때는 data file을 미리 준비해야 하고 데이터를 다운로드 할 때는 datafile이 생성된다.   
Data file은 텍스트 형식과 바이너리 형식을 지원한다.

- 텍스트 형식 데이터 파일은 파일의 내용을 확인하여 직접 수정할 수 있다는 장점이 있다.
- 바이너리 형식 데이터 파일은 텍스트 형식과 비교하여 빠르게 수행할 수 있다.

> gloader는 data file에 대해 default로 direct IO를 사용한다. Direct IO를 사용하여 data file을 업로드 할 때 파일 크기가 direct IO에 적합한 정렬이 아닐 경우, gloader가 임의로 파일 크기를 조절한다.

<a id="4b622207e0c3f915"></a>
#### Log File

Log file은 gloader가 동작하면서 발생하는 다음과 같은 에러와 결과를 기록하는 파일이다.

- 에러가 발생한 row 번호와 원인
- gloader 운영에 대한 결과

<a id="789c53419720f253"></a>
#### Bad File

Bad file은 gloader가 데이터를 업로드하면서 에러가 발생한 row를 기록하는 파일이다. Bad file을 기록할 때 column, row 사이의 구분자와 qualifier는 사용자가 지정한 것을 사용한다.

<a id="0c85316b6afd5c5f"></a>
### 사용 예

다음은 gloader를 이용하여 데이터를 다운로드하고 업로드하는 예이다.

다음과 같이 sql statement를 이용하여 table을 생성한다.

```
$ cat test.sql
CREATE TABLE TEST
(
TEST_NAME VARCHAR(60),
TEST_NUM  INTEGER,
TEST_TIME TIMESTAMP(0) WITH TIME ZONE
);

INSERT INTO TEST VALUES
( 'NAME', 1, '1999-01-08 04:05:06.789 -8:00' );
INSERT INTO TEST VALUES
( 'NAME', 2, '1999-01-08 04:05:06.789 -8:00' );
INSERT INTO TEST VALUES
( 'NAME', 3, '1999-01-08 04:05:06.789 -8:00' );
COMMIT;
```

다음과 같이 control file을 이용한다.

```
$ cat test.ctl
TABLE TEST
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

- Export: 데이터를 다운로드 한다.

```
$ gloader test test --export --control test.ctl --data test.dat --no-copyright

 COMPLETED IN EXPORTING TABLE: PUBLIC.TEST, 3 RECORDS
$ cat test.dat
"NAME","1","1999-01-08 04:05:07. -08:00"
"NAME","2","1999-01-08 04:05:07. -08:00"
"NAME","3","1999-01-08 04:05:07. -08:00"
$ cat test.log
cat test.log
COMPLETED IN EXPORTING TABLE: PUBLIC.TEST, 3 RECORDS [ Start Time: 2010-1-1 01:01:01 End Time: 2010-1-1 01:01:01 Taken Time: 56496 micro-sec ]
```

- Import: 데이터를 업로드 한다.

```
$ cat import.dat
"NAME","1","1999-01-08 04:05:07. -08:00"
"NAME","2","1999-01-08 04:05:07. -08:00"
"NAME","3","1999-01-08 04:05:07. -08:00"
"FAIL","FAIL","FAIL"

$ gloader test test --import --control test.ctl --data import.dat --no-copyright

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 4 RECORDS, SUCCEEDED 3 RECORDS

$ gsql test test
gSQL> select * from test;
TEST_NAME TEST_NUM TEST_TIME                        
--------- -------- ---------------------------------
NAME             1 1999-01-08 04:05:07.000000 -08:00
NAME             2 1999-01-08 04:05:07.000000 -08:00
NAME             3 1999-01-08 04:05:07.000000 -08:00
NAME             1 1999-01-08 04:05:07.000000 -08:00
NAME             2 1999-01-08 04:05:07.000000 -08:00
NAME             3 1999-01-08 04:05:07.000000 -08:00

6 rows selected.

$ cat import.log
Err Rec(4) Col(2): 22018(12006): data value is not a numeric literal
COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 4 RECORDS, SUCCEEDED 3 RECORDS [ Start Time: 2010-1-1 01:01:01 End Time: 2010-1-1 01:01:01 Taken Time: 56496 micro-sec ]

$ cat import.bad
"FAIL","FAIL","FAIL"
```

<a id="befd8268a762d6ef"></a>
## gloader 사용

<a id="5b723665f8b2c54f"></a>
### Datafile Type

<a id="f438161a74ee5f89"></a>
#### Text Datafile

사용자가 눈으로 확인하고 수정할 수 있는 문자열로 표현된다. 직접 파일을 생성하거나 수정할 수 있고 database에 있는 기존 테이블의 데이터를 다운로드 받을 수도 있다. 또한 다른 DBMS 제품에서 다운로드 받은 텍스트 형식의 데이터를 이용할 수도 있다.   
텍스트 타입 데이터 파일의 표현에 대한 설명은 control file에 기록된다.

<a id="7785c0a0611abfa4"></a>
#### Binary Datafile

이진 파일로 되어 있다. 사용자는 binary datafile을 직접 생성하거나 수정할 수 없고 database에 있는 기존 테이블의 데이터를 다운로드 받을 때 생성된다.

Binary 타입 파일의 데이터는 GOLDILOCKS에 정의된 각 데이터 타입의 구조에 적합하게 기록되기 때문에 텍스트 타입보다 빠르게 업로드 할 수 있다.

> GOLDILOCKS database 버전이 서로 다른 경우에는 binary 파일을 이용한 데이터 업로드/ 다운로드를 권하지 않는다. 또한 문자열 집합이 다른 database 사이에 업로드/ 다운로드 할 경우, column의 크기를 변경해야할 수도 있다.

<a id="8976681130c06f7b"></a>
### 데이터 다운로드

<a id="202fddbdee9a0a6c"></a>
#### Text File로 다운로드

<a id="232e90aa20be7b58"></a>
##### Simple Download

다음은 다운로드 할 테이블의 구조와 데이터를 보여준다.

```
$ cat test.sql
CREATE TABLE TEST ( I1 INTEGER PRIMARY KEY, I2 VARCHAR(10), I3 VARBINARY(10) );
INSERT INTO TEST VALUES( 1, 'LKH', X'10' );
INSERT INTO TEST VALUES( 2, 'KMM', X'A0' );
INSERT INTO TEST VALUES( 3, 'ksj', X'CD' );
COMMIT;

$ gsql test test
gSQL> SELECT * FROM TEST;

I1 I2  I3
-- --- --
 1 LKH 10
 2 KMM A0
 3 ksj CD

3 rows selected.
```

다음은 테이블 데이터를 다운로드하기 위해 작성한 control 파일의 내용이다.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
```

다음과 같이 gloader를 통해 T1 테이블의 데이터를 다운로드한다.

```
$ gloader test test --export --control test.ctl --data test.dat

 COMPLETED IN EXPORTING TABLE: PUBLIC.test, TOTAL 3 RECORDS, SUCCEEDED 3 RECORDS
```

다음과 같이 TEST 테이블의 데이터가 데이터 파일에 다운로드 되었다.

```
$ ls 
test.ctl test.dat test.log
$ cat test.dat
1,LKH,10
2,KMM,A0
3,ksj,CD
```

<a id="c32616faae989b22"></a>
##### 공백 문자 처리

다음은 다운로드 할 테이블의 구조와 데이터를 보여준다.

```
$ cat test.sql
CREATE TABLE TEST ( I1 INTEGER PRIMARY KEY, I2 VARCHAR(10), I3 VARBINARY(10) );
INSERT INTO TEST VALUES( 1, ' L K H ', X'10' );
INSERT INTO TEST VALUES( 2, 'KIM
MM', X'A0' );
INSERT INTO TEST VALUES( 3, ' KIM S 
J ', X'CD' );
COMMIT;

$ gsql test test
gSQL> SELECT * FROM TEST;

I1 I2      I3
-- ------- --
 1  L K H  10
 2 KIM     A0
   MM        
 3  KIM S  CD
   J       
3 rows selected.
```

- OPTIONALLY ENCLOSED BY 구문을 사용하지 않은 control 파일

    - 다음은 테이블 데이터를 다운로드하기 위해 작성한 control 파일의 내용이다.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
LINES TERMINATED BY '\n'
```

    - 다음은 TEST 테이블의 데이터가 데이터 파일에 다운로드된 모습이다.

```
$ ls 
test.ctl test.dat test.log
$ cat test.dat
1, L K H ,10
2,KIM
MM,A0
3, KIM S 
J ,CD
```

> 데이터에 공백 문자가 있는 경우 control 파일에 OPTIONALLY ENCLOSED BY 구문을 사용해야 다운로드 할 때와 업로드 할 때 모두 동일한 데이터를 유지할 수 있다.

- OPTIONALLY ENCLOSED BY 구문을 사용한 control 파일

    - 다음은 테이블 데이터를 다운로드하기 위해 작성한 control 파일의 내용이다.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

    - 다음은 TEST 테이블의 데이터가 데이터 파일에 다운로드된 모습이다.

```
$ ls 
test.ctl test.dat test.log
$ cat test.dat
"1"," L K H ","10"
"2","KIM
MM","A0"
"3"," KIM S 
J ","CD"
```

<a id="409df0034ef0265b"></a>
##### 시간 데이터 타입

DATE, TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE을 다운로드하면 프로퍼티 기본 포맷으로 출력된다.

다음은 DATE, TIME WITH TIME ZONE, TIMESTAMP WITH TIME ZONE의 데이터 형식을 보여준다.

```
$ gsql test test
gSQL> SELECT PROPERTY_VALUE, INIT_VALUE FROM V$PROPERTY WHERE PROPERTY_NAME LIKE 'NLS_DATE_FORMAT';

PROPERTY_VALUE                    INIT_VALUE                       
--------------------------------- ---------------------------------
YYYY-MM-DD                        YYYY-MM-DD 

1 row selected.

gSQL> SELECT PROPERTY_VALUE, INIT_VALUE FROM V$PROPERTY WHERE PROPERTY_NAME LIKE 'NLS_TIME_WITH_TIME_ZONE_FORMAT';

PROPERTY_VALUE                    INIT_VALUE                       
--------------------------------- ---------------------------------
HH24:MI:SS.FF6 TZH:TZM            HH24:MI:SS.FF6 TZH:TZM 

1 row selected.

gSQL> SELECT PROPERTY_VALUE, INIT_VALUE FROM V$PROPERTY WHERE PROPERTY_NAME LIKE 
'NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT';

PROPERTY_VALUE                    INIT_VALUE                       
--------------------------------- ---------------------------------
YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM

1 row selected.
```

다음은 다운로드 할 테이블의 구조와 데이터를 보여준다.

```
$ cat test.sql
CREATE TABLE TEST ( I1 INTEGER, I2 DATE, I3 TIME WITH TIME ZONE, I4 TIMESTAMP WITH TIME ZONE );

INSERT INTO TEST VALUES ( 1, '1999-12-31', '01:01:01', '1999-12-31 01:01:01.789 -8:00' );
INSERT INTO TEST VALUES ( 2, '2000-01-01', '23:12:12', '2000-01-01 23:12:06.0 +8:00' );
INSERT INTO TEST VALUES ( 3, '2000-12-31', '23:12:12', '2000-12-31 23:12:12.0 -8:00' );
COMMIT;

$ gsql test test
gSQL> SELECT * FROM T1;
I1 I2         I3                     I4                               
-- ---------- ---------------------- ---------------------------------
 1 1999-12-31 01:01:01.000000 +09:00 1999-12-31 01:01:01.789000 -08:00
 2 2000-01-01 23:12:12.000000 +09:00 2000-01-01 23:12:06.000000 +08:00
 3 2000-12-31 23:12:12.000000 +09:00 2000-12-31 23:12:12.000000 -08:00

3 rows selected.
```

다음은 테이블 데이터를 다운로드하기 위해 작성한 control 파일의 내용이다.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

다음은 TEST 테이블의 데이터를 데이터 파일에 다운로드한 모습이다.

```
$ gloader test test -e -c test.ctl -d test.dat

 COMPLETED IN EXPORTING TABLE: PUBLIC.TEST, 3 RECORDS 

$ ls 
test.ctl test.dat test.log
$ cat test.dat
"1","1999-12-31 00:00:00","01:01:01.000000 +09:00","1999-12-31 01:01:01.789000 -08:00"
"2","2000-01-01 00:00:00","23:12:12.000000 +09:00","2000-01-01 23:12:06.000000 +08:00"
"3","2000-12-31 00:00:00","23:12:12.000000 +09:00","2000-12-31 23:12:12.000000 -08:00"
```

<a id="bb20a2a846195b2b"></a>
#### Binary File로 다운로드

<a id="6e661c824f40fb7c"></a>
##### Simple Download

다음은 다운로드 할 테이블의 구조와 데이터를 보여준다.

```
$ cat test.sql
CREATE TABLE TEST ( I1 INTEGER PRIMARY KEY, I2 VARCHAR(10), I3 VARBINARY(10) );
INSERT INTO TEST VALUES( 1, 'LKH', X'10' );
INSERT INTO TEST VALUES( 2, 'KMM', X'A0' );
INSERT INTO TEST VALUES( 3, 'ksj', X'CD' );
COMMIT;

$ gsql test test
gSQL> SELECT * FROM TEST;

I1 I2  I3
-- --- --
 1 LKH 10
 2 KMM A0
 3 ksj CD

3 rows selected.
```

다음은 테이블 데이터를 다운로드하기 위해 작성한 control 파일의 내용이다.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
```

TEST 테이블의 데이터는 다음과 같이 gloader를 통해 다운로드된다.

```
$ gloader test test --export --control test.ctl --data test.dat --format binary

 COMPLETED IN EXPORTING TABLE: PUBLIC.test, 3 RECORDS
```

다음은 gloader를 수행한 후에 생성된 파일이다.

```
$ ls 
test.ctl test.dat test.log
```

> Binary 파일의 내용은 직접 확인하거나 수정할 수 없다.

<a id="b7ef26beb50caba0"></a>
##### Complex Download

다음은 다운로드 할 테이블의 구조와 데이터를 보여준다.

```
$ gsql test test
gSQL>\desc TEST

COLUMN_NAME TYPE                        IS_NULLABLE
----------- --------------------------- -----------
I1          NUMBER(10,0)                TRUE       
I2          DATE                        TRUE       
I3          TIME(6) WITH TIME ZONE      TRUE       
I4          TIMESTAMP(6) WITH TIME ZONE TRUE       

gSQL> SELECT COUNT(*) FROM TEST;

COUNT(*)
--------
 1572864

1 row selected.
```

다음은 테이블 데이터를 다운로드하기 위해 작성한 control 파일의 내용이다.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
```

- 하나의 파일로 다운로드

    - 다음과 같이 gloader를 통해 TEST 테이블의 데이터를 다운로드한다.

```
$ gloader test test --export --control test.ctl --data test.dat --format binary

loaded 1000 records into PUBLIC.TEST

loaded 2000 records into PUBLIC.TEST

... 중략 ...

loaded 1571000 records into PUBLIC.TEST

loaded 1572000 records into PUBLIC.TEST

COMPLETED IN EXPORTING TABLE: PUBLIC.TEST, TOTAL 1572864 RECORDS
```

    - 다음은 gloader를 수행한 후에 생성된 파일이다.

```
$ ll test.*
-rw-r--r-- 1 test test       71 2014-08-28 12:13 t1.ctl
-rw-r--r-- 1 test test 59930624 2014-08-28 12:49 t1.dat
-rw-r--r-- 1 test test      159 2014-08-28 12:49 t1.log
```

- 여러 파일로 다운로드

    - 다음과 같이 gloader를 통해 TEST 테이블의 데이터를 다운로드한다.

```
$ gloader test test --export --control test.ctl --data test.dat --format binary --filesize 31461376


loaded 1000 records into PUBLIC.TEST

loaded 2000 records into PUBLIC.TEST

... 중략 ... 

loaded 1571000 records into PUBLIC.TEST

loaded 1572000 records into PUBLIC.TEST

 COMPLETED IN EXPORTING TABLE: PUBLIC.TEST, TOTAL 1572864 RECORDS
```

    - 다음은 gloader를 수행한 후에 생성된 파일이다.

```
$ ll test.*
-rw-r--r-- 1 test test       71 2014-08-28 12:13 test.ctl
-rw-r--r-- 1 test test 31461376 2014-08-28 13:02 test.dat
-rw-r--r-- 1 test test 28474880 2014-08-28 13:02 test.dat.001
-rw-r--r-- 1 test test      159 2014-08-28 12:49 test.log
```

<a id="0e37c84db104dae3"></a>
##### Array 옵션

Binary file을 다운로드할 때 [--array](#2ab36613b71b6921) 옵션을 사용하여 bind 할 row 개수를 설정할 수 있다.  
Binary file은 다운로드와 업로드 시 동일한 array 크기를 사용하므로, --array 옵션은 다운로드 과정에서 반드시 지정해야 한다.

<a id="d8eacd48f5ba03c1"></a>
### 데이터 업로드

<a id="89b2436850b424fa"></a>
#### Text File 업로드

<a id="468d07f3cb3c8db8"></a>
##### Simple Upload

다음은 업로드 대상인 테이블을 보여준다.

```
gSQL> \DESC TEST

COLUMN_NAME TYPE                        IS_NULLABLE
----------- --------------------------- -----------
I1          NUMBER(10,0)                TRUE       
I2          DATE                        TRUE       
I3          TIME(6) WITH TIME ZONE      TRUE       
I4          TIMESTAMP(6) WITH TIME ZONE TRUE       

gSQL> SELECT * FROM TEST;

no rows selected.
```

다음은 업로드 할 데이터 파일을 보여준다.

```
$ cat test.dat
1,1999-12-31 00:00:00,01:01:01.000000 +09:00,1999-12-31 01:01:01.789000 -08:00
2,2000-01-01 00:00:00,23:12:12.000000 +09:00,2000-01-01 23:12:06.000000 +08:00
3,2000-12-31 00:00:00,23:12:12.000000 +09:00,2000-12-31 23:12:12.000000 -08:00
```

다음과 같이 gloader로 데이터 파일을 업로드하고 결과를 확인한다.

```
$ gloader test test --import --control test.ctl --data test.dat

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3 RECORDS, SUCCEEDED 3 RECORDS 

$ gsql test test

gSQL> select * from test;

I1 I2         I3                     I4                               
-- ---------- ---------------------- ---------------------------------
 1 1999-12-31 01:01:01.000000 +09:00 1999-12-31 01:01:01.789000 -08:00
 2 2000-01-01 23:12:12.000000 +09:00 2000-01-01 23:12:06.000000 +08:00
 3 2000-12-31 23:12:12.000000 +09:00 2000-12-31 23:12:12.000000 -08:00

3 rows selected.
```

<a id="0074a17f24585642"></a>
##### 공백 문자 처리

다음은 업로드 대상인 테이블을 보여준다.

```
gSQL> \DESC TEST

COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(10) TRUE       
I3          BINARY VARYING(10)    TRUE    

gSQL> SELECT * FROM TEST;

no rows selected.
```

- Control 파일에서 OPTIONALLY ENCLOSED BY 구문을 사용하지 않고 다운로드한 데이터 파일

    - 다음은 control 파일에서 OPTIONALLY ENCLOSED BY 구문을 사용하지 않고 다운로드한 데이터 파일이다. ([Text File로 다운로드](#202fddbdee9a0a6c)를 참조한다.)

```
$ cat test.dat
1, L K H ,10
2,KIM
MM,A0
3, KIM S 
J ,CD

```

    - 다음과 같이 gloader로 데이터 파일을 업로드하고 결과를 확인한다. 두 번째와 세 번째 레코드의 데이터 내에 New Line('`\`n')이 존재하는데도 불구하고 column 데이터의 시작과 끝을 알리는 qualifier가 설정되지 않아 이를 row 구분자로 인식하게 된다.

```
$ gloader test test --import --control test.ctl --data test.dat

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 5 RECORDS, SUCCEEDED 3 RECORDS

$ gsql test test

gSQL> select * from test;

I1 I2     I3  
-- ------ ----
 1 L K H  10  
 2 KIM    null
 3 KIM S  null

3 rows selected.
```

- Control 파일에서 OPTIONALLY ENCLOSED BY 구문을 사용하여 다운로드한 데이터 파일

    - 다음은 control 파일에서 OPTIONALLY ENCLOSED BY 구문을 사용하여 다운로드한 데이터 파일이다. ([Text File로 다운로드](#202fddbdee9a0a6c)를 참조한다.) 위의 결과와는 달리 아래 결과를 보면 New Line('`\n`')이 데이터의 일부로 취급되었다.

```
$ cat test.dat
"1"," L K H ","10"
"2","KIM
MM","A0"
"3"," KIM S 
J ","CD"
```

    - 다음과 같이 gloader로 데이터 파일을 업로드하고 결과를 확인한다.

```
$ gloader test test --import --control test.ctl --data test.dat

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 5 RECORDS, SUCCEEDED 3 RECORDS

$ gsql test test

gSQL> select * from test;


I1 I2      I3
-- ------- --
 1  L K H  10
 2 KIM     A0
   MM        
 3  KIM S  CD
   J         

3 rows selected.
```

<a id="5ce872d68af3e9e8"></a>
#### Binary File 업로드

<a id="a512eb155df6c1c0"></a>
##### Simple Upload

다음은 업로드 할 테이블의 구조를 보여준다.

```
gSQL> \DESC TEST

COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(10) TRUE       
I3          BINARY VARYING(10)    TRUE    

gSQL> SELECT * FROM TEST;

no rows selected.
```

다음은 테이블 데이터를 다운로드하기 위해 작성한 control 파일의 내용이다.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
```

다음은 gloader를 이용하여 업로드 할 파일이다. test.dat는 [Binary File로 다운로드](#bb20a2a846195b2b) 할 때 미리 다운로드 하였다.

```
$ ls 
test.dat
```

다음과 같이 TEST 테이블에 데이터를 업로드하고 결과를 보여준다.

```
$ gloader test test --import --control test.ctl --data test.dat --format binary

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3 RECORDS, SUCCEEDED 3 RECORDS

$ gsql test test
gSQL> SELECT * FROM TEST;

I1 I2  I3
-- --- --
 1 LKH 10
 2 KMM A0
 3 ksj CD

3 rows selected.
```

<a id="cb0a044daa1e7297"></a>
##### Complex Upload

다음은 업로드 할 테이블의 구조를 보여준다.

```
gSQL> \DESC TEST

COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(10) TRUE       
I3          BINARY VARYING(10)    TRUE    

gSQL> SELECT * FROM TEST;

no rows selected.
```

다음은 업로드하기 위한 데이터 파일이다.

```
$ ll test.*
 -rw-r--r-- 1 test test       71 2014-08-28 12:13 test.ctl
 -rw-r--r-- 1 test test 31461376 2014-08-28 13:02 test.dat
 -rw-r--r-- 1 test test 28474880 2014-08-28 13:02 test.dat.001
 -rw-r--r-- 1 test test      159 2014-08-28 12:49 test.log
```

--filesize로 download 한 여러 파일을 upload 하려면 각각의 데이터 파일에 대해 개별적으로 gloader를 수행해야 한다.

```
$ gloader test test --import --control test.ctl --data test.dat --format binary
 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 860728 RECORDS, SUCCEEDED 2285000 RECORDS, ERRORED 0 RECORDS 

$ gloader test test --import --control test.ctl --data test.dat.001 --format binary 
 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 860728 RECORDS, SUCCEEDED 860728 RECORDS, ERRORED 0 RECORDS
```

다음은 업로드한 결과이다.

```
gSQL> select count(*) from test;

COUNT(*)
--------
 3145728

1 row selected.
```

<a id="1493fd5f5c6b67c5"></a>
#### Upload 처리 단위 제어

데이터를 업로드 할 때 성능과 관련된 옵션을 사용하면 더 빠르게 실행할 수 있다.  
[--array](#2ab36613b71b6921), [--commit](#8dafd6123ae9c365), [--atomic](#a006bc95442ff10a)을 참조한다.

다음은 약 38만 레코드를 가진 데이터 파일이다.

```
$ ll test.dat
-rw-r--r-- 1 test test 75092480 2014-08-28 15:59 test.dat
```

다음은 업로드에 사용되는 control 파일이다.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

<a id="1e35f4db22d3e083"></a>
##### Array 바인딩과 Commit 주기

다음과 같이 gloader 명령을 실행하면 바인드하는 레코드를 5000 개, COMMIT하는 레코드는 20000 개로 하여 업로드한다.

```
$ gloader test test --import --control test.ctl --data test.dat --array 5000 --commit 20000


loaded 5000 records into PUBLIC.TEST


loaded 10000 records into PUBLIC.TEST


loaded 15000 records into PUBLIC.TEST

... 중략 ...
loaded 3810000 records into PUBLIC.TEST


loaded 3815000 records into PUBLIC.TEST


loaded 3818244 records into PUBLIC.TEST

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3818243 RECORDS, SUCCEEDED 3818243 RECORDS
```

gloader를 실행한 결과는 다음과 같다.

```
gSQL> SELECT I1, I2, I3 FROM TEST FETCH 3;
I1 I2 I3
-- ------- --
1 L K H 10
2 KIM A0
3 KIM S CD
3 rows selected.
gSQL> SELECT COUNT(*) FROM TEST;
COUNT(*)
--------
3818246
1 row selected.
```

<a id="ac633d65de2c638f"></a>
##### Array 바인딩과 Atomic 옵션

다음과 같이 gloader 명령을 실행하면 바인드하는 레코드를 5000 개씩 atomic INSERT로 업로드하고, 1000 개의 레코드가 실패한다.

```
$ gloader test test --import --control test.ctl --data test.dat --array 5000 --atomic


loaded 5000 records into PUBLIC.TEST


loaded 10000 records into PUBLIC.TEST


loaded 15000 records into PUBLIC.TEST

... 중략 ...
loaded 38175000 records into PUBLIC.TEST

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3818243 RECORDS, SUCCEEDED 3817243 RECORDS
```

다음은 gloader로 실행한 결과이다.

```
gSQL> SELECT I1, I2, I3 FROM TEST FETCH 3;
I1 I2 I3
-- ------- --
1 L K H 10
2 KIM A0
3 KIM S CD
3 rows selected.
gSQL> SELECT COUNT(*) FROM TEST;
COUNT(*)
--------
3817243
1 row selected.
```

다음은 업로드에 실패한 원인을 로그 파일에 기록한 결과인데 첫 번째 레코드의 첫 column에 숫자가 아닌 데이터가 저장되었기 때문에 업로드에 실패하였다.

```
$ cat test.log
Err Rec(1) Col(1): 22018(12006): data value is not a numeric literal
Err Rec(1) Col(-1): HY000(19041): Failed to atomic execution
Err Rec(1001) Col(1): 22018(12006): data value is not a numeric literal
Err Rec(1001) Col(-1): HY000(19041): Failed to atomic execution
COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3818243 RECORDS, SUCCEEDED 3817243 RECORDS [ Start Time: 2014-8-28 16:46:42 End Time: 2014-8-28 16:46:52 Taken Time: 10084582 micro-sec ]
```

다음은 업로드에 실패한 레코드를 bad file에 기록한 결과인데 500 개의 array 단위로 업로드하기 때문에 1000 개의 레코드가 저장되었다.

```
"s1"," L K H ","10"
"2","KIM","A0"
"3"," KIM S J ","CD"
... 생략 ...
```

> Array, commit 옵션은 수행 결과에 영향을 주지 않지만 atomic 연산의 경우 INSERT 성공이나 실패가 array 단위로 처리되기 때문에 하나의 레코드라도 업로드에 실패하면 해당 레코드가 속한 array의 모든 레코드가 INSERT 실패로 처리된다.   
> 로그 파일에는 array에서 처음 실패한 레코드의 원인만 기록되고 이후 레코드의 실패에 대해선 기록되지 않는다.

<a id="0ec79272e5e2850b"></a>
#### Parallel Upload

gloader가 업로드 작업을 수행할 때 작업을 부분별로 나누어 여러 thread로 처리할 수 있어 성능 향상에 도움이 된다. ([--parallel](#67f19d83aa3f4135)을 참조한다.)

다음은 약 38만 레코드를 가진 데이터 파일이다.

```
$ ll test.dat
-rw-r--r-- 1 test test 75092480 2014-08-28 15:59 test.dat
```

다음은 업로드에 사용되는 control 파일이다.

```
$ cat test.ctl
TABLE  PUBLIC.test
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

다음과 같이 gloader 명령을 실행하면 네 개의 업로드를 수행하는 thread로 바인드하는 레코드를 5000 개씩 INSERT로 업로드하고, 100 개의 레코드가 실패한다.

```
$ gloader test test --import --control test.ctl --data test.dat --array 5000 --parallel 4


loaded 5000 records into PUBLIC.TEST


loaded 10000 records into PUBLIC.TEST


loaded 15000 records into PUBLIC.TEST

... 중략 ...
loaded 3810000 records into PUBLIC.TEST

loaded 3815000 records into PUBLIC.TEST

 COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3818243 RECORDS, SUCCEEDED 3818143 RECORDS
```

다음은 gloader를 실행한 결과이다.

```
gSQL> SELECT I1, I2, I3 FROM TEST FETCH 3;
I1 I2 I3
-- ------- --
1 L K H 10
2 KIM A0
3 KIM S CD
3 rows selected.
gSQL> SELECT COUNT(*) FROM TEST;
COUNT(*)
--------
3818143
1 row selected.
```

다음은 업로드에 실패한 원인을 로그 파일에 기록한 결과이다.

```
$ cat test.log
Err Rec(1) Col(1): 22018(12006): data value is not a numeric literal
Err Rec(3) Col(1): 22018(12006): data value is not a numeric literal
Err Rec(5) Col(1): 22018(12006): data value is not a numeric literal
... 중략 ...
Err Rec(1001) Col(1): 22018(12006): data value is not a numeric literal
... 중략 ...
COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3818243 RECORDS, SUCCEEDED 3818143 RECORDS [ Start Time: 2014-8-28 16:46:42 End Time: 2014-8-28 16:46:52 Taken Time: 10084582 micro-sec ]
```

다음은 업로드에 실패한 레코드를 bad file에 기록한 결과인데 100 개의 레코드가 저장되었다.

```
"s1"," L K H ","10"
"s2","KIM","A0"
"s3"," KIM S J ","CD"
... 중략 ...
```

> 다중 thread로 데이터를 업로드 할 때 INSERT하고 에러가 발생한 레코드에 대한 내용을 로그 파일과 bad file에 기록하는데, 이 때 레코드의 순서는 데이터 파일에서의 순서와 다를 수 있다.

<a id="c647e49c40ab297e"></a>
### Upload 문제 해결

레코드 업로드 실패에는 다양한 원인이 있고 업로드에 실패한 레코드는 bad file에 기록된다. 또한 실패 원인에 대한 정보는 로그 파일에 기록된다.

<a id="b2e8324a9553289c"></a>
#### 중복 제약으로 인한 실패

<a id="2643e1961c163131"></a>
##### 제약 조건이 있는 업로드 할 테이블에 이미 중복된 데이터가 존재 (primary key 또는 unique index)

다음은 업로드 할 테이블 대상의 구조이다.

```
gSQL>\desc T1

COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(10) TRUE       
I3          BINARY VARYING(10)    TRUE    

gSQL> SELECT * FROM T1;

I1 I2  I3
-- --- --
 1 LKH 10
 2 KMM A0
 3 ksj CD

3 rows selected.
```

다음은 업로드 할 데이터 파일이다.

```
$ cat t1.dat
"1","LKH"
"4","SOS"
"5","OKO"
```

다음은 gloader로 업로드를 실행한 결과 및 생성된 로그 파일, bad file이다.   
레코드가 기본 key 제약 조건을 위반하였기 때문에 업로드에 실패하였다.

```
$ gloader test test -i -c t1.ctl -d t1.dat


 COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 3 RECORDS, SUCCEEDED 2 RECORDS 
$
$ cat t1.log
Err Rec(1) Col(-1): 40002(16057): unique constraint (PUBLIC.T1_PRIMARY_KEY) violated
COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 3 RECORDS, SUCCEEDED 2 RECORDS [ Start Time: 2014-8-26 16:19:51 End Time: 2014-8-26 16:19:51 Taken Time: 15455 micro-sec ]
$
$ cat t1.bad
"1","LKH"
```

<a id="252ee2a89b84d135"></a>
#### 날짜/ 시간 타입 포맷으로 인한 실패

DATE, TIME, TIME WITH TIME ZONE, TIMESTAMP, TIMESTAMP WITH TIME ZONE 데이터 타입에 대해서 포맷을 설정할 수 있고 이로 인해 gloader를 이용한 업로드에 실패할 수 있다.

다음은 업로드 할 테이블을 보여준다.

```
gSQL> \DESC T1

COLUMN_NAME TYPE IS_NULLABLE
----------- --------------------------- -----------
I1 NUMBER(10,0) TRUE
I2 TIMESTAMP(6) WITH TIME ZONE TRUE

gSQL> SELECT * FROM T1;
no rows selected.
```

다음은 서버에서 TIMESTAM WITH TIME ZONE의 포맷을 보여준다.

```
gSQL> SELECT PROPERTY_VALUE, INIT_VALUE FROM V$PROPERTY WHERE PROPERTY_NAME LIKE 'NLS_TIMESTAMP_WITH_TIME_ZONE_FORMAT';

PROPERTY_VALUE                    INIT_VALUE                       
--------------------------------- ---------------------------------
YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM YYYY-MM-DD HH24:MI:SS.FF6 TZH:TZM
```

다음은 업로드 할 데이터 파일이다.

```
$ cat t1.dat
"4","20000108 00:00:00"
"5","20000108 04:05:06"
"6","20000108 04:05:06"
```

다음은 gloader로 업로드한 결과이다.

```
$ gloader test test -i -c t1.ctl -d t1.dat
 
 COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 3 RECORDS, SUCCEEDED 0 RECORDS
```

다음은 업로드에 실패한 원인과 레코드가 기록된 로그 파일과 bad file이다.

```
$ cat t1.log
Err Rec(1) Col(2): HY000(12136): literal does not match format string
Err Rec(2) Col(2): HY000(12136): literal does not match format string
Err Rec(3) Col(2): HY000(12136): literal does not match format string
COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 3 RECORDS, SUCCEEDED 0 RECORDS [ Start Time: 2014-8-27 13:56:29 End Time: 2014-8-27 13:56:29 Taken Time: 20670 micro-sec ]

$ cat t1.bad 
"4","20000108 00:00:00"
"5","20000108 04:05:06"
"6","20000108 04:05:06"
```

<a id="a0e5d2b0a0571f0e"></a>
##### 문제 해결

데이터 파일과 서버에서 사용하는 데이터 타입의 포맷이 달라서 생긴 문제이므로 데이터 파일의 데이터 타입 포맷을 설정해줘야 한다. 이 때 .odbc.ini를 사용한다.

다음은 데이터 타입의 포맷을 설정한 .odbc.ini 파일이다.

```
$ cat .odbc.ini
[GOLDILOCKS]
HOST = 127.0.0.1
PORT = 21123
DATE_FORMAT = YYYYMMDD
TIME_FORMAT = HH24MISS
TIME_WITH_TIME_ZONE_FORMAT = HH24MISS TZHTZM
TIMESTAMP_FORMAT = YYYYMMDD HHMISS
TIMESTAMP_WITH_TIME_ZONE_FORMAT = YYYYMMDD HH:MI:SS
```

다음은 .odbc.ini를 설정하고 다시 gloader를 수행한 결과이다.

```
$ gloader test test -i -c t1.ctl -d t1.dat

 COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 3 RECORDS, SUCCEEDED 3 RECORDS
```


> 
> - .odbc.ini에 설정하는 데이터 타입의 포맷은 전체 column에 적용되고 각각의 column에 대해 개별적으로 설정할 수는 없다.
> - .odbc.ini에 데이터 타입의 포맷을 설정하면 gloader로 다운로드 할 때도 적용된다.
> 

<a id="9b589db9dbaa605d"></a>
#### 용량 부족으로 인한 실패

다음은 gloader를 수행하고 실패한 결과를 보여준다.

```
$ gloader test test -i -c t1.ctl -d t2.dat

loaded 4000 records into PUBLIC.T1
COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 4200 RECORDS, SUCCEEDED 0 RECORDS
```

다음은 테이블스페이스의 데이터 파일에 용량이 부족하여 실패하였다는 것을 보여준다.

```
$ cat t1.log
Err Rec(1) Col(-1): HY000(14015): there is no extendible datafile in tablespace 'MEM_DATA_TBS'
Err Rec(2) Col(-1): HY000(14015): there is no extendible datafile in tablespace 'MEM_DATA_TBS'
... 중략 ...
COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 4200 RECORDS, SUCCEEDED 0 RECORDS [ Start Time: 2014-8-27 15:7:28 End Time: 2014-8-27 15:7:29 Taken Time: 317885 micro-sec ]
```

<a id="43f02fa1c31072a1"></a>
##### 문제 해결

테이블스페이스의 데이터 파일을 확장하거나 추가한다.   
자세한 내용은 [ALTER TABLESPACE](../part-03-sql-manual/18-sql-references-a-b.md#7d3341dc7c3f738f)를 참조한다.

<a id="10ca9f8f0bf3bc01"></a>
#### 데이터 파일 분석 실패

Control 파일에서 기술한 field terminator와 qualifier, line terminator가 텍스트 데이터 파일 내에서 올바르게 사용되지 않아 일치하지 않을 수 있다.

다음은 업로드 할 테이블 대상의 구조이다.

```
gSQL>\desc T1
COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(10) TRUE       
I3          BINARY VARYING(10)    TRUE
```

다음은 업로드 할 control 파일의 내용이다.

```
$ cat t1.ctl
TABLE  T1
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

다음은 업로드 할 데이터 파일이다.

```
$ cat t1.dat
'1',"LKH","aa"
"2","SOS"","aa"
"5","OKO","00"
```

다음은 gloader로 업로드한 결과이다.

```
$ gloader test test --import --control t1.ctl --data t1.dat

 COMPLETED IN IMPORTING TABLE: PUBLIC.T1, TOTAL 3 RECORDS, SUCCEEDED 1 RECORDS
```

다음은 업로드 실패한 원인과 레코드를 보여준다.

```
$ cat t1.log
Err Rec(1) Col(1): 22018(12006): data value is not a numeric literal
COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 3 RECORDS, SUCCEEDED 1 RECORDS [ Start Time: 2014-8-28 18:6:13 End Time: 2014-8-28 18:6:13 Taken Time: 18679 micro-sec ]
$
$ cat t1.bad
"2","SOS"","aa"
'1',"LKH","aa"
```

<a id="fc866c57b3ed29f0"></a>
##### 문제 해결

데이터 파일 분석 실패의 주된 원인은 field terminator, qualifier, 또는 line terminator를 적절하게 사용하지 못한 것이다. 따라서 control 파일과 데이터 파일의 field terminator, qualifier와 line terminator를 확인하고 bad file에 기록된 레코드를 이용하여 데이터 파일을 수정해야 한다.

> 데이터 파일 분석 과정에서 파싱에 실패한 레코드는 로그 파일에 기록되지 않고 bad file에 기록된다.

<a id="fb09f0e78b0af08c"></a>
#### Character Set이 다른 Database에 업로드

Characeter set이 다른 database 사이에서 데이터를 binary 타입으로 다운로드/ 업로드 할 경우, column의 크기를 변환해야 할 수도 있다.

다음은 업로드 할 테이블 대상의 구조이다.

```
gSQL>\desc T1
COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(36) TRUE
```

다음은 테이블의 데이터인데 VARCHAR 타입이고 크기는 36이며 모두 채워져 있다.

```
SELECT * FROM T1;

I1    I2
---- ------------------------------------ 
   1 일이삼사오육칠팔구십일이삼사오육칠팔
```

위의 데이터를 UHC database에서 다운로드한 후에 동일한 스키마를 갖는 UTF8 database로 업로드하면 다음과 같은 에러가 발생한다.

```
$ gloader test test -i -f binary -T T1 -d t1.dup

ERR-HY000(42023): byte length of data greater than column length.

ERROR: FAILED TO IMPORT TABLE PUBLIC.T1
```

<a id="252a4a886bb526b0"></a>
##### 문제 해결

다음과 같이 column I2의 길이를 변경하면 데이터가 정상적으로 업로드된다.   
I2를 VARCHAR(18 CHAR)로 선언하거나 I2를 VARCAR(54) 크기로 선언한다.

```
gSQL>\desc T1
COLUMN_NAME TYPE                       IS_NULLABLE
----------- -------------------------- -----------
I1          NUMBER(10,0)               TRUE
I2          CHARACTER VARYING(18 CHAR) TRUE
```

```
gSQL>\desc T1
COLUMN_NAME TYPE                  IS_NULLABLE
----------- --------------------- -----------
I1          NUMBER(10,0)          TRUE
I2          CHARACTER VARYING(54) TRUE
```

<a id="815b915f23d2e72e"></a>
## Control File 구문

```
TABLE table_name [(column_description)]
FIELDS TERMINATED BY 'Field Terminator'
[OPTIONALLY ENCLOSED BY 'Open Qualifier' [AND 'Close Qualifier']]
[LINES TERMINATED BY 'Line Terminator']
[Characterset characterset_name]
[RTRIM [ON|OFF]]
[LTRIM [ON|OFF]]
[WHERE="conditional statement"]
```

> 한 개의 control file은 한 개의 table에 대해 설명한다. 따라서 control file에는 위의 각 항목들이 한 번씩만 기술되어야 하며 중복하여 기술될 경우 control file 파싱 에러가 발생한다.

<a id="4226a405e39b73f5"></a>
### CHARACTERSET

<a id="a021491fe45cdbb6"></a>
#### 구문

```
CHARACTERSET characterset_name
```

<a id="10ac3a3f8390c955"></a>
#### 설명

다운로드 또는 업로드할 데이터 파일의 character set을 의미한다.  
Character set이 별도로 지정되지 않은 경우에는 ODBC 데이터 원본의 CHARSET, 환경 변수 GOLDILOCKS_NLS_CHARACTERSET, 시스템 locale 정보의 우선 순위에 따라 client character set이 결정된다.  
Binary 포맷 데이터 다운로드 시에는 해당 구문이 적용되지 않으며, 업로드 시에만 적용된다.

<a id="8c025af8c9651b1f"></a>
#### 사용 예

다음은 다운로드 또는 업로드 할 데이터 파일의 character set이 ASCII 코드인 예이다.

```
% cat sample.ctl
CHARACTERSET ASCII
```

<a id="02d336624e03fe9f"></a>
### TABLE

<a id="48f93996033a6f59"></a>
#### 구문

```
TABLE <table_name> [( <column_description> )]

<table_name> ::=
    [schema_name.]table_name[@domain_name]
<column_description> ::=
    column_name [<column_bypass>] (, ... )

<column_bypass> ::=
    (ADD | SKIP) [<column_bypass_value>]

<column_bypass_value> ::=
      empty
    | DEFAULT
    | NULL
    | CONSTANT <quote_string>
    | SEQUENCE sequence_name (NEXTVAL | CURRVAL)
```

<a id="e3e2879c6df68f9a"></a>
#### 설명

<a id="605a9345ff08afca"></a>
##### 테이블

데이터를 업로드 또는 다운로드 할 대상 테이블 이름과 테이블이 속한 스키마 이름, 도메인 이름을 기술한다.   
도메인 이름은 데이터를 다운로드할 때만 사용할 수 있고 해당 멤버의 데이터만 다운로드 한다.   
테이블 이름에는 문자열이나 double quote (") 문자열이 사용된다.   
테이블 이름이 gloader의 명령행 인자로도 주어질 경우, 명령행 인자로 주어진 값이 control file의 값보다 우선적으로 사용된다.

<a id="257746fb52a2bb8f"></a>
##### Column

기본적으로 column을 명시하지 않더라도 테이블 이름만 있으면 데이터를 업로드하거나 다운로드할 수 있다.  
텍스트 모드에서는 column을 명세하여 업로드하거나 다운로드 할 column을 선택할 수 있다.  
Column을 명세하여 column 순서를 변경하거나 특정 column을 제외할 수도 있다. 단, column을 제외하는 경우에도 모든 column을 명시해야 한다. Column을 제외하려면 column 이름 뒤에 SKIP과 ADD를 명시하면 된다.

<a id="e43ec8ccf713b448"></a>
###### **SKIP/ADD**

- **SKIP:** 

- 데이터를 다운로드할 때 해당 column을 제외하거나 특정 데이터로 대체한다.
- 데이터를 업로드할 때 해당 column의 데이터를 NULL, 상수, DEFAULT 또는 SEQUENCE로 대체한다. 또한 해당 column과 매핑되는 데이터 필드 역시 무시된다.

- **ADD:** 

- 데이터를 다운로드할 때는 사용할 수 없다.
- 데이터를 업로드할 때 해당 column의 데이터를 NULL, 상수, DEFAULT 또는 SEQUENCE로 대체한다. 해당 column과 매핑되었던 데이터 필드는 다음 column과 매핑된다.

<a id="18ea3a185214c329"></a>
###### **VALUE**

- **empty:** 

SKIP 또는 ADD 뒤가 비어 있을 경우, 다운로드 할 때는 column을 제외하고, 업로드 할 때는 column의 기본 값인 NULL 또는 DEFAULT로 생성된다.

- **NULL:** 

다운로드 할 때는 column의 값을 빈 칸으로 한다. 업로드 할 때는 column의 값을 NULL로 생성한다.

- **DEFAULT:** 

다운로드 할 때는 column의 SKIP이 무시되어 column 데이터가 다운로드 된다. 업로드 할 때는 column의 DEFAULT 값이 생성된다.

- **CONSTANT:** 

다운로드 할 때는 column 데이터가 상수로 대체되어 다운로드 된다. 업로드 할 때는 column 값이 상수로 대체되어 생성된다.

- **SEQUENCE:** 

다운로드 할 때는 column 데이터가 SEQUENCE 값으로 대체되어 다운로드 된다. 업로드 할 때는 column 값이 SEQUENCE 값으로 대체되어 생성된다.

<a id="877e18f82a1a7045"></a>
#### 사용 예

<a id="b41608582b74058f"></a>
##### 테이블

다음은 테이블 이름만 기술하는 예이다.

```
% cat sample.ctl
TABLE lineitem
```

다음은 PUBLIC 스키마와 테이블 이름을 기술하는 예인데, 위 예제와 동일한 의미를 갖는다.

```
% cat sample.ctl
TABLE PUBLIC.lineitem
```

다음은 G1N1 멤버의 PUBLIC 스키마와 테이블 이름을 기술하는 예인데, 위 예제와 동일한 의미를 갖는다.

```
% cat sample.ctl
TABLE PUBLIC.lineitem@G1N1
```

다음은 delimited identifier로 생성한 테이블의 이름을 기술하는 예이다.

```
gSQL> CREATE TABLE "Tab*&^" ( id INTEGER );
```

```
% cat sample.ctl
TABLE "Tab*&^"
```

<a id="5b6ff6c485300efb"></a>
##### Column

다음은 사용 예시를 위한 샘플 테이블과 데이터 파일이다.

```
gSQL> \desc test

COLUMN_NAME TYPE         IS_NULLABLE
----------- ------------ -----------
C1          NUMBER(10,0) TRUE       
C2          NUMBER(10,0) TRUE       
C3          NUMBER(10,0) TRUE
```

```
% cat sample.dat
1,2,3
11,22,33
```

다음은 column을 기술하는 예이다.

```
% cat sample.ctl
TABLE test
(
    c1,
    c2,
    c3
)
```

다음은 column C2를 제외하고 업로드 하는 예와 그 결과이다.

```
% cat sample.ctl
TABLE test
(
    c1,
    c2 SKIP,
    c3
)

% gloader test test -i -c sample.ctl -d sample.dat
```

SKIP 키워드만 사용하였기 때문에 column C2 값으로 C2의 DEFAULT 값인 NULL이 생성되었다.

```
gSQL> SELECT * FROM TEST;

C1   C2 C3
-- ---- --
 1 null  3
11 null 33

2 rows selected.
```

다음은 위 예제의 SKIP 대신 ADD 키워드를 사용하는 예와 그 결과이다.

```
% cat sample.ctl
TABLE test
(
    c1,
    c2 SKIP,
    c3
)

% gloader test test -i -c sample.ctl -d sample.dat
```

데이터 파일에서 column C2와 매핑되었던 필드는 column C3와 매핑되었다.

```
gSQL> SELECT * FROM TEST;

C1   C2 C3
-- ---- --
 1 null  2
11 null 22

2 rows selected.
```

다음은 column C2를 제외하고 다운로드 하는 예와 그 결과이다.

```
% cat sample.ctl
TABLE test
(
    c1,
    c2 SKIP,
    c3
)

gSQL> SELECT * FROM TEST;

C1 C2 C3
-- -- --
 1  2  3
11 22 33

2 rows selected.

% gloader test test -e -c sample.ctl -d down_sample.dat
```

SKIP 키워드만 사용하였기 때문에 column C2 값으로 C2의 DEFAULT 값인 NULL이 생성되었다.

```
$ cat down_sample.dat
1,,3
11,,33
```

다음은 column C2를 SKIP 하면서 CONSTANT를 사용하는 예이다.

```
% cat sample.ctl
TABLE test
(
    c1,
    c2 SKIP CONSTANT '-2',
    c3
)

% gloader test test -i -c sample.ctl -d sample.dat
```

Column C2의 값으로 -2가 생성되었다.

```
gSQL> SELECT * FROM TEST;

C1 C2 C3
-- -- --
 1 -2  3
11 -2 33

2 rows selected.
```

다음은 column C2를 SKIP 하면서 SEQUENCE를 사용하는 예이다.

```
% cat sample.ctl
TABLE test
(
    c1,
    c2 SKIP SEQUENCE MY_SEQ NEXTVAL,
    c3
)

gSQL> SELECT MY_SEQ.CURRVAL FROM DUAL;

CURRVAL
-------
      4

1 row selected.

% gloader test test -i -c sample.ctl -d sample.dat
```

Column C2의 값으로 MY_SEQ의 NEXTVAL이 생성되었다.

```
gSQL> SELECT * FROM TEST;

C1 C2 C3
-- -- --
 1  4  3
11  5 33

2 rows selected.
```

<a id="960fdebd54602972"></a>
### FIELDS TERMINATED BY

<a id="490232a8f2bcd29d"></a>
#### 구문

```
FIELDS TERMINATED BY 'Field Terminator'
```

<a id="3ff4cb32f6d774c6"></a>
#### 설명

Field terminator는 데이터 파일의 record 데이터에서 각 column들 사이의 구분자로 사용된다. Control 파일에서 field terminator 설정은 생략할 수 없다.  
Field terminator는 하나 이상의 문자열로 설정할 수 있으며, qualifier 및 line terminator와 중복되거나 서로 간의 부분 집합 문자열을 사용해서는 안된다.  
Field terminator로 설정할 수 있는 문자열에는 제한이 없다. 다만 NEW LINE이나 TAB, CARRIAGE RETURN 문자를 설정하려면 각각 n, t, r 문자 앞에 역슬래시 (`\`) 또는 %를 추가해야 한다.  
Field terminator가 gloader의 명령행 인자로도 주어질 경우, 명령행 인자로 주어진 값이 control file의 값보다 우선적으로 사용된다.

<a id="c95b1fe212794a5e"></a>
#### 사용 예

다음은 field terminator를 COMMA와 NEW LINE으로 설정하는 예이다.

```
% cat sample.ctl

FIELDS TERMINATED BY ',\n'
```

```
% cat sample.ctl

FIELDS TERMINATED BY ',%n'
```

<a id="54e719a32a15af5f"></a>
### OPTIONALLY ENCLOSED BY

<a id="f2248edbcf9f2408"></a>
#### 구문

```
OPTIONALLY ENCLOSED BY 'Open Qualifier' [AND 'Close Qualifier']
```

<a id="424139f5317592b4"></a>
#### 설명

Qualifier는 column의 시작과 끝을 표현하는 구분자이다.  
Qualifier는 하나의 문자로만 설정할 수 있으며 첫 번째 qualifier는 open qualifier, 마지막 qualifier는 close qualifier라고 불린다. Open qualifier와 close qualifier를 같은 문자로 설정할 수도 있지만 각기 다른 문자로 설정하여 column의 시작과 끝을 표현할 수도 있다.  
Qualifier로 설정한 문자는 field terminator와 line terminator에서 사용할 수 없다.  
Close qualifier가 문자 그대로 column 데이터에 포함될 경우, 두 개의 close qualifier를 사용하여 하나의 유효한 데이터임을 표현한다.  
Close qualifier를 생략하고 open qualifier만 설정할 경우, close qualifier에는 open qualifier와 동일한 문자를 사용한다.

OPTIONALLY ENCLOSED BY 구문이 없는 경우, column의 데이터는 field terminator에 의해 구분된다.  
Qualifier가 gloader의 명령행 인자로도 주어질 경우, 명령행 인자로 주어진 값이 control file의 값보다 우선적으로 사용된다.

> OPTIONALLY ENCLOSED BY 구문이 없는 경우, 데이터 다운로드와 업로드 결과가 서로 다를 수 있다. ([Upload 문제 해결](#c647e49c40ab297e)을 참조한다.)

<a id="17e3f2c12d8875b9"></a>
#### 사용 예

다음은 open qualifier와 close qualifier를 각각 double quote (")와 single quote (')로 표현한 예이다.

```
% cat sample.ctl
OPTIONALLY ENCLOSED BY '"' AND "'"
```

<a id="91a5423ae900de63"></a>
### LINES TERMINATED BY

<a id="f3e2f46bda3467d8"></a>
#### 구문

```
LINES TERMINATED BY 'Line Terminator'
```

<a id="b054eab045ad31b6"></a>
#### 설명

Line terminator는 데이터 파일에서 각 record들의 구분자로 사용된다.  
Line terminator는 하나 이상의 문자열로 설정할 수 있으며, qualifier 및 field terminator와 중복되거나 서로 간의 부분집합 문자열을 사용해서는 안된다.

Line terminator 설정을 생략하면 NEW LINE('`\`n' 또는 '%n')이 기본값으로 사용된다.  
Line terminator가 gloader의 명령행 인자로도 주어질 경우, 명령행 인자로 주어진 값이 control file의 값보다 우선적으로 사용된다.

> • Unix와는 달리 Windows OS에서 export 받은 데이터 파일에는 하나의 NEW LINE 대신에 CARRIAGE RETURN과 NEW LINE이 함께 기록된다. 이런 데이터파일을 이용하여 import 할 때는 '`\`r`\`n'과 같이 control 파일의 LINES TERMINATED BY를 명확히 설정해 주어야 정상적으로 데이터를 import할 수 있다.   
>   
> • Field terminator와 line terminator는 각각 다른 문자열로 설정할 것을 권장한다. 첫 문자를 포함하여 일치하는 문자열이 많을수록 내부 비교 비용으로 인해 import 성능이 저하될 수 있다.  
> 즉, field terminator와 line terminator를 각각 다른 문자열로 하되 해당 문자열의 길이가 짧을수록 성능이 향상될 수 있다.

<a id="7aa1578fcc8e6ed3"></a>
#### 사용 예

다음은 '^^`\`t`\`r`\`n'를 line terminator로 사용하는 예이다.

```
% cat sample.ctl

LINES TERMINATED BY '^^\t\r\n'
```

<a id="fba86461e8b2df3c"></a>
### LTRIM

<a id="6d37d7b186508df8"></a>
#### 구문

```
LTRIM ON|OFF
```

<a id="6e5194277908b1f6"></a>
#### 설명

Left trim을 결정한다.   
Default 값은 OFF이며, OFF로 설정할 경우 왼쪽 WHITESPACE를 data로 간주한다.   
ON으로 설정할 경우 왼쪽 WHITESPACE는 무시한다.

> OPTIONALLY ENCLOSED BY 구문이 없을 경우에만 적용된다.  
> OPTIONALLY ENCLOSED BY 구문이 사용되고 데이터 파일에서 column이 구분자로 둘러싸여 있을 경우, RTRIM, LTRIM은 OFF이다.

<a id="454f483461c8dd18"></a>
#### 사용 예

다음은 LTRIM을 ON 하는 예이다.

```
% cat sample.ctl
LTRIM ON
```

<a id="b0f16278e5db41b0"></a>
### RTRIM

<a id="1b4006859726d02a"></a>
#### 구문

```
RTRIM ON|OFF
```

<a id="6c6d3983fce29663"></a>
#### 설명

Rigth trim을 결정한다.  
Default 값은 OFF이며, OFF로 설정할 경우 오른쪽 WHITESPACE를 data로 간주한다.  
ON으로 설정할 경우 오른쪽 WHITESPACE는 무시한다.

> OPTIONALLY ENCLOSED BY 구문이 없을 경우에만 적용이 된다.  
> OPTIONALLY ENCLOSED BY 구문이 사용되고 데이터 파일에서 column이 구분자로 둘러싸여 있을 경우, RTRIM과 LTRIM은 OFF이다.

<a id="413e119812661274"></a>
#### 사용 예

다음은 RTRIM을 ON 하는 예이다.

```
% cat sample.ctl
RTRIM ON
```

<a id="b212c0798fdc7250"></a>
### WHERE

<a id="d9dfcdeb72151161"></a>
#### 구문

```
WHERE="conditional_statement"
```

<a id="5d028115e112c086"></a>
#### 설명

데이터를 다운로드 할 경우 조건절을 사용한다.

<a id="c8dc7f998f79eda2"></a>
#### 사용 예

다음은 WHERE를 사용하는 예이다.

```
% cat sample.ctl
WHERE="I2 > 3"
```

<a id="81f8640f671ff188"></a>
## gloader Argument References

<a id="9a83e9d0061839aa"></a>
### 사용법

```
$ gloader --help
Usage 
    gloader user password mode data [control] [format] [options]

    user                user name
    password            password

mode: gloader's mode. 
  --export              export data
  --import              import data

data:
  --data                data file

options:
  --control                       control file
  --format                        file format(text|binary, Default text)
  --log                           log file
  --bad                           bad file
  --dsn                           dsn string
  --array                         number of rows in bind array(Default 1000)
  --filesize                      max file size
  --commit                        number of commit unit(Default 5000)
  --comment                       commenting on commit
  --atomic                        use atomic function
  --parallel                      use parallel in import
  --propagation                   enabling or disabling a redo log propagation(ON|OFF)
  --errors                        number of error count to allow(Default 100)
  --AsTIMESTAMP                   bind DATE as TIMESTAMP
  --buffered                      buffered disk io(Default direct io)
  --tablename                     [schema_name.]table_name[@domain_name]
  --fieldterm                     field terminator
  --lineterm                      line terminator
  --qualifier                     qualifier(column data encloser)
  --where                         export only rows selected by given WHERE condition
  --group-id                      importing distributed data by group id using global connections in a clustered environment
  --append                        action before data importing (APPEND|REPLACE|TRUNCATE, Default APPEND)
  --skip                          number of records to skip
  --no-copyright                  suppresses the display of the banner
  --silent                        suppresses the display of the result message
  --merge                         import data using new space (EXTENT|SEGMENT, Default NONE) 
  --skip_index_maintenance        index maintenance option to import data using new space
  --nologging                     nologging append insert option to import data using new space
  --help                          print help message
```

<a id="dfed88eae832dbfe"></a>
### 필수 인자

Database에 연결하기 위해 user name, password의 순서로 인자가 입력된다.  
gloader의 작업에 대한 mode, control file과 datafile이 인자로 입력된다.

<a id="1425f84fe540b0e0"></a>
| 인자 | 설명 |
| --- | --- |
| user_name | User name이다. User name의 최대 길이는 128 이다. |
| password | Password이다. Password의 최대 길이는 128 이다. |

<a id="a9a01c1c890b24af"></a>
#### --export

<a id="f2caeb807e6ff1e3"></a>
##### 설명

gloader가 database에서 데이터를 다운로드하도록 기술한다.

<a id="69e2c7266ef91198"></a>
##### 사용 예

```
$ gloader test test --export -c sample.ctl -d sample.dat
```

<a id="593c5eef8a07940d"></a>
#### --import

<a id="c0e9c2b5e4406bab"></a>
##### 설명

gloader가 database에서 데이터를 업로드 하도록 기술한다.

<a id="c7f887b51df696ef"></a>
##### 사용 예

```
$ gloader test test --import -c sample.ctl -d sample.dat
```

<a id="161a41f19aa137e8"></a>
#### --control

<a id="29e0893d7eef1381"></a>
##### 설명

Control file 경로를 기술한다.

--tablename이 argument 로 주어질 경우 control file을 생략할 수 있다. gloader를 수행하려면 테이블 이름이 필수 요소이므로 반드시 control file이나 argument를 통해 테이블 이름이 주어져야 한다. 만일 테이블 이름이 argument로 주어지지 않을 경우, control file을 통해 반드시 TABLE 항목을 설정해야 한다.

Control file이 생략되면 field terminator, qualifier, line terminator를 argument로 부여할 수 있다. 만약 이러한 구분자들이 argument로도 주어지지 않을 경우, CSV 형식의 구분자들을 기본으로 사용한다.

<a id="6970048a6991c7c2"></a>
##### 사용 예

다음은 sample.ctl 이라는 이름을 가진 control 파일을 사용하는 예이다.

```
$ gloader test test -i --control sample.ctl -d sample.dat
```

<a id="7331ec51bae2712d"></a>
#### --data

<a id="0ebcfbf959cbb95b"></a>
##### 설명

다운로드/ 업로드 할 data file 경로를 기술한다.

<a id="af34e5c746786582"></a>
##### 사용 예

다음은 sample.dat 이라는 이름을 가진 데이터 파일을 업로드하는 예이다.

```
$ gloader test test -i -c sample.ctl --data sample.dat
```

<a id="195a77b2c24b7fa7"></a>
### 옵션 인자

<a id="7a3c8af924827302"></a>
#### --tablename

<a id="3ec58022967e141a"></a>
##### 설명

[Schemaname.]Tablename[@domain_name] 형식으로 테이블 이름을 기술한다.

Argument 또는 control file의 TABLE 설정을 통해 테이블 이름을 반드시 부여해야 한다. 즉, control file이 생략되었을 경우, 테이블 이름 argument가 필수이다.   
만약 control file의 TABLE 항목이 설정되어 있는 상태에서 tablename argument도 주어졌다면 argument 값을 우선적으로 사용한다.

<a id="c8aa60840cfe8367"></a>
##### 사용 예

다음은 control file argument가 생략되어 tablename argument를 부여함으로써 CSV 형식으로 업로드하는 예이다.

```
$ gloader test test -i --tablename PUBLIC.T1 --data sample.dat
```

다음은 control file에 TABLE 항목이 설정되어 tablename argument를 생략한 예이다.

```
$ cat sample.ctl | grep TABLE
  TABLE T1
$ gloader test test -i -c sample.ctl --data sample.dat
```

<a id="f3e37c6f1c46bc3a"></a>
#### --format

<a id="81d73a96d30ea7fe"></a>
##### 설명

Datafile의 형식에 대해서 기술한다.   
Datafile에는 text 형식과 binary 형식이 있고, 설정되지 않았을 경우 text 형식이 기본으로 사용된다.

<a id="cbe4bbcf892cc881"></a>
##### 사용 예

다음과 같이 데이터가 sample.dat 파일에 binary 형식으로 다운로드 된다.

```
$ gloader test test --export --control sample.ctl --data sample.dat --format binary
```

다음은 위에서 gloader를 실행한 후에 생성된 sample.dat와 sample.log 파일을 보여준다.

```
$ ls
sample.ctl sample.dat sample.log
```

<a id="a2e3cc63b5c20fc6"></a>
#### --log

<a id="deba0041b7052ac1"></a>
##### 설명

Logfile 경로를 기술한다.   
gloader를 수행하면서 발생하는 에러와 작업 결과를 기록한다.   
설정되지 않았을 경우 확장자를 log로 바꾸어 datafile 이름과 동일한 이름으로 생성된다.

<a id="7fe0dbd12545eb37"></a>
##### 사용 예

다음은 --log 옵션을 사용하여 로그 파일 이름을 명시하는 예이다.

```
$ gloader test test --export --control sample.ctl --data sample.dat --log SAMPLE.log
```

다음은 위에서 gloader를 실행한 후 생성된 sample.dat와 SAMPLE.log 파일을 보여준다.

```
$ ls
sample.ctl sample.dat SAMPLE.log
```

다음은 --log 옵션을 사용하여 로그 파일 이름을 명시하지 않은 예이다.

```
$ gloader test test --export --control sample.ctl --data sample.dat
```

다음은 위에서 gloader를 실행한 후 생성된 sample.dat와 sample.log 파일을 보여준다.

```
$ ls
sample.ctl sample.dat sample.log
```

<a id="b993496510418fe2"></a>
#### --bad

<a id="3e3b92f910d12451"></a>
##### 설명

Bad file 경로를 기술한다.   
gloader가 import 작업을 할 때만 유효하며 오류가 발생하여 업로드 되지 못한 row를 저장한다.   
설정하지 않았을 경우, 확장자를 bad로 바꾸어 datafile 이름과 동일한 이름으로 생성된다.

<a id="f81843be97614052"></a>
##### 사용 예

다음은 --bad 옵션을 사용하여 bad file 이름을 명시하는 예이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --bad SAMPLE.bad
```

다음은 위에서 gloader를 실행한 후에 생성된 sample.dat, sample.log와 SAMPLE.bad 파일을 보여준다.

```
$ ls
SAMPLE.bad sample.ctl sample.dat sample.log
```

다음은 --bad 옵션을 사용하여 bad file 이름을 명시하지 않은 예이다.

```
$ gloader test test --export --control sample.ctl --data sample.dat
```

다음은 위에서 gloader를 실행한 후 생성된 sample.dat, sample.log와 sample.bad 파일을 보여준다.

```
$ ls
sample.bad sample.ctl sample.dat sample.log
```

<a id="eba79e05c76444c2"></a>
#### --dsn

<a id="87806b57b57755bd"></a>
##### 설명

dsn string이며 최대 길이는 128이다.  
다운로드/ 업로드 할 데이터 파일에 표현된 시간 관련 데이터 타입의 형식에 대해 기술해야 할 때 사용된다.  
Client/ Server (C/S) 환경에서 gloadernet을 이용하여 서버를 지정할 때 사용된다.  
자세한 내용은 [odbc.ini 파일](../part-05-developer-manual/34-odbc.md#1edb504add88d834)을 참조한다.

<a id="46571c0c5427af4c"></a>
##### 사용 예

다음은 --dsn 옵션을 사용하기 위해 기술된 .odbc.ini의 예이다.

```
$ cat .odbc.ini
[GOLDILOCKS]
HOST = 127.0.0.1
PORT = 21123
DATE_FORMAT = YYYYMMDD
TIME_FORMAT = HH24MISS
TIME_WITH_TIME_ZONE_FORMAT = HH24MISS TZHTZM
TIMESTAMP_FORMAT = YYYYMMDD HHMISS
TIMESTAMP_WITH_TIME_ZONE_FORMAT = YYYYMMDD HH:MI:SS
```

다음은 이름이 goldilocks인 서버에 --dsn 옵션을 사용하여 데이터를 업로드하는 예이다.

```
$ gloadernet test test --dsn goldilocks --import --control sample.ctl --data sample.dat
```

다음은 사용자가 --dsn 옵션을 사용하여 데이터 파일의 시간 관련 데이터 타입의 형식을 정의하여 다운로드하는 예이다.

```
$ gloader test test --dsn goldilocks --export --control sample.ctl --data sample.dat
```

자세한 내용은 [날짜/시간 타입 포맷으로 인한 실패](#252ee2a89b84d135)를 참조한다.

<a id="2ab36613b71b6921"></a>
#### --array

<a id="eefddb1e4335cf21"></a>
##### 설명

데이터를 import 할 때 bind 할 row 개수를 지정한다.  
Array 개수에 비례하여 메모리의 사용량이 증가하며, 옵션을 지정하지 않은 경우 text 모드에서는 1000 (rows), binary 모드에서는 40 (rows)가 기본값으로 사용된다.  
이 옵션은 text 모드에서는 업로드 할 때만 적용되고, binary 모드에서는 다운로드 할 때만 적용된다.

<a id="59a24652c67df97a"></a>
##### 사용 예

다음은 text 데이터 파일을 2,000 개 레코드 단위로 업로드하는 예이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --array 2000
```

다음은 binary 데이터 파일을 2,000 개 레코드 단위로 다운로드하는 예이다.

```
$ gloader test test --export --format binary --control sample.ctl --data sample.dup --array 2000
```

<a id="bb674fc2a68b078b"></a>
#### --filesize

<a id="286214a2b77f9a4c"></a>
##### 설명

gloader가 데이터를 다운로드 할 때 파일의 최대 크기를 설정할 수 있고, 데이터가 기술한 최대 크기를 초과하면 파일 확장자 뒤에 순열 번호를 더하여 파일을 생성한다.   
설정하지 않았을 경우, 파일의 최대 크기는 무한대이고, 최소값은 31,461,376 (30 Mbytes)이다.   
Binary 타입 데이터 파일에만 유효한 옵션이다.

<a id="580129e6f7eb1821"></a>
##### 사용 예

명령어를 실행한 결과 파일의 최대 크기를 초과하여 생성된 결과물은 다음과 같다.

```
$ gloader test test --export --control sample.ctl --data sample.dat --filesize 31461376
```

```
$ls -al
-rw-r--r-- 1 test test 31461376 sample.dat
-rw-r--r-- 1 test test 31461376 sample.dat.001
-rw-r--r-- 1 test test  6715392 sample.dat.002
```

<a id="8dafd6123ae9c365"></a>
#### --commit

<a id="d68fa72ad4616f17"></a>
##### 설명

gloader가 데이터를 업로드 할 때 트랜잭션은 no commit 상태이다. --commit option을 사용하여 레코드의 commit 주기를 설정할 수 있다.  
설정되지 않았을 경우 5000 (rows)가 사용된다.

<a id="added6ee97ac0887"></a>
##### 사용 예

다음은 --commit 옵션을 사용하는 예이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --commit 10000
```

<a id="ccc0cc775dc9e1af"></a>
#### --comment

<a id="e1c30ed1361563c5"></a>
##### 설명

gloader가 트랜잭션 commit 할 때 트랜잭션에 주석을 지정한다.

<a id="a46045dcedc33bfd"></a>
##### 사용 예

다음은 --comment 옵션을 사용하는 예이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --comment import_sample
```

<a id="a006bc95442ff10a"></a>
#### --atomic

<a id="26a6a816788d61d6"></a>
##### 설명

Array INSERT를 수행하는 옵션으로써 데이터를 업로드 할 때만 유용하다.   
Atomic array INSERT는 array 크기만큼의 insert 문을 하나의 트랜잭션으로 처리하기 때문에 기존의 array insert 보다 빠르게 처리된다.

<a id="fb4106ba760a69ab"></a>
##### 사용 예

다음은 --atomic 옵션을 사용하는 예이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --array 1000 --atomic
```

<a id="67f19d83aa3f4135"></a>
#### --parallel

<a id="dbb64f54f9151381"></a>
##### 설명

병렬 처리할 thread의 개수를 기술한다.   
gloader가 업로드 작업을 수행할 때만 유용하며 --parallel 옵션을 조정하여 각 부분 작업을 진행하는 thread의 개수를 늘리면 빠른 처리가 가능하다.   
Thread의 개수를 늘려서 빠르게 작업할 수 있지만 thread 개수는 작업환경에 따라 정해야 한다.   
기본값은 1이고, 최대값은 32이다.

<a id="53278619149dcd41"></a>
##### 사용 예

다음은 데이터를 업로드 할 때 여덟 개의 thread를 사용하는 예이다. 여덟 개의 업로드 thread 이외에 데이터 파일 분석하는 thread와 읽기 전용 thread를 포함하여 총 열 개의 thread가 동작한다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --parallel 8
```

<a id="1cb863544a71d51e"></a>
#### --propagation

<a id="b9f47ec55b72afc5"></a>
##### 설명

업로드 트랜잭션의 로그를 다른 복제 서버에 전파할지 여부를 결정한다.   
ON, OFF를 설정할 수 있다.

<a id="8804597e297f522c"></a>
##### 사용 예

다음은 업로드 트랜잭션의 로그를 다른 복제 서버에 전파하지 않을 경우의 예이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --propagation off
```

<a id="709285d398264ec4"></a>
#### --errors

<a id="c05dbbc30313fccf"></a>
##### 설명

gloader가 데이터를 업로드 할 때 허용되는 에러 개수를 설정한다.  
설정하지 않을 경우, 100 (rows)가 사용되고 0으로 설정할 경우, --errors 옵션을 무시한다.  
--array 옵션의 크기보다 작은 경우 허용되는 에러 개수는 array 개수이다.

<a id="273515fd8402731b"></a>
##### 사용 예

다음은 errors 옵션을 사용하는 예이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --errors 10000
```

<a id="b571e8f92fb63660"></a>
#### --AsTIMESTAMP

<a id="709a569e88a367c3"></a>
##### 설명

하위 호환을 위해 TIMESTAMP 형식으로 저장된 DATE 타입 데이터를 TIMESTAMP 형식으로 동작하도록 한다.  
--AsTIMESTAMP 옵션이 사용되면 DATE 데이터에도 TIMESTAMP_FORMAT이 적용된다.

<a id="fdf4825e101c616b"></a>
##### 사용 예

다음은 --AsTIMESTAMP 옵션을 사용하는 예이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --AsTIMESTAMP
```

<a id="1deef03d9db10673"></a>
#### --buffered

<a id="5d16d969bfbd6a51"></a>
##### 설명

Datafile에 한해 direct IO 대신 buffered IO를 사용하도록 한다.

Log file과 bad file은 buffered IO를 사용한다.

<a id="6ef196be740735e3"></a>
##### 사용 예

다음은 --buffered 옵션을 사용하는 예이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --buffered
```

<a id="575acb0b4994ecb0"></a>
#### --fieldterm

<a id="f68e1f5545b88765"></a>
##### 설명

Field terminator를 부여한다.  
Control file에도 설정되어 있을 경우 fieldterm argument 값이 우선적으로 사용된다.  
NEW LINE, CARRIAGE RETURN, TAB의 경우에는 각각 n, r, t 앞에 %를 붙여서 사용한다.  
Shell meta character로 사용되는 ', ", \, & 등의 문자는 되도록 사용하지 않아야 한다.

<a id="d2003b515c8ea5c7"></a>
##### 사용 예

다음은 --fieldterm 옵션을 사용하는 예이다.

```
$ gloader test test --i -c sample.ctl -d sample.dat --fieldterm ",,,"
$ gloader test test --i -c sample.ctl -d sample.dat --fieldterm ,,,
$ gloader test test --i -c sample.ctl -d sample.dat --fieldterm ',,,'
```

<a id="a24f7272a490c8c3"></a>
#### --lineterm

<a id="e2681197c65a84d5"></a>
##### 설명

Line terminator를 부여한다.   
Control file에도 설정되어 있을 경우 lineterm argument 값이 우선적으로 사용된다.   
자세한 입력 방법은 fieldterm argument와 같다.

<a id="8ab5df236c631506"></a>
##### 사용 예

다음은 --lineterm 옵션을 사용하는 예이다.

```
$ gloader test test --i -T PUBLIC.test -d sample.dat --lineterm ",,,"
$ gloader test test --i -T PUBLIC.test -d sample.dat --lineterm ,,,
$ gloader test test --i -T PUBLIC.test -d sample.dat --lineterm ',,,'
```

<a id="dd4fdbdcebf6a55e"></a>
#### --qualifier

<a id="590f9af2caecadd8"></a>
##### 설명

Column 데이터의 시작과 끝에 추가할 qualifier를 부여한다. Qualifier는 한 개 문자만 설정할 수 있다.  
Control file에도 설정되어 있을 경우 qualifier argument 값이 우선적으로 사용된다.   
자세한 입력 방법은 fieldterm argument와 같다.

<a id="085609ea87af4dd2"></a>
##### 사용 예

다음은 --qualifier 옵션을 사용하는 예이다.

```
$ gloader test test --i -T PUBLIC.test -d sample.dat --qualifier "|"
$ gloader test test --i -T PUBLIC.test -d sample.dat --qualifier '"'
```

<a id="67402efbb370b04a"></a>
#### --where

<a id="359bdf2a837ac1df"></a>
##### 설명

export 동작에서 조건절을 설정하여 데이터를 다운로드 한다.  
Control file에도 where절이 설정되어 있을 경우 where argument 값이 우선적으로 사용된다.

<a id="5805c626f40dc292"></a>
##### 사용 예

다음은 --where 옵션을 사용하는 예이다.

```
$ gloader test test --i -T PUBLIC.test -d sample.dat --where "I2 > 4"
```

<a id="78a7dd48c36575bd"></a>
#### --group-id

<a id="1bf08368c3be9191"></a>
##### 설명

클러스터 환경에서 sharded 테이블에 데이터를 업로드 할 때, 데이터를 그룹별로 정렬하여 직접 해당 그룹에 업로드 한다.  
이 옵션을 non-sharded 테이블에 데이터를 업로드 할 때 사용할 경우, 해당 옵션은 유효하지 않다.  
이 옵션은 C/S 환경에서만 동작하므로 gloadernet에서만 유효하며 텍스트 파일을 업로드 할 때만 사용할 수 있다.

--group-id 옵션은 ODBC의 [GLOBAL CONNECTION](../part-05-developer-manual/34-odbc.md#f7d7df0ca8076bd2)을 사용하므로 [데이터 원본 구성](../part-05-developer-manual/34-odbc.md#69c211015508ccf1)에 관련 내용을 설정해야 한다.

<a id="874d83d31c54bb34"></a>
##### 사용 예

다음은 global connection을 사용하기 위한 odbc.ini 설정 파일이다.

```
$cat .odbc.ini
[GOLDILOCKS]
HOST=127.0.0.1
PORT = 22581
LOCALITY_AWARE_TRANSACTION=1
LOCATOR_DSN = LOCATOR
[LOCATOR]
LOCATOR_FILE=.locator.ini
```

다음은 gloadernet에서 --group-id 옵션을 사용하는 예이다.

```
$ gloadernet test test --i -T PUBLIC.test -d sample.dat --group-id
COMPLETED IN IMPORTING TABLE: PUBLIC.TEST, TOTAL 20 RECORDS, SUCCEEDED 20 RECORDS
```

다음은 gloader에서 --group-id 옵션을 사용하여 에러가 발생한 예이다.

```
$ gloader test test --i -T PUBLIC.test -d sample.dat --group-id
ERR-HY010(19009): Function sequence error : The function should be called only when the SQL_ATTR_LOCALITY_AWARE_TRANSACTION connection attribute is set.

```

<a id="6eddf8d8acd11ff8"></a>
#### --append

<a id="597c7276ca61279a"></a>
##### 설명

import 모드에서 데이터를 로드하기 전에 기존 데이터를 처리하는 옵션이다. DEFAULT 값은 APPEND이다.  
APPEND는 데이터를 유지하고 새로운 데이터를 로드한다.  
REPLACE는 데이터를 DELETE 구문으로 삭제한 후에 새로운 데이터를 로드한다.  
TRUNCATE는 데이터를 TRUNCATE 구문으로 삭제한 후에 새로운 데이터를 로드한다.

<a id="4c30a80a12a6d584"></a>
##### 사용 예

다음은 --append 옵션에 TRUNCATE를 사용하는 예이다.

```
$ gloader test test --i -T PUBLIC.test -d sample.dat --append TRUNCATE
```

<a id="ef4ad6f4711de24f"></a>
#### --directio-size

<a id="8756780087b254d6"></a>
##### 설명

deprecated

<a id="345793ca7799ac7e"></a>
#### --skip

<a id="528cbda07670967c"></a>
##### 설명

데이터 파일 업로드할 때 제외할 레코드 개수를 설정한다. 기본값은 0이다.

<a id="3ca77f315288304e"></a>
##### 사용 예

다음은 gloader에서 skip을 설정하여 10 개의 레코드를 제외하는 예이다.

```
$ gloader test test --i -T PUBLIC.test -d sample.dat --skip 10
```

<a id="f958563f539470bd"></a>
#### --no-copyright

<a id="65d86f5471545672"></a>
##### 설명

Copyright와 version을 출력하지 않는다.

<a id="8e2d85c1800e2072"></a>
##### 사용 예

다음은 --no-copyright 옵션과 함께 gloader를 수행한 결과이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --no-copyright 
COMPLETED IN EXPORTING TABLE: PUBLIC.t1, 3 RECORDS 
$
```

<a id="fbeff18e515a8b9b"></a>
#### --silent

<a id="23707a4d3324634a"></a>
##### 설명

gloader 수행 결과를 출력하지 않는다.

<a id="b02ed412d8c0bcdf"></a>
##### 사용 예

다음은 --silent 옵션과 함께 gloader를 수행한 결과이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --silent

$
```

<a id="1740ac6239c20a32"></a>
#### --merge

<a id="6e8f510bff6081b4"></a>
##### 설명

APPEND INSERT 방식으로 데이터를 로드할 때 EXTENT 또는 SEGMENT 방식을 선택할 수 있다.

- EXTENT: Serial APPEND INSERT 방식으로 데이터를 로드한다.
- SEGMENT: PARALLEL APPEND INSERT 방식으로 데이터를 로드한다.

<a id="755a6fdd2fcc4e8f"></a>
##### 사용 예

다음은 --merge 옵션을 사용하여 gloader를 실행하는 예이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --merge EXTENT

$ gloader test test --import --control sample.ctl --data sample.dat --merge SEGMENT
```

<a id="0b020f291e4d228b"></a>
#### --skip_index_maintenance

<a id="d33dc7ebb67d8511"></a>
##### 설명

APPEND INSERT 방식으로 데이터를 로드할 때 인덱스를 갱신하지 않고 unsuable 세그먼트로 설정한다.  
이 옵션은 --merge 와 함께 사용해야 한다. 지정하지 않으면 DEFERRED_INDEX_MAINTENANCE 방식으로 수행한다.

<a id="42af34d00aacf922"></a>
##### 사용 예

다음은 --skip_index_maintenance 옵션을 사용하여 gloader를 실행하는 예이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --merge EXTENT --skip_index_maintenance
```

<a id="b5d07028418f43ee"></a>
#### --nologging

<a id="9943a089a50ca812"></a>
##### 설명

NOLOGGING APPEND INSERT 방식으로 데이터를 로드하는 옵션이다.  
이 옵션은 --merge SEGMENT 와 함께 사용해야 한다. 지정하지 않으면 LOGGING 방식으로 수행한다.

<a id="d222b218a1372399"></a>
##### 사용 예

다음은 --nologging 옵션을 사용하여 gloader를 실행하는 예이다.

```
$ gloader test test --import --control sample.ctl --data sample.dat --merge SEGMENT --nologging
```

<a id="c973dd221ca78135"></a>
#### --help

<a id="b02c7b20a7c1b165"></a>
##### 설명

도움말을 출력한다.  
자세한 내용은 [사용법](#9a83e9d0061839aa)을 참조한다.

---

[← 44. gsql/gsqlnet (Interactive SQL Tool)](44-gsql-gsqlnet-interactive-sql-tool.md) · [전체 목차](../README.md) · [46. gdump →](46-gdump.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
