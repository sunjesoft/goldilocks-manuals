<a id="bab4ef023959f000"></a>

# 39. aiogoldilocks

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/bab4ef023959f000)  
> 태그: `26c.1_0_tag`

[← 38. PyDBC](38-pydbc.md) · [전체 목차](../README.md) · [40. SQLAlchemy →](40-sqlalchemy.md)

<a id="8e5483f172ca0349"></a>
## aiogoldilocks

aiogoldilocks는 GOLDILOCKS 용 비동기 Python 드라이버이다.

pygoldilocks 를 기반으로 하며, [aioodbc](https://github.com/aio-libs/aioodbc) 구조를 참고하여 asyncio 기반의 안전하고 강력한 비동기 인터페이스를 제공한다.

<a id="8029d7e12d9f3405"></a>
### 주요 기능

- async/await 기반의 비동기 DB 접근 
- 안전한 커넥션 및 커서 자동 관리 (async with) 
- 커넥션 풀 (create_pool) 지원

<a id="bb887e65c6815d78"></a>
### 사용 예

```
import asyncio

import aiogoldilocks


async def test_example():
    dsn = "DSN=GOLDILOCKS;UID=test;PWD=test"
    conn = await aiogoldilocks.connect(dsn=dsn)

    cur = await conn.cursor()
    await cur.execute("SELECT 42 AS AGE FROM DUAL")
    rows = await cur.fetchall()
    print(rows)
    print(rows[0])
    print(rows[0].AGE)
    await cur.close()
    await conn.close()


asyncio.run(test_example())
```

<a id="c62e5a822da1e10f"></a>
### Connection Pool

```
import asyncio

import aiogoldilocks


async def test_pool():
    dsn = "DSN=GOLDILOCKS;UID=test;PWD=test"
    pool = await aiogoldilocks.create_pool(dsn=dsn)

    async with pool.acquire() as conn:
        cur = await conn.cursor()
        await cur.execute("SELECT 42 FROM DUAL")
        r = await cur.fetchall()
        print(r)
        await cur.close()
        await conn.close()
    pool.close()
    await pool.wait_closed()


asyncio.run(test_pool())
```

<a id="8fcbcd78d6897810"></a>
### Context Manager

```
import asyncio

import aiogoldilocks


async def test_example():
    dsn = "DSN=GOLDILOCKS;UID=test;PWD=test"

    async with aiogoldilocks.create_pool(dsn=dsn) as pool:
        async with pool.acquire() as conn:
            async with conn.cursor() as cur:
                await cur.execute("SELECT 42 AS AGE FROM DUAL")
                val = await cur.fetchone()
                print(val)
                print(val.AGE)


asyncio.run(test_example())
```

<a id="93af93fd3947bc16"></a>
### 설치 방법

$GOLDILOCKS_HOME/app_dev/aiogoldilocks 디렉토리에 다음과 같이 설치한다.

```
pip install .
```

설치를 위해서는 GOLDILOCKS 드라이버가 미리 설치되어 있어야 하며, DSN 또는 연결 문자열도 사전에 설정되어 있어야 한다.

<a id="234b67f4df937055"></a>
### 요구 사항

- Python 3.7 이상
- GOLDILOCKS 드라이버 설치 
    - pygoldilocks 버전 26.1.0 이상

---

[← 38. PyDBC](38-pydbc.md) · [전체 목차](../README.md) · [40. SQLAlchemy →](40-sqlalchemy.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
