<a id="bdced4d785e476bf"></a>

# 31. Embedded SQL

> 원본: [GOLDILOCKS 20c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/20c_1/manual/ko/bdced4d785e476bf)  
> 태그: `20c.1_30_tag`

[← 30. JDBC](30-jdbc.md) · [전체 목차](../README.md) · [32. PDO →](32-pdo.md)

<a id="4b0fc0fd8da19ed8"></a>
## Precompiler

<a id="88050fae954fbaff"></a>
### 개요

GOLDILOCKS의 precompiler는 high-level 프로그래밍 언어에서 embedded SQL을 사용할 수 있게 해 주는 프로그램 개발 도구이다. 현재 GOLDILOCKS에서는 C/ C++ 언어에 대한 precompiler만 지원하는데 이 도구의 이름은 gpec이다.

<a id="c8ae2a067eb5030b"></a>
#### Embedded SQL 응용 프로그램 개발

[Embedded SQL 응용 프로그램 개발](#e185cd7f79692695)에 설명된 것과 같이, 사용자가 embedded SQL을 포함하는 C 소스 프로그램을 작성하고, 이를 gpec precompiler를 통하여 변환하면 소스 코드 상에 있던 embedded SQL이 GOLDILOCKS의 library를 호출하는 내용으로 변환된 순수 C 코드가 만들어진다. 이 C 코드는 시스템의 C compiler를 이용하여 object code로 compile한 다음, GOLDILOCKS에서 제공하는 embedded SQL library인 libgoldilocksesql.a와 함께 링크하여 최종 목적인 응용 프로그램을 만든다.

<a id="e185cd7f79692695"></a>
![Embedded SQL 응용 프로그램 개발](../assets/images/282eafeb37b217c0.png)

<a id="b1f93c902ff6e268"></a>
#### Embedded SQL 응용 프로그램 개발 도구 구성

GOLDILOCKS의 embedded SQL 응용 프로그램은 다음과 같은 요소들로 구성되어 있다.

**Embeeded SQL 응용 프로그램 개발 도구 구성**

<a id="53c9932d5ea18edc"></a>
| Directory or file | Description |
| --- | --- |
| `\bin\gpec` | GOLDILOCKS precompiler embedded SQL for C |
| `\include\goldilocksesql.h` | Embedded SQL library header file. Precompiler가 자동으로 삽입하기 때문에 사용자가 별도로 조작할 것은 없다. |
| `\include\sqlca.h` | SQLCA 자료 구조 관련 header file 이다. |
| `\lib\libgoldilocksesql.a, \lib\libgoldilocksesqls.so` | Embedded SQL run-time library 이다. |
| `\lib\libgoldilocks.a, \lib\libgoldilockss.so` | GOLDILOCKS DA/ CS 혼용 mode library 이다. |
| `\lib\libgoldilocksa.a, \lib\libgoldilocksas.so` | GOLDILOCKS DA mode library 이다. |
| `\lib\libgoldilocksc.a, \lib\libgoldilockscs.so` | GOLDILOCKS CS mode library 이다. |
| `\sample\EmbeddedSQL` | Sample program 이다. |

<a id="a617f9f0843abfff"></a>
### Building Application

본 절에서는 GOLDILOCKS의 embedded SQL 소스 프로그램을 build하여 실행 형태의 응용 프로그램을 만드는 과정을 설명한다.

<a id="b22c072d21be935b"></a>
#### Precompile

<a id="0f1de7b919b00f77"></a>
##### 설명

사용자가 embedded SQL을 사용하여 작성한 C/ C++ 소스 코드를 precompile하여, 순수한 C/ C++ 소스 코드를 생성한다. 이 과정의 핵심은 사용자가 작성한 embedded SQL을 GOLDILOCKS에서 제공하는 library call로 변환하는 것이며, embedded SQL을 제외한 C/ C++ 소스 코드는 변환하지 않는다.

<a id="4f5f14bd96cd35a2"></a>
##### 사용 방법

GOLDILOCKS의 precompiler 이름은 gpec이고 $GOLDILOCKS_HOME/bin/에 위치한다.  
gpec은 다음과 같은 방법으로 사용한다.

```
$ gpec [OPTION]... <input file>
```

gpec은 &lt;input file&gt;을 입력 받아서 precompile 과정을 거친 다음 C/ C++ 소스 코드를 생성해낸다. &lt;input file&gt;은 기본적으로 *.gc 확장자를 가지고 있는데 이 확장자는 생략할 수 있다. 만약 &lt;input file&gt;이 *.gc 확장자를 가지고 있지 않을 경우, 반드시 file의 이름에 확장자까지 써 주어야 한다.  
gpec에 주어지는 옵션에 대한 자세한 내용은 [Precompiler Options](#f1b7f5b92f394d04)을 참조한다.

<a id="9c3b501c466fa0bd"></a>
##### Example

```
$ gpec sample1

FileName: sample1
Pre-compile sample1.gc -> sample1.c
```

<a id="017c7d2845b36b3e"></a>
#### Compile

Precompile 과정을 거쳐서 생성된 코드는 C/ C++ 소스 코드이다. 이 소스 코드는 platform에서 제공하는 C/ C++ compiler를 사용하여 object code를 생성한다. 이 과정에 대한 자세한 내용은 사용자 각자의 platform에서 제공하는 C/ C++ compiler 사용설명서를 참조한다.

<a id="31376d58447194ac"></a>
#### Link

위의 절차들을 통해 생성된 object code들을 link하여 응용 프로그램을 생성하는데, GOLDILOCKS에서는 embedded SQL에 대해 libgoldilocksesql.a를 제공한다. 이 library는 precompiler가 embedded SQL을 변환한 GOLDILOCKS API들을 포함하므로 embedded SQL 응용 프로그램을 만들 때 반드시 필요하다.

추가적으로 GOLDILOCKS의 다양한 동작 모드에 따라서 필요한 library가 달라지게 되는데, 현재 응용 프로그램의 동작 모드에 따라 다음과 같이 library를 선택하여 링크한다.

<a id="a4b225564b4d797b"></a>
| 동작 mode | Static library | Shared object |
| --- | --- | --- |
| DA 전용 | libgoldilocksa.a | libgoldilocksas.so |
| CS 전용 | libgoldilocksc.a | libgoldilockscs.so |
| DA/ CS 혼용 | libgoldilocks.a | libgoldilockss.so |

그 밖의 link 과정 역시 일반적인 C/ C++ 응용 프로그램 생성 과정과 다르지 않으므로, platform에서 제공하는 linker 매뉴얼을 참조한다.

<a id="5e68719f838651fe"></a>
#### Example

위의 precompile, compile, link 과정을 편하게 수행하기 위하여 make를 많이 이용한다. 다음은 간단한 sample 프로그램을 만들기 위한 makefile의 예이다. 아래 예제를 참조하여 각자의 환경에 맞는 makefile을 만들어 사용해야 한다.

```
CC = gcc 
CFLAGS = -g -Wall
 
INC = -I$(GOLDILOCKS_HOME)/include
LFLAGS = -L$(GOLDILOCKS_HOME)/lib
 
LIB = -lgoldilocksesql -lpthread -lm -lrt
ifeq ($(CSMODE), 1)
    LIB += -lgoldilocksc
else
    ifeq ($(MIXMODE), 1)
        LIB += -lgoldilocks
    else
        LIB += -lgoldilocksa
    endif
endif
 
GPEC = gpec
GPECFLAGS = 
#GPECFLAGS = --unsafe-null --no-prompt
BINS = overview sample1 sample2 sample3 sample4 sample5 dyn1 dyn2 number date_time thread1 fetch_struct_array
 
ifneq ($(MAKECMDGOALS), clean)
ifneq ($(MAKECMDGOALS), all)
TARGET = $(MAKECMDGOALS)
OBJECT = $(TARGET).o
C_SRC  = $(TARGET).c
endif
endif
```

- 암묵적 규칙

```
.SUFFIXES: .gc .c .o

.gc.c:
    $(GPEC) $(GPECFLAGS) $^         ❶ Precompile

.c.o:
    $(CC) $(CFLAGS) -c $(INC) $^    ❷ Compile
```

- Build 규칙

```
NoTarget :
    @echo "Syntax : make {all | sample_name | clean}"
    @echo "sample_name is one of '$(BINS)'"
 
all :
    for target in $(BINS); do \
        $(MAKE) $$target;     \
    done
 
$(OBJECT) : $(C_SRC)
$(TARGET) : $(OBJECT)
    $(CC) -o $@ $^ $(LFLAGS) $(LIB)   ❸ Link
 
clean :
    rm -rf $(BINS) *.o *.c *~ core
```

<a id="b2850855bca2fa14"></a>
#### Sample

GOLDILOCKS에서는 embedded SQL 응용 프로그램 작성에 대한 이해를 돕기 위해 간단한 embedded SQL sample 코드를 제공한다. Sample 코드는 $GOLDILOCKS_HOME/sample/EmbeddedSQL 디렉토리에 있으며, 이 sample들을 수행하기 위해서는 해당 디렉토리에 함께 존재하는 sample.sql을 먼저 수행해야 한다.

```
$ cd $GOLDILOCKS/sample/EmbeddedSQL
$ gsql test test -i sample.sql
$ make
Syntax : make {all | sample_name | clean}
sample_name is one of 'overview sample1 sample2 sample3 sample4 sample5 dyn1 dyn2 number date_time thread1 fetch_struct_array xa long_binary psm whenever preprocess'
```

make all은 모든 sample을 build하는데 특정 sample만 별도로 만들려면 make &lt;sample_name&gt;을 하면된다. &lt;sample_name&gt;은 위 메세지를 참조한다. sample2를 build하여 수행하면 다음과 같은 결과가 나온다.

```
$ make sample2
gpec  sample2.gc

FileName: sample2.gc
Pre-compile sample2.gc -> sample2.c
gcc -g -Wall -c -I/home/mycomman/work/product/Gliese/home/include sample2.c
gcc -o sample2 sample2.o -L/home/mycomman/work/product/Gliese/home/lib -lgoldilocksesql -lpthread -lm -lrt -lgoldilocksa
$ ./sample2 
Connect GOLDILOCKS ...
 EMPNO    ENAME                JOB      SALARY
====== ==================== ========== ========
  2854                 Park        RND      800
  2098                  Kim   SALESMAN     1600
  2175                 Choi   SALESMAN     1250
  2306                  Lee    SUPPORT     2975
  2122                  Lyu   SALESMAN     1250
  2999                  Ohn    SUPPORT     2850
  2012                Cheon    SUPPORT     2450
  2168                 Sohn        RND     3000
  2836                  Seo        CEO     5000
  2022                 Song   SALESMAN     1500
  2232                Jeong        RND     1100
  2676                 Kang        RND      950
  2714                  Cho        RND     3000
  2441                 Yoon        RND     1300
====== ==================== ========== ========
Record Count = 14
====== ==================== ========== ========

SUCCESS
############################
```

<a id="f1b7f5b92f394d04"></a>
### Precompiler Options

본 절에서는 gpec의 option들을 설명한다.

<a id="730c41260e233491"></a>
#### --no-prompt, -n

<a id="e5710a00a8107a40"></a>
##### 설명

Version 정보를 출력하지 않는다.

<a id="47b3de04c5681801"></a>
##### 사용 예

```
$ gpec --no-prompt sample2
FileName: sample2
Pre-compile sample2.gc -> sample2.c
$
```

<a id="5ecfb20eeb1c97d0"></a>
#### --version, -v

<a id="2581aa13b94226e7"></a>
##### 설명

Version 정보만 출력하고 종료한다.

<a id="0401bb64a8958d39"></a>
##### 사용 예

```
$ gpec --version

$
```

<a id="9b3a25fe81040c9e"></a>
#### --help, -h

<a id="dcf000f9642980a7"></a>
##### 설명

Help message를 출력한다. gpec에 아무런 option이나 &lt;input file&gt;을 주지 않을 때도 동일하게 동작한다.

<a id="aefa66d21e8e52f5"></a>
##### 사용 예

```
$ gpec --help

gpec is the GOLDILOCKS embedded SQL precompiler for C programs.
 
Usage:
  gpec [OPTION]... <input file>
 
Options:
  --no-prompt    No Print version information
  --version      Print version information and exit
  --help         Print help message
  --output       Describe output filename
  --unsafe-null  Allow a NULL fetch without indicator variable
  --include-path Describe header file path
  --no-lineinfo  Exclude line information
  --char_map     Mapping of character arrays ( CHARZ | STRING )

$
```

<a id="951f9bc62df280f9"></a>
#### --output, -o

<a id="469be17ad4fd9939"></a>
##### 설명

Precompile 결과 file의 이름을 지정한다. 이 옵션이 주어지지 않으면, &lt;input file&gt;과 같은 file 이름을 가지고 확장자가 .c 인 file이 만들어진다.

<a id="51a8fae56081f125"></a>
##### 사용 예

- Output을 사용하지 않은 경우

```
$ gpec sample2.gc

FileName: sample2.gc
Pre-compile sample2.gc -> sample2.c
$ ls
sample2.c  sample2.gc
```

- Output을 사용한 경우

```
$ gpec --output outfile.cpp sample2.gc
FileName: sample2.gc
Pre-compile sample2.gc -> outfile.cpp
$ ls
outfile.cpp  sample2.gc
```

<a id="f7931f64dbb04d81"></a>
#### --unsafe-null

<a id="2acde0254992b721"></a>
##### 설명

Host indicator variable을 사용하지 않은 경우에도 NULL fetch가 발생했을 때 성공하도록 해준다. 이것은 단지 연산이 성공했다는 의미일 뿐이지 NULL 값을 얻어올 수 있다는 의미는 아니다.

<a id="be38e588d22b9aec"></a>
##### 사용 예

```
$ gpec --unsafe-null sample2
FileName: sample2
Option : --unsafe-null
Pre-compile sample2.gc -> sample2.c
$
```

<a id="d9b32b976ddd0197"></a>
#### --include-path, -I

<a id="6dcbac3335129956"></a>
##### 설명

Precompile을 할 때 참조해야 할 header file의 경로를 기술한다. Precompile을 수행하면서 EXEC SQL INCLUDE 구문을 통해 다른 header file을 찾게 되는데, 우선 현재 file이 위치한 디렉토리부터 검색하고, 없으면 이 옵션이 기술된 디렉토리들에서 차례대로 찾는다.

<a id="f5549decb2fa449e"></a>
##### 사용 예

Header file이 include 디렉토리에 존재하는 경우의 예이다.

- 에러가 발생한 경우

```
$ gpec sample.gc 

FileName: sample.gc
Pre-compile sample.gc -> sample.c

ERR-42000(41000): syntax error 
Error at line 12, in file sample.gc
ERR-42000(41004): "decl.h": file not exist 

ERR-42000(41000): syntax error 
rsEmpRecord gRecord[] = {
^
Error at line 15, in file sample.gc
```

- -I 옵션을 사용한 경우

```
$ gpec -Iinclude sample.gc 
FileName: sample.gc
Pre-compile sample.gc -> sample.c
$
```

<a id="dee7d67eb3283f6f"></a>
#### --no-lineinfo

<a id="4c907cc8154c2c18"></a>
##### 설명

GPEC은 기본적으로 gc file을 c file로 변환할 때, gc file로 디버깅이 가능하도록 #line 정보를 추가한다. 그러나 이 옵션을 사용하면 c file을 생성할 때 #line preprocessor를 통한 line 정보를 추가하지 않는다.

<a id="4e99448777cea19a"></a>
##### 사용 예

```
$ gpec --no-lineinfo sample2
FileName: sample2
Pre-compile sample2.gc -> sample2.c
$
```

<a id="3595f7539708c120"></a>
#### --char_map, -c

<a id="e80a5f35f14c1276"></a>
##### 설명

DECLARE SECTION 내에 선언된 char 형식의 data를 어떤 type으로 mapping을 할지 설정한다. Default 값은 'STRING'인데 NULL로 종료되는 data형식이다. 'CHARZ'는 space padding되고 NULL로 종료되는 data형식이다.

<a id="55e0d9a32bf0b696"></a>
##### 사용 예

```
$ gpec --char_map=STRING overview
FileName: overview
Pre-compile overview.gc -> overview.c

$ gpec --char_map=CHARZ overview
FileName: overview
Pre-compile overview.gc -> overview.c
```

<a id="7706bc90c6896eff"></a>
#### --define, -D

<a id="f0bb7908511212b8"></a>
##### 설명

gpec에서 사용되는 define 이름으로써 1로 설정된다.

<a id="01ec0c22943eb12f"></a>
##### 사용 예

```
$ gpec --define=AAA preprocess
FileName: preprocess
Pre-compile preprocess.gc -> preprocess.c

$ gpec -D BBB preprocess
FileName: preprocess
Pre-compile preprocess.gc -> preprocess.c
ERR-42000(41028): 'BBB' macro is already defined at line 45, in file preprocess.gc
```

<a id="382e15424d707a60"></a>
#### --cumulative

<a id="1547e158084572d6"></a>
##### 설명

FETCH CURSOR 구문에 대해서 sqlerrd[2]을 누적된 합으로 처리하도록 한다.

<a id="91b24b4b7ab35936"></a>
##### 사용 예

```
$ gpec --cumulative sample
FileName: sample Option : --cumulative
Pre-compile sample.gc -> sample.c
$
```

<a id="4d9bd453b32acb53"></a>
#### --parse

<a id="2288a6ced94b6504"></a>
##### 설명

gpec이 입력 소스를 어느 수준까지 파싱할지 지정한다. 지정하지 않으면 기본값은 partial이 적용된다.

- none: gpec 실행에 필요한 최소한의 구조만 파싱한다.
- partial: gpec 전처리 단계에 필요한 범위까지 파싱한다.

<a id="2249f48a0337c1a9"></a>
##### 사용 예

```
$ gpec --parse=none sample.gc
FileName: sample Option : --pasrse=none
Pre-compile sample.gc -> sample.c
$
```

<a id="39245ca09c37e99b"></a>
## Embedded SQL

<a id="37fdea93b77302cd"></a>
### Preprocessing

<a id="103b4ad492d83c73"></a>
#### 개요

gpec에서 precompiling하기 전에 전처리 (preprocessing)를 수행한다.

gpec에서 지원하는 preprocess 지시문은 #if, #ifdef, #if defined, #ifndef, #else, #elif, #endif, #define, #undef 등이다.

gpec의 --define 옵션으로 predefine을 사용할 수 있다. gpec의 옵션으로 predefine된 경우, 1로 정의(definition) 된다.  
예: gpec --define=_DEV_ Test.gc는 Test.gc 파일 내의 #define _DEV_  (1)과 동일하다.

<a id="4b12c8ef6a130d22"></a>
#### 적용 범위

gpec에 대한 SQL precompiler 기능은 DECLARE SECTION 내에서 선언된 호스트 변수에만 적용되며, 해당 변수는 EXEC SQL 문에서만 사용할 수 있다. (DECLARE SECTION 외부에서 선언된 변수는 EXEC SQL 문에서 사용할 수 없다.)   
전처리는 parse=partial일 때 소스 전체에 적용되며, parse=none일 경우 전처리 과정은 생략된다.   
또한 Include 파일 전처리는 EXEC SQL INCLUDE로 지정된 헤더 파일에만 적용되며, 해당 헤더 파일에서 참조하는 외부 헤더의 매크로는 gpec에서 인식되지 않는다.

<a id="bd9bd70afe9e2984"></a>
##### parse = partial

parse 값을 partial로 설정하면 gpec은 소스 전체를 분석하고 전처리를 수행한다.

전처리 조건이 참 (true)인 영역 내의 EXEC SQL 문만 SQL precompiling 대상이 되며, 거짓 (false)인 영역은 그대로 무시된다.

Include 파일 전처리는 EXEC SQL INCLUDE로 추가된 header 파일에만 적용된다.

```
#define _DEV1_
EXEC SQL BEGIN DECLARE SECTION;
#define _DEV2_
char username[10]; 
char password[10];
#ifdef _DEV1_
VARCHAR conn_str[20]; ❶  
#elif defined _DEV2_
VARCHAR conn_str[30]; ❷
#endif
EXEC SQL END DECLARE SECTION;
```

> 1 위치의 _DEV1_는 DECLARE SECTION의 위치와 관계없이 전처리 시점에 평가될 수 있으므로 VARCHAR 선언은 정상적으로 변환된다.  
> 2 위치에서는 _DEV1_가 참이므로 전처리 시점에서 조건이 적용되어 VARCHAR가 변환되지 않는다.

그 결과 gpec을 이용하여 위 파일을 c 파일로 생성하면 다음과 같이 VARCHAR 타입 변수 conn_str[20] 만 변환된 상태로 출력된다.

```
#define _DEV1_
/* EXEC SQL BEGIN DECLARE SECTION; */
#define _DEV2_
char username[10]; 
char password[10];

#ifdef _DEV1_/* VARCHAR conn_str[20]; */
struct { int len; char arr[20]; } conn_str; ❶
#elif defined _DEV2_
VARCHAR conn_str[30];                       ❷
#endif
/* EXEC SQL END DECLARE SECTION; */
```

<a id="edc114b8cdb6fffb"></a>
##### parse = none

parse 값을 none으로 설정하면 gpec은 전처리를 수행하지 않는다. 그 결과 EXEC SQL 문은 전처리 조건과 무관하게 변환된다.

```
#define _DEV1_
EXEC SQL BEGIN DECLARE SECTION;
#define _DEV2_
char username[10]; 
char password[10];
#ifdef _DEV1_
VARCHAR conn_str[20]; ❶  
#elif defined _DEV2_
VARCHAR conn_str[30]; ❷
#endif
EXEC SQL END DECLARE SECTION;
```

> 전처리 조건을 평가하지 않으므로 1 , 2 위치의 VARCHAR 선언 모두 변환 대상이 된다. 이 경우 gpec은 마지막에 선언된 변수를 호스트 변수로 간주한다.

그 결과 gpec을 이용하여 위 파일을 c 파일로 생성하면 다음과 같이 VARCHAR 타입 변수 conn_str[20] 과 conn_str[30] 이 모두 변환된 상태로 출력된다.

```
#define _DEV1_
/* EXEC SQL BEGIN DECLARE SECTION; */
#define _DEV2_
char username[10]; 
char password[10];

#ifdef _DEV1_/* VARCHAR conn_str[20]; */
struct { int len; char arr[20]; } conn_str; ❶
#elif defined _DEV2_
/* VARCHAR conn_str[30]; */
struct { int len; char arr[30]; } conn_str; ❷
#endif
/* EXEC SQL END DECLARE SECTION; */
```

<a id="c85c1ffcc6e93358"></a>
#### 유형

parse 옵션이 partial로 설정된 경우 적용되는 전처리 유형은 다음과 같다.

<a id="18181b433389fcc8"></a>
##### #if

- 문법

```
#if constant
```

또는

```
#if defined identifier
```

또는

```
#if !defined identifier
```

- 예제

```
#if 0
int sVar1;
#endif

#if 3-2   ❶ 연산 가능
int sVar2;
#endif

#if defined _DEV_
int sVar3;
#endif

#if !defined (_DEV_)
int sVar4;
#endif
```

<a id="851bd375364d3a09"></a>
##### #ifdef, #ifndef

- 문법

```
#ifdef identifier
```

또는

```
#ifndef identifier
```

- 예제

```
#ifdef _DEV_
int sVar1;
#endif

#ifndef _DEV_
int sVar2;
#else
int sVar3;
#endif
```

<a id="cff9212e3c9d85e9"></a>
##### #else, #elif, #endif

- 문법

```
#else
```

또는

```
#endif
```

또는

```
#elif constant
```

또는

```
#elif defined identifier
```

- 예제

```
#if 1
int sVar1;
#else
int sVar2;
#endif

#if 0
int sVar3;
#elif 1
int sVar4;
#else
int sVar5;
#endif


#ifdef _DEV1_
int sVar6;

#elif defined _DEV2_
int sVar7;

#elif !defined _DEV3_
int sVar8;
#endif
```

<a id="3587c82aa611adc4"></a>
##### #define, #undef

- 문법

```
#define identifier
```

또는

```
#define identifier constant
```

또는

```
#undef identifier
```

- 예제

```
#define _DEV1_
EXEC SQL BEGIN DECLARE SECTION;
#define _DEV2_
char username[10]; 
char password[10];
#ifdef _DEV1_
VARCHAR conn_str[20]; ❶
#elif defined _DEV2_
VARCHAR conn_str[30]; ❷
#endif
#undef _DEV2_
#ifdef _DEV2_
VARCHAR sDept[10];  ❸
#endif
EXEC SQL END DECLARE SECTION;
```

> 1 _DEV1_가 정의되어 있기 때문에 gpec에서 host 변수로 처리된다.  
> 2 _DEV2_는 #ifdef _DEV1_이 true이므로 gpec에서 무시한다.  
> 3 _DEV2_가 undef 되었으므로 gpec에서 무시한다.

> #define에는 주석을 사용할 수 있다. 그러나 #define이 여러 라인으로 나뉘어 작성되면 주석을 정확하게 처리할 수 없다.

```
#define _DEF1_  1 \                           ❶ 
    + 1
#define _DEF2_   1 \ /* this is               ❷ 
  comment */  + 1
#define _DEF3_   1 \ /* this is comment */    ❸
    + 1
#define _DEF4_  1  /* this is comment */ + 1  ❹
```

> 1 _DEF1_은 1 + 1로 처리된다.  
> 2 _DEF2_는 1로 처리된다.   
>  3 _DEF3_은 정상적으로 처리되지 못한다.  
> 4 _DEF_4_는 1 + 1로 처리된다.

<a id="bdfd3f4bf3153e57"></a>
#### 제약사항

<a id="53fe98130cff562e"></a>
##### 매크로 사용 위치 제약

C 선언문의 중간이나 EXEC SQL 문의 중간에는 매크로를 사용할 수 없다.

```
EXEC SQL BEGIN DECLARE SECTION;
char 
#ifdef _DEV_
username[10]; ❶ 잘못된 MACRO 사용
#else
username[20]; ❷ 잘못된 MACRO 사용
#endif
EXEC SQL END DECLARE SECTION;
EXEC SQL 
    SELECT USERNAME INTO :username
#ifdef _DEV_
    FROM EMP ❸ 잘못된 MACRO 사용
#else
    FROM DEV_EMP ❹ 잘못된 MACRO 사용
#endif
    WHERE EMPNO = 10;
```

<a id="863b2fae5d393d8a"></a>
##### DECLARE SECTION 제약

Declare section 내부에 선언된 경우라도 해당 선언이 EXEC SQL 문까지 확장되지는 않는다.

```
EXEC SQL BEGIN DECLARE SECTION;
#define C_EMP_NO   14
char username[10]; 
EXEC SQL END DECLARE SECTION;


EXEC SQL 
	SELECT USERNAME INTO :username
	FROM EMP

	WHERE EMPNO = C_EMP_NO; ❶ 잘못된 MACRO 사용
```

<a id="23fdb2d0ebf80ce8"></a>
##### 전처리 조건식 제약

전처리 지시문의 조건식 (expression)은 반드시 한 줄로 작성해야 한다. 라인 연속 (\)을 사용한 다중 라인 조건식은 정상적으로 처리되지 않는다.

```
#if  1 && \  ❶ 반드시 한 줄로 작성해야 한다.
1
EXEC SQL INCLUDE "my.h";
#endif
```

<a id="1e1d9c5bcf2e0434"></a>
##### 매크로 지원 제약

gpec 전처리는 함수 형태의 매크로와, 매크로 내부에서 다른 매크로를 참조하는 형태의 매크로를 지원하지 않는다.

```
#define SIZE_1 10
#define SIZE_2 SIZE_1    ❶ 다른 매크로를 참조하는 경우 정상적인 값을 얻지 못한다.
#define FUNC_1( a, b ) a + b
#if FUNC_1( SIZE_1, SIZE_2 )
```

<a id="657765e09ec6af68"></a>
### 연결

<a id="05eeaac012850871"></a>
#### Database 연결

Embedded SQL 프로그램에서 database에 접속하여 작업을 수행하기 위해서는, database server에 연결하는 과정이 필요하다.   
GOLDILOCKS에서 database에 연결하는 구문은 다음과 같다.

```
EXEC SQL [ AT <db_name> ] CONNECT <user_name> IDENTIFIED BY <password> [ AT <db_name> ] [ USING <conn_string> ]

<db_name> := dbname | :hostvar
<user_name> := username | :hostvar
<password> := password | :hostvar
<conn_string> := connection_string | :hostvar
```

Database에 접속하는 가장 기본적인 방법은 다음과 같다.

```
EXEC SQL BEGIN DECLARE SECTION;
char username[10]; 
char password[10]; 
EXEC SQL END DECLARE SECTION;
strcpy( username, "test" );
strcpy( password, "test" );
...

EXEC SQL CONNECT :username IDENTIFIED BY :password;
```

GOLDILOCKS는 shared memory에 직접 attach하여 구동하는 D/A 모드와, TCP 통신을 사용하여 database에 접속하는 C/S 모드 둘 다 지원한다. D/A 모드로 동작할 때는 database의 동일한 호스트에서 직접 접근하게 되므로 위와 같이 별도의 서버 정보를 포함하지 않아도 사용할 수 있지만 C/S 모드로 동작하기를 원할 때는 Data Source Name (DSN)을 지정하여 접근하도록 해야 한다. DSN에 대한 자세한 내용은 [데이터 원본 구성](29-odbc.md#95f39b6bab8f3af7)을 참조한다.

DSN을 사용할 때는 connection_string 정보가 주어져야 하는데, 이 때 connection_string 정보를 사용하기 위하여 USING 절을 이용한다. 다음은 이름이 "GOLDILOCKS"인 DSN과 USING 절을 사용하는 연결 구문의 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
char username[10]; 
char password[10];
char conn_str[20];
EXEC SQL END DECLARE SECTION;
strcpy( username, "test" );
strcpy( password, "test" );
strcpy( conn_str, "DSN=GOLDILOCKS" );
...

EXEC SQL CONNECT :username IDENTIFIED BY :password USING :conn_str;
```

응용 프로그램을 개발하면서 각 연결을 독자적으로 식별해야 할 때가 있다. D/A 모드의 multi-thread 프로그램에서 각각 connection을 맺거나, C/S 모드에서 connection을 여러 개 맺는 경우가 이에 해당하는데, 이 때 각 connection에 이름을 부여하려면 AT 절을 사용한다.

AT 절은 CONNECT 구문의 가장 앞에 올 수도 있고, USING 절 앞에 위치하는 것도 가능하다. 다음은 AT 절을 사용한 CONNECT 구문의 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
char username[10]; 
char password[10];
char conn_str[20];
char conn_name[10];
EXEC SQL END DECLARE SECTION;
strcpy( username, "test" );
strcpy( password, "test" );
strcpy( conn_str, "DSN=GOLDILOCKS" );
strcpy( conn_name, "DBCONN1" );
...

EXEC SQL CONNECT :username IDENTIFIED BY :password AT :conn_name USING :conn_str;
```

<a id="6066df31b82aebe0"></a>
#### Database 연결 해제

응용 프로그램에서 database에 대한 연결을 해제한다. Connect 구문과 마찬가지로, 연결 해제 역시 기본연결을 해제하는 방법과 connection 이름을 주어서 해제하는 방법이 있다. 또한, 현재 응용 프로그램에서 연결한 모든 연결을 해제하는 구문도 제공한다.

<a id="a1e53fba0c89b7e8"></a>
##### 단일 연결 해제

단일 연결 해제에는 명시적인 방법과 암묵적인 방법이 있다.   
명시적인 방법은 DISCONNECT 구문을 사용하는 것으로써 그 사용 방법은 다음과 같다.

```
EXEC SQL [ AT <db_name> ] DISCONNECT;
```

Transaction은 commit이나 rollback을 통해 그 주기를 종료한다. 이 때 transaction 종료 구문 뒤에 RELEASE 옵션을 추가로 기술하여 암묵적으로 연결을 해제할 수 있다.

```
EXEC SQL [ AT <db_name> ] { COMMIT/ROLLBACK } [ WORK ] RELEASE;
```

<a id="2adc3361eabe257d"></a>
##### 전체 연결 해제

현재 응용 프로그램의 모든 연결을 한꺼번에 해제하기를 원할 경우, 다음과 같은 구문을 사용한다.

```
EXEC SQL DISCONNECT ALL;
```

<a id="bc67afaff45702b8"></a>
### Transaction

Database 응용 프로그램은 트랜잭션 단위로 구성된다. 따라서 embedded SQL 프로그램 역시 트랜잭션을 조작할 수 있어야 하며, 본 절에서는 그 방법에 대해 설명한다.

<a id="b18d44be0b03971b"></a>
#### Transaction의 시작과 종료

Transaction이 connection 된 후에 가장 처음으로 수행되는 SQL에서 시작된다. 이렇게 시작된 transaction은 명시적으로 종료 명령이 발생할 때까지 유지되며, 종료 명령은 완료 (COMMIT) 명령과 취소 (ROLLBACK) 명령 두 가지가 있다.

<a id="da0594164960a6a7"></a>
##### COMMIT

Transaction의 완료 명령이 주어지면 다음과 같은 작업들이 발생한다.

- 현재 transaction이 시작되고 나서 발생한 모든 data 갱신이 database에 영구적으로 반영된다.
- 반영된 갱신 사항이 이후에 시작된 모든 transaction이나 sensitive한 cursor에 visible하게 적용된다.
- 현재 transaction에서 생성된 모든 savepoint가 삭제된다.
- 현재 transaction에서 획득한 모든 lock이 해제된다.
- 현재 transaction에서 open 된 cursor들이 close된다. (단, holdable cursor는 예외이다.)
- Transaction을 종료한다

완료 명령은 다음과 같이 사용한다.

```
EXEC SQL COMMIT [ WORK ];
```

<a id="d42d8d18635a3591"></a>
##### ROLLBACK

취소 (rollback) 명령의 종류는 다음과 같다.

- Transaction 전체 rollback
- Transaction 부분 rollback
- Statement-level rollback

Transaction rollback 명령이 주어지면 다음과 같은 작업들이 발생한다.

- 현재 transaction이 시작되고 나서 발생한 모든 data 갱신 사항이 취소되어 transaction 발생 이전의 상태로 되돌아간다.
- 현재 transaction에서 생성된 모든 savepoint가 삭제된다.
- 현재 transaction에서 획득한 모든 lock이 해제된다.
- 현재 transaction에서 open 된 cursor들이 close된다. (단, holdable cursor는 예외이다.)
- Transaction을 종료한다

취소 명령은 다음과 같이 사용한다.

```
EXEC SQL ROLLBACK [ WORK ];
```

Transaction을 부분 rollback하려면 savepoint를 이용한다. 응용 프로그램 개발자는 명시적으로 savepoint를 지정하고, 이 savepoint까지 작업을 되돌려 취소하도록 함으로써 transaction을 부분적으로 rollback 할 수 있다. Transaction을 부분 rollback하면 다음과 같은 작업들이 발생한다.

- 취소된 savepoint 이후에 발생한 모든 갱신 사항이 취소된다.
- 취소된 savepoint 이후에 생성된 savepoint들이 삭제된다.
- 취소된 savepoint 이후에 획득한 lock들이 해제된다.

Transaction을 부분적으로 취소하는 명령은 다음과 같이 사용한다.

```
EXEC SQL ROLLBACK TO SAVEPOINT <savepoint_name>;
```

Statement-level rollback은 현재 수행중이었던 statement만 단독으로 취소하는 기능이다. 예를 들어, table에 row를 삽입하다가 unique violation이 발생한 경우처럼, 현재 statement를 더 이상 수행할 수 없는 경우에는 현재 statement만 취소해야 다음 작업을 계속 진행할 수 있다.

이 경우, GOLDILOCKS 내부에서 자체적으로 statement를 취소하기 때문에 별도로 구문상으로 지정할 명령은 없다.

<a id="c6c381bf2c18cec1"></a>
#### Auto Commit

일반적으로 GOLDILOCKS embedded SQL이 connection 될 때 transaction은 non auto-commit mode로 작동한다.

그러나 응용 프로그램의 개발 편의성이나, 특정 응용 프로그램의 논리 환경에서 auto-commit mode를 수정해야 할 때도 있다. 이러한 경우에 대비하여 GOLDILOCKS의 embedded SQL precompiler에서는 다음과 같은 구문을 사용하여 auto-commit mode를 켜거나 끌 수 있다.

```
EXEC SQL [ AT <db_name> ] AUTOCOMMIT { ON | OFF };
```

<a id="a398dbf14d7ed4af"></a>
#### RELEASE Option

Transaction을 종료 (commit/ rollback) 할 때 RELEASE option을 사용하여 현재 사용 중인 connection을 해제할 수 있다.   
이 옵션은 transaction 전체 종료에만 적용할 수 있고 transaction을 부분적으로 취소 (ROLLBACK TO SAVEPOINT) 할 때는 사용할 수 없다.

<a id="f6227d6c5418797e"></a>
### Host Variables and Datatypes

Embedded SQL 응용 프로그램은 database server와 연동하여 data를 조작 (manipulation)하고 질의(query)하여 원하는 결과를 획득하는 것을 목적으로 한다.

이러한 작업을 위해서는 응용 프로그램의 data를 database server로 전달하고, database server로부터 data를 얻어올 수 있는 수단이 필요한데 이 역할을 수행하는 매개체를 host variable이라고 정의한다.

Host variable은 C 언어의 변수로 선언되기 때문에, 응용 프로그램은 C 변수를 사용하는 것과 동일한 방법으로 host variable을 사용할 수 있고 이 변수가 SQL 문의 일부처럼 처리되어 database server와 응용 프로그램 사이의 value 입출력을 담당한다.

<a id="213821c4b5b8df6f"></a>
#### Host Variable 선언

Host variable은 다음과 같이 embedded SQL directive 내에 선언되어야 한다.

```
EXEC SQL BEGIN DECLARE SECTION;
```

- Host variable 선언

```
EXEC SQL END DECLARE SECTION;
```

위와 같은 영역을 declare section이라고 하며 declare section 내에는 host variable을 선언할 수 있는데, 그 선언 방법은 C variable을 선언하는 방법과 동일하다. 다음은 일부 host variable을 선언하는 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
    int     empno;
    char    ename[20];
    double  salary;
EXEC SQL END DECLARE SECTION;
```

<a id="a99fe253622bfa23"></a>
#### Host Variable을 위한 C Data Type

Host variable로 사용되는 C data type은 C 언어에서 제공하는 native type과 GOLDILOCKS에서 부가적으로 제공하는 data type이 있다. 다음 표는 GOLDILOCKS의 embedded SQL에서 제공하는 data type을 설명한다.

<a id="f75a733d4fe73183"></a>
##### C Native Datatype

C native datatype은 C 언어에서 제공하는 기본적인 type으로써 그 범위나 크기가 응용 프로그램을 개발할 때 사용된 platform에 전적으로 종속된다.

**C native datatype**

<a id="00d076a551cdbad3"></a>
| C datatype | description |
| --- | --- |
| char | single character |
| char[n] | 최대 길이가 n인 문자열 |
| short | small integer (2 bytes) |
| int | integer (4 bytes) |
| long | large integer (4/8 bytes) |
| long long | very large integer (8 bytes) |
| float | single precision floating-point number |
| double | double precision floating-point number |

- char

char type은 single character를 나타낸다.

- char[n]

char[n] type은 최대 길이 n을 갖는 문자열(string) data를 나타낸다.  
다음 예제를 참조한다.

```
EXEC SQL BEGIN DECLARE SECTION;
char strName[20];
EXEC SQL BEGIN DECLARE SECTION;
```

위와 같이 선언할 경우, strName은 최대 길이 20을 갖는 문자열 data를 의미한다.   
strName이 ESQL의 output으로 사용되면 space padding이 된다.

> char[]의 최대 길이는 2001을 초과할 수 없다.

- short

2 byte 정수형 datatype을 나타낸다.

- int

4 byte 정수형 datatype을 나타낸다.

- long

Long type은 large integer라는 의미이지만 그 값의 실제 범위는 platform에 따라 결정된다. 64 bit Unix/ Linux platform에서는 long이 8 byte형 정수이지만 32 bit Unix/ Linux platform에서는 4 byte 정수이다.

- long long

Very large integer라는 의미이고 8 byte 정수형을 표현한다.

- float

C 언어의 float type으로써 4 byte single-precision floating-point number를 나타낸다.

- double

C 언어의 double type으로써 double-precision floating-point number를 나타낸다.

<a id="bf4dcf1b39b660e4"></a>
##### Pseudo Datatype

Pseudo type은 다양한 형태의 GOLDILOCKS type을 지원하고 개발 편의성을 위해 GOLDILOCKS embedded SQL precompiler에서 제공하는 type으로써 그 내용의 대부분은 C의 구조체를 사용하여 구현된다.

<a id="090714e41871000e"></a>
<table class="table column_count_2"><caption>GOLDILOCKS embedded SQL pseudo type</caption><thead><tr><th class="to_center"><div>Pseudo type</div></th><th class="to_center"><div>설명</div></th></tr></thead><tbody><tr><td><div>VARCHAR[n]</div></td><td><div>최대 길이가 n인 가변 길이 문자열</div></td></tr><tr><td><div>LONG VARCHAR</div></td><td><div>최대 길이가 100M (104857600)인 가변 길이 문자열</div></td></tr><tr><td><div>BINARY[n]</div></td><td><div>최대 길이가 n인 binary data</div></td></tr><tr><td><div>VARBINARY[n]</div></td><td><div>최대 길이가 n인 가변 길이 binary data</div></td></tr><tr><td><div>LONG VARBINARY </div></td><td><div>최대 길이가 100M (104857600)인 가변 길이 binary data</div></td></tr><tr><td><div>NUMBER</div></td><td><div>유효 자릿수가 38 자리인 정수</div></td></tr><tr><td><div>NUMBER(p)</div></td><td><div>유효 자릿수가 p 자리인 정수</div></td></tr><tr><td><div>NUMBER(p, s)</div></td><td><div>유효 자릿수가 p, scale이 s인 실수</div></td></tr><tr><td><div>BOOLEAN</div></td><td><div>Boolean type</div></td></tr><tr><td><div>DATE</div></td><td><div>날짜형 data</div></td></tr><tr><td><div>TIME</div></td><td><div>시간형 data</div></td></tr><tr><td><div>TIME WITH TIMEZONE</div></td><td><div>Timezone을 갖는 시간형 data</div></td></tr><tr><td><div>TIMESTAMP</div></td><td><div>날짜시간형 data</div></td></tr><tr><td><div>TIMESTAMP WITH TIMEZONE</div></td><td><div>Timezone을 갖는 시간형 data</div></td></tr><tr><td><div>INTERVAL YEAR</div></td><td class="to_middle" rowspan="13"><div>Interval data type</div></td></tr><tr><td><div>INTERVAL MONTH</div></td></tr><tr><td><div>INTERVAL DAY</div></td></tr><tr><td><div>INTERVAL HOUR</div></td></tr><tr><td><div>INTERVAL MINUTE</div></td></tr><tr><td><div>INTERVAL SECOND</div></td></tr><tr><td><div>INTERVAL YEAR TO MONTH</div></td></tr><tr><td><div>INTERVAL DAY TO HOUR</div></td></tr><tr><td><div>INTERVAL DAY TO MINUTE</div></td></tr><tr><td><div>INTERVAL DAY TO SECOND</div></td></tr><tr><td><div>INTERVAL HOUR TO MINUTE</div></td></tr><tr><td><div>INTERVAL HOUR TO SECOND</div></td></tr><tr><td><div>INTERVAL MINUTE TO SECOND</div></td></tr></tbody></table>

<a id="db3a6a789e57647c"></a>
###### **VARCHAR**

VARCHAR type은 가변 길이 문자열을 저장할 수 있는 datatype으로써 다음과 같은 구조체로 구성되어 있다.

```
struct {
    int  len;
    char arr[n];
}
```

여기서 n은 VARCHAR type이 가질 수 있는 최대 길이를 의미한다.

```
EXEC SQL BEGIN DECLARE SECTION;
    VARCHAR varstr[100];
EXEC SQL END DECLARE SECTION;
```

예를 들어 위와 같이 선언할 경우 precompile 과정에서 다음과 같이 변환된다.

```
struct VARCHAR_varstr {
    int  len;
    char arr[100];
} varstr;
```

응용 프로그램에서는 다음과 같은 방법으로 VARCHAR type을 사용할 수 있다.

```
strcpy( varstr.arr, "abcde" );
varstr.len = strlen( varstr.arr );
 
EXEC SQL INSERT INTO TEST_T1 VALUES ( :varstr );
```

> VARCHAR의 길이는 4000을 초과할 수 없다

<a id="bb08c08935b8675c"></a>
###### **LONG VARCHAR**

LONG VARCHAR type은 길이가 긴 가변 길이 문자열을 저장할 수 있는 datatype으로써 다음과 같은 구조체로 구성되어 있다.

```
typedef struct SQL_LONG_VARIABLE_LENGTH_STRUCT
{
    SQLBIGINT   len;
    SQLCHAR   * arr;
} SQL_LONG_VARIABLE_LENGTH_STRUCT;
```

LONG VARCHAR type은 다음과 같이 선언할 수 있다.

```
EXEC SQL BEGIN DECLARE SECTION;
    LONGVARCHAR long_text;
EXEC SQL END DECLARE SECTION;
```

LONG VARCHAR와 VARCHAR의 차이점은 LONG VARCHAR 길이는 최대 100M (104857600)까지 가능하므로 선언할 때 문자열을 저장할 공간을 미리 할당해 놓지 않는다는 것이다. 즉, LONG VARCHAR를 선언한 후에는 실제로 사용하기 전에 long_text.arr에 실제 메모리 공간을 할당해 주어야 하며, 사용 후에 이 메모리 공간을 해제하는 것 역시 응용 프로그램에서 담당해야 한다. 다음은 LONG VARCHAR를 사용하는 예이다.

```
long_text.arr = malloc( 1048576 );
 
gets( long_text.arr );
long_text.len = strlen( long_text.arr );
 
EXEC SQL INSERT INTO TEST_T1 VALUES ( :long_text );
...
free( long_text.arr );
```

> LONG VARCHAR type의 길이는 현재 최대 100M (104857600)까지 지정하여 선언할 수 있다.

<a id="80f5baef0e6d84bf"></a>
###### **BINARY**

BINARY type은 정형화되지 않은 raw data를 그대로 다루기 위한 datatype으로써 다음과 같이 구성되어 있다. 다음은 BINARY type을 선언하는 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
    BINARY binary[100];
EXEC SQL END DECLARE SECTION;
```

위와 같이 선언하면 precompile 과정에서 다음과 같이 변환된다.

```
char binary[100];
```

문자열 저장과 형태는 같지만 char[n]로 정의하는 것이 database의 문자열을 저장하기 위한 것이라면 BINARY type의 내용은 binary data라는 것만 다르다.   
따라서 응용 프로그램에서는 문자열 데이터를 다루는 방법과 동일한 방법으로 BINARY type을 사용할 수 있다.

> BINARY의 최대 길이는 2000을 초과할 수 없다

<a id="9a7601baa8a75cf5"></a>
###### **VARBINARY**

VARBINARY type은 가변 길이 binary data를 저장할 수 있는 datatype으로써 다음과 같은 구조체로 구성되어 있다.

```
struct {
    int  len;
    char arr[n];
}
```

여기에서 n은 VARCHAR type이 가질 수 있는 최대 길이를 의미한다.

```
EXEC SQL BEGIN DECLARE SECTION;
    VARCHAR varbin[100];
EXEC SQL END DECLARE SECTION;
```

예를 들어 위와 같이 선언할 경우 precompile 과정에서 다음과 같이 변환된다.

```
struct VARBINARY_varbin {
    int  len;
    char arr[100];
} varbin;
```

VARBINARY type은 VARCHAR type과 그 형태가 동일하다. VARCHAR는 문자열을 저장하기 위해 사용되는 반면에 VARBINARY는 binary data를 다룬다는 것 외에는 사용방법을 포함한 모든 면에서 동일하다. 따라서 응용 프로그램에서는 VARCHAR를 사용할 때처럼 다음과 같은 방법으로 VARBINARY type을 사용할 수 있다.

```
memcpy( varbin.arr, binary_data, 50 );
varbin.len = 50;
 
EXEC SQL INSERT INTO TEST_T1 VALUES ( :varbin );
```

> VARBINARY의 길이는 4000을 초과할 수 없다

<a id="2062c5060799ee67"></a>
###### **LONG VARBINARY **

LONG VARBINARY type은 길이가 긴 가변 길이 binary data를 저장할 수 있는 datatype으로써 다음과 같은 구조체로 구성되어 있다.

```
typedef struct SQL_LONG_VARIABLE_LENGTH_STRUCT
{
    SQLBIGINT   len;
    SQLCHAR   * arr;
} SQL_LONG_VARIABLE_LENGTH_STRUCT;
```

LONG VARBINARY type은 다음과 같이 선언할 수 있다.

```
EXEC SQL BEGIN DECLARE SECTION;
    LONGVARBINARY long_bin;
EXEC SQL END DECLARE SECTION;
```

LONG VARBINARY 와 VARBINARY의 차이점은 LONG VARBINARY type을 선언할 때 binary data를 저장할 공간을 미리 할당해 놓지 않는다는 것이다. (LONG VARCHAR와 VARCHAR의 차이점과 같다.) 즉, LONG VARBINARY 를 선언한 후에는 실제로 사용하기 전에 long_bin.arr에 실제 메모리 공간을 할당해 주어야 하며, 사용 후에 이 메모리 공간을 해제하는 것 역시 응용 프로그램에서 담당해야 한다. 다음은 LONG VARBINARY를 사용하는 예이다.

```
long_bin.arr = malloc( 1048576 );
 
memcpy( long_bin.arr, long_binary_data, 1048576);
long_bin.len = 1048576;
 
EXEC SQL INSERT INTO TEST_T1 VALUES ( :long_bin );
...
free( long_bin.arr );
```

> LONG VARBINARY type의 길이는 현재 최대 100M (104857600)까지 지정하여 선언할 수 있다.

<a id="bac494efca69f02b"></a>
###### **NUMBER**

NUMBER type은 ODBC에서 정의된 SQL_NUMERIC_STRUCT를 응용 프로그램에서 사용할 수 있도록 제공하는 datatype이다.

```
#define SQL_MAX_NUMERIC_LEN 16
typedef struct tagSQL_NUMERIC_STRUCT
{
    SQLCHAR precision;
    SQLSCHAR scale;
    SQLCHAR sign; /* 1=pos 0=neg */
    SQLCHAR val[SQL_MAX_NUMERIC_LEN];
} SQL_NUMERIC_STRUCT;
```

NUMBER type은 precision과 scale을 가지는 실수형 data를 표현할 수 있도록 구성되어 있다. NUMBER type을 선언할 때는 precision과 scale을 결정하여 선언할 수 있고 경우에 따라 scale과 precision을 생략할 수도 있는데 그 의미는 다음과 같다.

**NUMBER type의 precision과 scale**

<a id="29ce25eb7e323d59"></a>
| NUMBER type 선언 | 설명 |
| --- | --- |
| NUMBER | NUMBER(38, 0)과 동일하다. |
| NUMBER(p) | NUMBER(p, 0)과 동일하다. |
| NUMBER(p, s) | Precision이 p이고 scale이 s인 실수형 data이다. |

```
EXEC SQL BEGIN DECLARE SECTION;
    NUMBER        number_default;
    NUMBER(20)    number_20;
    NUMBER(30,10) number_30_10;
EXEC SQL END DECLARE SECTION;
```

예를 들어 위와 같이 변수를 선언하였을 경우, number_default 변수는 NUMBER(38, 0)으로 선언된 것과 동일하고, number_20 변수는 NUMBER(20, 0)으로 선언된 것과 동일하다. NUMBER type은 ODBC type인 SQL_NUMERIC_STRUCT를 사용한다. 다음은 NUMBER type을 사용하는 예이다.

```
/*
 * number.gc
 *
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

EXEC SQL INCLUDE SQLCA;

#define  SUCCESS  0
#define  FAILURE  -1

#define  PRINT_SQL_ERROR(aMsg)                                      \
    {                                                               \
        printf("\n");                                               \
        printf(aMsg);                                               \
        printf("\nSQLCODE : %d\nSQLSTATE : %s\nERROR MSG : %s\n",   \
               sqlca.sqlcode,                                       \
               SQLSTATE,                                            \
               sqlca.sqlerrm.sqlerrmc );                            \
    }
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword);
int CreateTable();
int DropTable();
 
unsigned long long ConvertMantisaToDecimal(SQLCHAR *aNumStrValue)
{
    unsigned long long sResult = 0;
    unsigned long long sLast=1;
    unsigned int sCurrent;
    unsigned int sLSD = 0;
    unsigned int sMSD = 0;
    int          i    = 1;

    for(i = 0; i < SQL_MAX_NUMERIC_LEN; i ++)
    {
        sCurrent = (unsigned char) aNumStrValue[i];
        sLSD = sCurrent % 16; //Obtain LSD
        sMSD = sCurrent / 16; //Obtain MSD
        sResult += sLast * sLSD;
        sLast = sLast * 16;
        sResult += sLast * sMSD;
        sLast = sLast * 16;
    }

    return sResult;
}
 
void PrintNumber(SQL_NUMERIC_STRUCT *aNumber)
{
    unsigned long long  sDigit;
    unsigned long long  sFraction;
    unsigned long long  sMantisa;
    unsigned long long  sFactor;
    int     i;

    sMantisa = ConvertMantisaToDecimal( aNumber->val );

    sFactor = 1;
    for( i = 0; i < aNumber->scale; i ++ )
    {
        sFactor *= 10;
    }

    sDigit = sMantisa / sFactor;
    sFraction = sMantisa % sFactor;
    if( sFraction != 0 )
    {
        printf("%llu.%-3llu", sDigit, sFraction);
    }
    else
    {
        printf("%llu", sDigit);
    }
}
 
int main(int     argc,
         char  **argv)
{
    EXEC SQL BEGIN DECLARE SECTION;
    NUMBER        sNumber;
    NUMBER(10,5)  sResultNumber1;
    NUMBER(10,5)  sResultNumber2;
    char          sCharNumber[20];
    int           sNo;
    int           sResultNo;
    EXEC SQL END DECLARE SECTION;
    int   i;
    int   sState = 0;

    printf("#### Number Datatype Test ####\n");
    printf("Connect GOLDILOCKS ...\n");
    if(Connect("DSN=GOLDILOCKS", "test", "test") != SUCCESS)
    {
        goto fail_exit;
    }

    printf("Create table ...\n");
    if(CreateTable() != SUCCESS)
    {
        goto fail_exit;
    }
    sState = 1;

    printf("Insert record ...\n");
    for(i = 0; i < 20; i ++)
    {
        sNo = i + 1;
        memset( &sNumber, 0x00, sizeof(SQL_NUMERIC_STRUCT) );
        sNumber.precision = 38;
        sNumber.scale = 3;
        sNumber.sign = 1;
        /*
         * 0x627d = 25213
         */
        sNumber.val[0] = 0x7d + i;
        sNumber.val[1] = 0x62;

        snprintf( sCharNumber, 20, "25.2%02d", 13 + i );
        EXEC SQL
            INSERT INTO TEST_T1(C1, C2, C3)
            VALUES(:sNo, :sNumber, :sCharNumber);
        if(sqlca.sqlcode != 0)
        {
            goto fail_exit;
        }
    }

    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    printf("Retrive record\n");
    EXEC SQL
        DECLARE CUR1 CURSOR FOR
        SELECT C1, C2, C3
        FROM   TEST_T1;

    EXEC SQL OPEN CUR1;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    printf(" NO   Number1  Number2\n");
    printf("==== ======== ========\n");

    memset( &sResultNumber1, 0x00, sizeof(SQL_NUMERIC_STRUCT) );
    memset( &sResultNumber2, 0x00, sizeof(SQL_NUMERIC_STRUCT) );
    while( 1 )
    {
        EXEC SQL
            FETCH FROM CUR1
            INTO :sResultNo, :sResultNumber1, :sResultNumber2;

        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            /*
             * No more data
             */
            break;
        }

        if(sqlca.sqlcode != 0)
        {
            goto fail_exit;
        }

        printf("%3d   ", sResultNo);
        PrintNumber( &sResultNumber1 );
        printf("   ");
        PrintNumber( &sResultNumber2 );
        printf("\n");
    }

    printf("==== ======== ========\n");

    EXEC SQL CLOSE CUR1;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    sState = 0;
    printf("Drop table ...\n");
    if(DropTable() != SUCCESS)
    {
        goto fail_exit;
    }

    printf("Disconnect GOLDILOCKS ...\n");
    EXEC SQL COMMIT WORK RELEASE;

    printf("SUCCESS\n");
    printf("############################\n");

    return 0;

  fail_exit:
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    printf("FAILURE\n");
    printf("############################\n\n");

    switch(sState)
    {
        case 1:
            printf("Drop table ...\n");
            (void)DropTable();
        default:
            break;
    }

    EXEC SQL ROLLBACK WORK RELEASE;

    return 0;
}
 
int CreateTable()
{
    EXEC SQL DROP TABLE IF EXISTS TEST_T1;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
```

- Create table

```
EXEC SQL CREATE TABLE TEST_T1 ( C1  INTEGER,
                                    C2  NUMERIC(38,4),
                                    C3  VARCHAR(20) );
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    return SUCCESS;

  fail_exit:
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");

    EXEC SQL ROLLBACK WORK;

    return FAILURE;
}
```

- Drop table

```
int DropTable()
{
    EXEC SQL DROP TABLE TEST_T1;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    return SUCCESS;

  fail_exit:
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    EXEC SQL ROLLBACK WORK;

    return FAILURE;
}
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword)
{
    EXEC SQL BEGIN DECLARE SECTION;
    VARCHAR  sUid[80];
    VARCHAR  sPwd[20];
    VARCHAR  sConnStr[1024];
    EXEC SQL END DECLARE SECTION;
```

- Log on GOLDILOCKS

```
strcpy((char *)sUid.arr, aUserID);
sUid.len = (short)strlen((char *)sUid.arr);
strcpy((char *)sPwd.arr, sPassword);
sPwd.len = (short)strlen((char *)sPwd.arr);
strcpy((char *)sConnStr.arr, aHostInfo);
sConnStr.len = (short)strlen((char *)sConnStr.arr);
```

- DB 연결

```
EXEC SQL CONNECT :sUid IDENTIFIED BY :sPwd USING :sConnStr;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    return SUCCESS;

  fail_exit:
    PRINT_SQL_ERROR("[ERROR] Connection Failure!");

    return FAILURE;
}
```

<a id="9ba706948e23ef97"></a>
###### **BOOLEAN**

BOOLEAN type은 TRUE나 FALSE 값을 갖는다. 실제로는 이 변수가 C 언어의 변수로 사용되기 때문에 변수값이 1이면 TRUE를, 0이면 FALSE의 의미를 갖는다.  
다음은 BOOLEAN type 변수를 사용하는 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
    BOOLEAN boolean;
EXEC SQL END DECLARE SECTION;
 
EXEC SQL SELECT IsEnable INTO :boolean FROM STATUS WHERE ID = 100;
 
if( boolean != 0 )
{
    print( "Enable Status : TRUE\n" );
}
else
{
    print( "Enable Status : FALSE\n" );
}
```

<a id="176332d6b86837e7"></a>
###### **DATE**

Date type은 날짜와 시간을 다룰 수 있다. Date type은 ODBC의 SQL_TIMESTAMP_STRUCT를 구조로 갖는다.

```
typedef struct tagTIMESTAMP_STRUCT
{
        SQLSMALLINT    year;
        SQLUSMALLINT   month;
        SQLUSMALLINT   day;
        SQLUSMALLINT   hour;
        SQLUSMALLINT   minute;
        SQLUSMALLINT   second;
        SQLUINTEGER    fraction;
} TIMESTAMP_STRUCT;
typedef TIMESTAMP_STRUCT SQL_TIMESTAMP_STRUCT;
```

DATE 타입의 변수를 선언하면, precompiler가 위와 같은 구조체로 변환시키는데 각 field의 의미는 ODBC의 SQL_TIMESTAMP_STRUCT와 같다.

<a id="45d57b4f8a67d5ec"></a>
###### **TIME**

TIME type은 시간을 다루는 datatyp으로써 ODBC의 SQL_TIME_STRUCT를 구조로 갖는다.

```
typedef struct tagTIME_STRUCT
{
        SQLUSMALLINT   hour;
        SQLUSMALLINT   minute;
        SQLUSMALLINT   second;
} TIME_STRUCT;
typedef TIME_STRUCT SQL_TIME_STRUCT;
```

TIME 타입의 변수를 선언하면 precompiler가 위와 같은 구조체로 변환시키는데 각 field의 의미는 ODBC의 SQL_TIME_STRUCT와 같다.

<a id="ad740bb81f43286d"></a>
###### **TIME WITH TIMEZONE**

TIME WITH TIMEZONE type은 timezone이 있는 시간을 다루는 datatype으로써 다음과 같은 구조를 갖는다.

```
typedef struct tagTIME_WITH_TIMEZONE_STRUCT
{
   SQLUSMALLINT hour;
   SQLUSMALLINT minute;
   SQLUSMALLINT second;
   SQLUINTEGER  fraction;
   SQLSMALLINT  timezone_hour;
   SQLSMALLINT  timezone_minute;
} TIME_WITH_TIMEZONE_STRUCT;
typedef TIME_WITH_TIMEZONE_STRUCT SQL_TIME_WITH_TIMEZONE_STRUCT;
```

TIME WITH TIMEZONE 타입의 변수를 선언하면 precompiler가 위와 같은 구조체로 변환시키는데 각 field의 의미는 다음과 같다.

**TIME WITH TIMEZONE의 field**

<a id="e79080bbc181af65"></a>
| 파일 이름 | 설명 |
| --- | --- |
| hour | 시간 |
| minute | 분 |
| second | 초 |
| fraction | 소수점 이하 초 |
| timezone_hour | Timezone의 시간 |
| timezone_minute | Timezone의 분 |

<a id="2afa05345de290fe"></a>
###### **TIMESTAMP**

TIMESTAMP type은 날짜~시간을 다루는 datatype으로써 ODBC의 SQL_TIMESTAMP_STRUCT를 구조로 갖는다.

```
typedef struct tagTIMESTAMP_STRUCT
{
        SQLSMALLINT    year;
        SQLUSMALLINT   month;
        SQLUSMALLINT   day;
        SQLUSMALLINT   hour;
        SQLUSMALLINT   minute;
        SQLUSMALLINT   second;
        SQLUINTEGER    fraction;
} TIMESTAMP_STRUCT;
typedef TIMESTAMP_STRUCT SQL_TIMESTAMP_STRUCT;
```

TIMESTAMP 타입의 변수를 선언하면 precompiler가 위와 같은 구조체로 변환시키는데 각 field의 의미는 ODBC의 SQL_TIMESTAMP_STRUCT와 같다.

<a id="28accf727a817c1a"></a>
###### **TIMESTAMP WITH TIMEZONE**

TIMESTAMP WITH TIMEZONE type은 timezone이 있는 timestamp를 다루는 datatype으로써 다음과 같은 구조를 갖는다.

```
typedef struct tagTIMESTAMP_WITH_TIMEZONE_STRUCT
{
   SQLSMALLINT  year;
   SQLUSMALLINT month;
   SQLUSMALLINT day;
   SQLUSMALLINT hour;
   SQLUSMALLINT minute;
   SQLUSMALLINT second;
   SQLUINTEGER  fraction;
   SQLSMALLINT  timezone_hour;
   SQLSMALLINT  timezone_minute;
} TIMESTAMP_WITH_TIMEZONE_STRUCT;
typedef TIMESTAMP_WITH_TIMEZONE_STRUCT SQL_TIMESTAMP_WITH_TIMEZONE_STRUCT;
```

TIMESTAMP WITH TIMEZONE 타입의 변수를 선언하면 precompiler가 위와 같은 구조체로 변환시키는데 각 field의 의미는 다음과 같다.

**TIMESTAMP WITH TIMEZONE의 field**

<a id="fb62346f2ebdd2fa"></a>
| Field 이름 | 설명 |
| --- | --- |
| year | 연 |
| month | 월 |
| day | 일 |
| hour | 시간 |
| minute | 분 |
| second | 초 |
| fraction | 소수점 이하 초 |
| timezone_hour | Timezone의 시간 |
| timezone_minute | Timezone의 분 |

다음은 DATE, TIME, TIMESTAMP, TIME WITH TIMEZONE, TIMESTAMP WITH TIMEZONE type을 다루는 간단한 예이다.

```
/*
 * date_time.gc
 *
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
 
EXEC SQL INCLUDE SQLCA;
 
#define  SUCCESS  0
#define  FAILURE  -1
 
#define  PRINT_SQL_ERROR(aMsg)                                      \
    {                                                               \
        printf("\n");                                               \
        printf(aMsg);                                               \
        printf("\nSQLCODE : %d\nSQLSTATE : %s\nERROR MSG : %s\n",   \
               sqlca.sqlcode,                                       \
               SQLSTATE,                                            \
               sqlca.sqlerrm.sqlerrmc );                            \
    }
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword);
int CreateTable();
int DropTable();
 
int main(int     argc,
         char  **argv)
{
    EXEC SQL BEGIN DECLARE SECTION;
    int                      sNo;
    int                      sResultNo;
    DATE                     sDate, sResultDate;
    TIME                     sTime, sResultTime;
    TIME WITH TIMEZONE       sTimeTz, sResultTimeTz;
    TIMESTAMP                sTimestamp, sResultTimestamp;
    TIMESTAMP WITH TIMEZONE  sTimestampTz, sResultTimestampTz;
    EXEC SQL END DECLARE SECTION;
    int  sState = 0;
 
    printf("#### Datatype Insert Test ####\n");
    printf("Connect GOLDILOCKS ...\n");
    if(Connect("DSN=GOLDILOCKS", "test", "test") != SUCCESS)
    {
        goto fail_exit;
    }

    sState = 1;
    printf("Create table ...\n");
    if(CreateTable() != SUCCESS)
    {
        goto fail_exit;
    }

    sState = 2;
    printf("Insert record ...\n");
 
    sNo = 1;
    /**
     * Date : 2014-7-14 21:29:30
     */
    sDate.year  = 2014;
    sDate.month = 7;
    sDate.day   = 14;
    sDate.hour  = 21;
    sDate.minute = 29;
    sDate.second = 30;
    sDate.fraction = 0;
 
    /**
     * Time : 17:46:35
     */
    sTime.hour   = 17;
    sTime.minute = 46;
    sTime.second = 35;
 
    /**
     * Time With Timezone : 17:46:35.6789(+9:00)
     */
    sTimeTz.hour             = 17;
    sTimeTz.minute           = 46;
    sTimeTz.second           = 35;
    sTimeTz.fraction         = 678900000;
    sTimeTz.timezone_hour    = 9;
    sTimeTz.timezone_minute  = 0;
 
    /**
     * Timestamp : 2014-02-13 17:46:28.123
     */
    sTimestamp.year     = 2014;
    sTimestamp.month    = 2;
    sTimestamp.day      = 13;
    sTimestamp.hour     = 17;
    sTimestamp.minute   = 46;
    sTimestamp.second   = 28;
    sTimestamp.fraction = 123000000;
 
    /**
     * Time With Timezone : 2014-05-18 17:46:35.001(+9:00)
     */
    sTimestampTz.year     = 2014;
    sTimestampTz.month    = 5;
    sTimestampTz.day      = 18;
    sTimestampTz.hour     = 17;
    sTimestampTz.minute   = 46;
    sTimestampTz.second   = 35;
    sTimestampTz.fraction = 1000000;
    sTimestampTz.timezone_hour    = 9;
    sTimestampTz.timezone_minute  = 0;
 
    /**
     * Insert record
     */
    EXEC SQL
        INSERT INTO TEST_T1(C1, C2, C3, C4, C5, C6)
        VALUES(:sNo, :sDate, :sTime, :sTimeTz, :sTimestamp, :sTimestampTz);
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    printf("Retrive record\n");
    EXEC SQL
        SELECT C1, C2, C3, C4, C5, C6
        INTO   :sResultNo, :sResultDate, :sResultTime, :sResultTimeTz, :sResultTimestamp, :sResultTimestampTz
        FROM   TEST_T1
        WHERE  C1 = 1;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    printf("=================================================================\n");
    printf( "DATE                   : %04d-%02d-%02d %02d:%02d:%02d\n",
            sResultDate.year,
            sResultDate.month,
            sResultDate.day,
            sResultDate.hour,
            sResultDate.minute,
            sResultDate.second );
 
    printf( "TIME                   : %02d:%02d:%02d\n",
            sResultTime.hour,
            sResultTime.minute,
            sResultTime.second );
 
    printf( "TIME WITH TIMEZONE     : %02d:%02d:%02d.%09u(GMT %+02d:%02d)\n",
            sResultTimeTz.hour,
            sResultTimeTz.minute,
            sResultTimeTz.second,
            sResultTimeTz.fraction,
            sResultTimeTz.timezone_hour,
            sResultTimeTz.timezone_minute );
 
    printf( "TIMESTAMP              : %04d-%02d-%02d %02d:%02d:%02d.%09u\n",
            sResultTimestamp.year,
            sResultTimestamp.month,
            sResultTimestamp.day,
            sResultTimestamp.hour,
            sResultTimestamp.minute,
            sResultTimestamp.second,
            sResultTimestamp.fraction );
 
    printf( "TIMESTAMP WITH TIMEZONE: %04d-%02d-%02d %02d:%02d:%02d.%09u(GMT %+02d:%02d)\n",
            sResultTimestampTz.year,
            sResultTimestampTz.month,
            sResultTimestampTz.day,
            sResultTimestampTz.hour,
            sResultTimestampTz.minute,
            sResultTimestampTz.second,
            sResultTimestampTz.fraction,
            sResultTimestampTz.timezone_hour,
            sResultTimestampTz.timezone_minute );
 
    printf("=================================================================\n");
 
    sState = 0;
    printf("Drop table ...\n");
    if(DropTable() != SUCCESS)
    {
        goto fail_exit;
    }
 
    sState = 0;
    printf("Disconnect GOLDILOCKS ...\n");
    EXEC SQL COMMIT WORK RELEASE;
 
    printf("SUCCESS\n");
    printf("############################\n");
 
    return 0;
 
  fail_exit:
    printf("\n");
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
 
    printf("FAILURE\n");
    printf("############################\n\n");
 
    switch(sState)
    {
        case 1:
            printf("Drop table ...\n");
            (void)DropTable();
        default:
            break;
    }
 
    EXEC SQL ROLLBACK WORK RELEASE;
 
    return 0;
}
 
int CreateTable()
{
    EXEC SQL DROP TABLE IF EXISTS TEST_T1;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
```

- Create table

```
EXEC SQL CREATE TABLE TEST_T1 ( C1  INTEGER,
                                    C2  DATE,
                                    C3  TIME,
                                    C4  TIME WITH TIME ZONE,
                                    C5  TIMESTAMP,
                                    C6  TIMESTAMP WITH TIME ZONE );
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
 
    EXEC SQL ROLLBACK WORK;
 
    return FAILURE;
}
```

- Drop table

```
int DropTable()
{
    EXEC SQL DROP TABLE TEST_T1;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
 
    EXEC SQL ROLLBACK WORK;
 
    return FAILURE;
}
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword)
{
    EXEC SQL BEGIN DECLARE SECTION;
    VARCHAR  sUid[80];
    VARCHAR  sPwd[20];
    VARCHAR  sConnStr[1024];
    EXEC SQL END DECLARE SECTION;
```

- Log on GOLDILOCKS

```
strcpy((char *)sUid.arr, aUserID);
    sUid.len = (short)strlen((char *)sUid.arr);
    strcpy((char *)sPwd.arr, sPassword);
    sPwd.len = (short)strlen((char *)sPwd.arr);
    strcpy((char *)sConnStr.arr, aHostInfo);
    sConnStr.len = (short)strlen((char *)sConnStr.arr);
```

- DB 연결

```
EXEC SQL CONNECT :sUid IDENTIFIED BY :sPwd USING :sConnStr;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
    PRINT_SQL_ERROR("[ERROR] Connection Failure!");
 
    return FAILURE;
}
```

<a id="187bc8a0776815f8"></a>
###### **INTERVAL Types**

INTERAVAL type들은 두 개 시간 사이의 간격을 나타내는 datatype으로써 크게 year ~ month 계열과 day ~ second 계열로 구분되며 각 계열별로 다시 세분화된 type으로 구분된다.   
INTERVAL type의 상세한 구분은 다음 표와 같다

<a id="ae92986b62aa7a1c"></a>
<table class="table column_count_3"><caption>INTERVAL type 구분</caption><thead><tr><th class="to_center"><div>계열</div></th><th class="to_center"><div>세부 type</div></th><th class="to_center"><div>설명</div></th></tr></thead><tbody><tr><td class="to_left to_middle" rowspan="3"><div>YEAR TO MONTH</div></td><td class="to_left to_middle"><div>INTERVAL YEAR</div></td><td class="to_left to_middle"><div>연도 차이</div></td></tr><tr><td class="to_left to_middle"><div>INTERVAL MONTH</div></td><td class="to_left to_middle"><div>개월 차이</div></td></tr><tr><td class="to_left to_middle"><div>INTERVAL YEAR TO MONTH</div></td><td class="to_left to_middle"><div>연도부터 개월 차이</div></td></tr><tr><td class="to_left to_middle" rowspan="10"><div>DAY TO SECOND</div></td><td class="to_left to_middle"><div>INTERVAL DAY</div></td><td class="to_left to_middle"><div>날짜 차이</div></td></tr><tr><td class="to_left to_middle"><div>INTERVAL HOUR</div></td><td class="to_left to_middle"><div>시간 차이</div></td></tr><tr><td class="to_left to_middle"><div>INTERVAL MINUTE</div></td><td class="to_left to_middle"><div>분 차이</div></td></tr><tr><td class="to_left to_middle"><div>INTERVAL SECOND</div></td><td class="to_left to_middle"><div>초 차이</div></td></tr><tr><td class="to_left to_middle"><div>INTERVAL DAY TO HOUR</div></td><td class="to_left to_middle"><div>날짜부터 시간 차이</div></td></tr><tr><td class="to_left to_middle"><div>INTERVAL DAY TO MINUTE</div></td><td class="to_left to_middle"><div>날짜부터 분 차이</div></td></tr><tr><td class="to_left to_middle"><div>INTERVAL DAY TO SECOND</div></td><td class="to_left to_middle"><div>날짜부터 초 차이</div></td></tr><tr><td class="to_left to_middle"><div>INTERVAL HOUR TO MINUTE</div></td><td class="to_left to_middle"><div>시간부터 분 차이</div></td></tr><tr><td class="to_left to_middle"><div>INTERVAL HOUR TO SECOND</div></td><td class="to_left to_middle"><div>시간부터 초 차이</div></td></tr><tr><td class="to_left to_middle"><div>INTERVAL MINUTE TO SECOND</div></td><td class="to_left to_middle"><div>분부터 초 차이</div></td></tr></tbody></table>

INTERVAL type은 ODBC의 SQL_INTERVAL_STRUCT를 구조로 가지며 그 내용은 다음과 같다.

```
typedef enum
{
    SQL_IS_YEAR      = 1,
    SQL_IS_MONTH     = 2,
    SQL_IS_DAY      = 3,
    SQL_IS_HOUR      = 4,
    SQL_IS_MINUTE     = 5,
    SQL_IS_SECOND     = 6,
    SQL_IS_YEAR_TO_MONTH   = 7,
    SQL_IS_DAY_TO_HOUR    = 8,
    SQL_IS_DAY_TO_MINUTE   = 9,
    SQL_IS_DAY_TO_SECOND   = 10,
    SQL_IS_HOUR_TO_MINUTE   = 11,
    SQL_IS_HOUR_TO_SECOND   = 12,
    SQL_IS_MINUTE_TO_SECOND   = 13
} SQLINTERVAL;

typedef struct tagSQL_YEAR_MONTH
{
    SQLUINTEGER  year;
    SQLUINTEGER  month;
} SQL_YEAR_MONTH_STRUCT;

typedef struct tagSQL_DAY_SECOND
{
    SQLUINTEGER  day;
    SQLUINTEGER  hour;
    SQLUINTEGER  minute;
    SQLUINTEGER  second;
    SQLUINTEGER  fraction;
} SQL_DAY_SECOND_STRUCT;

typedef struct tagSQL_INTERVAL_STRUCT
{
    SQLINTERVAL  interval_type;
    SQLSMALLINT  interval_sign;
    union {
        SQL_YEAR_MONTH_STRUCT  year_month;
        SQL_DAY_SECOND_STRUCT  day_second;
   } intval;
} SQL_INTERVAL_STRUCT;
```

위의 모든 INTERVAL type은 동일한 구조체를 사용한다. 따라서 각 INTERVAL type에 대해 구조체 내에서 유효한 field를 별도로 구분하는데 구조체 내의 interval_type 필드를 가지고 INTERVAL type을 구분하고, 구조체 내의 intval 공용체로 실제 INTERVAL value를 표현한다. 각 type 별로 intval이 공용체에서 사용되는 field가 다른데 type별로 유효한 field는 다음 표와 같다.

**INTERVAL type별 유효 field**

<a id="f80dd122a6847be4"></a>
| Type | ?.interval_type | ?.intval 유효 field |
| --- | --- | --- |
| INTERVAL YEAR | SQL_IS_YEAR | *.year_month.year |
| INTERVAL MONTH | SQL_IS_MONTH | *.year_month.month |
| INTERVAL YEAR TO MONTH | SQL_IS_YEAR_TO_MONTH | *.year_month.year *.year_month.month |
| INTERVAL DAY | SQL_IS_DAY | *.day_second.day |
| INTERVAL HOUR | SQL_IS_HOUR | *.day_second.hour |
| INTERVAL MINUTE | SQL_IS_MINUTE | *.day_second.minute |
| INTERVAL SECOND | SQL_IS_SECOND | *.day_second.second *.day_second.fraction |
| INTERVAL DAY TO HOUR | SQL_IS_DAY_TO_HOUR | *.day_second.day *.day_second.hour |
| INTERVAL DAY TO MINUTE | SQL_IS_DAY_TO_MINUTE | *.day_second.day *.day_second.hour *.day_second.minute |
| INTERVAL DAY TO SECOND | SQL_IS_DAY_TO_SECOND | *.day_second.day *.day_second.hour *.day_second.minute *.day_second.second *.day_second.fraction |
| INTERVAL HOUR TO MINUTE | SQL_IS_HOUR_TO_MINUTE | *.day_second.hour *.day_second.minute |
| INTERVAL HOUR TO SECOND | SQL_IS_HOUR_TO_SECOND | *.day_second.hour *.day_second.minute *.day_second.second *.day_second.fraction |
| INTERVAL MINUTE TO SECOND | SQL_IS_MINUTE_TO_SECOND | *.day_second.minute *.day_second.second *.day_second.fraction |

Year, month, day, hour, minute, second는 각각 연, 월, 일, 시, 분, 초를 나타내며, fraction은 소수점 이하의 초를 표현한다. (Fraction field는 SECOND를 포함하는 INTERVAL type에서만 유효하다.)

<a id="2c78bf35b9e605e6"></a>
##### Special Type

Special type은 자체적으로 data를 다루기보다는 응용 프로그램 작성에 부가적인 기능과 편의성을 제공하는 특별한 형태의 data type이다. Special type에는 다음과 같은 type들이 있다.

**Special type**

<a id="ba20399e9fa67d9b"></a>
| Type | 설명 |
| --- | --- |
| SQL_CONTEXT | Multi-connection 구조에서 run-time context를 관리한다. |
| Struct | Column의 집합을 구조체로 구성하여 row를 다룰 때 사용한다. |
| Typedef | 기존에 정의된 type을 다른 이름으로 다시 정의한다. |

<a id="5d9a91f46d4c2768"></a>
###### **SQL_CONTEXT**

SQL_CONTEXT는 run-time context를 관리하기 위한 특별한 유형의 data type이다. Run-time context는 응용 프로그램이 실행되는 중에 run-time으로 connection과 connection에 관련된 개별 data를 관리하기 위해 사용된다.

SQL_CONTEXT 변수는 다음과 같이 선언한다.

```
EXEC SQL BEGIN DECLARE SECTION;
SQL_CONTEXT my_context;
EXEC SQL BEGIN DECLARE SECTION;
```

SQL_CONTEXT 변수를 선언한 뒤에는 다음과 같이 할당해 주어야 한다.

```
EXEC SQL CONTEXT ALLOCATE :my_context;
```

SQL_CONTEXT 변수를 사용하려면 USE 구문을 사용한다.

```
EXEC SQL CONTEXT USE :my_context;
```

USE 구문은 사용할 context를 지정하는 구문으로써, 응용 프로그램에서 선언한 context가 아닌 기본 context로 되돌리고자 할 때는 다음과 같이 사용한다.

```
EXEC SQL CONTEXT USE DEFAULT;
```

더 이상 사용하지 않는 SQL_CONTEXT 변수는 다음과 같이 해제할 수 있다.

```
EXEC SQL CONTEXT FREE :my_context;
```

다음은 SQL_CONTEXT를 사용하는 예이다.

```
/*
 * thread1.gc
 *
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <pthread.h>
 
EXEC SQL INCLUDE SQLCA;
 
#define  SUCCESS  0
#define  FAILURE  -1
 
#define  PRINT_SQL_ERROR(aMsg)                                      \
    {                                                               \
        printf("\n");                                               \
        printf(aMsg);                                               \
        printf("\nSQLCODE : %d\nSQLSTATE : %s\nERROR MSG : %s\n",   \
               sqlca.sqlcode,                                       \
               SQLSTATE,                                            \
               sqlca.sqlerrm.sqlerrmc );                            \
    }
 
int Connect(sql_context aCtx, char *aHostInfo, char *aUserID, char *sPassword);
int CreateEmpTempTable();
int DropEmpTempTable();
void *clientThread(void *args);
 
typedef struct thread_param
{
    int    mNo;
    char  *mJobName;
} thread_param;
 
#define  THREAD_COUNT    2

char gJobName[THREAD_COUNT][20]= {
    "RND",
    "SUPPORT"
};
 
int main(int argc, char **argv)
{
    EXEC SQL BEGIN DECLARE SECTION;
    int          sEmpNo;
    varchar      sEName[20 + 1];
    char         sJob[20];
    long         sSalary;
    EXEC SQL END DECLARE SECTION;
    int          sRecordCount = 0;
    pthread_t    thread_id[THREAD_COUNT];
    thread_param param[THREAD_COUNT];
    int          i;
 
    printf("Connect GOLDILOCKS ...\n");
    if(Connect(NULL, "DSN=GOLDILOCKS", "test", "test") != SUCCESS)
    {
        goto fail_exit;
    }
 
    if(CreateEmpTempTable() != SUCCESS)
    {
        goto fail_exit;
    }
```

- Create client thread

```
for( i = 0; i < THREAD_COUNT; i ++ )
    {
        param[i].mNo = i;
        param[i].mJobName = gJobName[i];
        if( pthread_create(&thread_id[i],
                           NULL,
                           clientThread,
                           &param[i]) != 0 )
        {
            printf( "Can't create thread %d!\n", i );
        }
        else
        {
            printf( "Create thread %d!\n", i );
        }
    }
 
    for( i = 0; i < THREAD_COUNT; i ++ )
    {
        if( pthread_join(thread_id[i],
                         NULL) != 0 )
        {
            printf( "Error when waiting for thread %d to terminate!\n", i );
        }
        else
        {
            printf( "Stopped thread %d!\n", i );
        }
    }
```

- Retrieve employee

```
EXEC SQL
        DECLARE EMP_CUR CURSOR FOR
        SELECT empno, ename, job, sal
        FROM   EMP_TEMP
        ORDER BY empno;
 
    EXEC SQL OPEN EMP_CUR;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf(" EMPNO    ENAME                JOB      SALARY\n");
    printf("====== ==================== ========== ========\n");
    while( 1 )
    {
        EXEC SQL
            FETCH EMP_CUR
            INTO  :sEmpNo, :sEName, :sJob, :sSalary;
        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
            goto fail_exit;
        }
 
        sRecordCount ++;
 
        printf("%6d %20s %10s %8ld\n",
               sEmpNo, sEName.arr, sJob, sSalary);
    }
 
    printf("====== ==================== ========== ========\n");
    printf("Record Count = %d\n", sRecordCount);
    printf("====== ==================== ========== ========\n");
 
    EXEC SQL CLOSE EMP_CUR;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    if(DropEmpTempTable() != SUCCESS)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK RELEASE;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf("SUCCESS\n");
    printf("############################\n");
 
    return 0;
 
  fail_exit:
 
    printf("FAILURE\n");
    printf("############################\n\n");
    EXEC SQL ROLLBACK WORK RELEASE;
 
    return 0;
}
 
int Connect(sql_context aCtx, char *aHostInfo, char *aUserID, char *sPassword)
{
    EXEC SQL BEGIN DECLARE SECTION;
    VARCHAR  sUid[80];
    VARCHAR  sPwd[20];
    VARCHAR  sConnStr[1024];
    EXEC SQL END DECLARE SECTION;
    struct sqlca sqlca;
```

- Log on GOLDILOCKS

```
strcpy((char *)sUid.arr, aUserID);
    sUid.len = (short)strlen((char *)sUid.arr);
    strcpy((char *)sPwd.arr, sPassword);
    sPwd.len = (short)strlen((char *)sPwd.arr);
    strcpy((char *)sConnStr.arr, aHostInfo);
    sConnStr.len = (short)strlen((char *)sConnStr.arr);
```

- DB 연결

```
if( aCtx != NULL )
    {
        EXEC SQL CONTEXT USE :aCtx;
        EXEC SQL CONNECT :sUid IDENTIFIED BY :sPwd USING :sConnStr;
    }
    else
    {
        EXEC SQL CONTEXT USE DEFAULT;
        EXEC SQL CONNECT :sUid IDENTIFIED BY :sPwd USING :sConnStr;
    }

    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] Connection Failure!");
 
    return FAILURE;
}
 
int Disconnect(sql_context aCtx)
{
    struct sqlca sqlca;
```

- DB 연결 해제

```
if( aCtx != NULL )
    {
        EXEC SQL CONTEXT USE :aCtx;
        EXEC SQL DISCONNECT;
    }
    else
    {
        EXEC SQL CONTEXT USE DEFAULT;
        EXEC SQL DISCONNECT;
    }
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] Connection Failure!");
 
    return FAILURE;
}
```

- Create table

```
int CreateEmpTempTable()
{
   EXEC SQL DROP TABLE IF EXISTS EMP_TEMP;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL
        CREATE TABLE EMP_TEMP (
            EMPNO NUMBER(4) CONSTRAINT PK_EMP_TEMP PRIMARY KEY,
            ENAME VARCHAR2(10),
            JOB VARCHAR2(9),
            SAL NUMBER(7,2),
            DEPTNO NUMBER(2) );
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    EXEC SQL ROLLBACK WORK;
 
    return FAILURE;
}
```

- Drop table

```
int DropEmpTempTable()
{
    EXEC SQL DROP TABLE EMP_TEMP;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    EXEC SQL ROLLBACK WORK;
 
    return FAILURE;
}
 
void *clientThread(void *args)
{
    EXEC SQL BEGIN DECLARE SECTION;
    SQL_CONTEXT   my_context;
    char          job_name[20 + 1];
    EXEC SQL END DECLARE SECTION;
    int           state = 0;
    thread_param *param = (thread_param *)args;
 
    EXEC SQL CONTEXT ALLOCATE :my_context;
    state = 1;
 
    EXEC SQL CONTEXT USE :my_context;
    if(Connect(my_context, "DSN=GOLDILOCKS", "test", "test") != SUCCESS)
    {
        goto fail_exit;
    }
    state = 2;
 
    strcpy( job_name, param->mJobName );
 
    EXEC SQL
        INSERT INTO EMP_TEMP
        SELECT *
        FROM   EMP
        WHERE  JOB = :job_name;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    state = 1;

    if(Disconnect(my_context) != SUCCESS)
    {
        goto fail_exit;
    }
    state = 0;

    EXEC SQL CONTEXT FREE :my_context;
    pthread_exit(0);

    return NULL;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    switch(state)
    {
        case 2:
            (void)Disconnect(my_context);
        case 1:
            EXEC SQL CONTEXT FREE :my_context;
            break;
        default:
            break;
    }
 
    pthread_exit(0);

    return NULL;
}
```

<a id="93168f6dcc50191a"></a>
###### **Host Structure**

GOLDILOCKS의 embedded SQL에서는 C의 구조체를 host 변수로 사용할 수 있다. 일반적인 scalar 변수는 단일 column을 나타내는 반면에 구조체를 사용하면 여러 개의 column 집합을 간단하게 표현할 수 있다.

Host structure는 그 member 변수들을 차례대로 나열한 것과 결과가 같으므로 SELECT INTO, FETCH INTO의 INTO 절과 INSERT 구문의 VALUES 절에만 사용할 수 있고, WHERE 절이나 UPDATE SET 절 등에서는 사용할 수 없다.

Host structure를 사용하려면 declare section 내에 구조체를 정의하고 이 구조체 변수를 선언한 뒤에 host variable처럼 사용하면 된다. 구조체 정의 방법은 C struct 정의 방법과 같고 typedef를 통해 type을 정의한 후에 사용할 수도 있다.

다음은 host structure를 사용하는 예이다.

```
/*
 * sample4.gc
 *
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
 
EXEC SQL INCLUDE SQLCA;
 
#define  SUCCESS  0
#define  FAILURE  -1
#define  PRINT_SQL_ERROR(aMsg)                                      \
    {                                                               \
        printf("\n");                                               \
        printf(aMsg);                                               \
        printf("\nSQLCODE : %d\nSQLSTATE : %s\nERROR MSG : %s\n",   \
               sqlca.sqlcode,                                       \
               SQLSTATE,                                            \
               sqlca.sqlerrm.sqlerrmc );                            \
    }

EXEC SQL BEGIN DECLARE SECTION;
typedef struct rsRecord
{
    int          mEmpNo;
    varchar      mEName[20 + 1];
    char         mJob[20 + 1];
    long         mSalary;
} rsRecord;
EXEC SQL END DECLARE SECTION;
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword);
 
int main(int argc, char **argv)
{
    EXEC SQL BEGIN DECLARE SECTION;
    rsRecord     sRecord;
    EXEC SQL END DECLARE SECTION;
    int  sRecordCount = 0;
 
    printf("Connect GOLDILOCKS ...\n");
    if(Connect("DSN=GOLDILOCKS", "test", "test") != SUCCESS)
    {
        goto fail_exit;
    }
```

- Retrieve employee

```
EXEC SQL
        DECLARE EMP_CUR CURSOR FOR
        SELECT empno, ename, job, sal
        FROM   EMP
        ORDER BY EMPNO;
 
    EXEC SQL OPEN EMP_CUR;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf(" EMPNO    ENAME                JOB      SALARY\n");
    printf("====== ==================== ========== ========\n");
    while( 1 )
    {
        EXEC SQL
            FETCH EMP_CUR
            INTO  :sRecord;
        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
            goto fail_exit;
        }
 
        sRecordCount ++;
 
        printf("%6d %20s %10s %8ld\n",
               sRecord.mEmpNo, sRecord.mEName.arr, sRecord.mJob, sRecord.mSalary);
    }
 
    printf("====== ==================== ========== ========\n");
    printf("Record Count = %d\n", sRecordCount);
    printf("====== ==================== ========== ========\n");
 
    EXEC SQL CLOSE EMP_CUR;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK RELEASE;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf("\n\nSUCCESS\n");
    printf("############################\n");
 
    return 0;
 
  fail_exit:
 
    printf("\n\nFAILURE\n");
    printf("############################\n\n");
 
    EXEC SQL ROLLBACK WORK RELEASE;
 
    return 0;
}
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword)
{
    EXEC SQL BEGIN DECLARE SECTION;
    VARCHAR  sUid[80];
    VARCHAR  sPwd[20];
    VARCHAR  sConnStr[1024];
    EXEC SQL END DECLARE SECTION;
```

- Log on GOLDILOCKS

```
strcpy((char *)sUid.arr, aUserID);
    sUid.len = (short)strlen((char *)sUid.arr);
    strcpy((char *)sPwd.arr, sPassword);
    sPwd.len = (short)strlen((char *)sPwd.arr);
    strcpy((char *)sConnStr.arr, aHostInfo);
    sConnStr.len = (short)strlen((char *)sConnStr.arr);
```

- DB 연결

```
EXEC SQL CONNECT :sUid IDENTIFIED BY :sPwd USING :sConnStr;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
    PRINT_SQL_ERROR("[ERROR] Connection Failure!");
 
    return FAILURE;
}
```

Host 변수를 사용하기 위해 구조체를 선언할 때는 제약사항이 있다. 구조체 선언에서 중첩된 구조체는 사용할 수 없다. 다음과 같이 구조체 선언 내부에 또 다른 구조체가 존재할 경우에는 host 변수로 사용할 수 없다.

```
EXEC SQL BEGIN DECLARE SECTION;
typedef struct rsRecord
{
    struct person {
        int          mEmpNo;
        varchar      mEName[20 + 1];
    } person;
    char         mJob[20 + 1];
    long         mSalary;
} rsRecord;
EXEC SQL END DECLARE SECTION;
```

<a id="6a7ba6261fb1f6c5"></a>
#### Indicator Variable

<a id="5a7af9afb8ab0dd7"></a>
##### Scalar Indicator

Host 변수들에는 그와 결합된 indicator 변수들이 함께 올 수 있는데 indicator 변수는 현재 host 변수의 값이 NULL인지 여부를 판별한다. Indicator 변수는 host 변수와 마찬가지로 선언하여 사용할 수 있는데 C의 정수형 type (short, int, long, long long)으로만 선언할 수 있다. Indicator는 다음과 같이 사용한다.

```
:hostvar INDICATOR :hostind
:hostvar :hostind (INDICATOR keyword는 생략할 수 있다.)
```

Indicator 변수값은 다음과 같은 의미를 갖는다.

**Input indicator 값**

<a id="91d989cdbc9ab6d9"></a>
| Value | 의미 |
| --- | --- |
| -1 | NULL |
| >= 0 | Host 변수의 값을 input 한다. |

**Output indicator 값**

<a id="79ecdf76008cc128"></a>
| Value | 의미 |
| --- | --- |
| -1 | NULL |
| 0 | Value가 host 변수에 모두 저장되었다. |
| > 0 | Host 변수의 buffer size가 부족하여 value를 host 변수에 모두 저장하지 못한 경우의 DB data 길이이다. |

다음은 indicator를 사용하는 예이다.

```
/*
 * sample5.gc
 *
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
 
EXEC SQL INCLUDE SQLCA;
 
#define  SUCCESS  0
#define  FAILURE  -1
#define  PRINT_SQL_ERROR(aMsg)                                      \
    {                                                               \
        printf("\n");                                               \
        printf(aMsg);                                               \
        printf("\nSQLCODE : %d\nSQLSTATE : %s\nERROR MSG : %s\n",   \
               sqlca.sqlcode,                                       \
               SQLSTATE,                                            \
               sqlca.sqlerrm.sqlerrmc );                            \
    }
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword);
int CreateEmpTempTable();
int DropEmpTempTable();
 
int main(int argc, char **argv)
{
    EXEC SQL BEGIN DECLARE SECTION;
    int          sEmpNo;
    varchar      sEName[20 + 1];
    char         sJob[20];
    long         sSalary;
    int          sDeptNo;
    int          sDeptNoInd;
    EXEC SQL END DECLARE SECTION;
    int          sRecordCount = 0;
    int          state = 0;
 
    printf("Connect GOLDILOCKS ...\n");
    if(Connect("DSN=GOLDILOCKS", "test", "test") != SUCCESS)
    {
        goto fail_exit;
    }
 
    if(CreateEmpTempTable() != SUCCESS)
    {
        goto fail_exit;
    }
    state = 1;
```

- Update Dept NULL where deptno = 10

```
EXEC SQL
        UPDATE EMP_TEMP
        SET    DEPTNO = NULL
        WHERE  DEPTNO = 10;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
```

- Retrieve employee

```
EXEC SQL
        DECLARE EMP_CUR CURSOR FOR
        SELECT empno, ename, job, sal, deptno
        FROM   EMP_TEMP
        ORDER BY empno;
 
    EXEC SQL OPEN EMP_CUR;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf(" EMPNO         ENAME           JOB      SALARY  DEPTNO\n");
    printf("====== ==================== ========== ======== ======\n");
    while( 1 )
    {
        EXEC SQL
            FETCH EMP_CUR
            INTO  :sEmpNo, :sEName, :sJob, :sSalary, :sDeptNo :sDeptNoInd;
        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
            goto fail_exit;
        }
 
        sRecordCount ++;
 
        if(sDeptNoInd == -1)
        {
            printf("%6d %20s %10s %8ld (null)\n",
                   sEmpNo, sEName.arr, sJob, sSalary);
        }
        else
        {
            printf("%6d %20s %10s %8ld %4d\n",
                   sEmpNo, sEName.arr, sJob, sSalary, sDeptNo);
        }
    }
 
    printf("====== ==================== ========== ======== ======\n");
    printf("Record Count = %d\n", sRecordCount);
    printf("====== ==================== ========== ======== ======\n");

    EXEC SQL CLOSE EMP_CUR;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    state = 0;
    if(DropEmpTempTable() != SUCCESS)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK RELEASE;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf("\n\nSUCCESS\n");
    printf("############################\n");
 
    return 0;
 
  fail_exit:
 
    printf("\n\nFAILURE\n");
    printf("############################\n\n");
 
    switch( state )
    {
        case 1:
            (void)DropEmpTempTable();
            break;
        default:
            break;
    }
 
    EXEC SQL ROLLBACK WORK RELEASE;
 
    return 0;
}
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword)
{
    EXEC SQL BEGIN DECLARE SECTION;
    VARCHAR  sUid[80];
    VARCHAR  sPwd[20];
    VARCHAR  sConnStr[1024];
    EXEC SQL END DECLARE SECTION;
```

- Log on GOLDILOCKS

```
strcpy((char *)sUid.arr, aUserID);
    sUid.len = (short)strlen((char *)sUid.arr);
    strcpy((char *)sPwd.arr, sPassword);
    sPwd.len = (short)strlen((char *)sPwd.arr);
    strcpy((char *)sConnStr.arr, aHostInfo);
    sConnStr.len = (short)strlen((char *)sConnStr.arr);
```

- DB 연결

```
EXEC SQL CONNECT :sUid IDENTIFIED BY :sPwd USING :sConnStr;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] Connection Failure!");
 
    return FAILURE;
}
```

- Create table

```
int CreateEmpTempTable()
{
    EXEC SQL DROP TABLE IF EXISTS EMP_TEMP;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL
        CREATE TABLE EMP_TEMP (
            EMPNO NUMBER(4) CONSTRAINT PK_EMP_TEMP PRIMARY KEY,
            ENAME VARCHAR2(10),
            JOB VARCHAR2(9),
            SAL NUMBER(7,2),
            DEPTNO NUMBER(2) );
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL
        INSERT INTO EMP_TEMP
        SELECT * FROM EMP;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
 
    EXEC SQL ROLLBACK WORK;
 
    return FAILURE;
}
```

- Drop table

```
int DropEmpTempTable()
{
    EXEC SQL DROP TABLE EMP_TEMP;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    EXEC SQL ROLLBACK WORK;
 
    return FAILURE;
}
```

<a id="612155f3f97e4888"></a>
##### Structure Indicator

Host 변수가 scalar 변수일 경우, indicator 변수를 선언하고 결합하여 사용한다. 하지만 host 변수가 structure일 경우에는 구조체의 구성 변수에 각각 indicator를 붙여쓸 수가 없다. 이렇게 host 변수가 구조체일 경우에는 indicator 역시 구조체로 만들어서 사용한다.

Indicator 구조체를 선언할 때는 다음과 같은 사항을 준수해야 한다.

- Indicator의 멤버 수와 결합할 host 변수 구조체의 멤버 수가 동일해야 한다.
- Indicator 구조체의 멤버는 모두 정수형 데이터 type을 가져야 한다.

예를 들어 다음과 같은 구조체를 선언했을 경우, 구조체 변수가 네 개이므로 indicator 구조체의 멤버도 네 개가 되어야 한다.

```
EXEC SQL BEGIN DECLARE SECTION;
typedef struct rsRecord
{
    int          mEmpNo;
    varchar      mEName[20 + 1];
    char         mJob[20 + 1];
    long         mSalary;
} rsRecord;
EXEC SQL END DECLARE SECTION;
```

즉, 다음과 같이 선언되어야 한다.

```
EXEC SQL BEGIN DECLARE SECTION;
typedef struct rsRecordInd
{
    int          mEmpNoInd;
    int          mENameInd;
    int          mJobInd;
    int          mSalaryInd;
} rsRecordInd;
EXEC SQL END DECLARE SECTION;
```

Indicator 구조체는 그것과 결합하는 host 변수 구조체와 순서대로 1 : 1 대응한다. 즉, 위와 같이 구조체 선언이 이루어졌을 경우, 다음과 같은 결합 관계를 갖는다.

```
:rsRecordVar INDICATOR :rsRecordIndVar
```

<a id="def2ce8016936685"></a>
| Host variable | 결합되는 indicator |
| --- | --- |
| rsRecordVar.mEmpNo | rsRecordIndVar.mEmpNoInd |
| rsRecordVar.mEName | rsRecordIndVar.mENameInd |
| rsRecordVar.mJob | rsRecordIndVar.mJobInd |
| rsRecordVar.mSalary | rsRecordIndVar.mSalaryInd |

<a id="d087ee4ee8862e20"></a>
### Embedded SQL

<a id="e260a9cd217cb089"></a>
#### Host Variable

Host variable은 응용 프로그램과 GOLDILOCKS 사이의 data 입출력 매개체로 사용된다. 응용 프로그램에서 GOLDILOCKS로 data를 전달할 때는 input host variable이라고 하고 GOLDILOCKS에서 응용 프로그램으로 data를 받아올 때는 output host variable이라고 한다. 그러나 이 두 가지 사이에 선언상의 차이점은 없으며 사용되는 SQL 문장에서 그 역할이 결정된다.

SELECT 또는 FETCH 문의 INTO 절에 위치한 host variable은 GOLDILOCKS에서 data를 받아오는 output host variable이며 그 외에는 모두 input host variable이 된다. Input host variable 값은 해당 SQL 문을 수행하기 전에 설정되어야 한다.

<a id="77744f8f036578e1"></a>
#### Host Indicator

Host variable은 C 언어의 변수를 그대로 사용하기 때문에, NULL을 표시할 수 있는 별도의 방법이 없다. 이 경우에 indicator 변수를 사용할 수 있으며 한 개의 indicator 변수는 한 개의 host variable과 결합한다.

Indicator 변수는 다음과 같은 의미를 갖는다.

**Input indicator 값**

<a id="ff976e87e613f486"></a>
| Value | 의미 |
| --- | --- |
| -1 | NULL |
| >= 0 | Host 변수값을 input 한다. |

**Output indicator 값**

<a id="2e0701a284d84cdf"></a>
| Value | 의미 |
| --- | --- |
| -1 | NULL |
| 0 | Value가 host 변수에 모두 저장되었다. |
| > 0 | Host 변수의 buffer size가 부족하여 value를 host 변수에 모두 저장하지 못한 경우의 DB data 길이이다. |

<a id="61b3de90404dcf25"></a>
##### Insert NULL

NULL 값은 다음과 같이 column에 insert 된다.

```
EXEC SQL INSERT INTO EMP ( EMPNO, DEPTNO ) VALUES ( :empno, NULL );
```

그러나 위와 같이 hard coding하여 응용 프로그램을 만들면 유연성이 매우 떨어진다. 다음은 indicator 변수를 사용하는 예이다.

```
deptno_ind = -1;
EXEC SQL INSERT INTO EMP ( EMPNO, DEPTNO ) VALUES ( :empno, :deptno :deptno_ind );
```

Indicator 변수인 deptno_ind에 -1 값이 주어지면 host variable인 deptno 값에 관계없이 NULL 값으로 인식된다.

<a id="0deac3379cb2f0e9"></a>
##### Fetch NULL

GOLDILOCKS에서 data를 받을 때 indicator 변수를 사용하여 NULL 여부를 판단할 수 있다.   
다음 예제를 참조한다.

```
EXEC SQL DECLARE CUR_1 CURSOR FOR
    SELECT  EMPNO, DEPTNO
    FROM    EMP
    WHERE   EMPNO = :emp_number;

EXEC SQL OPEN CUR_1;
 
while( 1 )
{
    EXEC SQL FETCH CUR_1 INTO :empno, :deptno :deptno_ind;
    if( sqlca.sqlcode == SQL_NO_DATA )
    {
        break;
    }
 
    if( deptno_ind == -1 )
    {
        printf( "empno : %d, deptno : (null)\n", empno );
    }
    else
    {
        printf( "empno : %d, deptno : %d\n", empno, deptno );
    }
}
 
EXEC SQL CLOSE CUR_1;
```

FETCH 후에 deptno_ind가 -1이면 deptno가 NULL인 것으로 판단한다.

<a id="726f359baa6c9c07"></a>
#### Basic SQL statement

Embedded SQL에서는 GOLDILOCKS에서 제공하는 모든 SQL 문을 사용할 수 있는데 SQL 문에 대한 자세한 내용은 [SQL Manual](../part-03-sql-manual/README.md#2cf19c96b41e0483)을 참조한다. Embedded SQL에서 SQL 문을 사용할 때는 EXEC SQL 키워드 뒤에 SQL 문을 기술하는데 본 장에서는 Data Definition Language (DDL)이나 Data Manipulation Language (DML)에 대한 내용을 기술하고 query와 같이 반복적으로 data를 가져오는 구문에 대해서는 다음 장에서 설명한다.

SQL 문을 실행한 이후에는 SQLCA를 검사하여 실행한 SQL 문의 성공 여부를 판단할 수 있으며, 자세한 내용은 [Handling Run-time Error](#4a21ae513791d8ed) 부분을 참조한다.

<a id="7dc4736b7e341962"></a>
##### DDL Statement

DDL statement는 GOLDILOCKS의 table, view, index 등과 같은 object들을 생성하거나, 제거, 변경 등의 작업을 수행하는 SQL 문이다. Embedded SQL 응용 프로그램에서 DDL문을 수행할 때는 EXEC SQL keyword 뒤에 해당 SQL 문을 기술한다.

```
EXEC SQL DROP TABLE IF EXISTS EMP;

EXEC SQL
    CREATE TABLE EMP (
        EMPNO NUMBER(4) CONSTRAINT PK_EMP PRIMARY KEY,
        ENAME VARCHAR2(10),
        JOB VARCHAR2(9),
        SAL NUMBER(7,2),
        DEPTNO NUMBER(2) );
```

DDL 문에서는 host variable을 사용할 수 없다. 따라서 다음은 잘못된 사용 방법이다.

```
strcpy( table_name, "T1" );
EXEC SQL CREATE TABLE :table_name ( C1 INTEGER );
```

만약, 응용 프로그램을 작성하는 도중에 DDL 구문을 확정하지 못하여 위와 같이 가변적으로 DDL 구문을 사용하고자 할 때는 다음과 같이 dynamic SQL 문을 사용할 수 있다.

```
strcpy( table_name, "T1" );
sprintf( sql_stmt, "CREATE TABLE %s ( C1 INTEGER )", table_name );
EXEC SQL EXECUTE IMMEDIATE :sql_stmt;
```

이에 대한 자세한 내용은 [Embedded Dynamic SQL](#bab9699b12f1bf0c)을 참조한다.

<a id="57707ee8e727571e"></a>
##### Select Into Statement

GOLDILOCKS에서 data를 가져 오기 위해서 query를 사용한다. 일반적인 경우에는 해당 결과의 개수를 알지 못하는 경우가 많기 때문에, query를 사용하기 위해서는 cursor라는 객체를 선언하여 open, fetch, close라는 복잡한 과정을 거치게 된다. 이러한 과정의 실행 방식은 다음 [Cursors](#46a3dade404496a5) 부분에서 기술할 것이다.

그런데 특별한 경우에는 이미 결과의 개수를 알고 있을 수도 있다. 예를 들어 primary key를 알고 있고 해당 primary key와 같은 key를 가진 record를 검색할 때는 결과가 없거나 최대 한 개의 결과만 가진다는 것을 예측할 수 있다. 이렇게 결과가 한 개 이하일 때 사용할 수 있는 구문이 select into 구문이며 다음과 같이 간단하게 실행할 수 있다.

```
EXEC SQL
    SELECT ename, job, sal 
    INTO :emp_name, :job_title, :salary 
    FROM emp 
    WHERE empno = :emp_number;
```

> Host array를 사용하면 select into 구문을 사용하여 여러 개의 결과를 가져올 수 있다. Host array 사용법은 [Host Arrays](#75c6479a40ead006)를 참조한다.

<a id="2db74aa34fccd0d5"></a>
##### Insert Statement

Insert 구문은 table에 row를 삽입하는 용도로 사용된다. Host variable을 사용하여 column값을 결정할 수 있고 indicator를 사용하여 NULL 값을 삽입할 수도 있다.

다음은 insert 구문의 예이다.

```
EXEC SQL
    INSERT INTO EMP ( empno, ename, job, sal )
    VALUES ( :emp_number, :emp_name, :job_name :job_ind, :saraly );
EXEC SQL
    INSERT INTO DEPT ( deptno, dname, loc )
    VALUES ( 1, :dept_name, NULL );
```

> Host structure를 사용하면 host variable을 개별적으로 사용하지 않고 structure 단위로 삽입할 수 있다.

```
EXEC SQL BEGIN DECLARE SECTION;
typedef struct rsRecord
{
    int          mEmpNo;
    varchar      mEName[20 + 1];
    char         mJob[20 + 1];
    long         mSalary;
} rsRecord;
 
rsRecord  sInsertRec;
EXEC SQL END DECLARE SECTION;
 
sInsertRec.mEmpNo = 3000;
strcpy( sInsertRec.mEName.arr, "John" );
sInsertRec.mEName.len = strlen( sInsertRec.mEName.arr );
strcpy( sInsertRec.mJob , "RND" );
sInsertRec.mSalary = 3500;
 
EXEC SQL INSERT INTO EMP ( empno, ename, job, sal ) VALUES ( :sInsertRec );
```

> Host array를 사용하면 한 번에 여러 개의 row를 삽입할 수 있다. 자세한 내용은 [Host Arrays](#75c6479a40ead006)를 참조한다.

<a id="a6b7125181065dbf"></a>
##### Update Statement

Update 구문은 table에서 특정 row의 column 값들을 갱신하는 용도로 사용된다. Host variable을 사용하여 column 값을 결정할 수 있고, indicator를 사용하여 NULL 값을 삽입할 수도 있다.

다음은 update 구문의 예이다.

```
EXEC SQL
    UPDATE emp 
    SET sal = :salary, deptno = :dept_number :deptno_ind
    WHERE empno = :emp_number;
```

> Host array를 사용하면 한 번에 여러 개의 row를 갱신할 수 있다. 자세한 내용은 [Host Arrays](#75c6479a40ead006)를 참조한다.

<a id="acadb8fc4a2bdf0c"></a>
##### Delete Statement

Delete 구문은 특정 row를 table에서 삭제한다.

다음은 delete 구문의 예이다.

```
EXEC SQL
    DELETE FROM emp 
    WHERE empno = :emp_number;
```

> Host array를 사용하면 한 번에 여러 개의 row를 삭제할 수 있다. 자세한 내용은 [Host Arrays](#75c6479a40ead006)를 참조한다.

<a id="f0e9d79c9e308571"></a>
##### PSM Statement

PSM 구문은 서버 내부에 procedure나 function을 만들어서 사용한다.  
PSM에 대한 자세한 내용은 [PSM Manual](../part-04-psm-manual/README.md#93323f028164b467)을 참조한다.

기본적으로 EXEC SQL EXECUTE로 시작해서 END-EXEC;로 끝난다. 단, procecure나 function을 생성할 때는 EXEC SQL EXECUTE 대신 EXEC SQL를 사용한다.

다음은 procedure를 생성하고 호출하는 구문의 예이다.

```
EXEC SQL
    CREATE OR REPLACE PROCEDURE PROC1( A1 INTEGER, A2 INTEGER )
      IS
        V1 INTEGER;
      BEGIN

        SELECT COUNT(*)
          INTO V1
          FROM T1
          WHERE T1.I1 >= A1 AND T1.I1 <= A2;

        DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
      END;
END-EXEC;

EXEC SQL CALL PROC1( 2, 4 );
```

다음은 function을 생성하고 호출하는 구문의 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
    int         sV1 = 0;
EXEC SQL END DECLARE SECTION;

EXEC SQL
    CREATE OR REPLACE FUNCTION FUNC1( A1 INTEGER, A2 INTEGER )
      RETURN INTEGER
      IS
        V1 INTEGER;
      BEGIN

        SELECT COUNT(*)
          INTO V1
          FROM T1
          WHERE T1.I1 >= A1 AND T1.I1 <= A2;

        RETURN V1;
      END;
END-EXEC;

EXEC SQL CALL FUNC1( 2, 4 ) INTO :sV1;
```

다음은 anonymous block 구문의 예이다.

```
EXEC SQL EXECUTE
    DECLARE
      V1 INTEGER := 0;
      FUNCTION FUNC1( A1 INTEGER )
        RETURN INTEGER
        IS
        BEGIN
          RETURN A1 * 10;
        END;
    BEGIN
      V1 := FUNC1( 10 );
      DBMS_OUTPUT.PUT_LINE( 'V1 = ' || V1 );
    END;
END-EXEC;
```

```
EXEC SQL EXECUTE
    DECLARE
      PROCEDURE PROC1( A1 INTEGER )
      IS
      BEGIN
        DBMS_OUTPUT.PUT_LINE( 'A1 = ' || A1 );
      END;
    BEGIN
      PROC1( 100 );
    END;
END-EXEC;
```

<a id="46a3dade404496a5"></a>
#### Cursor

응용 프로그램은 원하는 data를 GOLDILOCKS로 얻어오기 위해 질의를 수행한다. 일반적으로 질의를 수행할 때는 그 질의 결과의 양이 어느정도인지 정확히 알 수 없는 경우가 많기 때문에 cursor를 사용한다. Cursor는 질의 결과 집합에서 현재 row의 위치를 명시하는 식별자이며 다음과 같은 연산을 통해 cursor를 조작할 수 있다.

<a id="1fb35aa838c366ea"></a>
##### Declare Cursor

Cursor를 선언한다. Cursor를 선언할 때는 cursor 이름과 그에 부합하는 질의를 기술해야 한다. 여기서 선언된 cursor 이름은 이후에 다른 cursor 조작 명령에 사용된다.

다음은 cursor 선언문의 예이다.

```
EXEC SQL
    DECLARE RECORD_CUR1 CURSOR FOR
    SELECT   empno, ename, dept
    FROM     SEMP
    ORDER BY empno;
```

Cursor 이름은 precompiler에 의해 인식되고 사용되는 식별자로써 실제 C 프로그램의 변수와는 무관하다. Cursor의 Scope는 파일이다. 그러므로 동일한 이름의 Cursor를 다른 파일에 정의하여도 별개의 Cursor로 간주한다. 즉, cursor를 declare/ open/ fetch/ close 하는 구문은 모두 하나의 소스 파일 내에 위치해야 한다.

<a id="e844bbfa8c1bd6ff"></a>
##### Open Cursor

Cursor를 open한다.

```
EXEC SQL OPEN <cursor_name>;
Example)
EXEC SQL OPEN EMP_CURSOR;
```

커서를 open하면 선언된 커서의 질의를 수행한 결과 집합을 가져올 준비가 된다. 여기서는 실제로 결과를 가져오는 것은 아니기 때문에 실제 결과를 얻어오려면 [Fetch cursor](#85738290c933a1fc)를 수행해야 한다.  
질의를 수행할 때 사용한 host variable은 현재 커서가 close 될 때까지 결과 집합에 영향을 미치지 않는다.

```
EXEC SQL DECLARE EMP_CURSOR CURSOR FOR
        SELECT    empno, ename, dept
        FROM      EMP
        WHERE     empno < :sNo
        ORDER BY  empno;
 
    sNo = 100;
    EXEC SQL OPEN EMP_CURSOR;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    while( 1 )
    {
        sNo = 10;
        EXEC SQL FETCH EMP_CURSOR INTO :emp_number, :emp_name, :dept_name;

        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            goto fail_exit;
        }
        ...
    }
```

위의 예에서 커서가 sNo = 100으로 open 되었으면 중간에 sNo를 다른 값으로 바꾸더라도 이 커서가 close 될 때까지는 결과 집합이 변하지 않는다.

<a id="85738290c933a1fc"></a>
##### Fetch Cursor

커서의 위치에 있는 row를 가져온다.

```
EXEC SQL FETCH <cursor_name> INTO <host_variable_list>;
Example)
EXEC SQL FETCH EMP_CURSOR INTO :emp_number, :emp_name, :dept_name;
```

FETCH 연산을 수행하려면 해당 커서가 미리 선언되어야 하고 OPEN 되어 있어야 한다. 최초로 FETCH를 수행하면 커서가 결과 집합의 첫 번째 row로 이동하여 current row로 지정한 다음 current row를 INTO 절의 host variable에 넣어 반환한다. 이후에 FETCH가 반복적으로 수행되면 커서가 다음 row로 current row를 갱신한 후 current row를 INTO 절의 host variable로 반환하는 작업을 반복한다. FETCH를 수행했는데 더 이상 결과가 존재하지 않을 경우에는 sqlca.sqlcode에 SQL_NO_DATA 코드를 반환하므로 응용 프로그램에서는 이 코드값을 보고 검색이 종료되었는지 여부를 판단할 수 있다.

<a id="10c9846c3eeabfd5"></a>
##### Close Cursor

커서를 close 한다.

```
EXEC SQL CLOSE <cursor_name>;
Example)
EXEC SQL CLOSE EMP_CURSOR;
```

커서를 close 하기 위해서는 해당 커서가 미리 open 되어 있어야 하고 커서를 close 한 뒤에는 더 이상 이 커서에서 FETCH를 수행할 수 없다. 만약 커서를 close 한 이후에 다시 사용하기 위해서 open할 경우, 이는 새로 open 된 커서이므로 이전에 close 했던 커서와 결과 집합이 달라질 수 있다.

<a id="99a40d570de678bd"></a>
#### Cursor 재사용

이미 선언한 cursor 이름을 반복해서 재사용할 수 있다. 본 절에서는 동일한 cursor 이름을 재사용하기 위한 선후 관계에 대해 설명한다.

<a id="3935d45985e1e61c"></a>
##### Cursor 구문 선후 관계

- DECLARE CURSOR  
  Cursor CLOSE, COMMIT, ROLLBACK 구문을 수행한 후에 수행할 수 있다.
- OPEN   
  Cursor를 끝까지 FETCH 하였거나 CLOSE 구문을 수행한 후에 수행할 수 있다.
- FETCH  
  Cursor OPEN 구문을 수행한 후에 수행할 수 있다.
- CLOSE  
  Cursor OPEN 구문 또는 FETCH 구문을 수행한 후에 수행할 수 있다.

<a id="5ab281e161eaf9cb"></a>
##### Cursor 구문과 Host Variable

Cursor 구문은 파일 내에서 임의의 위치에 배치할 수 있다. 그러나 DECLARE 구문에 사용되는 input host variable이 전역 변수인지 지역 변수인지에 따라 cursor 구문 사용법도 달라진다.

- DECLARE 구문에 사용되는 input host variable이 지역 변수라면 OPEN 구문은 반드시 DECLARE 구문과 같은 함수 내에 위치해야 한다.
- DECLARE 구문에 사용되는 input host variable이 전역 변수라면 OPEN 구문은 DECLARE 구문과 다른 함수에 위치할 수 있다.
- DECLARE 구문에 input host variable이 없다면 OPEN 구문은 DECLARE 구문과 다른 함수에 위치할 수 있다.

이렇게 되는 이유는 cursor declare 구문에 사용되는 host variable의 포인터를 내부적으로 저장하고 cursor open 구문에서 포인터를 사용하는데 두 구문이 다른 함수에 위치하고 사용되는 host variable이 지역 변수일 경우 open 구문에서는 유효하지 않은 포인터를 참조하기 때문이다. 따라서 declare 구문과 open 구문은 같은 함수 내에 위치시킬 것을 권장한다.

<a id="d191bcd32ea32ef9"></a>
#### Cursor 사용 예

다음은 DDL, DML, cursor를 사용하는 예이다.

```
/*
 * overview.gc
 *
 * Connect / Disconnect
 * DDL(Create/Drop table)
 * Basic DML(Insert, Delete, Update)
 * Standing Cursor
 */
EXEC SQL INCLUDE SQLCA;
 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
 
#define  SUCCESS  0
#define  FAILURE  -1
#define  PRINT_SQL_ERROR(aMsg)                                      \
    {                                                               \
        printf("\n");                                               \
        printf(aMsg);                                               \
        printf("\nSQLCODE : %d\nSQLSTATE : %s\nERROR MSG : %s\n",   \
               sqlca.sqlcode,                                       \
               SQLSTATE,                                            \
               sqlca.sqlerrm.sqlerrmc );                            \
    }
 
EXEC SQL BEGIN DECLARE SECTION;
typedef struct rsEmpRecord
{
    int      mEmpNo;
    char     mEName[20];
    char     mDept[10];
} rsEmpRecord;
 
rsEmpRecord gRecord[10] = {
    { 1, "Park", "RND" },
    { 2, "Kim", "CEO" },
    { 3, "Choi", "SALES" },
    { 4, "Lee", "CTO" },
    { 5, "Lyu", "RND" },
    { 6, "Ohn", "SUPPORT" },
    { 7, "Cheon", "RND" },
    { 8, "Sohn", "SALES" },
    { 9, "Smith", "WAIT" },
    { 10, "mycomman", "WAIT" }
};
EXEC SQL END DECLARE SECTION;
 
int CreateEmpTable();
int DropEmpTable();
int Connect(char *aHostInfo, char *aUserID, char *sPassword);
int Disconnect();
int PrintRecord();
 
int main(int argc, char **argv)
{
    EXEC SQL BEGIN DECLARE SECTION;
    int          sEmpNo;
    char         sDept[10 + 1];
    EXEC SQL END DECLARE SECTION;
    int  sState = 0;
 
    printf("Connect GOLDILOCKS ...\n");

    if(Connect("DSN=GOLDILOCKS", "test", "test") != SUCCESS)
    {
        goto fail_exit;
    }
    sState = 1;
 
    printf("Create SEMP table ...\n");
    if(CreateEmpTable() != SUCCESS)
    {
        goto fail_exit;
    }
    sState = 2;
 
    printf("Insert record ...\n");
    EXEC SQL
        INSERT INTO SEMP(empno, ename, dept)
        VALUES(:gRecord);
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }

    printf("====== ==================== ==========\n");
    printf("%d Record Inserted\n", sqlca.sqlerrd[2]);
    printf("====== ==================== ==========\n");
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf("Current record\n");
    PrintRecord();
 
    sEmpNo = 9;
    printf("Delete record WHERE empno == %d\n", sEmpNo);
    EXEC SQL
        DELETE FROM SEMP
        WHERE  empno = :sEmpNo;

    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf("After Delete record\n");
    PrintRecord();
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    strcpy( sDept, "RND" );
    printf("Update record WHERE dept == 'WAIT'\n");
    EXEC SQL
        UPDATE SEMP
        SET    dept = :sDept
        WHERE  dept = 'WAIT';
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf("After Update record\n");
    PrintRecord();
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    sState = 1;
    printf("Drop SEMP table ...\n");
    if(DropEmpTable() != SUCCESS)
    {
        goto fail_exit;
    }
 
    sState = 0;
    printf("Disconnect GOLDILOCKS ...\n");
    if(Disconnect() != SUCCESS)
    {
        goto fail_exit;
    }
 
    printf("SUCCESS\n");
    printf("############################\n");
 
    return 0;
 
  fail_exit:
 
    printf("FAILURE\n");
    printf("############################\n\n");
 
    EXEC SQL ROLLBACK WORK;
    switch(sState)
    {
        case 2:
            printf("Drop SEMP table ...\n");
            (void)DropEmpTable();
        case 1:
            printf("Disconnect GOLDILOCKS ...\n");
            (void)Disconnect();
            break;
        default:
            break;
    }
 
    return 0;
}
```

- Create table

```
int CreateEmpTable()
{
    EXEC SQL DROP TABLE IF EXISTS SEMP;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL CREATE TABLE SEMP ( empno        INTEGER,
                                 ename        VARCHAR(20),
                                 dept         VARCHAR(10),
                                 PRIMARY KEY (empno) );
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
 
    EXEC SQL ROLLBACK WORK;
 
    return FAILURE;
}
```

- Drop table

```
int DropEmpTable()
{
    EXEC SQL DROP TABLE SEMP;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
 
    EXEC SQL ROLLBACK WORK;
 
    return FAILURE;
}
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword)
{
    EXEC SQL BEGIN DECLARE SECTION;
    VARCHAR  sUid[80];
    VARCHAR  sPwd[20];
    VARCHAR  sConnStr[1024];
    EXEC SQL END DECLARE SECTION;
```

- Log on GOLDILOCKS

```
strcpy((char *)sUid.arr, aUserID);
    sUid.len = (short)strlen((char *)sUid.arr);
    strcpy((char *)sPwd.arr, sPassword);
    sPwd.len = (short)strlen((char *)sPwd.arr);
    strcpy((char *)sConnStr.arr, aHostInfo);
    sConnStr.len = (short)strlen((char *)sConnStr.arr);
```

- DB 연결

```
EXEC SQL CONNECT :sUid IDENTIFIED BY :sPwd USING :sConnStr;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] Connection Failure!");
 
    return FAILURE;
}
 
