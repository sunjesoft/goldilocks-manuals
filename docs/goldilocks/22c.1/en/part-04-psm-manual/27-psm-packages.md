<a id="081c484622729756"></a>

# 27. PSM Packages

> Source: [GOLDILOCKS 22c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/22c_1/manual/en/081c484622729756)  
> Tag: `22c.1_10_tag`

[← 26. Using SQLs in PSM](26-using-sqls-in-psm.md) · [Table of contents](../README.md) · [28. PSM Language Element References →](28-psm-language-element-references.md)

This chapter describes how to modularize common data and PSM codes used in various applications into the package.

<a id="ada39676ce0a675f"></a>
## Definition

A package is a schema object which bundles items such as logically-related PSM types, variables, subprograms, cursors and exceptions. A package is stored in the database through the compiling process, so that another program (another package, procedure, external program) may refer, share and execute the items in the package.

Every package has a specification in which referable multiple public items and subprograms are listed.  
If a cursor exists among public items or a public subprogram exists, then the package may have a package body. The body includes the following contents.

- SQL statement to be performed by a public cursor, or PSM code which is to be executed by a public subprogram
- Items such as multiple variables and types subprograms which are private and used only internally
- Code for initializing public items (initialization part) which is performed only once when the package is used for the first time (instantiation).

AUTHID statement of the package specification determines whether to perform the package with an invoker privilege or with a definer privilege (Default: definer). It also determines whether to translate the unqualified object in the invoker or in the definer when referring to it.

Only the package owner and the user with EXECUTE PACKAGE privilege can retrieve the definition statement of package specification. However, only the package owner can retrieve the definition statement of package body.

<a id="8c9cc4c493cd0d5d"></a>
## Features

The following features of package provides an application developer and an operator with high reliability and reusability.

- Modularity
    - It bundles related items and subprograms together, so it is easy to manage the database and understand its structure.
- Easy programming
    - A user can program the related application only by defining a specification even without defining the body.
- Encapsulating
    - It can hide the body contents which is an internal implementation of the package from the package user. 
    - It can alter the body (implementation) without recompiling SQL and application which use the package. 
- Performance optimization
    - The entire package is loaded on the memory at once, so that it can quickly call the subprogram ins the memory. 
- Easy privilege control
    - It can bundle all separate privileges for using all public items and subprograms into a single privilege for the entire package.

A package does not support a subprogram overloading, so functions of the same names can not be defined in the same block scope.

<a id="a66e1f262e20b594"></a>
## Specification

The following public items can be declared in the package specification.

- User-defined type
    - Record or collection (Associative array)
    - A user-defined type declared in a package can be used only in a PSM-family statement.
- Variable
    - It is recommended to define a get/ set subprogram for each variable not to directly refer to the variable.
- Subprogram
    - Procedure
    - Function
- Explicit cursor
    - It is allowed to define only a name and a returned type in a package specification and define SQL statement performed by a cursor in a body.
    - A cursor variable can not be defined with a public item in a package.
- User-defined exception

<a id="effba9acec62630d"></a>
### Creating Package Specification

Create a package specification by using CREATE PACKAGE statement.

```
CREATE OR REPLACE PACKAGE MY_PKG
IS
  TYPE MY_REC IS RECORD (F1 INTEGER, F2 INTEGER );
END;
/

Package created.
```

Public items in a defined package can be referred from outside of a package by specifying the package name together as follows.

```
DECLARE
V1 MY_PKG.MY_REC;
BEGIN
    V1.F1 := 10;
    V1.F2 := 20;
    DBMS_OUTPUT.PUT_LINE( 'V1.F1 = ' || V1.F1 || ', V1.F2 = ' || V1.F2 );
END;
/
V1.F1 = 10, V1.F2 = 20
Anonymous PL block executed.
```

<a id="1ca6809548effe57"></a>
### Creating Package Body

The body should be declared when a public cursor or subprogram exists in a package, or the initialization code is required. Otherwise, body definition is optional.

The package body has the following constraints.

- The package body should be created in the schema which is as same as that of the package specification.
- The package body should have the name as same as that of the package specification.
- If a cursor in which the SQL statement is not defined exists among open cursors declared in a package specification, then the cursor with the same name, record type and argument should be declared by specifying SQL in the body.
- A subprogram whose name, argument and return type are same as those of an open subprogram declared in a package specification should be defined in the body. 
- The variable, type, exception which are as same as those defined in a package specification can not be declared in the package body.

Create a package body as follows.

```
CREATE TABLE emp( empno NUMBER, sal NUMBER, comm NUMBER );
Table created.

INSERT INTO emp VALUES( 3548, 6000, 1000 );
1 row created.

INSERT INTO emp VALUES( 9369, 5000, NULL );
1 row created.

INSERT INTO emp VALUES( 7294, 4000, 500 );
1 row created.

COMMIT;
Commit complete.


CREATE OR REPLACE PACKAGE emp_mgmt
IS
  PROCEDURE adjust_sal(v_flag VARCHAR, v_empno NUMBER, v_pct NUMBER);
  FUNCTION get_annual_sal(v_empno NUMBER) RETURN NUMBER;
END;
/

Package created.


CREATE OR REPLACE PACKAGE BODY emp_mgmt
IS
  PROCEDURE adjust_sal(v_flag VARCHAR, v_empno NUMBER, v_pct NUMBER) IS
  BEGIN
    IF v_flag = 'INCREASE' THEN
      UPDATE emp SET sal = sal + (sal * (v_pct / 100)) WHERE empno = v_empno;
    ELSE
      UPDATE emp SET sal = sal - (sal * (v_pct / 100)) WHERE empno = v_empno;
    END IF;
  END;
  FUNCTION get_annual_sal (v_empno NUMBER) RETURN NUMBER
  IS
    v_sal NUMBER;
  BEGIN
    SELECT (sal + NVL(comm,0)) * 12 INTO v_sal FROM emp WHERE empno = v_empno;
    RETURN v_sal;
  END;
END;
/

Package created.
```

Call subprograms of the created package body as follows.

```
call emp_mgmt.adjust_sal('INCREASE',7369, 10);

Procedure Call complete.


SELECT emp_mgmt.get_annual_sal(7294) FROM DUAL;
EMP_MGMT.GET_ANNUAL_SAL(7294)
-----------------------------
                        54000
1 row selected.
```

<a id="a72469b119a2406e"></a>
### Package State

Packages are classified into a stateful package and a stateless package.

A stateful package includes one or more variables or cursors, and a stateless package is configured with subprograms only such as a procedure or a function.

A stateful package creates a package instance in a session when referring to the variable or the cursor of the package for the first time. In this case, it performs the following operations.

- Initialize a package variable
- Execute an initialize section

Generally, a package state is maintained as same as the lifetime of a session. However, a stateful package is invalidated and an instance is initialized in the following cases.

- When the package is recreated by executing REPLACE PACKAGE statement
- When the package is recompiled by executing ALTER PACKAGE statement
- When altering operation (DDL) which affects the package instance form occurs on any object which was referenced by the package.

A stateless package does not have a state, so it is automatically recompiled even when the related object's form is altered. However, a stateful package drops the existing package instance, then it recreates a package instance based on the updated package information.

Therefore, be cautious to handle the situational exception when using a package in an application.

---

[← 26. Using SQLs in PSM](26-using-sqls-in-psm.md) · [Table of contents](../README.md) · [28. PSM Language Element References →](28-psm-language-element-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
