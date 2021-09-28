## functions
These are set of PL/SQL Statements which returns a value.In Function we cannot use DML/DDL/DCL statements we can use DQL (SELECT).

### InBuilt Functions
These functions are already available in oracle, like upper(),lower(),Round() etc.

### User Defined Functions
These are customized means created by user.

#### Example1
```sql
create or replace function adder(n1 in number, n2 in number)    
return number    
is     
n3 number(8);    
begin    
n3 :=n1+n2;    
return n3;    
end;    

DECLARE
n number;

BEGIN
n:=adder(2,3);
DBMS_OUTPUT.put_line(n);
END;
```

### Example2
```sql
CREATE OR REPLACE FUNCTION FUNC1(N NUMBER) RETURN NUMBER IS
BEGIN
RETURN N+10;
END;
 
SELECT FUNC1(4) FROM DUAL;
SELECT ENAME,SAL,FUNC1(SAL) FROM EMP;
```

### Example3
```sql
create or replace function emp_grade(sal in number)    
return varchar  
is     
grade varchar(20);    
begin    
IF sal>=30000 THEN  
grade:='Manager';
ELSIF sal>20000 THEN
grade:='Ass. Manager';
ELSIF sal>1000 THEN
grade:='Developer';
ELSE    
grade:='Need Improve';
END IF;
return grade;
end;
select ename,sal,EMP_GRADE(sal) Grade from EMP;

```
### Example 4
```sql
create or replace function emp_office(location in varchar)
   return varchar
   AS
    office_type varchar(20);
    begin
    IF location='NY'
    THEN
    office_type:='Head Office';
    ELSIF location='BANGALORE' 
  THEN
  office_type:='Branch Office';
   ELSE
   office_type:='No Location';
   END IF;
   return office_type;
  end;
select * from dept
select ename ,sal,dname,loc,emp_office(loc) from emp e inner join dept t on e.deptno=t.deptno;
```

### Example 5
```sql
CREATE OR REPLACE Function func1(n in number, n1 in out number) RETURN Number IS
Begin
n1:=n1+3;
return n+5;
end;

Declare
n1 number:=10;
n number;
Begin
n:=func1(2,n1);
DBMS_OUTPUT.put_line(n1);
DBMS_OUTPUT.put_line(n);
select func1(2,n1) into n1 from dual;  -- Error because we are using INOUT parameter
End;
```