int Disconnect()
{
    EXEC SQL DISCONNECT;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] [ERROR] Disconnect Failure!");
 
    return FAILURE;
}
 
int PrintRecord()
{
    EXEC SQL BEGIN DECLARE SECTION;
    rsEmpRecord sResultRecord;
    EXEC SQL END DECLARE SECTION;
    int   sRecordCount = 0;
 
    EXEC SQL
        DECLARE RECORD_CUR1 CURSOR FOR
        SELECT   empno, ename, dept
        FROM     SEMP
        ORDER BY empno;
 
    EXEC SQL OPEN RECORD_CUR1;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    printf(" EMPNO    ENAME               DEPT\n");
    printf("====== ==================== ==========\n");
    while( 1 )
    {
        EXEC SQL FETCH RECORD_CUR1 INTO :sResultRecord;
        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            goto fail_exit;
        }
 
        sRecordCount ++;
 
        printf("%6d %20s %10s\n",
               sResultRecord.mEmpNo,
               sResultRecord.mEName,
               sResultRecord.mDept);
    }
 
    printf("====== ==================== ==========\n");
    printf("Record Count = %d\n", sRecordCount);
    printf("====== ==================== ==========\n");
 
    EXEC SQL CLOSE RECORD_CUR1;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
 
    return FAILURE;
}
```

<a id="89dbb469a078b345"></a>
#### Cursor Property

앞 장에서는 가장 기본적인 커서에 대해서만 설명하였다. 그러나 커서는 다양한 속성들을 가질 수 있으며 커서가 갖는 속성에 따라 다양한 기능을 수행할 수 있다. GOLDILOCKS의 embedded SQL은 ISO/ IEC-9075-2 SQL foundation에서 제안하는 cursor 속성과 ODBC에서 제안하는 cursor 속성을 제공한다.  
커서 정의 구문과 속성에 대한 자세한 내용은 [DECLARE cursor_name](../part-03-sql-manual/18-sql-references.md#45b9d98474d5f09d)을 참조한다.

<a id="0efbc2ca41b3ef41"></a>
##### Scrollable Cursor

SCROLL은 ISO type의 cursor 속성으로써 커서의 scroll 가능 여부를 결정한다. Scroll 가능한 커서는 FETCH 구문에서 위치 옵션을 받을 수 있고 이 옵션에 따른 위치의 row를 FETCH한다. Scroll 불가능한 커서는 결과 집합에 대해 순차적으로만 FETCH 할 수 있다.

Scroll cursor를 선언할 때는 SCROLL 옵션을 사용하는데 다음은 그 예이다.

```
EXEC SQL DECLARE cur_scroll SCROLL CURSOR FOR SELECT c1, c2 FROM t1;
```

NO SCROLL 옵션을 사용할 때는 scroll 불가능한 커서가 선언되고 scroll 옵션을 주지 않았을 경우에는 기본적으로 NO SCROLL이 된다.   
Scrollable cursor의 경우에는 FETCH 할 때 위치 정보를 줄 수 있다. 이 위치 정보를 fetch orientation이라고 하며 다음 표와 같다.

**Fetch orientation**

<a id="beced670a7a30480"></a>
<table><thead><tr><th align="center">Fetch orientation</th><th align="center">설명</th></tr></thead><tbody><tr><td align="left" valign="middle">NEXT</td><td>현재 위치의 다음 row를 fetch 한다.</td></tr><tr><td align="left" valign="middle">PRIOR</td><td>현재 위치의 이전 row를 fetch 한다.</td></tr><tr><td align="left" valign="middle">FIRST</td><td>결과 집합의 첫 번째 row를 fetch 한다.</td></tr><tr><td align="left" valign="middle">LAST</td><td>결과 집합의 마지막 row를 fetch 한다.</td></tr><tr><td align="left" valign="middle">CURRENT</td><td>현재 위치의 row를 fetch 한다.</td></tr><tr><td align="left" valign="middle">ABSOLUTE &lt;position&gt;</td><td align="left" valign="middle"><ul><li>결과 집합에서 position의 위치에 해당하는 row를 fetch 한다.</li><li>Position 값이 음수일 경우, AFTER THE LAST ROW로부터 이전 위치에 해당하는 row를 fetch한다.</li></ul></td></tr><tr><td align="left" valign="middle">RELATIVE &lt;position&gt;</td><td align="left" valign="middle">현재 위치에서 position 만큼 떨어진 위치에 해당하는 row를 fetch 한다.</td></tr></tbody></table>

Fetch orientation이 ABSOLUTE, RELATIVE인 경우에는 &lt;position&gt; 값을 추가적으로 요구하는데, 이 &lt;position&gt; 값으로 정수형 상수나 정수형 type의 host variable이 사용될 수 있다. 다음은 fetch orientation을 사용하는 예이다.

```
EXEC SQL FETCH NEXT;
EXEC SQL FETCH PRIOR;
EXEC SQL FETCH FIRST;
EXEC SQL FETCH LAST;
EXEC SQL FETCH CURRENT;
EXEC SQL FETCH ABSOLUTE 100;
EXEC SQL FETCH RELATIVE :position;
```

<a id="ead31832e2c2a372"></a>
##### Sensitive Cursor

Sensitivity는 ISO type의 cursor 속성으로써 커서를 운용하는 도중에 결과 집합이 변경될 경우 그 변경 내용을 볼 수 있는지 여부를 결정한다. Sensitivity에는 다음과 같은 세 가지 옵션이 있다.

**Sensitivity**

<a id="e4c00746c2e4bf99"></a>
| Option | 설명 |
| --- | --- |
| SENSITIVE | 다른 트랜잭션에서 변경하거나 삭제한 내용을 볼 수 있다. |
| INSENSITIVE | 커서를 open한 이후에 변경하거나 삭제한 내용을 볼 수 없다. |
| ASENSITIVE | &lt;query&gt;의 내용에 따라, SENSITIVE/ INSENSITIVE가 결정된다. |

Sensitive option을 명시하지 않았을 경우 기본값은 INSENSITIVE이며 sensitive 옵션을 사용한 커서는 다음과 같은 방법으로 선언한다.

```
EXEC SQL DECLARE <cur_name> SENSITIVE CURSOR FOR SELECT c1, c2 FROM t1;
EXEC SQL DECLARE <cur_name> INSENSITIVE CURSOR FOR SELECT c1, c2 FROM t1;
EXEC SQL DECLARE <cur_name> ASENSITIVE CURSOR FOR SELECT c1, c2 FROM t1;
```

<a id="150e180ed4d33b2c"></a>
##### Holdable Cursor

Holdability는 ISO type의 cursor 속성으로써 현재 커서를 open한 트랜잭션이 commit된 이후에도 커서가 계속 유지되고 있는지 여부를 결정한다. Holdability에는 다음과 같은 두 가지 옵션이 있다.

**Holdability**

<a id="c9a5c4b32a66d1b8"></a>
<table><thead><tr><th align="center">Option</th><th align="center">설명</th></tr></thead><tbody><tr><td align="left" valign="middle">WITH HOLD</td><td align="left" valign="middle"><ul><li>트랜잭션의 COMMIT 이후에도 커서가 유지된다.</li><li>FOR UPDATE 구문과 함께 사용할 수 없다</li><li>INSERT INTO ... RETURNING 구문과 함께 사용할 수 없다.</li><li>UPDATE ... RETURNING 구문과 함께 사용할 수 없다.</li><li>DELETE FROM ... RETURNING 구문과 함께 사용할 수 없다.</li></ul></td></tr><tr><td align="left" valign="middle">WITHOUT HOLD</td><td align="left" valign="middle">트랜잭션을 COMMIT/ ROLLBACK 하면 커서를 닫는다.</td></tr><tr><td align="left" valign="middle">Rollback 과 Cursor</td><td align="left" valign="middle"><ul><li>트랜잭션을 rollback하면 트랜잭션에 포함된 커서를 닫는다.</li><li>Savepoint까지 rollback하면 savepoint 이후에 생성된 커서를 닫는다.</li></ul></td></tr></tbody></table>

Holdable option을 명시하지 않았을 경우 기본값은 &lt;cursor updatability&gt;에 따라 결정된다.

- FOR READ ONLY 또는 &lt;cursor updatability&gt;가 명시되지 않은 경우, WITH HOLD 이다.
- FOR UPDATE 구문과 함께 사용될 경우, WITHOUT HOLD 이다.

Holdable option을 사용한 커서는 다음과 같은 방법으로 선언한다.

```
EXEC SQL DECLARE <cur_name> CURSOR WITH HOLD FOR SELECT c1, c2 FROM t1;
EXEC SQL DECLARE <cur_name> CURSOR WITHOUT HOLD FOR SELECT c1, c2 FROM t1 FOR UPDATE;
```

<a id="ec7d3cd9a5acb068"></a>
##### Static Cursor

Static 커서는 ODBC type의 cursor 속성으로써 ISO type의 INSENSITIVE SCROLL 커서와 동일하다.

```
EXEC SQL DECLARE cur_static STATIC CURSOR FOR SELECT c1, c2 FROM t1;
```

Static cursor의 fetch 방법은 [Scrollable Cursor](#0efbc2ca41b3ef41)를 참조한다

<a id="9d3d8cb93193c2ed"></a>
##### Keyset Driven Cursor

Keyset driven 커서는 ODBC type의 cursor 속성으로써 ISO type의 ASENSITIVE SCROLL 커서와 동일하다.

```
EXEC SQL DECLARE cur_static KEYSET CURSOR FOR SELECT c1, c2 FROM t1;
```

Keyset driven 커서 역시 scroll 기능을 가지고 있으므로 fetch 방법은 [Scrollable Cursor](#0efbc2ca41b3ef41)를 참조한다.

<a id="444fd5d949e0eb7b"></a>
#### Positioned DML

CURRENT OF &lt;cursor_name&gt; 구문을 사용하여 마지막으로 fetch된 row에 대해 delete나 update 구문을 사용한 연산을 수행할 수 있는데, 이를 positioned DML이라고 한다. Positioned DML을 수행하려면 cursor가 open되어 있어야 하고, fetch가 최소 한 번 이상 수행되어 커서가 row의 위치를 가리키고 있어야만 한다.

다음은 positioned DML을 수행하는 예이다.

```
EXEC SQL DECLARE emp_cursor CURSOR FOR 
     SELECT ename, sal FROM emp WHERE job = 'SALES'
     FOR UPDATE; 
