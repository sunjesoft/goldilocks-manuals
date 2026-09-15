<a id="86106a7a48b89ee6"></a>

# 40. SQLAlchemy

> 원본: [GOLDILOCKS 26c.1 User Manual (ko)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/ko/86106a7a48b89ee6)  
> 태그: `26c.1_0_tag`

[← 39. aiogoldilocks](39-aiogoldilocks.md) · [전체 목차](../README.md) · [41. Hibernate →](41-hibernate.md)

<a id="b5066579b3e35d92"></a>
## GOLDILOCKS 를 위한 SQLAlchemy dialect

이 매뉴얼은 SQLAlchemy 를 사용하여 GOLDILOCKS 데이터베이스와 함께 작업하려는 개발자들을 위한 것이다. 여기서는 GOLDILOCKS 데이터베이스의 기본적인 사용법과 함께 SQLAlchemy 의 다양한 기능을 어떻게 활용할 수 있는지 설명한다.

<a id="afb7b376fe480849"></a>
### 필수 요건

- Python 3.8 이상
- alembic
- SQLAlchemy 1.4 or 2.x
- pygoldilocks

<a id="861cec1b263dcc40"></a>
### 설치

소스 폴더에서 다음 명령어를 실행한다.

```
$ pip install .
```

이 명령어는 현재 위치한 폴더에서 sqlalchemy-goldilocks 를 설치한다.

<a id="f15749289b96618b"></a>
### 시작하기

설치 후, GOLDILOCKS 데이터베이스에 연결하는 SQLAlchemy 엔진을 만들 수 있다. 기본적인 연결 방법은 다음과 같다.

```
from sqlalchemy import create_engine

engine = create_engine('goldilocks://사용자명:비밀번호@호스트:포트', echo=True)
```

여기서 사용자명과 비밀번호는 GOLDILOCKS 계정 정보이고, 호스트와 포트는 데이터베이스 서버의 주소와 포트 번호를 의미한다. `echo=True` 는 실행하는 SQL 문을 콘솔에 출력한다.

<a id="4e54843f278e540f"></a>
### 사용법

<a id="1febfeb000667877"></a>
#### 자동 증가 (Auto Increment) 동작

SQLAlchemy 의 정수 기본 키가 있는 Table 객체는 자동 증가하는 것으로 간주되지만, GOLDILOCKS에서는 IDENTITY 열이나 SEQUENCE를 사용해야 한다.

<a id="ff56ecdca5b8c6b4"></a>
##### IDENTITY 열 사용하기

GOLDILOCKS 는 Identity 를 사용하여 자동 증가를 구현할 수 있다. 이렇게 하면 새 레코드가 삽입될 때마다 ID 값이 자동으로 생성된다.

```
t = Table('mytable', metadata,
    Column('id', Integer, Identity(start=3), primary_key=True),
    Column(...), ...
)
```

이 코드는 'id' 열이 자동으로 증가하는 테이블을 생성한다. 시작 번호는 3이다.

<a id="50423994011b6346"></a>
##### SEQUENCE 사용하기

Sequence 객체를 사용하여 명시적으로 시퀀스를 지정할 수 있다.

```
t = Table('mytable', metadata,
      Column('id', Integer, Sequence('id_seq', start=1), primary_key=True),
      Column(...), ...
)
```

이 코드는 'id' 열에 'id_seq'라는 시퀀스를 사용하여 자동 증가를 구현한다.

<a id="9dda7afabf649653"></a>
#### 식별자 대소문자 처리

GOLDILOCKS 는 식별자를 대문자로 처리하는 반면, SQLAlchemy 는 모든 소문자 식별자를 대소문자 구분 없이 처리한다. SQLAlchemy 에서 대문자를 사용하면 GOLDILOCKS의 식별자와 일치하지 않을 수 있으므로 가능한 한 소문자를 사용하는 것이 좋다.

<a id="9d6b836d5ba36796"></a>
#### RETURNING 지원

