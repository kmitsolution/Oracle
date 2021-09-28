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

### Example -DDL Trigger

```sql
CREATE TABLE AUDIT_DDL (
  d date,
  OSUSER varchar2(255),
  CURRENT_USER varchar2(255),
  HOST varchar2(255),
  TERMINAL varchar2(255),
  owner varchar2(30),
  type varchar2(30),
  name varchar2(30),
  sysevent varchar2(30));
  
create or replace trigger audit_ddl_trg after ddl on schema
begin
  if (ora_sysevent='TRUNCATE')
  then
    null; -- I do not care about truncate
  else
    insert into audit_ddl(d, osuser,current_user,host,terminal,owner,type,name,sysevent)
    values(
      sysdate,
      sys_context('USERENV','OS_USER') ,
      sys_context('USERENV','CURRENT_USER') ,
      sys_context('USERENV','HOST') ,
      sys_context('USERENV','TERMINAL') ,
      ora_dict_obj_owner,
      ora_dict_obj_type,
      ora_dict_obj_name,
      ora_sysevent
    );
  end if;
end;


create table temp(id number);
drop table temp
select * from AUDIT_DDL
```