... 

EXEC SQL OPEN emp_cursor; 
EXEC SQL WHENEVER NOT FOUND GOTO ... 

while( 1 )
{
    EXEC SQL FETCH emp_cursor INTO :emp_name, :salary; 
    ... 
    EXEC SQL UPDATE emp SET sal = :new_salary 
         WHERE CURRENT OF emp_cursor; 
}
```

<a id="25c8eaca8bed2851"></a>
### Options

본 장에서는 embedded SQL 소스 코드를 precompile 할 때 적용할 수 있는 option에 대해 설명한다.

<a id="fabc1e92e7bd94de"></a>
#### Precompiled Header File

Embedded SQL 프로그램을 작성할 때, 여러 개의 소스 코드에서 공통적으로 참조하는 내용들은 별도의 header file로 작성하여 소스 코드가 해당 header File을 포함하도록 하는 것이 효율적이다. 이미 C 언어에서는 #include 문장을 사용하여 이런 기능을 지원하고 있다. 그런데 C 언어의 #include를 통해 header file을 포함할 때는 대상 파일을 precompile을 하지 않고 C 언어 컴파일러에 그 해석을 맡기기 때문에 그 파일 내의 declare section 등은 precompiler에 의해 변환되지 않는다.

이렇게 header file을 만들 때, 이 header file을 precompiler로 변환하여 소스 코드에 삽입하려면 EXEC SQL INCLUDE 구문을 사용해야 하며, 그 구문은 다음과 같다.

```
EXEC SQL INCLUDE <filename>;
```

이 구문은 주어진 파일을 precompile하여 소스 코드에 삽입해 준다.

<a id="38ded575a22e124e"></a>
#### Header File 경로 지정

기본적으로 header file을 찾을 때는 현재 소스 코드가 위치한 디렉토리를 우선 검색한다. 그러나 대체로 header file들은 별도로 모아 놓는 경우가 많고 모아놓지 않더라도 여러 가지 이유로 인해 다른 경로에 존재하는 경우가 많다.

이 때, header file을 검색할 디렉토리를 별도 옵션으로 줄 수 있으며, 그 구문은 다음과 같은 형식이다.

```
EXEC SQL OPTION( INCLUDE = <directory path> );
```

이 옵션 여러 개를 나열하여 부여할 수 있고 EXEC SQL INCLUDE를 통해 header file을 찾을 때, 이 옵션이 주어진 순서대로 디렉토리를 검색한다.

> 이 옵션은 precompiler의 command-line option을 통해서도 부여할 수 있다. 자세한 내용은 [Precompiler Options](#f1b7f5b92f394d04)의 [--include-path, -I](#d9b32b976ddd0197)를 참조한다.

<a id="75c6479a40ead006"></a>
### Host Array

지금까지는 host variable로 단일 값만을 갖는 scalar 변수에 대해 설명하였다. 본 장에서는 array를 host variable로 사용하는 방법에 대해 설명한다.

Host array를 사용하면 프로그램 소스 코드가 간결해지고 performance가 향상되지만 사용에 제한적인 면이 있으므로 주의해서 사용해야 한다.

<a id="332a3523d3743021"></a>
#### Host Array 선언

Host array 선언은 scalar variable을 선언하는 경우와 다르지 않다. 변수 선언 자체를 배열로 선언하기만 하면 된다. 다음은 host array를 배열 크기 10으로 선언하는 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
    int    empno[10];
    char   ename[10][20];
    double salary[10];
EXEC SQL END DECLARE SECTION;
```