GOLDILOCKS 는 INSERT, UPDATE, DELETE 문에서 RETURNING 절을 완벽하게 지원한다. 이 기능은 특히 데이터베이스에서 쿼리 실행 후 바로 결과를 받아야 할 때 유용하다.

<a id="5890094711b2611f"></a>
#### 동의어 리플렉션 (Synonym Reflection)

GOLDILOCKS 에서는 동의어를 사용하여 다른 이름으로 테이블을 참조할 수 있다.

`goldilocks_resolve_synonyms=True` 플래그를 설정하면 동의어를 통해 테이블을 찾을 수 있다.

```
some_table = Table('some_table', autoload_with=some_engine, goldilocks_resolve_synonyms=True)
```

<a id="085999671771a689"></a>
### 사용 예

다음 예제는 SQLAlchemy 2.0 스타일로 작성되었다.

```
# Working with Transactions and the DBAPI
# https://docs.sqlalchemy.org/en/20/tutorial/dbapi_transactions.html

from sqlalchemy import create_engine, text
from sqlalchemy.orm import Session

engine = create_engine("goldilocks://test:test@127.0.0.1:22581", echo=True)


# Getting a Connection
with engine.connect() as conn:
    result = conn.execute(text("select 'hello world' from dual"))
    print(result.all())


# Committing Changes

# "commit as you go"
with engine.connect() as conn:
    conn.execute(text("DROP TABLE IF EXISTS some_table"))
    conn.execute(text("CREATE TABLE some_table (x int, y int)"))
    conn.execute(
        text("INSERT INTO some_table (x, y) VALUES (:x, :y)"),
        [{"x": 1, "y": 1}, {"x": 2, "y": 4}],
    )
    conn.commit()


# "begin once"
with engine.begin() as conn:
    conn.execute(
        text("INSERT INTO some_table (x, y) VALUES (:x, :y)"),
        [{"x": 6, "y": 8}, {"x": 9, "y": 10}],
    )


# Basics of Statement Execution

# Fetching Rows
with engine.connect() as conn:
    result = conn.execute(text("SELECT X, Y FROM some_table"))
    for row in result:
        print(f"X: {row.X}  Y: {row.Y}")


# Sending Parameters
with engine.connect() as conn:
    result = conn.execute(text("SELECT X, Y FROM some_table WHERE Y > :y"), {"y": 2})
    for row in result:
        print(f"X: {row.X}  Y: {row.Y}")


# Sending Multiple Parameters
with engine.connect() as conn:
    conn.execute(
        text("INSERT INTO some_table (x, y) VALUES (:x, :y)"),
        [{"x": 11, "y": 12}, {"x": 13, "y": 14}],
    )
    conn.commit()


# Executing with an ORM Session
stmt = text("SELECT X, Y FROM some_table WHERE y > :y ORDER BY x, y")
with Session(engine) as session:
    result = session.execute(stmt, {"y": 6})
    for row in result:
        print(f"X: {row.X}  Y: {row.Y}")

with Session(engine) as session:
    result = session.execute(
        text("UPDATE some_table SET y=:y WHERE x=:x"),
        [{"x": 9, "y": 11}, {"x": 13, "y": 15}],
    )
    session.commit()
```

