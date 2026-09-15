<a id="55c15063acbc1394"></a>

# 40. SQLAlchemy

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/55c15063acbc1394)  
> Tag: `26c.1_0_tag`

[← 39. aiogoldilocks](39-aiogoldilocks.md) · [Table of contents](../README.md) · [41. Hibernate →](41-hibernate.md)

<a id="1cf527567fd413e9"></a>
## SQLAlchemy Dialect for GOLDILOCKS

This user manual is intended for the developer who works with GOLDILOCKS database by using SQLAlchemy. This manual describe the basic usage of GOLDILOCKS database and how to utilize the various features of SQLAlchemy.

<a id="963ac5e4906f5e4a"></a>
### Requirement

- Python 3.8 or higher
- alembic
- SQLAlchemy 1.4 or 2.x
- pygoldilocks

<a id="06fcb9e10fa915eb"></a>
### Installing

Execute the following command in the source folder.

```
$ pip install .
```

This command installs sqlalchemy-goldilocks in the current folder.

<a id="99fd1aaff7a8c4b5"></a>
### Getting Started

After the installation, SQLAlchemy engine which is connected to GOLDILOCKS database can be created. The basic way of connection is as follows.

```
from sqlalchemy import create_engine

engine = create_engine('goldilocks://user name:password@host:port', echo=True)
```

The user and the password are the account information of GOLDILOCKS, and the host and the port are the address and the port number of the database server. `echo=True` outputs the executing SQL statement in the console.

<a id="e83c8cf2a023e4ca"></a>
### Usage

<a id="f3cc806fb999b2cf"></a>
#### Auto Increment

The table object including the integer primary key in SQLAlchemy is supposed to be automatically increased, but it is required to use IDENTITY column or SEQUENCE in GOLDILOCKS.

<a id="ec6f1dcbd98e9379"></a>
##### Using IDENTITY Column

GOLDILOCKS can implement the auto increment by using Identity. In this way, ID is automatically created every time a new record is inserted.

```
t = Table('mytable', metadata,
    Column('id', Integer, Identity(start=3), primary_key=True),
    Column(...), ...
)
```

This code creates the table in which 'id' column is automatically increased. The number starts from 3.

<a id="c9af56dcb386a34b"></a>
##### Using SEQUENCE

The sequence can be explicitly specified by using a sequence object.

```
t = Table('mytable', metadata,
      Column('id', Integer, Sequence('id_seq', start=1), primary_key=True),
      Column(...), ...
)
```

This code implements the auto increment by using the 'id_seq' sequence in the 'id' column.

<a id="14d41553b378b1fc"></a>
#### Capitalization Rules for Identifiers

GOLDILOCKS processes identifiers as uppercase letters, but SQLAlchemy processes all lowercase identifies as case insensitive. Using uppercase letters in SQLAlchemy may cause mismatch with the identifier of GOLDILOCKS, so it is recommended to use lowercase letters.

<a id="57c4f452bb60b4ae"></a>
#### Supporting RETURNING

GOLDILOCKS fully supports RETURNING clause in INSERT, UPDATE, DELETE statements. This feature is useful especially when it is required to receive the result right after executing a query in the database.

<a id="c8ebbc91ee2d442c"></a>
#### Synonym Reflection

It is possible to refer to the table by using a synonym as a different name in GOLDILOCKS.

`Set goldilocks_resolve_synonyms=True` flag to find the table by using a synonym.

```
some_table = Table('some_table', autoload_with=some_engine, goldilocks_resolve_synonyms=True)
```

<a id="c5de6ada5c54b94f"></a>
### Examples

The following examples are written in SQLAlchemy 2.0 style.

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

[← 39. aiogoldilocks](39-aiogoldilocks.md) · [Table of contents](../README.md) · [41. Hibernate →](41-hibernate.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