Host array 선언에는 다음과 같은 제약 사항이 있다.

- 2차원 이상의 배열은 허용되지 않는다.
- 예외적으로 문자열 계열 (char, varchar)과 binary 계열 (binary, varbinary)은 array size를 나타내는 배열 첨자와 데이터 size를 나타내는 배열 첨자로 구성되어 2차원 배열이 쓰일 수 있다.
- Pointer의 배열은 허용되지 않는다.

<a id="fadc4e3d7a11ddab"></a>
#### Host Array 사용

<a id="869b38a1f3aa814b"></a>
##### Host Array 접근

Host array를 SQL 구문에서 사용하는 방법은 scalar host variable을 사용하는 것과 동일하다.

다음은 간단한 host array의 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
int    emp_number[20]; 
char   emp_name[20][10]; 
int    dept_number[20]; 
EXEC SQL END DECLARE SECTION;
```

- emp_number, emp_name, dept_number 값을 설정

```
...
```

- emp_number, emp_name, dept_number 값을 INSERT

```
EXEC SQL INSERT INTO emp (empno, ename, deptno) 
    VALUES (:emp_number, :emp_name, :dept_number);
```

위의 예는 다음 코드와 동일한 작업을 수행한다.

```
EXEC SQL BEGIN DECLARE SECTION;
int    emp_number[20]; 
char   emp_name[20][10]; 
int    dept_number[20]; 
EXEC SQL END DECLARE SECTION;
```

- emp_number, emp_name, dept_number 값을 설정

```
...
```

- emp_number, emp_name, dept_number를 INSERT

```
for( i = 0; i < 20; i ++ )
{
    EXEC SQL INSERT INTO emp (empno, ename, deptno) 
        VALUES (:emp_number[i], :emp_name[i], :dept_number[i]);
}
```

여러 개의 host variable array가 사용되었을 때는, 각 host array 중에 array size가 가장 작은 것에 대해서만 연산이 이루어진다. 위의 예에서는 모든 host variable의 크기가 20 이므로 20 개의 row가 삽입되지만 다음과 같이 dept_number의 배열 크기를 10으로 지정한 경우, 결과적으로 삽입되는 row의 수는 10 개가 된다.

```
EXEC SQL BEGIN DECLARE SECTION;
int    emp_number[20]; 
char   emp_name[20][10]; 
int    dept_number[10]; 
EXEC SQL END DECLARE SECTION;
```

- emp_number, emp_name, dept_number 값을 설정

```
...
```

- emp_number, emp_name, dept_number를 INSERT

```
EXEC SQL INSERT INTO emp (empno, ename, deptno) 
    VALUES (:emp_number, :emp_name, :dept_number);