```
# ORM Quick Start
# https://docs.sqlalchemy.org/en/20/orm/quickstart.html

from typing import Optional, List

from sqlalchemy import String, ForeignKey, select, create_engine, Identity, Sequence
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column, relationship, Session


# Declare Models
class Base(DeclarativeBase):
    pass


class User(Base):
    __tablename__ = "user_account"
    id: Mapped[int] = mapped_column(Identity(), primary_key=True)
    name: Mapped[str] = mapped_column(String(30))
    fullname: Mapped[Optional[str]] = mapped_column(String(255))

    addresses: Mapped[List["Address"]] = relationship(
        back_populates="user", cascade="all, delete-orphan"
    )

    def __repr__(self) -> str:
        return f"User(id={self.id!r}, name={self.name!r}, fullname={self.fullname!r})"


class Address(Base):
    __tablename__ = "address"
    id: Mapped[int] = mapped_column(Sequence("address_id_seq"), primary_key=True)
    email_address: Mapped[str] = mapped_column(String(255))
    user_id: Mapped[int] = mapped_column(ForeignKey("user_account.id"))

    user: Mapped["User"] = relationship(back_populates="addresses")

    def __repr__(self) -> str:
        return f"Address(id={self.id!r}, email_address={self.email_address!r})"


# Create an Engine
engine = create_engine("goldilocks://test:test@127.0.0.1:22581", echo=True)


# Emit CREATE TABLE DDL
Base.metadata.drop_all(engine)
Base.metadata.create_all(engine)


# Create Objects and Persist
with Session(engine) as session:
    spongebob = User(
        name="spongebob",
        fullname="Spongebob Squarepants",
        addresses=[Address(email_address="spongebob@sqlalchemy.org")],
    )
    sandy = User(
        name="sandy",
        fullname="Sandy Cheeks",
        addresses=[
            Address(email_address="sandy@sqlalchemy.org"),
            Address(email_address="sandy@squirrelpower.org"),
        ],
    )
    patrick = User(name="patrick", fullname="Patrick Star")
    session.add_all([spongebob, sandy, patrick])
    session.commit()


# Simple SELECT
session = Session(engine)

stmt = select(User).where(User.name.in_(["spongebob", "sandy"]))

for user in session.scalars(stmt):
    print(user)


# SELECT with JOIN
stmt = (
    select(Address)
    .join(Address.user)
    .where(User.name == "sandy")
    .where(Address.email_address == "sandy@sqlalchemy.org")
)
sandy_address = session.scalars(stmt).one()

print(sandy_address)


# Make Changes
stmt = select(User).where(User.name == "patrick")
patrick = session.scalars(stmt).one()

patrick.addresses.append(Address(email_address="patrickstar@sqlalchemy.org"))

sandy_address.email_address = "sandy_cheeks@sqlalchemy.org"

session.commit()


# Some Deletes
sandy = session.get(User, 2)

sandy.addresses.remove(sandy_address)

session.flush()

session.delete(patrick)

session.commit()
```

