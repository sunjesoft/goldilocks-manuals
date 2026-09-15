<a id="a2e2b957d58a7960"></a>

# 39. aiogoldilocks

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/a2e2b957d58a7960)  
> Tag: `26c.1_0_tag`

[← 38. PyDBC](38-pydbc.md) · [Table of contents](../README.md) · [40. SQLAlchemy →](40-sqlalchemy.md)

<a id="7991b568bdfc22d7"></a>
## aiogoldilocks

aiogoldilocks is an asynchronous Python driver for GOLDILOCKS.

It is based on pygoldilocks and modeled after the [aioodbc](https://github.com/aio-libs/aioodbc) architecture, providing a reliable and efficient asyncio-based asynchronous interface.

<a id="ae4dfe3a3e74f164"></a>
### Key Features

- Asynchronous database access using async/await
- Safe connection and automatic cursor management (async with)
- Connection pooling (create_pool) support

<a id="8835772e49dd3dc8"></a>
### Example

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

<a id="10caba62fc859765"></a>
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

<a id="fee003eab2ba6ea1"></a>
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

<a id="b4dbd19a8e0a7c8a"></a>
### Installation

Install it under the $GOLDILOCKS_HOME/app_dev/aiogoldilocks directory as follows.

```
pip install .
```

Before installation, the GOLDILOCKS driver must already be installed, and either a DSN or a connection string must be configured in advance.

<a id="103765ed76457464"></a>
### Requirements

- Python 3.7 or higher
- GOLDILOCKS driver installed 
    - pygoldilocks version 26.1.0 or higher

---

[← 38. PyDBC](38-pydbc.md) · [Table of contents](../README.md) · [40. SQLAlchemy →](40-sqlalchemy.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