```

<a id="61d6342fe4ec29fe"></a>
##### Host Indicator Array 사용

Host 변수가 배열일 경우, 여기에 결합되는 indicator 변수도 배열이어야 하며 indicator 변수의 배열 크기와 host 변수의 배열 크기는 같아야 한다. 위의 예에 indicator 변수가 추가될 경우, 다음과 같은 형태가 될 것이다.

```
EXEC SQL BEGIN DECLARE SECTION;
int    emp_number[20];
int    emp_number_ind[20]; 
char   emp_name[20][10];
int    emp_name_ind[20];
int    dept_number[20];
int      dept_number_ind[20];
EXEC SQL END DECLARE SECTION;
```

- emp_number, emp_name, dept_number 값을 설정
- emp_number_ind, emp_name_ind, dept_number_ind의 각 indicator 값을 설정

```
...
```

- emp_number, emp_name, dept_number를 INSERT

```
EXEC SQL INSERT INTO emp (empno, ename, deptno) 
    VALUES (:emp_number :emp_number_ind,
            :emp_name :emp_name_ind,
            :dept_number :dept_number_ind);
```

<a id="c9720a06197610f4"></a>
##### 제약 사항

- Host 변수가 여러 개 사용될 때는 scalar 변수와 array 변수를 혼합하여 사용할 수 없다.
- Select 구문의 WHERE 절에는 host array를 사용할 수 없다.
- Update, delete 구문의 CURRENT OF 절에는 host array를 사용할 수 없다.

<a id="21d0bf5fe5e95932"></a>
#### INTO 절에서의 Array

GOLDILOCKS에서 row를 가져 오기 위해서는 SELECT INTO 구문이나 cursor를 사용할 수 있다. Embedded SQL에서는 이 두 가지 방법에 공통적으로 INTO 절을 사용하는데 이 INTO 절에 host array를 사용하면 여러 row를 가지고 올 수 있다.

<a id="5ee97e199e4d944e"></a>
##### SELECT INTO에서의 Array

가져와야 할 row의 개수를 정확히 알고 있을 경우에는 [Select Into Statement](#57707ee8e727571e)를 사용하여 간단하게 구현할 수 있다. [Select Into Statement](#57707ee8e727571e)에서는 결과가 없거나 한 개일 경우에 대해서만 언급하였지만 여기에 host array를 사용하면 다수의 row를 가져올 수 있다.

사용 방법은 scalar 변수를 쓰는 것과 동일하지만 host variable을 array로 선언하는 것만으로도 array를 사용한 select into 구문을 작성할 수 있다.

```
EXEC SQL BEGIN DECLARE SECTION;
char   emp_name[50][20];
int    emp_number[50];
float  salary[50];
EXEC SQL END DECLARE SECTION;
 
EXEC SQL SELECT ENAME, EMPNO, SAL 
    INTO :emp_name, :emp_number, :salary 
    FROM EMP 
    WHERE SAL > 1000;
```

위의 예를 보면 단지 host 변수들을 배열로 선언하는 것만으로 SELECT INTO 구문으로 50 개의 row를 가져오는 문장이 작성된다. 이 문장은 독립적인 실행 단위를 갖기 때문에 질의 조건에 부합하는 처음의 50개 row만 가져온다.

> 만약 질의 조건에 부합하는 row의 개수가 50 개 이상이라고 해도 SELECT INTO 구문을 사용할 때는 뒷 부분의 51 번째 row부터 가져올 수 있는 방법은 없다. 연속적으로 row를 fetch하려면 cursor를 사용해야만 한다.

<a id="0d492bfdd1348d3e"></a>
##### Cursor 사용에서 Array

현재 질의에 대한 결과 집합 개수를 알 수 없는 경우에는 커서를 사용해야만 한다. 커서를 사용하는 방법은 [Cursor](#46a3dade404496a5) 부분을 참조한다. 커서를 선언한 이후에 FETCH 구문에서 INTO 절의 host 변수를 array로 사용하는 것만으로도 다수의 row를 한 번에 가져올 수 있다.

```
EXEC SQL BEGIN DECLARE SECTION;
    int   emp_number[50];
    char  emp_name[50][20];
    char  dept_name[50][20];
EXEC SQL END DECLARE SECTION;
 
EXEC SQL DECLARE EMP_CURSOR CURSOR FOR
        SELECT    empno, ename, dept
        FROM      EMP
        WHERE     empno < :sNo
        ORDER BY  empno;
 
    sNo = 100;
    EXEC SQL OPEN EMP_CURSOR;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    while( 1 )
    {
        EXEC SQL FETCH EMP_CURSOR INTO :emp_number, :emp_name, :dept_name;

        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            goto fail_exit;
        }
        ...
    }
```

FETCH 구문에서 host array를 사용하는 것만으로도 한 번에 50 개의 row를 fetch하는 기능을 구현할 수 있다.

<a id="8ea7b2f9b35c2499"></a>
##### sqlca.sqlerrd[2]

Array를 사용하면 선언된 배열 크기만큼의 row를 fetch하는데 더 이상 row가 없어서 배열 크기만큼 가져오지 못하는 경우가 있다. 예를 들어, 배열 크기는 50으로 선언되었지만 결과 집합의 row가 30 개일 경우, 30 개의 row밖에 가지고 오지 못한다. 이런 경우에 대비하여 GOLDILOCKS의 embedded SQL은 현재 수행한 구문이 몇 개의 row를 처리하였는지에 대한 정보를 sqlca.sqlerrd[2]에 제공한다.   
sqlca.sqlerrd[2]에는 INSERT, UPDATE, DELETE, SELECT INTO, FETCH 구문에서 처리된 row의 개수를 반환한다.

```
EXEC SQL BEGIN DECLARE SECTION;
    int   emp_number[50];
    char  emp_name[50][20];
    char  dept_name[50][20];
EXEC SQL END DECLARE SECTION;
 
EXEC SQL DECLARE EMP_CURSOR CURSOR FOR
        SELECT    empno, ename, dept
        FROM      EMP
        WHERE     empno < :sNo
        ORDER BY  empno;
 
    sNo = 100;
    EXEC SQL OPEN EMP_CURSOR;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    while( 1 )
    {
        EXEC SQL FETCH EMP_CURSOR INTO :emp_number, :emp_name, :dept_name;

        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            goto fail_exit;
        }
 
        for( i = 0; i < sqlca.sqlerrd[2]; i ++ )
        {
            printf( "%d %s %s\n", emp_number[i], emp_name[i], dept_name[i] );
        }
        ...
    }
```

sqlca에 대한 자세한 내용은 [Handling Runtime Errors](#4a21ae513791d8ed)를 참조한다.

<a id="229cf35bb9d34bac"></a>
#### Insert 구문에서 Array

INSERT 구문에서 host 변수를 array로 선언하면 array insert가 구현된다.

```
EXEC SQL BEGIN DECLARE SECTION;
int    emp_number[20]; 
char   emp_name[20][10]; 
int    dept_number[20]; 
EXEC SQL END DECLARE SECTION;
```

- emp_number, emp_name, dept_number 값을 설정

```
...
```

- emp_number, emp_name, dept_number를 INSERT

```
EXEC SQL INSERT INTO emp (empno, ename, deptno) 
    VALUES (:emp_number, :emp_name, :dept_number);
```

위의 예는 다음 코드와 동일한 작업을 수행한다.

```
EXEC SQL BEGIN DECLARE SECTION;
int    emp_number[20]; 
char   emp_name[20][10]; 
int    dept_number[20]; 
EXEC SQL END DECLARE SECTION;
```

- emp_number, emp_name, dept_number 값을 설정

```
...
```

- emp_number, emp_name, dept_number를 INSERT

```
for( i = 0; i < 20; i ++ )
{
    EXEC SQL INSERT INTO emp (empno, ename, deptno) 
        VALUES (:emp_number[i], :emp_name[i], :dept_number[i]);
}
```


> 
> - Array insert를 사용할 때는 host 변수가 모두 array 변수이거나 모두 scalar 변수이어야 한다.
> - sqlca.sqlerrd[2]를 확인하여 몇 건의 row가 insert 되었는지 확인할 수 있다.
> 

<a id="9d320ac7d0ed5de2"></a>
#### Atomic Insert

Atomic insert는 array insert의 특별한 형태이지만 다음과 같은 두 가지 특징이 있다.

- Insert 하는 모든 row 중에 한 개라도 실패하면 전체 insert 작업이 실패한다.
- 응용 프로그램에서 GOLDILOCKS로 한 번만 명령어가 전달되기 때문에 performance가 뛰어나다.

Atomic insert를 위해 다음과 같은 ATOMIC 키워드를 사용한다.

```
EXEC SQL BEGIN DECLARE SECTION;
int    emp_number[20]; 
char   emp_name[20][10]; 
int    dept_number[20]; 
EXEC SQL END DECLARE SECTION;
```

- emp_number, emp_name, dept_number 값을 설정

```
...
```

- emp_number, emp_name, dept_number를 INSERT

```
EXEC SQL ATOMIC INSERT INTO emp (empno, ename, deptno) 
    VALUES (:emp_number, :emp_name, :dept_number);
```

<a id="0ca2059855c5a8ce"></a>
#### Update 구문에서의 Array

다음은 update 구문에서 array를 사용하는 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
char  job_title [10][20]; 
float commission[10]; 
EXEC SQL END DECLARE SECTION;
 
... 
 
EXEC SQL UPDATE emp SET comm = :commission 
    WHERE job = :job_title;
```

위의 예는 다음과 동일한 기능을 수행한다.

```
EXEC SQL BEGIN DECLARE SECTION;
char  job_title [10][20]; 
float commission[10]; 
EXEC SQL END DECLARE SECTION;
 
... 

for( i = 0; i < 10; i ++ )
{ 
    EXEC SQL UPDATE emp SET comm = :commission[i] 
        WHERE job = :job_title[i];
}
```


> 
> - Array update를 사용할 때는 host 변수가 모두 array 변수이거나 모두 scalar 변수이어야 한다.
> - sqlca.sqlerrd[2]를 확인하여 몇 건의 row가 update 되었는지 확인할 수 있다.
> - UPDATE 구문의 CURRENT OF 절에는 array를 사용할 수 없다.
> 

<a id="780b5ebe88a2ea2e"></a>
#### Delete 구문에서의 Array

Array는 delete 구문에서 다음과 같이 사용할 수 있다.

```
EXEC SQL BEGIN DECLARE SECTION;
char job_title[10][20]; 
EXEC SQL BEGIN DECLARE SECTION;

... 
EXEC SQL DELETE FROM emp 
    WHERE job = :job_title;
```

위의 예는 다음과 동일한 기능을 수행한다.

```
EXEC SQL BEGIN DECLARE SECTION;
char job_title[10][20]; 
EXEC SQL BEGIN DECLARE SECTION;

...
for( i = 0; i < 10; i ++ )
{
    EXEC SQL DELETE FROM emp 
        WHERE job = :job_title[i];
}
```


> 
> - Array delete를 사용할 때는 host 변수가 모두 array 변수이거나 모두 scalar 변수이어야 한다.
> - sqlca.sqlerrd[2]를 확인하여 몇 건의 row가 delete 되었는지 확인할 수 있다.
> - DELETE 구문의 CURRENT OF 절에는 array를 사용할 수 없다.
> 

<a id="2e64e479c93a33d2"></a>
#### FOR 절 사용

SQL 문을 실행하면서 처리하고자 하는 배열 크기를 명시하고자 할 때 FOR 구문을 사용한다. FOR 구문은 다음과 같은 문장에서 사용될 수 있다.

- SELECT INTO
- FETCH
- INSERT
- UPDATE
- DELETE

For 절은 다음과 같이 사용된다.

```
EXEC SQL FOR :host_variable <sql_stmt>
EXEC SQL FOR <integer_constant> <sql_stmt>
```

For 문을 사용하는 예는 다음과 같다.

```
EXEC SQL BEGIN DECLARE SECTION;
int    emp_number[20]; 
char   emp_name[20][10]; 
int    dept_number[20]; 
int      record_cnt;
EXEC SQL END DECLARE SECTION;
```

- emp_number, emp_name, dept_number 값을 설정

```
...
```

- emp_number, emp_name, dept_number를 INSERT

```
record_cnt = 10;
EXEC SQL FOR :record_cnt INSERT INTO emp (empno, ename, deptno) 
    VALUES (:emp_number, :emp_name, :dept_number);
```

위의 예에서 host array의 크기는 20으로 주어졌지만 FOR 구문을 사용하여 record_cnt 만큼만 수행하도록 지정하였기 때문에 실제로는 10 건만 insert 된다.

> FOR 절은 UPDATE/ DELETE CURRENT OF 구문에서는 사용할 수 없다.

<a id="650ea77bd0a47858"></a>
#### 구조체 Array