```
from sqlalchemy import create_engine, inspect

engine = create_engine("goldilocks://test:test@127.0.0.1:22581", echo=False)


def drop_object():
    with engine.begin() as conn:
        conn.exec_driver_sql("DROP SYNONYM IF EXISTS s_sequence1")
        conn.exec_driver_sql("DROP SYNONYM IF EXISTS s_view1")
        conn.exec_driver_sql("DROP SYNONYM IF EXISTS s_table1")
        conn.exec_driver_sql("DROP SEQUENCE IF EXISTS sequence1")
        conn.exec_driver_sql("DROP VIEW IF EXISTS view1")
        conn.exec_driver_sql("DROP INDEX IF EXISTS index1")
        conn.exec_driver_sql("DROP TABLE IF EXISTS table1")
        conn.exec_driver_sql("DROP SCHEMA IF EXISTS schema1")


def create_object():
    with engine.begin() as conn:
        conn.exec_driver_sql("CREATE SCHEMA schema1")
        conn.exec_driver_sql("CREATE TABLE table1 ( i1 INTEGER PRIMARY KEY, i2 integer)")
        conn.exec_driver_sql("COMMENT ON TABLE table1 IS 'this is table1 comment'")
        conn.exec_driver_sql("CREATE INDEX index1 on table1(i2)")
        conn.exec_driver_sql("CREATE VIEW view1 as SELECT * FROM table1")
        conn.exec_driver_sql("CREATE SEQUENCE sequence1")
        conn.exec_driver_sql("CREATE SYNONYM s_table1 for table1")
        conn.exec_driver_sql("CREATE SYNONYM s_view1 for view1")
        conn.exec_driver_sql("CREATE SYNONYM s_sequence1 for sequence1")


drop_object()
create_object()

insp = inspect(engine)

# schema
print("get_schema_names()                                                : " +
      str(insp.get_schema_names()))
print("has_schema('schema1')                                             : " +
      str(insp.has_schema("schema1")))

# table
print("get_table_names()                                                 : " +
      str(insp.get_table_names()))
print("has_table('table1')                                               : " +
      str(insp.has_table("table1")))

print("get_table_names(goldilocks_resolve_synonyms=True)                 : " +
      str(insp.get_table_names(goldilocks_resolve_synonyms=True)))
print("has_table('table1', goldilocks_resolve_synonyms=True)             : " +
      str(insp.has_table("table1", goldilocks_resolve_synonyms=True)))
print("has_table('s_table1', goldilocks_resolve_synonyms=True)           : " +
      str(insp.has_table("s_table1", goldilocks_resolve_synonyms=True)))

# view
print("get_view_names()                                                  : " +
      str(insp.get_view_names()))
print("has_table('view1')                                                : " +
      str(insp.has_table("view1")))
print("get_view_definition('view1')                                      : " +
      str(insp.get_view_definition("view1")))

print("get_view_names(goldilocks_resolve_synonyms=True)                  : " +
      str(insp.get_view_names(goldilocks_resolve_synonyms=True)))
print("has_table('view1', goldilocks_resolve_synonyms=True)              : " +
      str(insp.has_table("view1", goldilocks_resolve_synonyms=True)))
print("has_table('s_view1', goldilocks_resolve_synonyms=True)            : " +
      str(insp.has_table("s_view1", goldilocks_resolve_synonyms=True)))
print("get_view_definition('view1', goldilocks_resolve_synonyms=True)    : " +
      str(insp.get_view_definition("view1", goldilocks_resolve_synonyms=True)))
print("get_view_definition('s_view1', goldilocks_resolve_synonyms=True)  : " +
      str(insp.get_view_definition("s_view1", goldilocks_resolve_synonyms=True)))

# sequence
print("get_sequence_names()                                              : " +
      str(insp.get_sequence_names()))
print("has_sequence('sequence1')                                         : " +
      str(insp.has_sequence("sequence1")))

print("get_sequence_names(goldilocks_resolve_synonyms=True)              : " +
      str(insp.get_sequence_names(goldilocks_resolve_synonyms=True)))
print("has_sequence('sequence1', goldilocks_resolve_synonyms=True)       : " +
      str(insp.has_sequence("sequence1", goldilocks_resolve_synonyms=True)))
print("has_sequence('s_sequence1', goldilocks_resolve_synonyms=True)     : " +
      str(insp.has_sequence("s_sequence1", goldilocks_resolve_synonyms=True)))

# index
print("get_indexes('table1')                                             : " +
      str(insp.get_indexes("table1")))
print("has_index('table1', 'index1')                                     : " +
      str(insp.has_index("table1", "index1")))

print("get_indexes('table1', goldilocks_resolve_synonyms=True)           : " +
      str(insp.get_indexes("table1", goldilocks_resolve_synonyms=True)))
print("has_index('table1', 'index1', goldilocks_resolve_synonyms=True)   : " +
      str(insp.has_index("table1", "index1", goldilocks_resolve_synonyms=True)))

print("get_indexes('s_table1', goldilocks_resolve_synonyms=True)         : " +
      str(insp.get_indexes("s_table1", goldilocks_resolve_synonyms=True)))
print("has_index('s_table1', 'index1', goldilocks_resolve_synonyms=True) : " +
      str(insp.has_index("s_table1", "index1", goldilocks_resolve_synonyms=True)))

# pk_constraint
print("get_pk_constraint('table1')                                       : " +
      str(insp.get_pk_constraint("table1")))
print("get_pk_constraint('table1', goldilocks_resolve_synonyms=True)     : " +
      str(insp.get_pk_constraint("table1", goldilocks_resolve_synonyms=True)))
print("get_pk_constraint('s_table1', goldilocks_resolve_synonyms=True)   : " +
      str(insp.get_pk_constraint("s_table1", goldilocks_resolve_synonyms=True)))

# columns
print("get_columns('table1')                                             : " +
      str(insp.get_columns("table1")))
print("get_columns('table1', goldilocks_resolve_synonyms=True)           : " +
      str(insp.get_columns("table1", goldilocks_resolve_synonyms=True)))
print("get_columns('s_table1', goldilocks_resolve_synonyms=True)         : " +
      str(insp.get_columns("s_table1", goldilocks_resolve_synonyms=True)))

# comment
print("get_table_comment('table1')                                       : " +
      str(insp.get_table_comment("table1")))
print("get_table_comment('table1', goldilocks_resolve_synonyms=True)     : " +
      str(insp.get_table_comment("table1", goldilocks_resolve_synonyms=True)))
print("get_table_comment('s_table1', goldilocks_resolve_synonyms=True)   : " +
      str(insp.get_table_comment("s_table1", goldilocks_resolve_synonyms=True)))
```

