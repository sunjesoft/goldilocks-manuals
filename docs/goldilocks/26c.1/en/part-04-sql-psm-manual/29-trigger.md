<a id="9e3bdbcf1ed13933"></a>

# 29. Trigger

> Source: [GOLDILOCKS 26c.1 User Manual (en)](https://manual.sunjesoft.co.kr/goldilocks/26c_1/manual/en/9e3bdbcf1ed13933)  
> Tag: `26c.1_0_tag`

[← 28. External Routine](28-external-routine.md) · [Table of contents](../README.md) · [30. PSM Language Element References →](30-psm-language-element-references.md)

This section describes the definition and execution of triggers, which are automatically invoked when a specified event occurs on a table.

<a id="5df34298d42b1e21"></a>
## Trigger Overview

A trigger is a database object that automatically performs a series of operations or processing within the database when a DML (Data Manipulation Language) statement such as INSERT, DELETE, or UPDATE is executed on a specific base table.

A trigger is a stored program unit written in PSM. Like stored procedures, it is stored in the database and can be executed repeatedly. However, it cannot be invoked explicitly. When a trigger is enabled, the database automatically executes it whenever the corresponding triggering event occurs. If it is disabled, it will not be executed.

Triggers are created using the [CREATE TRIGGER](31-psm-sql-references.md#44e30f425949fd8e) statement and removed using the [DROP TRIGGER](31-psm-sql-references.md#c5e9e28a6d05bf8b) statement. Since a trigger is a base table–dependent object, it is automatically dropped when the associated table is deleted.

<a id="a48fb6d8e684da74"></a>
![Trigger overview](../assets/images/06d4b68939c3dc5a.png)

<a id="d3117a22c57d04d0"></a>
## Trigger Components

A trigger consists of a target object, an event, a timing and execution unit, and a set of defined actions.  
This section describes these key components. Conditional predicates for DML event detection, as well as transition tables and transition variables, are described separately in the [DML Trigger](#41d6f8bd3864459d) chapter.

<a id="5290f9446742f58c"></a>
### Trigger Target Object

In a DML trigger, the target object refers to the base table on which the trigger detects DML events. The target object must be associated with a single specific table and is used to detect data changes occurring in that table.

In addition, a public synonym or a view cannot be specified as the target object of a DML trigger; only base tables are allowed.

```
gSQL> CREATE TABLE t1 ( c1 INTEGER );
Table created.

gSQL> CREATE VIEW v1 AS SELECT * FROM t1;
View created.

gSQL>
CREATE TRIGGER t1_trig
  AFTER INSERT 
  ON v1
BEGIN
    NULL;
END;
/
ERR-42000(16650): object "V1" is not BASE TABLE :
AFTER INSERT ON V1
                *
ERROR at line 2:

gSQL>
CREATE OR REPLACE TRIGGER t1_trig
  AFTER INSERT 
  ON t1                     --# Target object
BEGIN
    NULL;
END;
/
Trigger created.
```

<a id="c7d68d705fd13608"></a>
### Trigger Event

A trigger event is a condition defined to determine whether a trigger should be executed based on DML operations performed on the target table.  
Supported event types include INSERT, UPDATE, and DELETE. One or more trigger events can be specified; however, the same event cannot be specified more than once.  
For UPDATE events, the trigger can be restricted to specific columns using the &lt; UPDATE [ OF &lt;column list&gt; ] &gt; clause, allowing the trigger to fire only when the specified columns are updated.

```
gSQL>
CREATE OR REPLACE TRIGGER t1_trig
  AFTER
  INSERT OR UPDATE OR UPDATE
  ON t1  
BEGIN
    NULL;
END;
/
ERR-42000(16651): duplicate trigger event :
  INSERT OR UPDATE OR UPDATE
                      *
ERROR at line 3:

gSQL>
CREATE OR REPLACE TRIGGER t1_trig
  AFTER
  INSERT OR UPDATE OF c1 OR DELETE  --# Trigger event
  ON t1  
BEGIN
    NULL;
END;
/
Trigger created.
```

<a id="3d59199e84dd9b42"></a>
### Trigger Timing

The trigger timing defines when a trigger is executed after a specified trigger event occurs on the target table.  
Triggers are classified into BEFORE triggers, which execute prior to the execution of the event on the target object, and AFTER triggers, which execute after the event has been performed.  
When multiple triggers are defined, the execution order is independent of their creation order. All BEFORE triggers are executed first, followed by all AFTER triggers.

```
gSQL>
CREATE OR REPLACE TRIGGER t1_trig_after
  AFTER                      --# Trigger timing
  INSERT ON t1  
BEGIN
    DBMS_OUTPUT.PUT_LINE('After insert trigger');
END;
/
Trigger created.

gSQL>
CREATE OR REPLACE TRIGGER t1_trig_before
  BEFORE                      --# Trigger timing
  INSERT ON t1  
BEGIN
    DBMS_OUTPUT.PUT_LINE('Before insert trigger');
END;
/
Trigger created.

gSQL> set serveroutput on
gSQL> INSERT INTO t1 VALUES ( 10 );

Before insert trigger
After insert trigger
1 row created.
```

<a id="b3a9e03e1388feaa"></a>
### Trigger Execution Unit

The execution unit of a trigger is classified into statement-level execution (FOR EACH STATEMENT) and row-level execution (FOR EACH ROW).  
A statement-level trigger is executed once for each triggering event, whereas a row-level trigger is executed individually for each row affected by the data modification.  
If no execution unit is explicitly specified, the trigger operates in FOR EACH STATEMENT mode by default.

```
gSQL> CREATE TABLE t1 ( c1 INTEGER );
Table created.

gSQL> INSERT INTO t1 VALUES ( 10 ), ( 20 );
2 rows created.

gSQL> COMMIT;
Commit complete.

gSQL>
CREATE OR REPLACE TRIGGER t1_trig_stmt
  AFTER
  UPDATE ON T1
  FOR EACH STATEMENT     --# Trigger execution unit
BEGIN
  DBMS_OUTPUT.PUT_LINE('Each statement trigger');
END;
/
Trigger created.

gSQL>
CREATE OR REPLACE TRIGGER t1_trig_row
  AFTER
  DELETE ON T1
  FOR EACH ROW          --# Trigger execution unit
BEGIN
  DBMS_OUTPUT.PUT_LINE('Each row trigger');
END;
/
Trigger created.

gSQL> set serveroutput on
gSQL> UPDATE t1 SET c1 = c1;

Each statement trigger
2 rows updated.

gSQL> DELETE FROM t1;

Each row trigger
Each row trigger
2 rows deleted.
```

<a id="b2ffebceb8c88f5b"></a>
### Trigger Action

The trigger action defines the execution control and operational behavior of a trigger. It consists of the &lt;trigger enforcement&gt; option, the &lt;triggered when clause&gt; option, and the &lt;trigger body&gt;.  
The &lt;trigger enforcement&gt; option controls whether a trigger is enabled or disabled, allowing it to be set to an active or inactive state.  
The &lt;triggered when clause&gt; option specifies that the trigger should be executed only when a given condition is satisfied.  
The &lt;trigger body&gt; defines the actual operations performed when the trigger is executed.

When creating a trigger, the &lt;trigger enforcement&gt; option can be used to specify whether the trigger is created in an enabled or disabled state. If not explicitly specified, the trigger is created in an enabled state by default.

```
gSQL> 
CREATE OR REPLACE TRIGGER t1_trig
  AFTER INSERT ON t1  
  DISABLE                --# DISABLE or NOT ENFORCED
BEGIN
    DBMS_OUTPUT.PUT_LINE('Insert trigger');
END;
/
Trigger created.

gSQL> set serveroutput on
gSQL> INSERT INTO t1 VALUES ( 10 );
1 row created.
```

The &lt;triggered when clause&gt; option defines a conditional expression that determines whether a trigger should be executed.  
If the condition evaluates to TRUE, the trigger is executed. If it evaluates to FALSE, the trigger is not executed.  
If this clause is not specified, the trigger is executed unconditionally.

```
gSQL> 
CREATE OR REPLACE TRIGGER t1_trig
  AFTER INSERT ON t1
  REFERENCING NEW ROW n_row
  FOR EACH ROW
  WHEN (n_row.c1 > 10)
BEGIN
    DBMS_OUTPUT.PUT_LINE('Insert trigger');
END;
/
Trigger created.

gSQL> set serveroutput on
gSQL> INSERT INTO t1 VALUES ( 10 );
1 row created.

gSQL> INSERT INTO t1 VALUES ( 20 );

Insert trigger
1 row created.
```

The &lt;trigger body&gt; executed by a trigger is typically written in the form of a PSM block. If necessary, it can also be structured to invoke stored procedures using the CALL statement.

For more information about PSM, refer to [Using PSM Subprograms](25-using-psm-subprograms.md#31048831dcb5b296).

<a id="41d6f8bd3864459d"></a>
## DML Trigger

A DML trigger is defined on a base table and can detect data modification events such as INSERT, UPDATE, and DELETE in real time.  
It enables the implementation of complex business rules and helps maintain data integrity. In addition, it allows dynamic data control based on the state of data before and after changes.

<a id="5aa625a34d60c46c"></a>
### Characteristics and Classification of DML Triggers

DML triggers are classified according to their timing and execution unit. Each trigger has distinct characteristics, and different attributes cannot be combined within a single trigger definition.

- Statement-level before trigger ( Before statement trigger )
    - Executed before the triggering statement is executed.
- Statement-level after trigger ( After statement trigger )
    - Executed after the triggering statement has been executed.
- Row-level before trigger ( Before row trigger )
    - Executed before each row affected by the triggering statement is processed.
- Row-level after trigger ( After row trigger )
    - Executed after each row affected by the triggering statement has been processed.

When multiple triggers with different timing and execution units are defined for the same triggering event, they are executed in the following order. For triggers with the same execution unit, execution order follows the order in which they were created.

1. Before statement trigger 
2. Before row trigger 
3. After row trigger 
4. After statement trigger

> The execution order of triggers can be checked through the INFORMATION_SCHEMA.[TRIGGERS](../part-02-administration-manual/9-database-information.md#aff8e3dd7e5fce2f) view.

- Example of Creating Triggers with Different Timing

```
gSQL> CREATE TABLE t1 ( c1 INTEGER );
Table created.

gSQL> 
CREATE TRIGGER t1_trig_post_row
  AFTER INSERT ON t1
  FOR EACH ROW
BEGIN
    DBMS_OUTPUT.PUT_LINE('After row trigger');
END;
/
Trigger created.

gSQL> 
CREATE TRIGGER t1_trig_pre_row
  BEFORE INSERT ON t1
  FOR EACH ROW
BEGIN
    DBMS_OUTPUT.PUT_LINE('Before row trigger');
END;
/
Trigger created.

gSQL> 
CREATE TRIGGER t1_trig_post_stmt
  AFTER INSERT ON t1
  FOR EACH STATEMENT
BEGIN
    DBMS_OUTPUT.PUT_LINE('After statement trigger');
END;
/
Trigger created.

gSQL> 
CREATE TRIGGER t1_trig_pre_stmt
  BEFORE INSERT ON t1
  FOR EACH STATEMENT
BEGIN
    DBMS_OUTPUT.PUT_LINE('Before statement trigger');
END;
/
Trigger created.

gSQL> COMMIT;
Commit complete.
```

- Execution Result

```
gSQL> set serveroutput on
gSQL> INSERT INTO t1 VALUES ( 10 ) ;

Before statement trigger
Before row trigger
After row trigger
After statement trigger
1 row created.
```

- Querying Created Trigger Information

```
gSQL>
SELECT EVENT_OBJECT_TABLE
      ,TRIGGER_NAME
      ,ACTION_ORDER
      ,ACTION_TIMING
      ,ACTION_ORIENTATION
  FROM INFORMATION_SCHEMA.TRIGGERS
 WHERE EVENT_OBJECT_TABLE = 'T1';

EVENT_OBJECT_TABLE TRIGGER_NAME      ACTION_ORDER ACTION_TIMING ACTION_ORIENTATION
------------------ ----------------- ------------ ------------- ------------------
T1                 T1_TRIG_PRE_STMT             1 BEFORE        STATEMENT
T1                 T1_TRIG_PRE_ROW              1 BEFORE        ROW
T1                 T1_TRIG_POST_ROW             1 AFTER         ROW
T1                 T1_TRIG_POST_STMT            1 AFTER         STATEMENT
4 rows selected.
```

<a id="470992325746d96e"></a>
### DML Triggers and Transactions

Triggers are not executed as independent transactions; instead, they run within the same transaction scope as the DML statement that invoked them.  
In other words, the trigger and the triggering DML statement are treated as a single atomic transaction. Therefore, the use of transaction control language (TCL) statements such as COMMIT, ROLLBACK, and SAVEPOINT is restricted within the &lt;trigger body&gt;.  
Furthermore, if an error occurs during the execution of either the DML statement or the trigger, the entire transaction is rolled back as a whole.

```
gSQL> CREATE TABLE t1 ( c1 INTEGER );
Table created.

gSQL>
CREATE OR REPLACE TRIGGER t1_trig
  AFTER INSERT ON t1
BEGIN
    COMMIT;
END;
/
Trigger created.

gSQL> COMMIT;
Commit complete.

gSQL> INSERT INTO t1 values ( 10 );

ERR-0W000(17132): cannot execute in a trigger (COMMIT) :
    COMMIT;
    *
ERROR at line 4:
ERROR at TRIGGER("T1_TRIG")

gSQL> SELECT * FROM t1;
no rows selected.

gSQL> ROLLBACK;
Rollback complete.
```

<a id="1adddfebccb37378"></a>
### Conditional Predicates for DML Event Detection

DML triggers are executed by INSERT, UPDATE, and DELETE events. Within a trigger, conditional predicates can be used to identify which type of DML event caused the trigger to fire.

**Conditional predicates**

<a id="8818b04184894c4d"></a>
| Conditional predicate | Evaluates to TRUE |
| --- | --- |
| INSERTING | When the trigger is fired by an INSERT statement |
| UPDATING | When the trigger is fired by an UPDATE statement |
| UPDATING OF ( column ) | When the trigger is fired by an UPDATE statement on the specified column |
| DELETING | When the trigger is fired by a DELETE statement |

```
gSQL> CREATE TABLE t1 ( c1 INTEGER, c2 INTEGER );
Table created.

gSQL>
CREATE OR REPLACE TRIGGER t1_trig
  BEFORE
  INSERT OR UPDATE OR DELETE
  ON t1  
BEGIN
  IF INSERTING THEN
    DBMS_OUTPUT.PUT_LINE('Inserting');
  ELSIF UPDATING OF (c2) THEN
    DBMS_OUTPUT.PUT_LINE('Updating of column');
  ELSIF UPDATING THEN
    DBMS_OUTPUT.PUT_LINE('Updating');
  ELSIF DELETING THEN
    DBMS_OUTPUT.PUT_LINE('Deleting');
  ELSE 
    DBMS_OUTPUT.PUT_LINE('Unknown');  
  END IF;
END;
/
Trigger created.

gSQL> COMMIT;
Commit complete.

gSQL> set serveroutput on
gSQL> INSERT INTO t1 VALUES ( 10, 20 ) ;
Inserting
1 row created.

gSQL> UPDATE t1 SET c2 = c2 + c2;
Updating of column
1 row updated.

gSQL> UPDATE T1 SET C1 = C1;
Updating
1 row updated.

gSQL> DELETE FROM T1;
Deleting
1 row deleted.
```

<a id="fc8455e499120b38"></a>
### Transition Tables and Transition Variables

When creating a trigger, the REFERENCING clause can be used to specify transition tables or transition variables. These are used to access data before and after DML operations within the trigger.

- Transition table
    - A transition table provides a set of rows affected by a DML operation in table form.
    - Not available in BEFORE triggers 
    - Not available in multi-event triggers 
- Transition variable
    - Not available in statement-level (STATEMENT) triggers 
    - The OLD transition variable cannot be used in INSERT event triggers 
    - The NEW transition variable cannot be used in DELETE event triggers 
    - In multi-event triggers that include INSERT, if the trigger is fired by an INSERT event, the OLD transition variable is NULL 
    - In multi-event triggers that include DELETE, if the trigger is fired by a DELETE event, the NEW transition variable is NULL

Transition tables and transition variables cannot be declared together, and they can only be used within the &lt;triggered action&gt;.

**Availability of Transition Tables and Transition Variables by Trigger Components**

<a id="bdba82e0fd985e3d"></a>
| Execution unit | Timing | Event | Transition table | Transition variable |
| --- | --- | --- | --- | --- |
| ROW | BEFORE | INSERT | - | NEW |
| - | - | UPDATE | - | OLD, NEW |
| - | - | DELETE | - | OLD |
| - | AFTER | INSERT | NEW | NEW |
| - | - | UPDATE | OLD, NEW | OLD, NEW |
| - | - | DELETE | OLD | OLD |
| STATEMENT | AFTER | INSERT | NEW | - |
| - | - | UPDATE | OLD, NEW | - |
| - | - | DELETE | OLD | - |

- Example of using a transition table

```
gSQL> CREATE TABLE t1 ( c1 INTEGER, c2 INTEGER );
Table created.

gSQL> INSERT INTO t1 VALUES (1, 10), (2, 20), (3, 30), (4, 40);
4 rows created.

gSQL> 
CREATE OR REPLACE TRIGGER t1_trig
  AFTER UPDATE ON t1
  REFERENCING OLD TABLE o_tbl 
              NEW TABLE n_tbl
  FOR EACH STATEMENT
DECLARE
  o_count INTEGER;
  n_count INTEGER;
  v1 INTEGER;
  v2 INTEGER;
  
  CURSOR n_cur IS SELECT * FROM n_tbl ORDER BY c1 DESC;
BEGIN
  SELECT COUNT(*) INTO o_count FROM o_tbl;
  DBMS_OUTPUT.PUT_LINE('Old transition table, row count: ' || o_count );
  
  SELECT COUNT(*) INTO n_count FROM n_tbl;
  DBMS_OUTPUT.PUT_LINE('New transition table, row count: ' || n_count );
  
  OPEN n_cur;
  DBMS_OUTPUT.PUT_LINE('New transition table record');
  LOOP
    FETCH n_cur INTO v1, v2;
    EXIT WHEN n_cur%NOTFOUND;
    
    DBMS_OUTPUT.PUT_LINE('C1: ' || v1 || ', C2: ' || v2 );
  END LOOP;
  CLOSE n_cur;
END;
/
Trigger created.

gSQL> set serveroutput on
gSQL> UPDATE t1 SET c2 = c2 * c2;

Old transition table, row count: 4
New transition table, row count: 4
New transition table record
C1: 4, C2: 1600
C1: 3, C2: 900
C1: 2, C2: 400
C1: 1, C2: 100
4 rows updated.
```

- Example of using a transition variable

```
gSQL> CREATE TABLE t1 ( c1 INTEGER, c2 INTEGER );
Table created.

gSQL>
CREATE OR REPLACE TRIGGER t1_trig
  AFTER INSERT OR DELETE 
  ON t1
  REFERENCING OLD ROW AS o_row
              NEW ROW AS n_row
  FOR EACH ROW
BEGIN
  --# INSERT
  IF INSERTING THEN
    CASE WHEN o_row.c1 IS NULL THEN
      DBMS_OUTPUT.PUT_LINE('Insert, Old transition variable is null');
    ELSE
      DBMS_OUTPUT.PUT_LINE('Insert, Old transition variable is not null');
    END CASE;
    
    CASE WHEN n_row.c1 IS NULL THEN
      DBMS_OUTPUT.PUT_LINE('Insert, New transition variable is null');
    ELSE
      DBMS_OUTPUT.PUT_LINE('Insert, New transition variable is not null');
    END CASE;
    
  --# DELETE
  ELSIF DELETING THEN
    CASE WHEN o_row.c1 IS NULL THEN
      DBMS_OUTPUT.PUT_LINE('Delete, Old transition variable is null');
    ELSE
      DBMS_OUTPUT.PUT_LINE('Delete, Old transition variable is not null');
    END CASE;
    
    CASE WHEN n_row.c1 IS NULL THEN
      DBMS_OUTPUT.PUT_LINE('Delete, New transition variable is null');
    ELSE
      DBMS_OUTPUT.PUT_LINE('Delete, New transition variable is not null');
    END CASE;  

  ELSE
    DBMS_OUTPUT.PUT_LINE('Unknown conditional predicates');
  END IF;
END;
/
Trigger created.

gSQL> set serveroutput on
gSQL> INSERT INTO t1 VALUES ( 10, 20 );

Insert, Old transition variable is null
Insert, New transition variable is not null
1 row created.

gSQL> DELETE FROM t1;

Delete, Old transition variable is not null
Delete, New transition variable is null
1 row deleted.
```

<a id="d1f2ff782510df2e"></a>
## Trigger Management

This section describes the management framework and key configuration methods for efficiently operating and controlling created triggers.

<a id="758e05eb7a7bfd76"></a>
### Querying Trigger Information

Detailed information about trigger objects can be checked through the *_TRIGGERS views in the DICTIONARY_SCHEMA or the INFORMATION_SCHEMA.TRIGGERS view.

For a detailed list of related views, refer to [Information on trigger objects](../part-03-sql-manual/13-sql-objects.md#02e48b10eacf5913).

```
gSQL> CREATE TABLE t1 ( c1 INTEGER, c2 INTEGER );
Table created.

gSQL> 
CREATE OR REPLACE TRIGGER t1_trig
  AFTER UPDATE ON t1
  REFERENCING OLD TABLE o_tbl 
              NEW TABLE n_tbl
  FOR EACH STATEMENT
BEGIN
  NULL;
END;
/
Trigger created.

gSQL>
SELECT TRIGGER_SCHEMA
      ,TRIGGER_NAME
      ,TRIGGER_TYPE
      ,TRIGGERING_EVENT
      ,TABLE_OWNER
      ,TABLE_SCHEMA
      ,TABLE_NAME
      ,ACTION_TYPE
      ,STATUS
  FROM USER_TRIGGERS;
  
TRIGGER_SCHEMA TRIGGER_NAME TRIGGER_TYPE    TRIGGERING_EVENT TABLE_OWNER TABLE_SCHEMA TABLE_NAME ACTION_TYPE STATUS
-------------- ------------ --------------- ---------------- ----------- ------------ ---------- ----------- ------
PUBLIC         T1_TRIG      AFTER STATEMENT UPDATE           TEST        PUBLIC       T1         PSM BLOCK   ENABLE
1 row selected.
```

<a id="18c12f71c4ebf9ee"></a>
### Renaming a Trigger

The name of a created trigger can be changed by dropping the existing trigger and recreating it with a new name. However, by using the ALTER TRIGGER RENAME statement, only the name can be changed efficiently while preserving the existing definition.

For more information, refer to [ALTER TRIGGER name RENAME TO](31-psm-sql-references.md#7a2a65b5c770fb59).

```
gSQL> ALTER TRIGGER t1_trig RENAME TO t1_trig_post_update;
Trigger altered.

gSQL>
SELECT TRIGGER_SCHEMA
      ,TRIGGER_NAME
      ,TRIGGER_TYPE
      ,TRIGGERING_EVENT
      ,TABLE_OWNER
      ,TABLE_SCHEMA
      ,TABLE_NAME
      ,ACTION_TYPE
      ,STATUS
  FROM USER_TRIGGERS;

TRIGGER_SCHEMA TRIGGER_NAME        TRIGGER_TYPE    TRIGGERING_EVENT TABLE_OWNER TABLE_SCHEMA TABLE_NAME ACTION_TYPE STATUS
-------------- ------------------- --------------- ---------------- ----------- ------------ ---------- ----------- ------
PUBLIC         T1_TRIG_POST_UPDATE AFTER STATEMENT UPDATE           TEST        PUBLIC       T1         PSM BLOCK   ENABLE
1 row selected.
```

<a id="b128787d0bc534d9"></a>
### Enabling and Disabling a Trigger

When creating a trigger, if the &lt;trigger enforcement&gt; option is omitted or specified as ENABLE or ENFORCED, the trigger is created in an active state. The status of a trigger can be changed using the ALTER TRIGGER ENABLE/DISABLE statement.

For more information, refer to [ALTER TRIGGER name ENABLE/DISABLE](31-psm-sql-references.md#87a5b7084ef9f6ba).

- Disabling a trigger

```
gSQL> ALTER TRIGGER t1_trig_post_update DISABLE;
Trigger altered.

gSQL>
SELECT TRIGGER_SCHEMA
      ,TRIGGER_NAME
      ,STATUS
  FROM USER_TRIGGERS;

TRIGGER_SCHEMA TRIGGER_NAME        STATUS
-------------- ------------------- -------
PUBLIC         T1_TRIG_POST_UPDATE DISABLE
1 row selected.
```

- Enabling a trigger

```
gSQL> ALTER TRIGGER t1_trig_post_update ENABLE;
Trigger altered.

gSQL>
SELECT TRIGGER_SCHEMA
      ,TRIGGER_NAME
      ,STATUS
  FROM USER_TRIGGERS;

TRIGGER_SCHEMA TRIGGER_NAME        STATUS
-------------- ------------------- ------
PUBLIC         T1_TRIG_POST_UPDATE ENABLE
1 row selected.
```

> The STATUS column in the USER_TRIGGERS view indicates the operational state of a trigger object and is displayed as either ENABLE or DISABLE.

<a id="226d12bb0b931f2e"></a>
### Trigger Compilation

A trigger is automatically compiled upon creation and becomes valid (VALID). However, if an object referenced by the trigger is dropped or structurally modified, the trigger is marked as invalid (INVALID). Although the database automatically recompiles the trigger at execution time, it is recommended to manually recompile and validate it in advance to prevent performance degradation during execution and to ensure operational stability.

For more information, refer to [ALTER TRIGGER name COMPILE](31-psm-sql-references.md#d86df859bc319efc).

```
gSQL> CREATE TABLE t1_history( sess_id INTEGER, stmt_view_scn VARCHAR(64), tran_date DATE );
Table created.

gSQL>
CREATE OR REPLACE TRIGGER t1_trig
AFTER INSERT ON t1
DECLARE
  t1_his t1_history%ROWTYPE;
BEGIN
  t1_his.sess_id := SESSION_ID();
  t1_his.stmt_view_scn := STATEMENT_VIEW_SCN();
  t1_his.tran_date := TRANSACTION_DATE();
  
  INSERT INTO t1_history VALUES t1_his;
END;
/
Trigger created.

gSQL> DROP TABLE IF EXISTS t1_history;
Table dropped.

gSQL> COMMIT;
Commit complete.

gSQL> 
SELECT SCHEMA_NAME
      ,OBJECT_NAME
      ,OBJECT_TYPE
      ,STATUS
  FROM USER_OBJECTS
 WHERE OBJECT_NAME = 'T1_TRIG';

SCHEMA_NAME OBJECT_NAME OBJECT_TYPE STATUS
----------- ----------- ----------- -------
PUBLIC      T1_TRIG     TRIGGER     INVALID
1 row selected.

gSQL> ALTER TRIGGER t1_trig COMPILE;

ERR-01000(16659): Warning: trigger "PUBLIC"."T1_TRIG" has compilation errors :
(1) at (6:10): ERR-2F000(17012): unknown type name
(2) at (8:3): ERR-2F000(17006): unknown variable or column name (T1_HIS)
(3) at (9:3): ERR-2F000(17006): unknown variable or column name (T1_HIS)
(4) at (10:3): ERR-2F000(17006): unknown variable or column name (T1_HIS)
(5) at (12:33): ERR-2F000(17006): unknown variable or column name (T1_HIS)
Trigger altered.

gSQL> CREATE TABLE t1_history( sess_id INTEGER, stmt_view_scn VARCHAR(64), tran_date DATE );
Table created.

gSQL> ALTER TRIGGER t1_trig COMPILE;
Trigger altered.

gSQL> 
SELECT SCHEMA_NAME
      ,OBJECT_NAME
      ,OBJECT_TYPE
      ,STATUS
  FROM USER_OBJECTS
 WHERE OBJECT_NAME = 'T1_TRIG';

SCHEMA_NAME OBJECT_NAME OBJECT_TYPE STATUS
----------- ----------- ----------- ------
PUBLIC      T1_TRIG     TRIGGER     VALID
1 row selected.
```

> The STATUS column in the USER_OBJECTS view indicates the state of an object and is displayed as either VALID or INVALID.

<a id="78237a6c709bb28c"></a>
### Trigger Execution Order

When multiple triggers share the same timing and event level, they are assigned priority based on their creation time and are executed sequentially in that order. The execution order of triggers can be modified using the ALTER TABLE SET TRIGGER ORDER statement.

For more information, refer to [ALTER TABLE name SET TRIGGER ORDER](../part-03-sql-manual/18-sql-references-a-b.md#24a95716d0044b84).

```
gSQL>
SELECT EVENT_OBJECT_TABLE
      ,TRIGGER_NAME
      ,ACTION_ORDER
      ,ACTION_TIMING
      ,ACTION_ORIENTATION
  FROM INFORMATION_SCHEMA.TRIGGERS
 WHERE EVENT_OBJECT_TABLE = 'T1';

EVENT_OBJECT_TABLE TRIGGER_NAME        ACTION_ORDER ACTION_TIMING ACTION_ORIENTATION
------------------ ------------------- ------------ ------------- ------------------
T1                 T1_TRIG_POST_UPDATE            1 AFTER         STATEMENT
T1                 T1_TRIG                        2 AFTER         STATEMENT
2 rows selected.

gSQL> ALTER TABLE t1 SET TRIGGER ORDER t1_trig, t1_trig_post_update;
Table altered.

gSQL>
SELECT EVENT_OBJECT_TABLE
      ,TRIGGER_NAME
      ,ACTION_ORDER
      ,ACTION_TIMING
      ,ACTION_ORIENTATION
  FROM INFORMATION_SCHEMA.TRIGGERS
 WHERE EVENT_OBJECT_TABLE = 'T1';
 
EVENT_OBJECT_TABLE TRIGGER_NAME        ACTION_ORDER ACTION_TIMING ACTION_ORIENTATION
------------------ ------------------- ------------ ------------- ------------------
T1                 T1_TRIG                        1 AFTER         STATEMENT
T1                 T1_TRIG_POST_UPDATE            2 AFTER         STATEMENT
2 rows selected.
```

---

[← 28. External Routine](28-external-routine.md) · [Table of contents](../README.md) · [30. PSM Language Element References →](30-psm-language-element-references.md)

<sub>Copyright © 2010 SUNJESOFT Inc. All rights reserved.</sub>