일반적인 scalar 변수들을 배열로 사용하면 한 번에 다수의 row를 처리할 수 있어 편리하지만 한 개의 변수당 한 개의 column만 표시할 수 있다는 한계가 있다. 한 개의 host 변수에서 다수의 column에 접근하려면 [Host structure](#93168f6dcc50191a)를 사용하면 되는데 이렇게 host 변수를 구조체로 선언하여 그 구조체를 array로 사용하면 다수의 column을 갖는 다수의 row를 한 번에 처리할 수 있다.

구조체 배열은 다음과 같은 경우에 사용될 수 있다.

- Output host variable array: SELECT INTO, FETCH INTO 구문
- Input host variable array: INSERT 구문의 VALUES 항목

<a id="bb4aee9b5ecc40c0"></a>
##### 제약 사항

다음과 같은 경우에는 구조체 배열을 사용할 수 없다.

- WHERE 절이나 FROM 절
- UPDATE 구문의 SET 절

<a id="acdf2a36d5e7cb71"></a>
##### 구조체 배열 선언

구조체는 일반적인 C 언어의 구조체 선언 방식으로 선언한다. 직접 구조체 변수를 선언할 수도 있고 typedef를 통해서 type을 선언한 후에 host 변수를 선언할 수도 있다.

```
EXEC SQL BEGIN DECLARE SECTION;
typedef struct rsRecord
{
    int          mEmpNo;
    varchar      mEName[20 + 1];
    char         mJob[20 + 1];
    long         mSalary;
} rsRecord;
rsRecord     sRecord[10];
 
struct {
    int          mEmpNo;
    varchar      mEName[20 + 1];
    char         mJob[20 + 1];
    long         mSalary;
} sResultRecord[10]; 
EXEC SQL END DECLARE SECTION;
```

Host 변수를 사용하기 위한 구조체를 선언할 때 중첩된 구조체는 사용할 수 없다. 다음과 같이 구조체 선언 내부에 또 다른 구조체가 존재할 경우에는 host 변수로 사용할 수 없다.

```
EXEC SQL BEGIN DECLARE SECTION;
typedef struct rsRecord
{
    struct person {
        int          mEmpNo;
        varchar      mEName[20 + 1];
    } person;
    char         mJob[20 + 1];
    long         mSalary;
} rsRecord;
EXEC SQL END DECLARE SECTION;
```

<a id="4e966c4b78b83ed1"></a>
##### 구조체 배열 Indicator

[Structure Indicator](#612155f3f97e4888)에 기술된 것과 같이 host 변수가 구조체이면 indicator 변수도 구조체이어야 한다. 따라서 host 변수가 구조체 배열일 경우 indicator 변수도 대응하는 구조체 배열이어야 한다.

Indicator 구조체 배열 선언은 다음 사항을 준수한다.

- Indicator의 멤버 수는 결합할 host 변수 구조체의 멤버 수와 같아야 한다.
- Indicator 구조체의 멤버는 모두 정수형 데이터 type을 가져야 한다.
- Indicator 구조체 배열의 크기는 host 변수 구조체 배열의 크기와 같아야 한다. 만약 indicator 구조체 배열의 크기가 작으면 SQL 문을 실행할 때 FOR 절을 이용하여 배열 실행 횟수를 제한해야 한다.

<a id="8655d859024a2abd"></a>
##### Structure와 Scalar 변수 혼용

Host structure가 GOLDILOCKS로 전달될 때 그 structure member들은 순차적으로 나열된다. 다음은 host structure와 scalar 변수를 섞어서 사용하는 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
    typedef struct rsEmp
    {
        int          mEmpNo;
        varchar      mEName[20 + 1];
    } rsEmp;

    rsEmp     sEmp[5];
    char      sJob[5][20 + 1];
    long      sSalary[5];
EXEC SQL END DECLARE SECTION;
 
EXEC SQL
    DECLARE EMP_CUR CURSOR FOR
    SELECT empno, ename, job, sal
    FROM   EMP
    ORDER BY EMPNO;
EXEC SQL OPEN EMP_CUR;
 
EXEC SQL
    FETCH EMP_CUR
    INTO  :sEmp, :sJob, :sSalary;
```

FETCH 구문에는 rsEmp라는 structure와 sJob, sSalary라는 scalar 변수가 함께 사용되었다. 이 문장은 내부적으로 sEmp.mEmpNo, sEmp.mEName, sJob, sSalary 라는 네 개의 변수로 해석된다. 이런 식으로 host structure와 host scalar variable을 섞어서 사용할 수 있다.

다음은 host structure array, structure array indicator, structure와 scalar 변수를 섞어서 사용하는 예이다.

```
/*
 * fetch_struct_array.gc
 *  : structure array fetch
 *  : structure indicators
 *  : mix structure, scalar variable
 *  : sqlca.sqlerrd[2]
 *
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
 
EXEC SQL INCLUDE SQLCA;
 
#define  SUCCESS  0
#define  FAILURE  -1
 
#define  PRINT_SQL_ERROR(aMsg)                                      \
    {                                                               \
        printf("\n");                                               \
        printf(aMsg);                                               \
        printf("\nSQLCODE : %d\nSQLSTATE : %s\nERROR MSG : %s\n",   \
               sqlca.sqlcode,                                       \
               SQLSTATE,                                            \
               sqlca.sqlerrm.sqlerrmc );                            \
    }

EXEC SQL BEGIN DECLARE SECTION;
typedef struct rsEmp
{
    int          mEmpNo;
    varchar      mEName[20 + 1];
} rsEmp;
EXEC SQL END DECLARE SECTION;
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword);
 
int main(int argc, char **argv)
{
    EXEC SQL BEGIN DECLARE SECTION;
    rsEmp     sEmp[5];
    char      sJob[5][20 + 1];
    long      sSalary[5];
    EXEC SQL END DECLARE SECTION;
    int  sRecordCount = 0;
    int  i;
 
    printf("Connect GOLDILOCKS ...\n");
    if(Connect("DSN=GOLDILOCKS", "test", "test") != SUCCESS)
    {
        goto fail_exit;
    }
```

- Retrieve employee

```
EXEC SQL
        DECLARE EMP_CUR CURSOR FOR
        SELECT empno, ename, job, sal
        FROM   EMP
        ORDER BY EMPNO;
 
    EXEC SQL OPEN EMP_CUR;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf(" EMPNO    ENAME                JOB      SALARY\n");
    printf("====== ==================== ========== ========\n");
 
    while( 1 )
    {
        EXEC SQL
            FETCH EMP_CUR
            INTO  :sEmp, :sJob, :sSalary;
        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
            goto fail_exit;
        }
 
        sRecordCount += sqlca.sqlerrd[2];
 
        for( i = 0; i < sqlca.sqlerrd[2]; i ++ )
        {
            printf("%6d %20s %10s %8ld\n",
                   sEmp[i].mEmpNo, sEmp[i].mEName.arr, sJob[i], sSalary[i]);
        }
    }
    printf("====== ==================== ========== ========\n");
    printf("Record Count = %d\n", sRecordCount);
    printf("====== ==================== ========== ========\n");
 
    EXEC SQL CLOSE EMP_CUR;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK RELEASE;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf("\n\nSUCCESS\n");
    printf("############################\n");
 
    return 0;
 
  fail_exit:
 
    printf("\n\nFAILURE\n");
    printf("############################\n\n");
 
    EXEC SQL ROLLBACK WORK RELEASE;
 
    return 0;
}
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword)
{
    EXEC SQL BEGIN DECLARE SECTION;
    VARCHAR  sUid[80];
    VARCHAR  sPwd[20];
    VARCHAR  sConnStr[1024];
    EXEC SQL END DECLARE SECTION;
```

- Log on GOLDILOCKS

```
strcpy((char *)sUid.arr, aUserID);
sUid.len = (short)strlen((char *)sUid.arr);
strcpy((char *)sPwd.arr, sPassword);
sPwd.len = (short)strlen((char *)sPwd.arr);
strcpy((char *)sConnStr.arr, aHostInfo);
sConnStr.len = (short)strlen((char *)sConnStr.arr);
```

- DB 연결

```
EXEC SQL CONNECT :sUid IDENTIFIED BY :sPwd USING :sConnStr;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] Connection Failure!");
 
    return FAILURE;
}
```

<a id="4a21ae513791d8ed"></a>
### Handling Run-time Error

<a id="6d0ee56ca30bde80"></a>
#### 개요

응용 프로그램이 실행되는 중에 기대했던 수행 결과를 내지 못하는 경우에 대비하여 embedded SQL 응용 프로그램을 작성할 때 이런 예외 상황에 대처할 필요가 있다. 본 절에서는 SQL 실행 후에 반환되는 실행 결과를 감지하는 방법에 대해서 설명한다.

<a id="931dc70af5b97e02"></a>
#### Run-time Error 감지

<a id="5a1c694137e9683c"></a>
##### SQLCA

Embedded SQL에서 발생하는 모든 종류의 에러는 SQL Communication Area (SQLCA)라고 하는 영역에 보고된다. 따라서 응용 프로그램에서 SQLCA의 내용을 확인하면 현재 연산의 성공 여부와 함께 에러가 발생했을 경우 그 에러의 종류까지 파악할 수 있다.

SQLCA는 error, warning, SQL 문의 수행 상태 등을 저장하는 자료 구조이다. SQLCA는 이 자료 구조가 결합된 마지막 SQL의 실행 결과를 가지고 있을 뿐, SQL 문 실행 이력에 대한 내용은 저장되지 않는다. Embedded SQL 문이 실행되면 기존의 SQLCA 내용은 사라지기 때문에 예외를 처리하기 위해서는 SQL을 실행한 후에 SQLCA를 바로 확인해서 필요한 조치를 취해야 한다.

<a id="d70a9ae69feb21ad"></a>
##### SQLCA 사용

SQLCA를 사용하기 위해서는 다음과 같은 구문을 사용한다.

```
EXEC SQL INCLUDE SQLCA;
```

위 문장은 precompile 과정에서 다음 문장으로 치환된다.

```
#include "sqlca.h"
```

이 문장은 첫 번째 embedded SQL 문장이 사용되기 전에 미리 쓰여야 하며 통상적으로 소스 코드의 상단에 배치하도록 권장한다.

GOLDILOCKS의 embedded SQL 응용 프로그램은 기본적으로 sqlca를 전역으로 가지고 있다. 따라서 single thread program에서는 별다른 선언 없이 sqlca를 사용할 수 있다. 그러나 multi thread program에서는 동시에 sqlca에 접근할 경우 동시성 문제가 발생하기 때문에 별도의 선언 방법을 가져야 한다. 이에 대한 내용은 [Multithread Applications](#a642155c111f3d59)에서 설명한다.

<a id="9a9fe49d35e934fd"></a>
##### SQLCA 구조

다음은 sqlca의 구조체이다.

```
struct sqlca
{
    char    sqlcaid[8];   ❶ 문자열 SQLCA로 초기화한다.
    int     sqlabc;       ❷ sqlca 구조체의 크기이다.
```

- 가장 최근에 실행한 문장에서 발생한 error code가 0이면 성공, 양수이면 warning, 음수이면 error이다.

```
int     sqlcode;
```

- sqlcode에 해당하는 에러 메세지를 저장한다.
- .sqlerrml은 sqlerrmc의 길이이다.
- .sqlerrmc는 에러 메세지를 string 형태로 저장한다.

```
struct
    {
        unsigned short sqlerrml;
        char           sqlerrmc[SQLERRMC_LEN];
    } sqlerrm;
 
    char    sqlerrp[8];   ❸ unused                        
    int     sqlerrd[6];
```

- 0: empty
- 1: empty
- 2: INSERT, UPDATE, DELETE 후에 처리된 row의 개수이다.
- 3: empty
- 4: empty
- 5: empty

```
char    sqlwarn[8];
```

- 0: 임의의 warning이 한 개라도 발생할 경우 'W'이다.
- 1: SELECT, FETCH에서 결과 string이 truncate 된 경우 'W'이다.
- 2: unused
- 3: unused
- 4: unused
- 5: unused
- 6: unused
- 7: unused

```
char    sqlext[8];    ❹ unused                         
char    sqlstate[8];  ❺ SQLSTATE                       
unsigned short  *rowstatus;    ❻ fetched row status array
};
```

다음 절에서 각 구성 요소들을 설명한다.

<a id="f2272e1d3861722b"></a>
###### **SQLCODE**

SQLCODE는 다음과 같이 정의되어 있다.

```
#define SQLCODE          (sqlca.sqlcode)
```

SQLCODE는 embedded SQL 문을 실행한 후에 그 실행 결과 코드를 반환한다. SQLCODE는 ISO/ IEC-9075에서 초기에 제안되었으나 SQL-92에서 deprecate 되었다. 그러나 많은 응용 프로그램에서 사용되고 있기 때문에 하위 호환성을 위해서 제공되고 있다. 실행 결과 코드는 다음과 같다.

**SQLCODE 실행결과**

<a id="c7028f3e89ee72e9"></a>
| SQLCODE | 결과 |
| --- | --- |
| 0 | 성공 |
| > 0 | Warning 발생 |
| SQL_NO_DATA | 결과 없음 |
| < 0 | Error 발생 |

sqlcode는 다음과 같은 방법으로 확인할 수 있다. sqlca.sqlcode나 SQLCODE를 사용할 수 있다.

```
EXEC SQL
        DECLARE EMP_CUR CURSOR FOR
        SELECT empno, ename, job, sal
        FROM   EMP;
 
    EXEC SQL OPEN EMP_CUR;
    if(SQLCODE != 0)
    {
        goto fail_exit;
    }

    while( 1 )
    {
        EXEC SQL
            FETCH EMP_CUR
            INTO  :sEmpNo, :sEName, :sJob, :sSalary;
        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            goto fail_exit;
        }
 
        ...
    }
```

<a id="5b760af7a77ce319"></a>
###### **SQLSTATE**

SQLSTATE는 다음과 같이 정의되어 있다.

```
#define SQLSTATE         (sqlca.sqlstate)
```

ISO/ IEC-9075에서 SQLCODE가 deprecate된 후 이를 대신해 제안되었다. SQLSTATE는 다섯 개의 문자 (숫자, 영문 대문자 알파벳)로 구성되어 있는데 앞의 두 자리는 class이고, 뒤의 세 자리는 subclass 이다. SQLSTATE의 실행 결과는 다음과 같다.

**SQLSTATE 실행 결과**

<a id="36d0a5a912b4cbf2"></a>
| SQLSTATE | 결과 |
| --- | --- |
| 00000 | 성공 |
| 01xxx | Warning 발생 |
| 02000 | 결과 없음 |
| 그 밖의 모든 State | Error 발생 |

위 예제의 SQLCODE 대신 SQLSTATE를 확인하여 코드를 수정하면 다음과 같다. sqlca.sqlstate나 SQLSTATE를 사용할 수 있다.

```
EXEC SQL
        DECLARE EMP_CUR CURSOR FOR
        SELECT empno, ename, job, sal
        FROM   EMP;
 
    EXEC SQL OPEN EMP_CUR;
    if(strcmp(SQLSTATE, "00000") != 0)
    {
        goto fail_exit;
    }

    while( 1 )
    {
        EXEC SQL
            FETCH EMP_CUR
            INTO  :sEmpNo, :sEName, :sJob, :sSalary;
        if(strcmp(sqlca.sqlstate, "02000") == 0)
        {
            break;
        }
        else if(strcmp(sqlca.sqlstate, "00000") != 0)
        {
            goto fail_exit;
        }
 
        ...
    }
```

<a id="a10f92f33f4a9275"></a>
###### **처리된 Row의 개수**

Update, delete 구문이나 array를 사용한 insert, select into, fetch 구문을 수행했을 때 몇 개의 row가 처리되었는지를 알려준다. 해당 정보는 sqlca.sqlerrd[2]에 저장되며 응용 프로그램에서는 해당 필드의 값을 참조하여 처리된 row의 개수를 파악할 수 있다. 다음은 sqlca.sqlerrd[2]를 사용하는 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
    typedef struct rsEmp
    {
        int          mEmpNo;
        varchar      mEName[20 + 1];
    } rsEmp;
    rsEmp     sEmp[5];
    char      sJob[5][20 + 1];
    long      sSalary[5];
EXEC SQL END DECLARE SECTION;

    EXEC SQL
        DECLARE EMP_CUR CURSOR FOR
        SELECT empno, ename, job, sal
        FROM   EMP;
 
    EXEC SQL OPEN EMP_CUR;
    if(SQLCODE != 0)
    {
        goto fail_exit;
    }

    while( 1 )
    {
        EXEC SQL
            FETCH EMP_CUR
            INTO  :sEmpNo, :sEName, :sJob, :sSalary;
        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            goto fail_exit;
        }
 
        sRecordCount += sqlca.sqlerrd[2];
        ...
    }
```

fetch 구문에 한하여 sqlca.sqlerrd[2]의 값을 누적된 row 개수로 처리할 수 있다. 이와 관련된 자세한 내용은 gpec(Precompiler)의 옵션 [--cumulative](#382e15424d707a60)을 참조한다.

<a id="5f5c186817301cc4"></a>
###### **처리된 Row의 상태**

sqlca.rowstatus는 현재 처리된 row의 상태를 나타낸다. Scroll sensitive cursor를 사용하거나 where CURRENT OF를 사용하여 row를 갱신/ 삭제하였을 경우, row의 상태가 갱신될 수 있으며 array를 사용한 SQL 구문을 사용했을 경우, array 크기만큼의 row status를 갖는다.

**Row 상태**

<a id="c37041ea31fc5a34"></a>
| Row 개수 | Row 상태 |
| --- | --- |
| 1개 | *sqlca.rowstatus |
| Array size n | sqlca.rowstats[0] sqlca.rowstats[1] sqlca.rowstats[2] ... sqlca.rowstats[n-1] |

**Row 상태 값**

<a id="d10bb62d18b33780"></a>
| Row 상태 | 설명 |
| --- | --- |
| SQL_ROW_SUCCESS | Row의 상태가 정상이다. |
| SQL_ROW_DELETED | Row가 삭제되었다. |
| SQL_ROW_UPDATED | Row가 갱신되었다. |
| SQL_ROW_NOROW | Row가 존재하지 않는다. |
| SQL_ROW_ADDED | Row가 추가되었다. |
| SQL_ROW_ERROR | Row의 상태가 비정상이다. |

다음은 row status를 참조하는 예이다.

```
EXEC SQL BEGIN DECLARE SECTION;
    typedef struct rsEmp
    {
        int          mEmpNo;
        varchar      mEName[20 + 1];
    } rsEmp;
    rsEmp     sEmp[5];
    char      sJob[5][20 + 1];
    long      sSalary[5];
EXEC SQL END DECLARE SECTION;

    EXEC SQL
        DECLARE EMP_CUR CURSOR FOR
        SELECT empno, ename, job, sal
        FROM   EMP;
 
    EXEC SQL OPEN EMP_CUR;
    if(SQLCODE != 0)
    {
        goto fail_exit;
    }

    while( 1 )
    {
        EXEC SQL
            FETCH EMP_CUR
            INTO  :sEmpNo, :sEName, :sJob, :sSalary;
        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            goto fail_exit;
        }
 
        sRecordCount += sqlca.sqlerrd[2];
 
        for( i = 0; i < sqlca.sqlerrd[2]; i ++ )
        {
            if( sqlca.rowstatus[i] == SQL_ROW_SUCCESS )
            {
                printf("%6d %20s %10s %8ld\n",
                       sEmp[i].mEmpNo, sEmp[i].mEName.arr, sJob[i], sSalary[i]);
            }
        }
        
        ...
    }
```

<a id="44dacaa7e466095f"></a>
###### **Error Message Text**

Embedded SQL 문을 실행한 결과 error나 warning이 발생하면 해당 메세지를 text 형태로 전송할 수 있다. 에러 메세지는 sqlca.sqlerrm에 저장되는데 sqlca.sqlerrm.sqlerrml은 text의 길이이고 실제 메세지는 sqlca.sqlerrm.sqlerrmc에 저장되어 있다. 에러 메세지 text는 응용 프로그램에서 이상 현상이 발생하였을 경우 이를 출력해서 사용자에게 정보를 전달할 때 유용하다. 다음은 error message text를 사용하는 예이다.

```
EXEC SQL INSERT INTO EMP VALUES ( :sEmp );
if( SQLCODE != 0 )
{
    printf("\nSQLCODE : %d\nSQLSTATE : %s\nERROR MSG : %s\n",
           SQLCODE,
           SQLSTATE,
           sqlca.sqlerrm.sqlerrmc );
}
```

<a id="4d7c9abfe0b166dc"></a>
###### **Warning Flags**

sqlca.sqlwarn은 embedded SQL을 수행한 후에 warning이 발생했을 때 warning을 mark해 주는 flag로 사용된다. 여덟 개의 char array로 구성되어 있으며 warning이 발생하였을 경우 'W' 마크를 남긴다.

**Warning flag**

<a id="cb9488d9e41a8bfb"></a>
| Warning flag | 설명 |
| --- | --- |
| sqlca.sqlwarn[0] | 임의의 warning이 한 개라도 발생할 경우 'W'가 된다. |
| sqlca.sqlwarn[1] | Select into, fetch에서 결과 string이 truncate된 경우 'W'가 된다. |
| sqlca.sqlwarn[2] | reserved |
| sqlca.sqlwarn[3] | reserved |
| sqlca.sqlwarn[4] | reserved |
| sqlca.sqlwarn[5] | reserved |
| sqlca.sqlwarn[6] | reserved |
| sqlca.sqlwarn[7] | reserved |

<a id="3a7a59b85301cdcd"></a>
#### Handling Implicit Error

Embedded SQL 문을 실행한 후에는 반드시 SQLCA를 확인하여 수행 결과에 대한 조치를 취해야만 한다. 그러나 embedded SQL 문을 실행한 뒤에 동일한 예외 처리를 하는 경우에는 WHENEVER 지시자를 사용하여 이를 자동화할 수 있다.

<a id="72511f22832425f6"></a>
##### WHENEVER 구문 사용

WHENEVER 구문의 문법은 다음과 같다.

```
EXEC SQL WHENEVER conditions actions;
```

<a id="c7b6b8b2af8214b9"></a>
##### WHENEVER Condition

WHENEVER 구문의 condition은 다음과 같다.

```
<conditions> ::=
      SQLERROR
    | SQLWARNING
    | NOT FOUND
    | SQLSTATE <sqlstate class value>[<sqlstate subclass value>]
    ;
 
<sqlstate_char> ::= [0-9A-Z];
<sqlstate class value> ::= <sqlstate_char><sqlstate_char>;
<sqlstate subclass value> ::= <sqlstate_char><sqlstate_char><sqlstate_char>;
```

**Conditions of WHENEVER statement**

<a id="10bcbe0e8f1ee1df"></a>
| Condition | 설명 |
| --- | --- |
| SQLERROR | Embedded SQL을 수행하는 중에 error가 발생했다. |
| SQLWARNING | Embedded SQL을 수행하는 중에 warning이 발생했다. |
| NOT FOUND | 결과 row가 없다. |
| SQLSTATE &lt;sqlstate&gt; | Embedded SQL을 수행하는 중에 SQLSTATE &lt;sqlstate&gt;가 발생하였다. |

<a id="f74ff9f205239ef4"></a>
##### WHENEVER Action

Action은 앞서 기술한 condition을 만족할 때 실제로 수행되는 동작을 기술한 것으로써 그 문법은 다음과 같다.

```
<actions> ::=
      CONTINUE
    | GOTO <label>
    | STOP
    | DO <c statements>
    ;
```

**Actions of WHENEVER statement**

<a id="2a3a92b268007fdf"></a>
| Action | 설명 |
| --- | --- |
| CONTINUE | 아무런 action을 취하지 않는다. 즉, 주어진 condition을 무시한다. |
| GOTO &lt;label&gt; | &lt;label&gt;로 프로그램 흐름을 분기한다. |
| STOP | 프로그램 실행을 종료한다. |
| DO &lt;c statements&gt; | &lt;c statements&gt;를 실행한다. |

<a id="2b5e9d79b4ec79aa"></a>
##### WHENEVER 구문 적용 범위

WHENEVER 구문은 conditions에 대한 actions를 기술하는데 하나의 condition에 대해 하나의 action만 기술할 수 있다. 따라서 WHENEVER 구문을 사용하면 현재 정의된 condition 이후에 다른 condition 정의가 나올 때까지 모든 embedded SQL 구문에 동일한 action이 사용된다.

WHENEVER 구문은 각 condition 별로 따로 관리되기 때문에 특정 시점에 적용할 수 있는 WHENEVER 구문의 최대 개수는 네 개이다. 같은 condition에 대해서 새로운 WHENEVER 구문이 적용될 경우, 기존 action은 취소되고 이후부터 해당 action이 적용된다. 다음은 그 예이다.

```
EXEC SQL WHENEVER SQLERROR STOP;
EXEC SQL INSERT INTO emp VALUES ( :emp_number, :emp_name, :salary ); ❶
...
EXEC SQL WHENEVER SQLERROR CONTINUE;
EXEC SQL UPDATE emp SET sal = sal * 1.1 WHERE sal < :sal_bound; ❷
...
EXEC SQL WHENEVER SQLERROR GOTO exit_label;
EXEC SQL WHENEVER NOT FOUND DO break;
EXEC SQL DECLARE EMP_CURSOR FOR
         SELECT empno, ename, sal
         FROM   emp;
 
EXEC SQL OPEN EMP_CURSOR; ❸
 
EXEC SQL WHENEVER SQLERROR GOTO close_label;
while( 1 )
{
    EXEC SQL FETCH EMP_CURSOR
             INTO   :emp_number, :emp_name, :salary; ❹
 
    printf( "emp number : %d, emp name : %s, salary : %lf\n",
            emp_number, emp_name, salary );
}

close_label:
EXEC SQL WHENEVER SQLERROR DO sql_error();
EXEC SQL CLOSE EMP_CURSOR; ❺
...
exit_label:
...
```

Line 1에서 SQLERROR의 경우에 STOP하도록 지시하였으므로 문장 1을 실행하다가 에러가 발생하면 응용 프로그램이 종료된다. Line 4에서 SQLERROR일 경우 CONTINUE하도록 지시하므로 SQLERROR의 action은 아무것도 하지 않고 진행하는 것으로 변경되고, 그에 따라 문장 2를 실행하다가 에러가 발생하더라도 아무 일도 없이 다음으로 넘어가게 된다. Line 7에서 SQLERROR의 action을 exit_label로 분기하는 것으로 설정하므로 문장 3을 실행하다가 에러가 발생하면 exit_label로 분기한다. Line 8에서 NOT FOUND에 대해 break를 수행하도록 지정하였고 line 15에서 SQLERROR의 action은 close_label로 다시 지정하였기 때문에 문장 4에는 두 가지의 condition이 적용되어 FETCH를 실행하는 도중에 error가 발생할 경우에는 close_label로 분기하고 FETCH의 결과가 없으면 break 문이 실행된다. Line 26에서 SQLERROR의 action을 sql_error()를 실행하는 것으로 지정하였으므로 문장 5를 실행하는 도중에 error가 발생하면 sql_error() 함수가 호출된다.

<a id="ce592c9f4d9ffe83"></a>
##### WHENEVER 구문 사용 시 주의 사항

WHENEVER 구문을 사용할 때는 그 동작 원리를 정확히 파악하여 주의 깊게 사용해야 한다. WHENEVER 구문을 사용할 때 주의할 점은 다음과 같다.

- 소스 코드 상에서 WHENEVER 구문의 위치: WHENEVER 구문은 precompiler에게 exception handling 코드를 자동으로 삽입하도록 알려주는 지시자일 뿐, 논리적으로 실행되는 코드가 아니다. 따라서 WHENEVER 구문을 사용할 때는 소스 코드 상에서 적용할 embedded SQL 문의 앞 부분에 써 주어야 하고 이후에 등장하는 다른 embedded SQL에 영향을 주지 않으려면 반드시 CONTINUE action을 사용하여 초기화해 주어야 한다.
- Break, continue 키워드 사용: Action 구문에서 DO break, DO continue를 사용할 때는 반드시 loop의 영역을 확인해야 한다. 다음 예제를 참조한다.

```
EXEC SQL WHENEVER SQLERROR GOTO fail_exit;
EXEC SQL WHENEVER NOT FOUND DO break; ❶

EXEC SQL DECLARE EMP_CURSOR FOR
         SELECT empno, ename, sal
         FROM   emp;
 
EXEC SQL OPEN EMP_CURSOR; 
while( 1 )
{
    EXEC SQL FETCH EMP_CURSOR
             INTO   :emp_number, :emp_name, :salary;  ❷
    printf( "emp number : %d, emp name : %s, salary : %lf\n",
            emp_number, emp_name, salary );
}

EXEC SQL CLOSE EMP_CURSOR;
 
EXEC SQL
    SELECT MAX(sal)
    INTO   :max_salary
    FROM   emp;         ❸
...
```

1에서 NOT FOUND에 대한 action으로 DO break;를 정의하였으므로 이후 SQL 문을 실행할 때 NOT FOUND가 발생하면 break;를 실행하려 할 것이다. 2에서 FETCH를 수행하다가 NOT FOUND가 발생하면 break가 수행되어 while loop에서 빠져 나온다. 그러나 3의 경우에는 NOT FOUND가 발생할 때 break를 수행하려고 하여도 loop가 아니기 때문에 break를 실행할 수 없다. 이 경우에는 소스 프로그램을 build하여 응용 프로그램을 만드는 단계에서 이미 compile 에러가 발생한다.

- 무한 loop 회피

Action으로 분기를 사용할 때 잘못하면 무한 loop에 빠질 수 있다. 다음 예제를 참조한다.

```
EXEC SQL WHENEVER SQLERROR GOTO sql_error; 
...
EXEC SQL INSERT INTO emp VALUES ( :emp_number, :emp_name, :salary );
...
sql_error: 
    EXEC SQL ROLLBACK WORK RELEASE;
```

SQL을 실행하는 중에 error가 발생하면 sql_error 레이블로 분기하게 하였다. 이 때 embedded SQL 문을 실행하다가 error가 발생하면 sql_error로 분기한다. 그런데 이 에러처리 과정에서 또 다른 embedded SQL을 실행하도록 하고 여기서 반복적으로 error가 발생할 경우, 응용 프로그램이 무한 loop에 빠지게 된다. 이 경우에는 다음과 같이 error 처리 부분을 안전하게 초기화해 주는 것이 좋다.

```
EXEC SQL WHENEVER SQLERROR GOTO sql_error; 
...
EXEC SQL INSERT INTO emp VALUES ( :emp_number, :emp_name, :salary );
...
sql_error: 
    EXEC SQL WHENEVER SQLERROR CONTINUE; 
    EXEC SQL ROLLBACK WORK RELEASE;
```

- 분기 label의 scope

Action에서 분기할 때는 반드시 접근 가능한 곳에 해당 label이 존재해야 한다. 다음 예제를 참조한다.

```
func1() 
{ 
  
    EXEC SQL WHENEVER SQLERROR GOTO labelA; 
    EXEC SQL DELETE FROM emp WHERE deptno = :dept_number; 
    ... 
labelA: 
... 
} 

func2() 
{ 
  
    EXEC SQL INSERT INTO emp (job) VALUES (:job_title); 
    ... 
}
```

func1()에서 SQLERROR에 대하여 labelA 분기를 지정하였다. func1()에는 labelA가 있기 때문에 문제가 없지만 func2()에는 labelA가 존재하지 않기 때문에 compile 오류가 발생한다. 이 경우에는 func2()에도 동일한 labelA를 만들어 주거나 다음과 같이 action을 초기화 해주어야 한다.

```
func1() 
{ 
  
    EXEC SQL WHENEVER SQLERROR GOTO labelA; 
    EXEC SQL DELETE FROM emp WHERE deptno = :dept_number; 
    ... 
labelA: 
... 
} 

func2() 
{ 
    EXEC SQL WHENEVER SQLERROR CONTINUE; 
    EXEC SQL INSERT INTO emp (job) VALUES (:job_title); 
    ... 
}
```

<a id="38e2585027846c5f"></a>
## Advanced Topic

<a id="bab9699b12f1bf0c"></a>
### Embedded Dynamic SQL

<a id="e7537d807f0982d4"></a>
#### 개요

대부분의 embedded SQL 응용 프로그램은 GOLDILOCKS에 대한 구체적인 동작을 가지고 있다. 특정 테이블에 row를 삽입, 갱신, 삭제, 조회하는 것을 목표로 하고 있으며 그에 따른 동작 방법을 SQL이라는 database 언어를 사용하여 기술한다. 이를 위해 embedded SQL 소스 코드에 SQL을 직접 작성하면 precompiler는 이 SQL을 해석하여 주어진 SQL 내용과 input/ output host variable을 모두 알고 있는 상태에서 GOLDILOCKS에 동작 가능한 API 호출로 변환한다.

그러나 어떤 응용 프로그램의 경우에는 프로그램을 작성할 때 SQL을 미리 알 수 없는 경우도 있다. 예를 들어 GUI tool과 같은 응용 프로그램에서 사용자가 연산 종류, 테이블 이름, 조건 등을 선택하여 조회하기 위해 static SQL을 사용할 경우, 사용자가 선택할 수 있는 모든 조합에 대해 미리 SQL을 생성해야 하는데 이는 현실적으로 불가능할 뿐만 아니라 만약에 가능하다고 하더라도 매우 비효율적인 작업이 된다. 이 때 사용자가 선택하는 옵션을 가지고 SQL을 생성하여 실행할 수 있다면 프로그램 작성이 매우 유연해진다. 이렇게 소스 코드 상에서 SQL이 정의되지 않고 실행 시점에 가변적으로 변경되는 SQL을 dynamic SQL 이라고 하며 GOLDILOCKS에서는 embedded dynamic SQL 기능을 제공하고 있다.

Embedded dynamic SQL 응용 프로그램은 static SQL에 비해 좀 더 유연한 사용방법을 제공한다는 장점이 있지만 소스 코드 작성이 좀 더 까다로워진다는 특징이 있고 동일한 query를 하더라도 static SQL에 비해 dynamic SQL의 수행 성능이 더 떨어질 수 있다는 단점이 있다.

따라서 응용 프로그램을 작성할 때는 이러한 특징을 고려하여 static SQL과 dynamic SQL 중에 주의깊게 선택해야 한다.

본 장에서는 embedded dynamic SQL 프로그램을 작성하는 방법에 대해 설명한다.

<a id="bbadfd111e118d7a"></a>
#### Dynamic SQL의 종류

Dynamic SQL은 그 사용 방법에 따라 다음과 같이 분류된다.

**Dynamic SQL의 종류**

<a id="61c608deb5f0c05f"></a>
| Method | 설명 | 지원 여부 |
| --- | --- | --- |
| Method 1 | Non-query, host variable이 없다. | O |
| Method 2 | Non-query, 그 개수와 type을 알고 있는 host variable이 있다. | O |
| Method 3 | Query, 그 개수와 type을 알고 있는 host variable이 있다. | O |
| Method 4 | Query, host variable의 존재 여부, 개수와 type등을 알지 못한다. | X |

현재 GOLDILOCKS에서는 method 3 까지만 지원하고 있다.

<a id="3b94230c68c7f7ca"></a>
##### Method 1

가장 단순한 형태의 dynamic SQL로써, non-query이면서 host variable이 없는 경우에 사용할 수 있다. 일반적으로 DDL이나 host variable 없는 DML에 사용한다.

- EXECUTE IMMEDIATE

Method 1은 그 특성상 non-query이면서 host variable도 없기 때문에 SQL 문을 즉시 실행할 수 있다. SQL의 즉시 실행 문법은 다음과 같다.

```
EXEC SQL EXECUTE IMMEDIATE { :host_variable | <string_literal> };
<string_literal> ::=
      ' <sql_statement> '
    | " <sql_statement> "
    | <sql_statement>
    ;
```

Method 1은 다음과 같이 사용할 수 있다.

```
sprintf(sSqlStmt, "CREATE TABLE EMP_RND (\n"
            "EMPNO NUMBER(4) CONSTRAINT PK_EMP_RND PRIMARY KEY,\n"
            "ENAME VARCHAR2(10),\n"
            "JOB VARCHAR2(9),\n"
            "SAL NUMBER(7,2),\n"
            "DEPTNO NUMBER(2) )\n" );
    EXEC SQL EXECUTE IMMEDIATE :sSqlStmt;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }

    sprintf(sSqlStmt, "INSERT INTO EMP_RND\n"
            "SELECT *\n"
            "FROM   EMP\n"
            "WHERE  JOB = 'RND'\n" );
    EXEC SQL EXECUTE IMMEDIATE :sSqlStmt;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
```

<a id="de2733f0184f4c12"></a>
##### Method 2

Method 2는 non-query이면서 input host variable이 존재하는 경우에 사용한다. 이 때 input host variable의 개수와 data type을 모두 알고 있어야 하며 준비 (prepare) 단계와 실행 (execute) 단계를 통해구현된다.

- Prepare

Prepare 단계에서는 SQL statement를 분석하고 이 statement에 이름을 부여한다. Prepare의 문법은 다음과 같다.

```
EXEC SQL PREPARE <statement_name> FROM { :host_variable | <string_literal> };
<string_literal> ::=
      ' <sql_statement> '
    | " <sql_statement> "
    | <sql_statement>
    ;
```

&lt;statement_name&gt;은 precompiler에게 알려주는 식별자로써 host variable이 아니기 때문에 별도의 type을 갖거나 변수를 선언할 필요가 없다.

- Execute

Execute 단계에서는 분석된 statement를 실행한다. Execute 구문의 문법은 다음과 같다.

```
EXEC SQL EXECUTE <statement_name> [ USING <host_variable_list> ];
<host_variable_list> ::= <host_variable_entry> [ , <host_variable_list> ];
<host_variable_entry> ::= :host_variable [ [ INDICATOR ] :host_indicator ];
```

Input host variable이 있을 경우에는 USING 절을 사용한다. Host variable이 없을 경우, USING 절은 생략한다. USING 절에 등장하는 host variable의 순서대로 prepare된 SQL 문의 host variable에 binding된다.

Method 2에서 동일한 SQL 문을 반복 실행할 때, prepare는 한 번만 수행한 뒤에 execute를 반복 실행할 수 있다. 이 prepare된 statement는 현재 소스 코드 내에서 같은 statement name으로 다른 SQL 문을 prepare 하거나 disconnect 할 때까지 유효하다.

<a id="3910b7bba8894a06"></a>
##### Method 3

Method 3는 query를 지원할 수 있도록 method 2에서 확장된 형태이다. 기본적으로 query prepare 과정을 통해 statement를 분석하고 query하기 위해 cursor를 다룰 수 있어야 하기 때문에 cursor에 대해 declare, open, fetch, close하는 구문이 추가된다.

- Prepare

Prepare 단계는 method 2와 마찬가지로 SQL statement를 분석하고 이 statement에 이름을 부여한다. Prepare의 문법은 다음과 같다.

```
EXEC SQL PREPARE <statement_name> FROM { :host_variable | <string_literal> };
<string_literal> ::=
      ' <sql_statement> '
    | " <sql_statement> "
    | <sql_statement>
    ;
```

&lt;statement_name&gt;은 precompiler에게 알려주는 식별자로 host variable이 아니기 때문에 별도의 type을 갖거나 변수를 선언할 필요가 없다.

- Declare cursor

Declare 구문은 prepare된 statement에 대해 cursor를 선언한다. Cursor를 선언할 때 standing cursor와 동일한 cursor property를 사용할 수 있으며 그 구문은 다음과 같다.

```
EXEC SQL <dynamic declare cursor>;
 
<dynamic declare cursor> ::=
    DECLARE <cursor_name> <cursor properties> { FOR | IS } <statement_name>
    ;

<cursor properties> ::=
      [ <cursor sensitivity> ] [ <cursor scrollability>] ] CURSOR [ <cursor holdability> ] 
    | [ <odbc cursor type] CURSOR [ <cursor holdability> ] 
    ;

<cursor sensitivity> ::=
      INSENSITIVE
    | SENSITIVE
    | ASENSITIVE
    ;

<cursor scrollability> ::=
      NO SCROLL
    | SCROLL
    ;

<cursor holdability> ::=
      WITH HOLD
    | WITHOUT HOLD
    ;

<odbc cursor type> ::=
      STATIC
    | KEYSET
    ;
```

&lt;cursor properties&gt;는 standing cursor와 의미 및 사용 이름이 동일하므로 이와 관련된 내용은 [Cursor Property](#89dbb469a078b345)를 참조한다.

&lt;statement_name&gt;은 PREPARE 구문에서 지정된 이름이며, &lt;cursor name&gt;과 &lt;statement name&gt;은 precompiler에게 알려주는 식별자로써 host variable이 아니기 때문에 별도의 type을 갖거나 변수를 선언할 필요가 없다.

- Open cursor

Cursor를 open한다. Standing cursor의 [Open](#e844bbfa8c1bd6ff)과 비교하여 기본적인 면에서는 동일하지만 dynamic cursor의 open만 갖는 중요한 차이점이 있다. Dynamic cursor는 run-time에 SQL 문을 자유롭게 변경하여 사용할 수 있기 때문에 declare된 statement의 SQL에 따라 host variable이 결정된다. 따라서 dynamic cursor를 open 할 때는 open 시점에 USING 절을 사용하여 host variable을 전달한다.

Dynamic cursor의 open 구문은 다음과 같다.

```
EXEC SQL <dynamic cursor open>;
 
<dynamic cursor open> ::=
    OPEN <cursor_name> [ USING <host_variable_list> ]
    ;
 
<host_variable_list> ::= <host_variable_entry> [ , <host_variable_list> ];
<host_variable_entry> ::= :host_variable [ [ INDICATOR ] :host_indicator ];
```

- Fetch cursor

Cursor로부터 fetch한다. Dynamic cursor의 fetch는 [Standing cursor의 Fetch](#85738290c933a1fc)와 동일하다.

- Close cursor

Cursor를 close한다. Dynamic cursor의 close는 [Standing cursor의 Close](#10c9846c3eeabfd5)와 동일하다.

<a id="039c8b6c9e7d5cad"></a>
#### Example Program

다음은 dynamic method 1, 2, 3을 사용한 sample program이다.

```
/*
 * dyn2.gc
 *  : dynamic method 1
 *  : dynamic method 2
 *  : dynamic method 3
 *
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
EXEC SQL INCLUDE SQLCA;
 
#define  SUCCESS  0
#define  FAILURE  -1
#define  PRINT_SQL_ERROR(aMsg)                                      \
    {                                                               \
        printf("\n");                                               \
        printf(aMsg);                                               \
        printf("\nSQLCODE : %d\nSQLSTATE : %s\nERROR MSG : %s\n",   \
               sqlca.sqlcode,                                       \
               SQLSTATE,                                            \
               sqlca.sqlerrm.sqlerrmc );                            \
    }
 
EXEC SQL BEGIN DECLARE SECTION;
typedef struct Record
{
    int          mEmpNo;
    varchar      mEName[20 + 1];
    char         mJob[20];
    char         mSalary[10];
} Record;
EXEC SQL END DECLARE SECTION;
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword);
int CreateEmpTempTable();
int DropEmpTempTable();
int UpdateSalary(char *aJob, int aBound, double aRatio);
 
int main(int argc, char **argv)
{
    EXEC SQL BEGIN DECLARE SECTION;
    EXEC SQL END DECLARE SECTION;
    printf("Connect GOLDILOCKS ...\n");
    if(Connect("DSN=GOLDILOCKS", "test", "test") != SUCCESS)
    {
        goto fail_exit;
    }
 
    if(CreateEmpTempTable() != SUCCESS)
    {
        goto fail_exit;
    }
```

- Print RND employee increate 20% salary where salary < 2000

```
printf("print RND employee increate 20%% salary where salary < 2000\n");
UpdateSalary( "RND", 2000, 1.2 );
printf("\n\n");
```

- Print SUPPORT employee increate 10% salary where salary < 3000

```
printf("print SUPPORT employee increate 10%% salary where salary < 3000\n");
UpdateSalary( "SUPPORT", 3000, 1.1 );
printf("\n\n");
 
if(DropEmpTempTable() != SUCCESS)
{
     goto fail_exit;
}
 
printf("Disconnect GOLDILOCKS ...\n");
EXEC SQL COMMIT WORK RELEASE;
if(sqlca.sqlcode != 0)
{
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    goto fail_exit;
}
 
printf("SUCCESS\n");
printf("############################\n");
 
return 0;
 
  fail_exit:
 
    printf("\n\nFAILURE\n");
    printf("############################\n\n");
    EXEC SQL ROLLBACK WORK RELEASE;
 
    return 0;
}
 
int Connect(char *aHostInfo, char *aUserID, char *sPassword)
{
    EXEC SQL BEGIN DECLARE SECTION;
    VARCHAR  sUid[80];
    VARCHAR  sPwd[20];
    VARCHAR  sConnStr[1024];
    EXEC SQL END DECLARE SECTION;
```

- • Log on GOLDILOCKS

```
strcpy((char *)sUid.arr, aUserID);
sUid.len = (short)strlen((char *)sUid.arr);
strcpy((char *)sPwd.arr, sPassword);
sPwd.len = (short)strlen((char *)sPwd.arr);
strcpy((char *)sConnStr.arr, aHostInfo);
sConnStr.len = (short)strlen((char *)sConnStr.arr);
```

- DB 연결

```
EXEC SQL CONNECT :sUid IDENTIFIED BY :sPwd USING :sConnStr;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] Connection Failure!");
 
    return FAILURE;
}
```

- Create table

```
int CreateEmpTempTable()
{
    EXEC SQL BEGIN DECLARE SECTION;
    char   sSqlStmt[8192];
    EXEC SQL END DECLARE SECTION;
    sprintf(sSqlStmt, "DROP TABLE IF EXISTS EMP_RND" );
    EXEC SQL EXECUTE IMMEDIATE :sSqlStmt;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    sprintf(sSqlStmt, "CREATE TABLE EMP_RND (\n"
            "EMPNO NUMBER(4) CONSTRAINT PK_EMP_RND PRIMARY KEY,\n"
            "ENAME VARCHAR2(10),\n"
            "JOB VARCHAR2(9),\n"
            "SAL NUMBER(7,2),\n"
            "DEPTNO NUMBER(2) )\n" );
    EXEC SQL EXECUTE IMMEDIATE :sSqlStmt;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    sprintf(sSqlStmt, "INSERT INTO EMP_RND\n"
            "SELECT *\n"
            "FROM   EMP\n"
            "WHERE  JOB = 'RND'\n" );
    EXEC SQL EXECUTE IMMEDIATE :sSqlStmt;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    sprintf(sSqlStmt, "DROP TABLE IF EXISTS EMP_SUPPORT" );
    EXEC SQL EXECUTE IMMEDIATE :sSqlStmt;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    sprintf(sSqlStmt, "CREATE TABLE EMP_SUPPORT (\n"
            "EMPNO NUMBER(4) CONSTRAINT PK_EMP_SUPPORT PRIMARY KEY,\n"
            "ENAME VARCHAR2(10),\n"
            "JOB VARCHAR2(9),\n"
            "SAL NUMBER(7,2),\n"
            "DEPTNO NUMBER(2) )\n" );
    EXEC SQL EXECUTE IMMEDIATE :sSqlStmt;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    sprintf(sSqlStmt, "INSERT INTO EMP_SUPPORT\n"
            "SELECT *\n"
            "FROM   EMP\n"
            "WHERE  JOB = 'SUPPORT'\n" );
    EXEC SQL EXECUTE IMMEDIATE :sSqlStmt;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    EXEC SQL ROLLBACK WORK;
 
    return FAILURE;
}
```

- Drop table

```
int DropEmpTempTable()
{
    EXEC SQL DROP TABLE EMP_RND;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL DROP TABLE EMP_SUPPORT;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    EXEC SQL ROLLBACK WORK;
 
    return FAILURE;
}
 
int UpdateSalary(char *aJob, int aBound, double aRatio)
{
    EXEC SQL BEGIN DECLARE SECTION;
    Record       sRecord;
    char         sSelectSql[128];
    char         sUpdateSql[128];
    int          sBound = aBound;
    double       sRatio = aRatio;
    EXEC SQL END DECLARE SECTION;
 
    int  sRecordCount = 0;
    int  i;
    int  sIsOpenCur = 0;
 
    sprintf( sSelectSql, "SELECT EMPNO, ENAME, JOB, SAL FROM EMP_%s WHERE sal < :v1 FOR UPDATE", aJob );
    sprintf( sUpdateSql, "UPDATE EMP_%s SET sal = sal * :v1 WHERE CURRENT OF DYN_CUR", aJob);
 
    EXEC SQL PREPARE SELECT_STMT FROM :sSelectSql;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL DECLARE DYN_CUR KEYSET CURSOR FOR SELECT_STMT;
    EXEC SQL OPEN DYN_CUR USING :sBound;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    sIsOpenCur = 1;
 
    EXEC SQL PREPARE UPDATE_STMT FROM :sUpdateSql;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    while( 1 )
    {
        EXEC SQL
            FETCH NEXT DYN_CUR
            INTO  :sRecord;
        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            goto fail_exit;
        }
 
        EXEC SQL EXECUTE UPDATE_STMT USING :sRatio;
        if(sqlca.sqlcode != 0)
        {
            goto fail_exit;
        }
    }
 
    sIsOpenCur = 0;
    EXEC SQL CLOSE DYN_CUR;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    sprintf( sSelectSql, "SELECT EMPNO, ENAME, JOB, SAL FROM EMP_%s ORDER BY SAL DESC", aJob );
    EXEC SQL PREPARE SELECT_STMT FROM :sSelectSql;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL OPEN DYN_CUR;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    sIsOpenCur = 1;
 
    printf("%s salary list\n", aJob);
    sRecordCount = 0;
    printf(" EMPNO    ENAME                JOB       SALARY\n");
    printf("====== ==================== ========== ==========\n");
    while( 1 )
    {
        EXEC SQL
            FETCH DYN_CUR
            INTO  :sRecord;
        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
            goto fail_exit;
        }
 
        for(i = 0; i < sqlca.sqlerrd[2]; i ++)
        {
            sRecordCount ++;
            printf("%6d %20s %10s %10s\n",
                   sRecord.mEmpNo,
                   sRecord.mEName.arr,
                   sRecord.mJob,
                   sRecord.mSalary);
        }
    }
 
    printf("====== ==================== ========== ==========\n");
    printf("Record Count = %d\n", sRecordCount);
    printf("====== ==================== ========== ==========\n");
 
    sIsOpenCur = 0;
    EXEC SQL CLOSE DYN_CUR;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");

    if(sIsOpenCur == 1)
    {
        EXEC SQL CLOSE DYN_CUR;
    }
    return FAILURE;
}
```

<a id="a642155c111f3d59"></a>
### Multi-threaded Application

Multi-threaded application이란 하나의 process 안에서 다수의 실행 단위를 갖도록 작성된 응용 프로그램이다. Multi-threaded application은 여러 개의 응용 프로그램을 동시에 실행하는 것처럼 여러 개의 작업을 병렬로 처리할 수 있으며 하나의 process이기 때문에 동일한 주소 영역을 공유할 수 있다는 장점이 있다.

동일한 주소 영역을 공유한다는 것은 global 변수와 static 변수를 공유한다는 의미이므로 이러한 변수들에 접근할 때는 각 thread에서 이들에 대한 동시성 제어를 감안해서 접근할 수 있도록 응용 프로그램을 작성할 때 주의를 기울여야 한다.

GOLDILOCKS에서는 이를 위해 run-time context를 제공하고 있으며 run-time context는 Direct Attach (D/A) 모드와 Client/Server (C/S) 모드에서 약간의 차이점이 있다. 다음 장에서는 run-time context와 multi-threaded application을 작성하는 guideline에 대해 설명한다.

<a id="0d93c7c8e227f405"></a>
#### Run-time Context

GOLDILOCKS의 embedded SQL에서 run-time context는 응용 프로그램에서 GOLDILOCKS로의 connection을 관리하기 위해 사용된다. Run-time context와 connection은 1 : 1 대응 관계를 가지며 run-time context를 connection 자체로 보아도 무방하다.

GOLDILOCKS는 구조적으로 D/A 모드에서 하나의 thread에 하나의 connection만 허용하므로 다수의 connection을 사용하려면 응용 프로그램을 multi-thread로 작성해야만 한다. 물론 C/S 모드는 network를 통한 server와의 connection이므로 하나의 thread에서 다수의 connection을 가질 수도 있다.

<a id="838a4033b1854952"></a>
##### Direct Attach (D/A) 모드

D/A 모드로 동작할 때는 한 개의 thread가 한 개의 connection만 가질 수 있다. 따라서 n개의 connection을 소유한 응용 프로그램을 작성할 때는 n개의 thread로 작동시켜야 한다.

<a id="98806e1a69555c81"></a>
![D/A 모드에서 각 thread가 각자의 connection을 가지는 경우](../assets/images/413a838efa72749b.png)

<a id="f7d1329720110ac6"></a>
##### Client/Server (C/S) 모드

C/S 모드로 동작할 때는 connection에 대한 별도의 제약이 없다. 한 개의 thread가 다수의 connection을 가질 수도 있고, 다수의 thread가 한 개의 connection을 공유할 수도 있다. 물론, n개의 thread가 m개의 connection을 공유할 수도 있다.

<a id="03bea7b70d9d4a6f"></a>
![다수의 thread가 한 개의 connection을 공유하는 경우](../assets/images/0ba2aa6040fc1365.png)

<a id="487ca2126d427152"></a>
![한 개의 thread가 다수의 connection을 갖는 경우](../assets/images/f823114d1eab9d83.png)

<a id="2025b75bdcf23fa8"></a>
#### Guideline

Multi-threaded application을 작성할 때는 다음 사항들을 고려해야 한다.

- SQLCA 변수를 thread-safe하게 선언한다. 각 thread 내에서 stack 변수로 선언하는 방법이 권장되며 그 예는 다음 단락의 example program을 참조한다.
- Multi-thread는 하나의 process 내에서 동일한 주소 영역을 갖기 때문에 static 변수나 global 변수를 공유한다. 따라서 이러한 변수들을 사용할 때 응용 프로그램에서 동시성 제어를 고려해야 한다.
- 하나의 run-time context를 여러 thread에서 동시에 사용하지 못하도록 해야 한다. 즉, run-time context를 사용할 때의 동시성 제어도 고려해야 한다.

<a id="743939564a49f527"></a>
#### Example Program

다음은 multi-threaded application의 sample 프로그램이다.

```
/*
 * thread1.gc
 *
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <pthread.h>
 
EXEC SQL INCLUDE SQLCA;
 
#define  SUCCESS  0
#define  FAILURE  -1
 
#define  PRINT_SQL_ERROR(aMsg)                                      \
    {                                                               \
        printf("\n");                                               \
        printf(aMsg);                                               \
        printf("\nSQLCODE : %d\nSQLSTATE : %s\nERROR MSG : %s\n",   \
               sqlca.sqlcode,                                       \
               SQLSTATE,                                            \
               sqlca.sqlerrm.sqlerrmc );                            \
    }
 
int Connect(sql_context aCtx, char *aHostInfo, char *aUserID, char *sPassword);
int CreateEmpTempTable();
int DropEmpTempTable();
void *clientThread(void *args);
 
typedef struct thread_param
{
    int    mNo;
    char  *mJobName;
} thread_param;
 
#define  THREAD_COUNT    2

char gJobName[THREAD_COUNT][20]= {
    "RND",
    "SUPPORT"
};
 
int main(int argc, char **argv)
{
    EXEC SQL BEGIN DECLARE SECTION;
    int          sEmpNo;
    varchar      sEName[20 + 1];
    char         sJob[20];
    long         sSalary;
    EXEC SQL END DECLARE SECTION;
    int          sRecordCount = 0;
    pthread_t    thread_id[THREAD_COUNT];
    thread_param param[THREAD_COUNT];
    int          i;
 
    printf("Connect GOLDILOCKS ...\n");
    if(Connect(NULL, "DSN=GOLDILOCKS", "test", "test") != SUCCESS)
    {
        goto fail_exit;
    }
 
    if(CreateEmpTempTable() != SUCCESS)
    {
        goto fail_exit;
    }
```

- Create client thread

```
for( i = 0; i < THREAD_COUNT; i ++ )
    {
        param[i].mNo = i;
        param[i].mJobName = gJobName[i];
        if( pthread_create(&thread_id[i],
                           NULL,
                           clientThread,
                           &param[i]) != 0 )
        {
            printf( "Can't create thread %d!\n", i );
        }
        else
        {
            printf( "Create thread %d!\n", i );
        }
    }
 
    for( i = 0; i < THREAD_COUNT; i ++ )
    {
        if( pthread_join(thread_id[i],
                         NULL) != 0 )
        {
            printf( "Error when waiting for thread %d to terminate!\n", i );
        }
        else
        {
            printf( "Stopped thread %d!\n", i );
        }
    }
```

- Retrieve employee

```
EXEC SQL
        DECLARE EMP_CUR CURSOR FOR
        SELECT empno, ename, job, sal
        FROM   EMP_TEMP
        ORDER BY empno;
 
    EXEC SQL OPEN EMP_CUR;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf(" EMPNO    ENAME                JOB      SALARY\n");
    printf("====== ==================== ========== ========\n");
    while( 1 )
    {
        EXEC SQL
            FETCH EMP_CUR
            INTO  :sEmpNo, :sEName, :sJob, :sSalary;
        if(sqlca.sqlcode == SQL_NO_DATA)
        {
            break;
        }
        else if(sqlca.sqlcode != 0)
        {
            PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
            goto fail_exit;
        }
 
        sRecordCount ++;
 
        printf("%6d %20s %10s %8ld\n",
               sEmpNo, sEName.arr, sJob, sSalary);
    }
 
    printf("====== ==================== ========== ========\n");
    printf("Record Count = %d\n", sRecordCount);
    printf("====== ==================== ========== ========\n");
 
    EXEC SQL CLOSE EMP_CUR;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    if(DropEmpTempTable() != SUCCESS)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK RELEASE;
    if(sqlca.sqlcode != 0)
    {
        PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
        goto fail_exit;
    }
 
    printf("SUCCESS\n");
    printf("############################\n");
 
    return 0;
 
  fail_exit:
 
    printf("FAILURE\n");
    printf("############################\n\n");
    EXEC SQL ROLLBACK WORK RELEASE;
 
    return 0;
}
 
int Connect(sql_context aCtx, char *aHostInfo, char *aUserID, char *sPassword)
{
    EXEC SQL BEGIN DECLARE SECTION;
    VARCHAR  sUid[80];
    VARCHAR  sPwd[20];
    VARCHAR  sConnStr[1024];
    EXEC SQL END DECLARE SECTION;
    struct sqlca sqlca;
```

- Log on GOLDILOCKS

```
strcpy((char *)sUid.arr, aUserID);
sUid.len = (short)strlen((char *)sUid.arr);
strcpy((char *)sPwd.arr, sPassword);
sPwd.len = (short)strlen((char *)sPwd.arr);
strcpy((char *)sConnStr.arr, aHostInfo);
sConnStr.len = (short)strlen((char *)sConnStr.arr);
```

- DB 연결

```
if( aCtx != NULL )
    {
        EXEC SQL CONTEXT USE :aCtx;
        EXEC SQL CONNECT :sUid IDENTIFIED BY :sPwd USING :sConnStr;
    }
    else
    {
        EXEC SQL CONTEXT USE DEFAULT;
        EXEC SQL CONNECT :sUid IDENTIFIED BY :sPwd USING :sConnStr;
    }

    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] Connection Failure!");
 
    return FAILURE;
}
```

- DB 연결 해제

```
int Disconnect(sql_context aCtx)
{
    struct sqlca sqlca;
    if( aCtx != NULL )
    {
        EXEC SQL CONTEXT USE :aCtx;
        EXEC SQL DISCONNECT;
    }
    else
    {
        EXEC SQL CONTEXT USE DEFAULT;
        EXEC SQL DISCONNECT;
    }
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] Connection Failure!");
 
    return FAILURE;
}
```

- Create table

```
int CreateEmpTempTable()
{
    EXEC SQL DROP TABLE IF EXISTS EMP_TEMP;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL
        CREATE TABLE EMP_TEMP (
            EMPNO NUMBER(4) CONSTRAINT PK_EMP_TEMP PRIMARY KEY,
            ENAME VARCHAR2(10),
            JOB VARCHAR2(9),
            SAL NUMBER(7,2),
            DEPTNO NUMBER(2) );
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    EXEC SQL ROLLBACK WORK;
 
    return FAILURE;
}
```

- Drop table

```
int DropEmpTempTable()
{
    EXEC SQL DROP TABLE EMP_TEMP;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    return SUCCESS;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    EXEC SQL ROLLBACK WORK;
 
    return FAILURE;
}
 
void *clientThread(void *args)
{
    EXEC SQL BEGIN DECLARE SECTION;
    SQL_CONTEXT   my_context;
    char          job_name[20 + 1];
    EXEC SQL END DECLARE SECTION;
    int           state = 0;
    thread_param *param = (thread_param *)args;
 
    EXEC SQL CONTEXT ALLOCATE :my_context;
    state = 1;
 
    EXEC SQL CONTEXT USE :my_context;
    if(Connect(my_context, "DSN=GOLDILOCKS", "test", "test") != SUCCESS)
    {
        goto fail_exit;
    }
    state = 2;
 
    strcpy( job_name, param->mJobName );
 
    EXEC SQL
        INSERT INTO EMP_TEMP
        SELECT *
        FROM   EMP
        WHERE  JOB = :job_name;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
 
    EXEC SQL COMMIT WORK;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    state = 1;

    if(Disconnect(my_context) != SUCCESS)
    {
        goto fail_exit;
    }
    state = 0;

    EXEC SQL CONTEXT FREE :my_context;
    pthread_exit(0);

    return NULL;
 
  fail_exit:
 
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    switch(state)
    {
        case 2:
            (void)Disconnect(my_context);
        case 1:
            EXEC SQL CONTEXT FREE :my_context;
            break;
        default:
            break;
    }
 
    pthread_exit(0);

    return NULL;
}
```

<a id="60eefdbbcb93ab73"></a>
### Multi-process Application

Multi-process application이란 하나의 process를 이용해서 다수의 process를 생성하여 실행하도록 작성된 응용 프로그램이다.

GOLDILOCKS embedded SQL은 multi-process application을 지원하지 않는다. Multi-process application을 작성할 때는 fork 함수를 사용한다. fork 함수를 호출한 후에 새로운 프로그램을 실행하는 것이 아니고 기존 작업을 이어서 실행하는 응용 프로그램이라면 다음 내용을 인지하고 주의해야 한다.

- 부모 프로세스에서 연결된 context는 fork 후 자식 프로세스에게 복사 되기 때문에 어떠한 문제가 발생할지 예측하기 어렵다.
- OS 마다 세마포어 관리 정책이 다르다. 부모 프로세스에서 생성된 세마포어를 부모, 자식 프로세스에서 이중으로 정리하는 것을 허용하지 않는 OS가 있다.

만약 multi-process application을 작성할 경우 어떠한 connection도 맺지 않은 상태에서 fork 해야 한다. 또한 해당 OS의 세마포어 관리 정책도 확인해야 한다.

<a id="867a751f8927dc6f"></a>
### C++ Application

<a id="6b50f637d2f138fd"></a>
#### Output Filename의 확장자

GOLDILOCKS의 precompiler (gpec)은 embedded SQL 소스 코드를 precompile하여 C 코드를 생성한다. 따라서 출력 파일의 확장자는 기본적으로 .c가 된다. 일반적인 C++ 소스 코드는 compiler의 종류에 따라 다양한 형태의 파일 확장자를 갖는다.

이렇게 파일 확장자를 원하는 것으로 출력하고 싶은 경우 gpec의 출력 파일 지정 옵션인 -o를 사용한다. 예를 들어, testfile.gc를 testfile.cpp로 변환하려면 다음과 같이 실행한다.

```
gpec $(GPEC_OPT) testfile.gc -o testfile.cpp
```

<a id="2904a6a0d2a76ab6"></a>
#### SQLCA_STORAGE_CLASS

C++ application에서 동일한 symbol을 global 변수로 선언한 경우, symbol에 대한 충돌이 발생한다. GOLDILOCKS의 embedded SQL에서는 default로 sqlca 변수를 가지고 있는데 다수의 C++ file을 link 할 때 이 변수의 충돌이 문제가 된다.

이를 피하기 위해 하나의 파일을 제외한 나머지 모든 파일들에 SQLCA_STORAGE_CLASS 매크로를 정의해야 한다. 가령 세 개의 파일들을 링크하여 응용 프로그램을 만들면 세 개 중에 두 개의 파일에 다음과 같이 SQLCA_STORAGE_CLASS 매크로를 정의한다.

```
#define SQLCA_STORAGE_CLASS extern
EXEC SQL INCLUDE SQLCA;
```

SQLCA_STORAGE_CLASS 매크로 정의는 반드시 다음 문장의 앞에 위치해야 한다.

```
EXEC SQL INCLUDE SQLCA;
```

<a id="b61c4bafb33460da"></a>
### XA

<a id="ff04aadfa8705061"></a>
#### xa_open string 정의

xa_open string은 Resource Manager (RM)에 접속하기 위한 정보를 포함하고 있는데 자세한 내용은 [SQLDriverConnect 인자설명](29-odbc.md#70e5ae82c9309412)을 참조한다.

다음은 xa_open string의 예이다.

```
DSN=GOLDILOCKS;UID=test;PWD=test;CONN_NAME=XA_CONN
```

<a id="5ded3b82b2cd8e27"></a>
#### Precompiler에서 XA 사용

Precompiler에서 XA를 사용할 때 다음 중 하나를 선택할 수 있다.

- Default connection을 사용
- Named connection을 사용

<a id="19a7a5da9aa12431"></a>
##### Default Connection 사용

xa_open string에 접속 정보만을 가지고 맺어진 connection을 사용한다.   
다음은 default connection을 위한 xa_open string의 예이다.

```
DSN=GOLDILOCKS;UID=test;PWD=test
```

Default connection을 사용한 embedded SQL을 사용할 때는 다음과 같은 형태로 기술한다.

```
EXEC SQL
        UPDATE Deposit
        Set InterestRates = :value :value_ind
        WHERE AccountNumber = :account_number;
```

> XA를 default context로 사용하려면 xa open 전 default context에 어떤 connection도 없어야 한다.  
> CONN_NAME이 없는 xa_open string으로 XA connection을 여러 개 생성하지 말아야 한다. CONN_NAME이 없는 connection을 여러 개 생성하면 가장 먼저 생성된 connection이 default context와 짝지어진다.

<a id="5042d60bc983fe07"></a>
##### Named Connection 사용

xa_open string에 접속 정보와 함께 connection 이름을 사용한다.   
Named connection을 위한 xa_open string의 예는 다음과 같다.

```
DSN=GOLDILOCKS;UID=test;PWD=test;CONN_NAME=XA_CONN
```

Named connection을 사용한 embedded SQL에서는 다음과 같이 connection 이름을 기술해 주어야 한다.

```
EXEC SQL AT XA_CONN
        UPDATE Deposit
        Set InterestRates = :value :value_ind
        WHERE AccountNumber = :account_number;
```

<a id="311f55ff158ae784"></a>
#### Example Program

• GOLDILOCKS Sample - XA

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
```

• Include GOLDILOCKS ODBC header

```
#include <goldilocks.h>

EXEC SQL INCLUDE SQLCA;
#define  SUCCESS  0
#define  FAILURE  -1

#define  PRINT_SQL_ERROR(aMsg)                                      \
    {                                                               \
        printf("\n");                                               \
        printf(aMsg);                                               \
        printf("\nSQLCODE : %d\nSQLSTATE : %s\nERROR MSG : %s\n",   \
               sqlca.sqlcode,                                       \
               SQLSTATE,                                            \
               sqlca.sqlerrm.sqlerrmc );                            \
    }
```

• User-specific definitions

```
#define  BUF_LEN 101
#define GOLDILOCKS_SQL_THROW( aLabel )               \
    goto aLabel;
#define GOLDILOCKS_SQL_TRY( aExpression )            \
    do                                          \
    {                                           \
        if( !(SQL_SUCCEEDED( aExpression ) ) )  \
        {                                       \
            goto GOLDILOCKS_FINISH_LABEL;            \
        }                                       \
    } while( 0 )
#define GOLDILOCKS_FINISH                           \
    goto GOLDILOCKS_FINISH_LABEL;                   \
    GOLDILOCKS_FINISH_LABEL:
```

• Print diagnostic record to console

```
void PrintDiagnosticRecord( SQLSMALLINT aHandleType, SQLHANDLE aHandle )
{
    SQLCHAR       sSQLState[6];
    SQLINTEGER    sNaiveError;
    SQLSMALLINT   sTextLength;
    SQLCHAR       sMessageText[SQL_MAX_MESSAGE_LENGTH];
    SQLSMALLINT   sRecNumber = 1;
    SQLRETURN     sReturn;
```

• SQLGetDiagRec returns the current values which includes an error, warning.

```
while( 1 )
    {
        sReturn = SQLGetDiagRec( aHandleType,
                                 aHandle,
                                 sRecNumber,
                                 sSQLState,
                                 &sNaiveError,
                                 sMessageText,
                                 100,
                                 &sTextLength );
        if( sReturn == SQL_NO_DATA )
        {
            break;
        }
        GOLDILOCKS_SQL_TRY( sReturn );
        printf("\n=============================================\n" );
        printf("SQL_DIAG_SQLSTATE     : %s\n", sSQLState );
        printf("SQL_DIAG_NATIVE       : %d\n", sNaiveError );
        printf("SQL_DIAG_MESSAGE_TEXT : %s\n", sMessageText );
        printf("=============================================\n" );
        sRecNumber++;
    }
    return;
    GOLDILOCKS_FINISH;
    printf("SQLGetDiagRec failure.\n" );
    return;
}
```

• Create table

```
int testCreateTable()
{
    EXEC SQL AT XA_CONN
        DROP TABLE IF EXISTS DEPOSIT;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    EXEC SQL AT XA_CONN
        CREATE TABLE DEPOSIT (
            NAME          VARCHAR(30),
            BALANCE       INTEGER,
            ACCOUNTNUMBER VARCHAR(100),
            ACCOUNTDAY    DATE,
            INTERESTRATES NUMBER(10, 5),
            PHONENUMBER   VARCHAR(30) );
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    EXEC SQL AT XA_CONN COMMIT;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    return SUCCESS;
  fail_exit:
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    EXEC SQL AT XA_CONN ROLLBACK;
    return FAILURE;
}
```

• Drop table

```
int testDropTable()
{
    EXEC SQL AT XA_CONN
        DROP TABLE DEPOSIT;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    EXEC SQL AT XA_CONN COMMIT;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
    return SUCCESS;
  fail_exit:
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    EXEC SQL AT XA_CONN ROLLBACK;
    return FAILURE;
}
```

• Insert function

```
int testInsert( )
{
    EXEC SQL BEGIN DECLARE SECTION;
    char             sName[BUF_LEN];
    int              sNameInd                    = 0;
    int              sBalance                    = 0;
    int              sBalanceInd                 = 0;
    char             sAccountNumber[BUF_LEN];
    int              sAccountNumberInd           = 0;
    DATE             sAccountDay;
    int              sAccountDayInd              = 0;
    double           sInterestRates              = 0;
    int              sInterestRatesInd           = 0;
    char             sPhoneNumber[BUF_LEN];
    int              sPhoneNumberInd             = 0;
    EXEC SQL END DECLARE SECTION;
    sNameInd              = snprintf( (char*)sName, BUF_LEN, "sunje" );
    sBalance              = 30000000;
    sAccountNumberInd     = snprintf( (char*)sAccountNumber, BUF_LEN, "9999-99-9999" );
    sAccountDay.year      = 2009;
    sAccountDay.month     = 1;
    sAccountDay.day       = 1;
    sAccountDay.hour      = 0;
    sAccountDay.minute    = 0;
    sAccountDay.second    = 0;
    sAccountDay.fraction  = 0;
    sInterestRates        = (double)5.0;
    sPhoneNumberInd       = snprintf( (char*)sPhoneNumber, BUF_LEN, "010-9999-9999" );
    EXEC SQL AT XA_CONN
        INSERT INTO DEPOSIT
        VALUES ( :sName :sNameInd,
                 :sBalance :sBalanceInd,
                 :sAccountNumber :sAccountNumberInd,
                 :sAccountDay :sAccountDayInd,
                 :sInterestRates :sInterestRatesInd,
                 :sPhoneNumber :sPhoneNumberInd );
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
```

• The number of rows affected by INSERT statement

```
printf("\n%d row created.\n\n", sqlca.sqlerrd[2] );
    return SUCCESS;
  fail_exit:
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    return FAILURE;
}
```

• Update function

```
int testUpdate( )
{
    EXEC SQL BEGIN DECLARE SECTION;
    char     sCondition[BUF_LEN];
    int      sConditionInd           = 0;
    double   sValue                  = 0;
    int      sValueInd               = 0;
    EXEC SQL END DECLARE SECTION;
    sValue        = (SQLREAL)6.0;
    sConditionInd = snprintf( (char*)sCondition,
                              BUF_LEN,
                              "9999-99-9999" );
    EXEC SQL AT XA_CONN
        UPDATE Deposit
        Set InterestRates = :sValue :sValueInd
        WHERE AccountNumber = :sCondition :sConditionInd;
    if(sqlca.sqlcode != 0)
    {
        goto fail_exit;
    }
```

• The number of rows affected by UPDATE statement

```
printf("\n%d row updated.\n\n", sqlca.sqlerrd[2] );
    return SUCCESS;
  fail_exit:
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    return FAILURE;
}
```

• Select function

```
int testSelect( )
{
    EXEC SQL BEGIN DECLARE SECTION;
    char             sName[BUF_LEN];
    int              sNameInd                    = 0;
    int              sBalance                    = 0;
    int              sBalanceInd                 = 0;
    char             sAccountNumber[BUF_LEN];
    int              sAccountNumberInd           = 0;
    DATE             sAccountDay;
    int              sAccountDayInd              = 0;
    double           sInterestRates              = 0;
    int              sInterestRatesInd           = 0;
    char             sPhoneNumber[BUF_LEN];
    int              sPhoneNumberInd             = 0;
    EXEC SQL END DECLARE SECTION;
    int              sCount                      = 0;
    int              sIsOpen                     = 0;
    EXEC SQL DECLARE CUR1 CURSOR FOR
        SELECT NAME, BALANCE, ACCOUNTNUMBER, ACCOUNTDAY, INTERESTRATES, PHONENUMBER
        FROM DEPOSIT;
    EXEC SQL AT XA_CONN
        OPEN CUR1;
    if( sqlca.sqlcode != 0 )
    {
        goto fail_exit;
    }
    sIsOpen = 1;
    printf( "==========================================\n" );
    while( 1 )
    {
        EXEC SQL AT XA_CONN
            FETCH CUR1 INTO
            :sName :sNameInd,
            :sBalance :sBalanceInd,
            :sAccountNumber :sAccountNumberInd,
            :sAccountDay :sAccountDayInd,
            :sInterestRates :sInterestRatesInd,
            :sPhoneNumber :sPhoneNumberInd;
        if( sqlca.sqlcode == SQL_NO_DATA )
        {
            break;
        }
        else if( sqlca.sqlcode != 0 )
        {
            goto fail_exit;
        }
        printf( "NAME          : " );
        if( sNameInd == -1 )
        {
            printf( "(null)" );
        }
        else
        {
            printf( "%s", sName );
        }
        printf( "\n" );
        printf( "BALANCE       : " );
        if( sBalanceInd == -1 )
        {
            printf( "(null)" );
        }
        else
        {
            printf( "%d", sBalance );
        }
        printf( "\n" );
        printf( "ACCOUNTNUMBER : " );
        if( sAccountNumberInd == -1 )
        {
            printf( "(null)" );
        }
        else
        {
            printf( "%s", sAccountNumber );
        }
        printf( "\n" );
        printf( "ACCOUNTDAY    : " );
        if( sAccountDayInd == -1 )
        {
            printf( "(null)" );
        }
        else
        {
            printf( "%4d-%02d-%02d", sAccountDay.year, sAccountDay.month, sAccountDay.day);
        }
        printf( "\n" );
        printf( "INTERESTRATES : " );
        if( sInterestRatesInd == -1 )
        {
            printf( "(null)" );
        }
        else
        {
            printf( "%lf", sInterestRates );
        }
        printf( "\n" );
        printf( "PHONENUMBER   : " );
        if( sPhoneNumberInd == -1 )
        {
            printf( "(null)" );
        }
        else
        {
            printf( "%s", sPhoneNumber );
        }
        printf( "\n" );
        printf( "------------------------------------------\n" );
        sCount ++;
    }
    printf( "==========================================\n" );
    printf( "\n%d rows selected.\n\n", sCount );
    sIsOpen = 0;
    EXEC SQL AT XA_CONN
        CLOSE CUR1;
    if( sqlca.sqlcode != 0 )
    {
        goto fail_exit;
    }
    return SUCCESS;
  fail_exit:
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    if( sIsOpen == 1 )
    {
        EXEC SQL AT XA_CONN
            CLOSE CUR1;
    }
    return FAILURE;
}
```

• Delete function

```
int testDelete( )
{
    EXEC SQL BEGIN DECLARE SECTION;
    char     sCondition[BUF_LEN];
    int      sConditionInd           = 0;
    EXEC SQL END DECLARE SECTION;
    sConditionInd = snprintf( (char*)sCondition,
                              BUF_LEN,
                              "9999-99-9999" );
    EXEC SQL AT XA_CONN
        DELETE FROM DEPOSIT WHERE AccountNumber = :sCondition :sConditionInd;
    if( sqlca.sqlcode != 0 )
    {
        goto fail_exit;
    }
```

• The number of rows affected by DELETE statement

```
printf("\n%d row deleted.\n\n", sqlca.sqlerrd[2] );
    return SUCCESS;
  fail_exit:
    PRINT_SQL_ERROR("[ERROR] SQL ERROR -");
    return FAILURE;
}
```

• Start function

```
int main( int aArgc, char** aArgv )
{
    SQLHENV       sEnv    = NULL;
    SQLINTEGER    sState  = 0;
    xa_switch_t * sXaSwitch;
    XID           sXid;
    sXaSwitch = SQLGetXaSwitch();
```

• If a user calls SQLAllocEnv() which is included in GOLDILOCKS ODBC

```
GOLDILOCKS_SQL_TRY( SQLAllocHandle( SQL_HANDLE_ENV,
                                   NULL,
                                   &sEnv ) );
    sState = 1;
```

• SQLSetEnvAttr sets attributes which controls aspects of environments.

```
GOLDILOCKS_SQL_TRY( SQLSetEnvAttr( sEnv,
                                  SQL_ATTR_ODBC_VERSION,
                                  (SQLPOINTER)SQL_OV_ODBC3,
                                  0 ) );
    if( (sXaSwitch->xa_open_entry)( "DSN=GOLDILOCKS;UID=test;PWD=test;CONN_NAME=XA_CONN", 0, TMNOFLAGS ) != XA_OK )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
    sState = 2;
    sXid.formatID = 0;
    sXid.gtrid_length = 2;
    sXid.bqual_length = 1;
    memcpy( sXid.data, "100", sXid.gtrid_length + sXid.bqual_length );
```

• Create table

```
if( testCreateTable() != SUCCESS )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
    sState = 3;
    if( (sXaSwitch->xa_start_entry)( &sXid, 0, TMNOFLAGS ) != XA_OK )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
    sState = 4;
```

• Insert row

```
if( testInsert() != SUCCESS )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
```

• Update row

```
if( testUpdate() != SUCCESS )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
```

• Select row

```
if( testSelect() != SUCCESS )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
```

• Delete row

```
if( testDelete() != SUCCESS )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
    sState = 3;
    if( (sXaSwitch->xa_end_entry)( &sXid, 0, TMSUCCESS ) != XA_OK )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
    if( (sXaSwitch->xa_prepare_entry)( &sXid, 0, TMNOFLAGS ) != XA_OK )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
    if( (sXaSwitch->xa_commit_entry)( &sXid, 0, TMNOFLAGS ) != XA_OK )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
    sState = 2;
```

• Drop table

```
if( testDropTable() != SUCCESS )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
    sState = 1;
    if( (sXaSwitch->xa_close_entry)( "", 0, TMNOFLAGS ) != XA_OK )
    {
        GOLDILOCKS_SQL_THROW( GOLDILOCKS_FINISH_LABEL );
    }
```

• SQLFreeHandleEnv releases resources related to the environment.

```
sState = 0;
    GOLDILOCKS_SQL_TRY( SQLFreeHandle( SQL_HANDLE_ENV,
                                  sEnv ) );
    sEnv = NULL;
    return EXIT_SUCCESS;
    GOLDILOCKS_FINISH;
    if( sEnv != NULL)
    {
        PrintDiagnosticRecord( SQL_HANDLE_ENV, sEnv );
    }
    switch( sState )
    {
        case 4:
            (void)(sXaSwitch->xa_end_entry)( &sXid, 0, TMSUCCESS );
            (void)(sXaSwitch->xa_prepare_entry)( &sXid, 0, TMNOFLAGS );
            (void)(sXaSwitch->xa_commit_entry)( &sXid, 0, TMNOFLAGS );
        case 3:
            (void)testDropTable();
        case 2:
            (void)(sXaSwitch->xa_close_entry)( "", 0, TMNOFLAGS );
        case 1:
            (void)SQLFreeHandle( SQL_HANDLE_ENV, sEnv );
            sEnv = NULL;
        default:
            break;
    }
    return EXIT_FAILURE;
}
```

<a id="1d6fc4c45ec38db5"></a>
## Embedded SQL Reference

본 장에서는 GOLDILOCKS의 embedded SQL 응용 프로그램에서만 사용할 수 있는 SQL 문에 대해 설명한다. 소스 코드 상에서 embedded SQL 문을 다룰 때는 반드시 다음 문법을 따른다.

```
<statement> ::= EXEC SQL <exec sql statement>;
<exec sql statement> ::=
      <embedded SQL statement>
    | <embedded get group_id statement>
    | <embedded specific statement>
    ;
 
<embedded SQL statement> ::=
    [ AT <db_name> ] [ ATOMIC ] [ FOR <iteration_count> ] <sql statement>
    ;
<embedded get group_id statement> ::=
    [ AT <db_name> ]  <get group_id statement> <sql statement>

<embedded specific statement> ::=
      <autocommit statement>
    | <declare section statement>
    | <include statement>
    | <exception statement>
    | <context statement>
    | <option statement>
    ;
 
<autocommit statement> ::= [ AT <db_name> ] AUTOCOMMIT { ON | OFF };
<declare section statement> ::= { BEGIN | END } DECLARE SECTION;
<include statement> ::= INCLUDE { SQLCA | <identifier> };
<exception statement> ::= WHENEVER <exception_condition> <exception_action>;
<context statement> ::= CONTEXT <context action>;
<context action> ::=
      ALLOCATE :context_name
    | FREE :context_name
    | USE :context_name
    | USE DEFAULT
    ;
<option statement> ::= OPTION ( <option> );
<get group_id statement> :: GET GROUPID INTO :group_id;
```

<a id="fed87ddf09a60d2e"></a>
### EXEC SQL AT

<a id="e4577c11043b225a"></a>
#### 기능

Embedded SQL 문에 적용할 connection 이름을 지정한다.

<a id="e6ca6ec71053e4b7"></a>
#### 구문

```
EXEC SQL [ AT <db_name> ] ...

<db_name> ::=
      <identifier>
    | :hostvar
    ;
```

<a id="e80d8271ed8d8516"></a>
#### 설명

Embedded SQL 응용 프로그램에서 connect 할 때, connection 이름을 지정할 수 있다. 이 이름은 특정 connection을 사용하여 embedded SQL 문을 수행하려 할 때 사용된다.

<a id="239b6ab3006055ca"></a>
#### 사용 예

```
{
    ...
    EXEC SQL AT :conn_name CONNECT :uid IDENTIFIED BY :pwd USING :conn_str;
 
    EXEC SQL AT :conn_name
        UPDATE EMP
        SET    sal = sal * 1.1
        WHERE  JOB = 'SALES';
 
    ...
}
```

<a id="1b7a1c93ab693db6"></a>
#### 참조

관련 내용은 [연결](#657765e09ec6af68)을 참조한다.

<a id="e1a2fc42394dfe8f"></a>
### EXEC SQL ATOMIC INSERT

<a id="4494dd035c3d48c6"></a>
#### 기능

Atomic array insert를 수행한다.

<a id="f1e8145731fc90ea"></a>
#### 구문

```
EXEC SQL ATOMIC <insert_statement>;
```

<a id="668d787f9fa8b53d"></a>
#### 설명

Embedded SQL 응용 프로그램에서 atomic array insert를 수행한다. Atomic array insert는 한 번의 명령으로 다수의 row를 삽입하기 위한 구문으로써 삽입되는 모든 row가 성공을 해야만 성공을 반환하고, row 중에 한 개라도 실패할 경우 전체 row 삽입이 실패한다.   
한 번의 명령으로 삽입되기 때문에 개별적으로 row를 삽입하는 것보다 성능이 좋다.

<a id="916f72b9f521b585"></a>
#### 사용 예

```
{
    EXEC SQL BEGIN DECLARE SECTION;
    int    emp_number[20]; 
    char   emp_name[20][10]; 
    int    dept_number[20]; 
    EXEC SQL END DECLARE SECTION;
```

- emp_number, emp_name, dept_number 값 설정

```
...
```

- emp_number, emp_name, dept_number를 INSERT

```
EXEC SQL ATOMIC INSERT INTO emp (empno, ename, deptno) 
                            VALUES (:emp_number, :emp_name, :dept_number);
}
```

<a id="ee72a2849dc02e6e"></a>
#### 참조

관련 내용은 [Atomic Insert](#9d320ac7d0ed5de2)를 참조한다.

<a id="3b8d53a8e2fe5cab"></a>
### EXEC SQL AUTOCOMMIT

<a id="354692cd166e9b13"></a>
#### 기능

Autocommit 설정을 변경한다.

<a id="ed6e0b91000be24f"></a>
#### 구문

```
EXEC SQL AUTOCOMMIT { ON | OFF };
```

<a id="66119e54034d4395"></a>
#### 설명

Autocommit은 다음과 같이 설정할 수 있다.

<a id="d17166811515565a"></a>
| Flag | 설명 |
| --- | --- |
| ON | Statement를 수행한 후에 자동으로 commit 한다. |
| OFF | 명시적인 commit 문장이 올 때까지 commit 하지 않는다. |

<a id="2930a8d8687ecc3f"></a>
#### 사용 예

```
{
    ...
    EXEC SQL AT :conn_name CONNECT :uid IDENTIFIED BY :pwd USING :conn_str;
 
    EXEC SQL AUTOCOMMIT ON;

    EXEC SQL AT :conn_name
        UPDATE EMP
        SET    sal = sal * 1.1
        WHERE  JOB = 'SALES';
 
    ...
}
```

<a id="c583aeaa665d7f86"></a>
#### 참조

관련 내용은 [Auto Commit](#c6c381bf2c18cec1)을 참조한다.

<a id="f576f4c35ed7bc20"></a>
### EXEC SQL BEGIN DECLARE SECTION

<a id="4bb8b9a1bf895c0e"></a>
#### 기능

Precompiler의 지시자로써 host variable 선언 영역을 지정한다.

<a id="a582fe7e9243582c"></a>
#### 구문

```
EXEC SQL BEGIN DECLARE SECTION;
```

<a id="710d87e10cc5263f"></a>
#### 설명

Host variable 선언 영역을 지정하는 precompiler 지시자로써 항상 EXEC SQL END DECLARE SECTION과 함께 사용된다. Precompiler가 이 문장을 만나면 declare section의 시작으로 판단하고 이후에 나오는 변수 선언을 host variable로 인식하여 처리한다.

<a id="28328c402907e29b"></a>
#### 사용 예

```
{
    EXEC SQL BEGIN DECLARE SECTION;
    int    emp_number[20]; 
    char   emp_name[20][10]; 
    int    dept_number[20]; 
    EXEC SQL END DECLARE SECTION;
 
    ...
}
```

<a id="33152592fa61c60a"></a>
#### 참조

관련 내용은 다음을 참조한다.

- [Host Variable의 선언](#213821c4b5b8df6f)
- [EXEC SQL END DECLARE SECTION](#31ce6cc26a339f60)

<a id="9820843eae10a5c6"></a>
### EXEC SQL COMMIT RELEASE

<a id="f8c9bca3a1338f49"></a>
#### 기능

트랜잭션을 완료한 후에 connection을 종료한다.

<a id="3affcba3d0d98b88"></a>
#### 구문

```
EXEC SQL [ AT <db_name> ] COMMIT [ WORK ] RELEASE;
```

<a id="56b9663c613e0e51"></a>
#### 설명

트랜잭션을 완료한 후에, 현재 connection을 종료한다.

```
EXEC SQL AT :conn_name COMMIT RELEASE;
```

위의 문장은 다음과 동일하다.

```
EXEC SQL AT :conn_name COMMIT;
EXEC SQL AT :conn_name DISCONNECT;
```

<a id="e12c06861a64c50d"></a>
#### 사용 예

```
{
    ...
    EXEC SQL AT :conn_name CONNECT :uid IDENTIFIED BY :pwd USING :conn_str;
 
    EXEC SQL AT :conn_name
        UPDATE EMP
        SET    sal = sal * 1.1
        WHERE  JOB = 'SALES';

    EXEC SQL AT :conn_name COMMIT RELEASE; 
    ...
}
```

<a id="560af04d329528bf"></a>
#### 참조

관련 내용은 [RELEASE Option](#a398dbf14d7ed4af)을 참조한다.

<a id="39d2d9afb3d411d5"></a>
### EXEC SQL CONNECT

<a id="55a55281c9efe24e"></a>
#### 기능

GOLDILOCKS와 connection을 맺는다.

<a id="f089c0f1c0484cff"></a>
#### 구문

```
EXEC SQL [ AT <db_name> ] CONNECT <user_name> IDENTIFIED BY <password> [ AT <db_name> ] [ USING <conn_string> ]

<db_name> ::=
      <identifier>
    | :hostvar
    ;
<user_name> ::=
      <identifier>
    | :hostvar
    ;
<password> ::=
      <identifier>
    | :hostvar
    ;
<conn_string> ::= :hostvar;
```

<a id="c12178fd37f9363f"></a>
#### 설명

GOLDILOCKS에 연결을 설정한다.

<a id="621a1bf82abaa204"></a>
#### 사용 예

```
{
    ...
    EXEC SQL CONNECT :uid IDENTIFIED BY :pwd USING :conn_str;
 
    ...
}
```

<a id="c14e138eedd807be"></a>
#### 참조

관련 내용은 [Database 연결](#05eeaac012850871)을 참조한다.

<a id="87da20388b97653c"></a>
### EXEC SQL CONTEXT ALLOCATE

<a id="f23962130de57c09"></a>
#### 기능

Run-time context 메모리를 할당한다.

<a id="914bb0558d135d79"></a>
#### 구문

```
EXEC SQL CONTEXT ALLOCATE :context;
```

<a id="e67907816c48a362"></a>
#### 설명

Run-time context 메모리를 할당한다. Run-time context를 할당하려면 declare section에 SQL_CONTEXT type의 변수를 선언한 후, 이 변수에 대해서 할당해야 한다. 이 구문은 단지 메모리를 할당하는 역할만 수행하므로 이를 사용하려면 USE를 지정한 뒤에 connect를 수행해야 한다.

<a id="977beca0049def0e"></a>
#### 사용 예

```
{
    ...
    EXEC SQL BEGIN DECLARE SECTION;
    SQL_CONTEXT ctxt;
    EXEC SQL END DECLARE SECTION;

    EXEC SQL CONTEXT ALLOCATE :ctxt;
 
    EXEC SQL CONTEXT USE :ctxt;
    EXEC SQL CONNECT :uid IDENTIFIED BY :pwd USING :conn_str;
 
    EXEC SQL
        UPDATE EMP
        SET    sal = sal * 1.1
        WHERE  JOB = 'SALES';

    EXEC SQL DISCONNECT;
    EXEC SQL CONTEXT FREE :ctxt;
 
    ...
}
```

<a id="20e945b49a2a47b0"></a>
#### 참조

관련 내용은 [SQL_CONTEXT](#5d9a91f46d4c2768)를 참조한다.

<a id="a83db55615470f9f"></a>
### EXEC SQL CONTEXT FREE

<a id="9bd51fbe657c7fa0"></a>
#### 기능

Run-time context 메모리를 해제한다.

<a id="e7e284133d1ceef1"></a>
#### 구문

```
EXEC SQL CONTEXT FREE :context;
```

<a id="997e6d583b5fa504"></a>
#### 설명

Run-time context 메모리를 해제한다. Run-time context를 해제하기 전에는 반드시 disconnect를 하여 더 이상 connection을 사용하지 않도록 해야한다. 그렇지 않으면 예기치 못한 오류가 발생할 수 있다.

<a id="1cc898c3e045b9f0"></a>
#### 사용 예

```
{
    ...
    EXEC SQL BEGIN DECLARE SECTION;
    SQL_CONTEXT ctxt;
    EXEC SQL END DECLARE SECTION;

    EXEC SQL CONTEXT ALLOCATE :ctxt;
 
    EXEC SQL CONTEXT USE :ctxt;
    EXEC SQL CONNECT :uid IDENTIFIED BY :pwd USING :conn_str;
 
    EXEC SQL
        UPDATE EMP
        SET    sal = sal * 1.1
        WHERE  JOB = 'SALES';

    EXEC SQL DISCONNECT;
    EXEC SQL CONTEXT FREE :ctxt;
 
    ...
}
```

<a id="258f811557a7fb4f"></a>
#### 참조

관련 내용은 [SQL_CONTEXT](#5d9a91f46d4c2768)를 참조한다.

<a id="169c1380e78d1cb7"></a>
### EXEC SQL CONTEXT USE

<a id="fd3a6dbbe0b79989"></a>
#### 기능

Run-time context 사용을 알린다.

<a id="56f736bbc583f380"></a>
#### 구문

```
EXEC SQL CONTEXT USE { :context | DEFAULT };
```

<a id="5e47ffa4897f7e91"></a>
#### 설명

Run-time context의 사용을 precompiler에 알리는 지시자로써 이제부터 사용할 run-time context를 지정한다. USE 구문에 SQL_CONTEXT 변수를 사용하면 사용자가 선언하여 할당한 run-time context를 사용하게 할 수 있으며, USE DEFAULT를 사용하면 응용 프로그램이 기본적으로 가지고 있는 default context를 사용하게 한다.

<a id="e4de2feae9e1a319"></a>
#### 사용 예

```
{
    ...
    EXEC SQL BEGIN DECLARE SECTION;
    SQL_CONTEXT ctxt;
    double      max_sal;
    EXEC SQL END DECLARE SECTION;

    EXEC SQL CONTEXT ALLOCATE :ctxt;
 
    EXEC SQL CONTEXT USE :ctxt;
    EXEC SQL CONNECT :uid IDENTIFIED BY :pwd USING :conn_str;
 
    EXEC SQL
        UPDATE EMP
        SET    sal = sal * 1.1
        WHERE  JOB = 'SALES';

    EXEC SQL COMMIT RELEASE;
    EXEC SQL CONTEXT FREE :ctxt;
 
    EXEC SQL CONTEXT USE DEFAULT;
    EXEC SQL CONNECT :uid IDENTIFIED BY :pwd USING :conn_str;
 
    EXEC SQL
        SELECT MAX(sal)
        INTO   max_sal
        FROM   EMP
        WHERE  JOB = 'SALES';

    EXEC SQL DISCONNECT;
    ...
}
```

<a id="b6a958bb5057cda6"></a>
#### 참조

관련 내용은 [SQL_CONTEXT](#5d9a91f46d4c2768)를 참조한다.

<a id="6a43510771a54c7a"></a>
### EXEC SQL DISCONNECT

<a id="0d1693232651be45"></a>
#### 기능

GOLDILOCKS와의 connection을 종료한다.

<a id="8c25ace9387592df"></a>
#### 구문

```
EXEC SQL [ AT <db_name> ] DISCONNECT [ ALL ]
```

<a id="80c15f9dcec7c880"></a>
#### 설명

GOLDILOCKS와의 연결을 종료한다. AT 절을 이용하여 특정 connection을 해제할 수도 있고, AT 절을 사용하지 않으면 현재 자신이 사용하던 connection이 해제된다. DISCONNECT ALL을 사용하면 현재 응용 프로그램에서 사용하던 모든 connection이 해제된다.

<a id="d8e144779f7eb302"></a>
#### 사용 예

```
{
    ...
    EXEC SQL AT :conn_name DISCONNECT;
 
    ...
}
```

<a id="c7cdb7ddb41a5971"></a>
#### 참조

관련 내용은 [Database 연결 해제](#6066df31b82aebe0)를 참조한다.

<a id="31ce6cc26a339f60"></a>
### EXEC SQL END DECLARE SECTION

<a id="d15ddeed02e6bec2"></a>
#### 기능

Precompiler 지시자로써 host variable 선언 영역을 지정한다.

<a id="d5164aa078819c3c"></a>
#### 구문

```
EXEC SQL END DECLARE SECTION;
```

<a id="90bbed3d3538cc93"></a>
#### 설명

Host variable 선언 영역을 지정하는 precompiler 지시자로써 항상 EXEC SQL BEGIN DECLARE SECTION과 함께 사용된다. Precompiler가 declare section의 분석을 진행하는 도중에 이 문장을 만나면 declare section이 종료되었다고 판단한다.

<a id="03a1bda5085bcfc6"></a>
#### 사용 예

```
{
    EXEC SQL BEGIN DECLARE SECTION;
    int    emp_number[20]; 
    char   emp_name[20][10]; 
    int    dept_number[20]; 
    EXEC SQL END DECLARE SECTION;
 
    ...
}
```

<a id="a740450b6030feae"></a>
#### 참조

관련 내용은 다음을 참조한다.

- [Host Variable의 선언](#213821c4b5b8df6f)
- [EXEC SQL BEGIN DECLARE SECTION](#f576f4c35ed7bc20)

<a id="70f3610553cc8ce7"></a>
### EXEC SQL FOR

<a id="995c1f8b551c69eb"></a>
#### 기능

Array operation에서 array 개수를 지정한다.

<a id="eab1e6305fae6203"></a>
#### 구문

```
EXEC SQL FOR { :array_count | integer_constant } <sql statement>;
```

<a id="b36e032354c79bc3"></a>
#### 설명

SQL 문의 host 변수가 array일 경우 array count를 지정하는 precompiler 지시자이다. FOR 절이 주어지면 실제 host array의 array count는 무시하고 FOR 절에서 지정된 개수만큼의 array만 수행한다.

Array count를 의미하는 상수나 변수는 반드시 정수형이어야만 한다.

<a id="6a62d2db3d1e5a04"></a>
#### 사용 예

```
EXEC SQL BEGIN DECLARE SECTION;
int    emp_number[20]; 
char   emp_name[20][10]; 
int    dept_number[20]; 
int    record_cnt;
EXEC SQL END DECLARE SECTION;
```

• emp_number, emp_name, dept_number 값을 설정

```
...
```

- emp_number, emp_name, dept_number를 INSERT

```
record_cnt = 10;
EXEC SQL FOR :record_cnt INSERT INTO emp (empno, ename, deptno) 
    VALUES (:emp_number, :emp_name, :dept_number);
```

<a id="a474e056fbd39819"></a>
#### 참조

관련 내용은 [FOR 절 사용](#2e64e479c93a33d2)을 참조한다.

<a id="f5fc45d40dd52471"></a>
### EXEC SQL GET GROUPID INTO

<a id="7342e7a98589810a"></a>
#### 기능

SQL statement의 group ID를 얻는다.

<a id="870828f157ca0931"></a>
#### 구문

```
EXEC SQL [ AT <db_name> ] GET GROUPID INTO :group_id { delete_stmt | insert_stmt | select_stmt | update_stmt };
```

<a id="312638d9086f7be1"></a>
#### 설명

Global connection을 사용하는 cluster 환경에서 SQL statement의 group ID를 얻는다. 호스트 변수 :group_id에는 signed numeric type만 사용할 수 있다. Group ID를 얻을 수 있는 SQL statement는 delete, insert, select, update로 한정되며 table에 shard key가 설정되어 있어야 한다.

group ID를 얻은 SQL statement는 내부적으로 SQLExecute를 실행하지 않은 SQLPrepare 상태로 cache 된다.

> 유효하지 않은 group ID 값인 -1이 반환될 수 있다.

<a id="d9d922b9e5f13e66"></a>
#### 사용 예

```
{
EXEC SQL BEGIN DECLARE SECTION;
int  group_id[10];
int  emp_no[10];
char emp_name[10][20];
int  dept_no[10];
EXEC SQL END DECLARE SECTION;
```

- emp_no, emp_name, dept_no 값을 설정한다.

```
...
```

- group id를 얻는다.

```
EXEC SQL GET GROUPID INTO :group_id 
         INSERT INTO emp (empno, ename, deptno) VALUES (:emp_no, :emp_name, :dept_no);
```

- emp_no, emp_name, dept_no을 INSERT 한다.

```
EXEC SQL INSERT INTO emp (empno, ename, deptno) VALUES (:emp_no, :emp_name, :dept_no);
}
```

<a id="af51075d430d5206"></a>
### EXEC SQL INCLUDE

<a id="1f78eb0211fc2599"></a>
#### 기능

Embedded SQL header file을 포함시킨다.

<a id="a5edbbb52686b0b6"></a>
#### 구문

```
EXEC SQL INCLUDE <Header file name>;
```

<a id="3cd749d754a1257b"></a>
#### 설명

Embedded SQL header file을 포함시킨다. C 언어의 #include 문으로 header file을 포함시킬 경우, 이는 precompiler에서 해석하지 않기 때문에 header file 내에 declare section등 precompiler가 알아야 할 내용이 있어도 이를 인식할 수가 없다. 따라서 precompiler가 알아야 하는 embedded SQL 구문이 사용될 경우, EXEC SQL INCLUDE 구문을 사용해야 한다.

<a id="55689cb3384178b0"></a>
#### 사용 예

```
EXEC SQL INCLUDE decl.h;
```

<a id="c7670e62c8530511"></a>
#### 참조

관련 내용은 [Precompiled Header File](#fabc1e92e7bd94de)을 참조한다.

<a id="7fbe7d08e75ed1a8"></a>
### EXEC SQL INCLUDE SQLCA

<a id="63949de6e9ab3f97"></a>
#### 기능

*sqlca.h* header file을 포함시킨다.

<a id="fb5eecf6ad632f1c"></a>
#### 구문

```
EXEC SQL INCLUDE SQLCA;
```

<a id="8a82701904575913"></a>
#### 설명

EXEC SQL INCLUDE 구문의 특별한 형태로써 GOLDILOCKS에서 제공하는 sqlca.h header file을 포함시킨다. 이 header file은 embedded SQL 응용 프로그램에서 run-time exception handling을 하기 위해 반드시 필요하다.

<a id="509dd568a91c540e"></a>
#### 사용 예

```
EXEC SQL INCLUDE SQLCA;
```

<a id="1b32505449217ac4"></a>
#### 참조

관련 내용은 [Run-time Error 감지](#931dc70af5b97e02)를 참조한다.

<a id="f1efe72c41371f6a"></a>
### EXEC SQL OPTION

<a id="4ff95d3d2b5cb228"></a>
#### 기능

Embedded SQL 소스 코드를 precompile 하는 과정에서 option을 적용한다.

<a id="301d858c28f5bceb"></a>
#### 구문

```
EXEC SQL OPTION ( <option_desc> );
<option_desc> ::=
      INCLUDE = <directory path>
    ;
```

<a id="4d76f9171700299e"></a>
#### 설명

Embedded SQL 소스 코드를 Precompiler 하는 과정에 적용할 Option을 기술한다. 현재 Version에서는 INCLUDE 경로 지정만 지원하고 있으며, 이 Option은 EXEC SQL INCLUDE 에서 Precompiler할 Header file이 위치한 디렉토리를 기술한다.

<a id="e1ac0774ff5759a7"></a>
#### 사용 예

```
EXEC SQL OPTION ( INCLUDE = include );
```

<a id="2cb8f208b092dc43"></a>
#### 참조

관련 내용은 [Header File 경로 지정](#38ded575a22e124e)을 참조한다.

<a id="62ee3043013149f9"></a>
### EXEC SQL ROLLBACK RELEASE

<a id="0635c5b89c466bc7"></a>
#### 기능

트랜잭션을 rollback 한 후에 현재 connection을 종료한다.

<a id="8f39ded526f12725"></a>
#### 구문

```
EXEC SQL [ AT <db_name> ] ROLLBACK [ WORK ] RELEASE;
```

<a id="39aea310c0950b8f"></a>
#### 설명

트랜잭션을 rollback 한 후에 현재 connection을 종료한다.

```
EXEC SQL AT :conn_name ROLLBACK RELEASE;
```

위의 문장은 다음과 동일하다.

```
EXEC SQL AT :conn_name ROLLBACK;
EXEC SQL AT :conn_name DISCONNECT;
```

<a id="4f1a3c379e19f81a"></a>
#### 사용 예

```
{
    ...
    EXEC SQL AT :conn_name CONNECT :uid IDENTIFIED BY :pwd USING :conn_str;
 
    EXEC SQL AT :conn_name
        UPDATE EMP
        SET    sal = sal * 1.1
        WHERE  JOB = 'SALES';

    EXEC SQL AT :conn_name ROLLBACK RELEASE; 
    ...
}
```

<a id="d5bbc3ebdc40c3ef"></a>
#### 참조

관련 내용은 [RELEASE Option](#a398dbf14d7ed4af)을 참조한다.

<a id="cedb5d757b722fa7"></a>
### EXEC SQL WHENEVER

<a id="03a66b97f92593e2"></a>
#### 기능

Embedded SQL 응용 프로그램에서 run-time exception handling을 실행한다.

<a id="d05a9645b13a5a23"></a>
#### 구문

```
EXEC SQL WHENEVER <conditions> <actions>;
<conditions> ::=
      SQLERROR
    | SQLWARNING
    | NOT FOUND
    | SQLSTATE <sqlstate class value>[<sqlstate subclass value>]
    ;
<sqlstate_char> ::= [0-9A-Z];
<sqlstate class value> ::= <sqlstate_char> <sqlstate_char>;
<sqlstate subclass value> ::= <sqlstate_char> <sqlstate_char> <sqlstate_char>;
<actions> ::=
      CONTINUE
    | GOTO <label>
    | STOP
    | DO <c statements>
    ;
```

<a id="6f211e27633d01ac"></a>
#### 설명

Embedded SQL 응용 프로그램에서 run-time exception handling을 자동화하여 처리한다. 네 가지 condition이 있고 condition마다 한 개의 action을 지정할 수 있는데 이 action은 필요에 따라 다시 지정할 수도 있다. 자세한 사항은 [Handling Implicit Error](#3a7a59b85301cdcd)를 참조한다.

<a id="9c7bfe2d5d2c9802"></a>
#### 사용 예

```
EXEC SQL WHENEVER SQLERROR STOP;
EXEC SQL WHENEVER SQLERROR CONTINUE;
EXEC SQL WHENEVER SQLERROR GOTO exit_label;
EXEC SQL WHENEVER NOT FOUND DO break;
EXEC SQL WHENEVER SQLERROR GOTO close_label;
EXEC SQL WHENEVER SQLERROR DO sql_error();
EXEC SQL WHENEVER SQLWARNING CONTINUE;
EXEC SQL WHENEVER SQLSTATE HY000 DO sql_error();
```

<a id="d51d673728549a14"></a>
#### 참조

관련 내용은 [Handling Implicit Error](#3a7a59b85301cdcd)를 참조한다.

---

[← 30. JDBC](30-jdbc.md) · [전체 목차](../README.md) · [32. PDO →](32-pdo.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