```
from sqlalchemy import create_engine, Column, Integer, String, Float, DateTime, Numeric, Date, Time, Boolean, \
    LargeBinary, Text, BigInteger, Interval, SmallInteger, Double, CHAR, VARCHAR, BINARY, VARBINARY, CLOB, BLOB, BIGINT, \
    BOOLEAN, REAL, FLOAT, DOUBLE, DOUBLE_PRECISION, NUMERIC, DECIMAL, INTEGER, SMALLINT, TIMESTAMP, DATETIME, \
    DATE, TIME, TEXT
from sqlalchemy.orm import declarative_base

import sqlalchemy_goldilocks
from sqlalchemy_goldilocks import NATIVE_INTEGER, NATIVE_SMALLINT, NATIVE_BIGINT, NATIVE_DOUBLE, NATIVE_REAL, \
    LONGVARCHAR, LONGVARBINARY, NUMBER, INTERVAL, ROWID

engine = create_engine("goldilocks://test:test@127.0.0.1:22581", echo=True)

Base = declarative_base()


class CamelCaseTypesTable(Base):
    __tablename__ = 'camel_case_types_table'

    string_field = Column(String(30), primary_key=True)
    text_field = Column(Text)

    smallint_field = Column(SmallInteger)
    integer_field = Column(Integer)
    big_integer_field = Column(BigInteger)

    numeric_field1 = Column(Numeric)
    numeric_field2 = Column(Numeric(precision=10))
    numeric_field3 = Column(Numeric(precision=15, scale=2))

    float_field1 = Column(Float)
    float_field2 = Column(Float(precision=8).with_variant(
        sqlalchemy_goldilocks.FLOAT(binary_precision=26), 'goldilocks'))

    double_field = Column(Double)

    datetime_field1 = Column(DateTime)
    datetime_field2 = Column(DateTime().with_variant(
        sqlalchemy_goldilocks.TIMESTAMP(precision=2), 'goldilocks'))

    datetime_tz_field1 = Column(DateTime(timezone=True))
    datetime_tz_field2 = Column(DateTime(timezone=True).with_variant(
        sqlalchemy_goldilocks.TIMESTAMP(timezone=True, precision=3), 'goldilocks'))

    date_field = Column(Date)

    time_field1 = Column(Time)
    time_field2 = Column(Time().with_variant(
        sqlalchemy_goldilocks.TIME(precision=3), 'goldilocks'))

    time_tz_field1 = Column(Time(timezone=True))
    time_tz_field2 = Column(Time(timezone=True).with_variant(
        sqlalchemy_goldilocks.TIME(timezone=True, precision=3), 'goldilocks'))

    large_binary_field = Column(LargeBinary)

    boolean_field = Column(Boolean)

    interval_field1 = Column(Interval)
    interval_field2 = Column(Interval(day_precision=2))
    interval_field3 = Column(Interval(day_precision=3, second_precision=4))


class UpperCaseTypesTable(Base):
    __tablename__ = 'upper_case_types_table'

    boolean_field = Column(BOOLEAN)

    real_field = Column(REAL)

    float_field1 = Column(FLOAT)
    float_field2 = Column(FLOAT(precision=8).with_variant(
        sqlalchemy_goldilocks.FLOAT(binary_precision=26), 'goldilocks'))

    double_field = Column(DOUBLE)
    double_precision_field = Column(DOUBLE_PRECISION)

    numeric_field1 = Column(NUMERIC)
    numeric_field2 = Column(NUMERIC(precision=8))
    numeric_field3 = Column(NUMERIC(precision=10, scale=2))

    decimal_field1 = Column(DECIMAL)
    decimal_field2 = Column(DECIMAL(precision=8))
    decimal_field3 = Column(DECIMAL(precision=8, scale=2))

    integer_field = Column(INTEGER, primary_key=True)
    smallint_field = Column(SMALLINT)
    bigint_field = Column(BIGINT)

    timestamp_field1 = Column(TIMESTAMP)
    timestamp_field2 = Column(TIMESTAMP().with_variant(
        sqlalchemy_goldilocks.TIMESTAMP(precision=2), 'goldilocks'))

    timestamp_tz_field1 = Column(TIMESTAMP(timezone=True))
    timestamp_tz_field2 = Column(TIMESTAMP(timezone=True).with_variant(
        sqlalchemy_goldilocks.TIMESTAMP(timezone=True, precision=3), 'goldilocks'))

    datetime_field1 = Column(DATETIME)
    datetime_field2 = Column(DATETIME().with_variant(
        sqlalchemy_goldilocks.TIMESTAMP(precision=2), 'goldilocks'))

    datetime_tz_field1 = Column(DATETIME(timezone=True))
    datetime_tz_field2 = Column(DATETIME(timezone=True).with_variant(
        sqlalchemy_goldilocks.TIMESTAMP(timezone=True, precision=3), 'goldilocks'))

    date_field = Column(DATE)

    time_field1 = Column(TIME)
    time_field2 = Column(TIME().with_variant(
        sqlalchemy_goldilocks.TIME(precision=3), 'goldilocks'))

    time_tz_field1 = Column(TIME(timezone=True))
    time_tz_field2 = Column(TIME(timezone=True).with_variant(
        sqlalchemy_goldilocks.TIME(timezone=True, precision=3), 'goldilocks'))

    char_field = Column(CHAR(10))
    varchar_field = Column(VARCHAR(10))
    clob_field = Column(CLOB)
    text_field = Column(TEXT)

    binary_field = Column(BINARY(10))
    varbinary_field = Column(VARBINARY(10))
    blob_field = Column(BLOB)


class goldilocksTypesTable(Base):
    __tablename__ = 'goldilocks_types_table'

    number_field1 = Column(NUMBER)
    number_field2 = Column(NUMBER(precision=10))
    number_field3 = Column(NUMBER(precision=10, scale=2))

    native_bigint_field = Column(NATIVE_BIGINT, primary_key=True)
    native_integer_field = Column(NATIVE_INTEGER)
    native_smallint_field = Column(NATIVE_SMALLINT)

    native_double_field = Column(NATIVE_DOUBLE)
    native_real_field = Column(NATIVE_REAL)

    interval_field1 = Column(INTERVAL)
    interval_field2 = Column(INTERVAL(day_precision=2))
    interval_field3 = Column(INTERVAL(day_precision=3, second_precision=4))

    long_varchar_field = Column(LONGVARCHAR)
    long_varbinary_field = Column(LONGVARBINARY)

    rowid_field = Column(ROWID)


Base.metadata.create_all(engine)
```

---

[← 39. aiogoldilocks](39-aiogoldilocks.md) · [전체 목차](../README.md) · [41. Hibernate →](41-hibernate.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
