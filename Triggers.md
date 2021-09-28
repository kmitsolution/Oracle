## Trigger
```sql
CREATE [OR REPLACE] TRIGGER trigger_name
{BEFORE | AFTER } triggering_event ON table_name
[FOR EACH ROW]
[FOLLOWS | PRECEDES another_trigger]
[ENABLE / DISABLE ]
[WHEN condition]
DECLARE
    declaration statements
BEGIN
    executable statements
EXCEPTION
    exception_handling statements
END;
```

### Example
```sql
--Creating a trigger which fired when update statement is executed on emp table
CREATE OR REPLACE TRIGGER TRG1
AFTER UPDATE ON EMP
FOR EACH ROW
BEGIN
DBMS_OUTPUT.put_line('Trigger fired');
END;

Update Emp set sal=sal+100 where empno=1001
```

### Example

```sql
create table Audit1( Trans Varchar(30), remarks varchar(30))

--Creating a trigger which fired when update statement is executed on emp table
CREATE OR REPLACE TRIGGER TRG1
AFTER UPDATE ON EMP
FOR EACH ROW
BEGIN
INSERT into  Audit1 Values('Update','EMP Table');
END;

Update Emp set sal=sal+100 where empno=1001
select * from Audit1

```

### Example

```sql
--Creating a trigger which fired when update statement is executed on emp table and we can capture old and new value of a column
CREATE OR REPLACE TRIGGER TRG1
AFTER UPDATE  ON EMP
FOR EACH ROW
BEGIN
INSERT into  Audit1 Values('EMP Old',TO_CHAR(:old.sal));
INSERT into  Audit1 Values('EMP Old',TO_CHAR(:new.sal));
END;

Update Emp set sal=sal+100 where empno=1001

select * from Audit1
```

### Example
```sql
--Creating a trigger which fired when update statement is executed on emp table and we can capture old and new value of a column
CREATE OR REPLACE TRIGGER TRG1
AFTER DELETE OR INSERT OR UPDATE OF SAL ON EMP
FOR EACH ROW
BEGIN
IF INSERTING THEN
    INSERT into  Audit1 Values('INSERT :-> NEW SAL=' || TO_CHAR(:new.sal));
ELSIF UPDATING THEN
    INSERT into  Audit1 Values('UPDATE:-> OLD SAL='|| TO_CHAR(:old.sal) || ',NEW SAL=' || TO_CHAR(:new.sal));
ELSIF DELETING THEN
   INSERT into  Audit1 Values('DELETE:->OLD SAL='|| TO_CHAR(:old.sal));
END IF;
END;

```

### Example
```sql
CREATE OR REPLACE TRIGGER TRG1
AFTER DELETE OR INSERT OR UPDATE OF SAL ON EMP
FOR EACH ROW
BEGIN
IF INSERTING THEN
    INSERT into  Audit1 Values('INSERT :-> NEW SAL=' || TO_CHAR(:new.sal));
ELSIF UPDATING THEN
IF :new.sal = :old.sal THEN
DBMS_OUTPUT.put_line('No Sal Updated');
ELSE
 INSERT into  Audit1 Values('UPDATE:-> OLD SAL='|| TO_CHAR(:old.sal) || ',NEW SAL=' || TO_CHAR(:new.sal));
DBMS_OUTPUT.put_line('Sal Updated');
END IF;
ELSIF DELETING THEN
   INSERT into  Audit1 Values('DELETE:->OLD SAL='|| TO_CHAR(:old.sal));
END IF;
END;

```
