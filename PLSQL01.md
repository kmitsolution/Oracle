## Examples
### Example 1
```sql
-- PLSQL Program to Find the EmpName whose EmpNo =1001
DECLARE
Name1 VARCHAR2(20);
Sal1 number;
BEGIN
SELECT ENAME,SAL INTO Name1,Sal1  FROM EMP WHERE EMPNO=1001;
dbms_output.put_line(Name1);
dbms_output.put_line(Sal1);
END;
```
### Example 2
```sql
-- This program to delete a particualr record
DECLARE
Name1 VARCHAR2(20);
Sal1 number;
BEGIN
SELECT ENAME,SAL INTO Name1,Sal1  FROM EMP WHERE EMPNO=1001;
DELETE from Emp where Ename=Name1;
END;
```
### Example 3
```sql
-- PLSQL Program to Find the EmpName whose EmpNo =1001 and Update the salary =5000 if salary is <5000
DECLARE
Name1 VARCHAR2(20);
Sal1 number;
BEGIN
    SELECT ENAME,SAL INTO Name1,Sal1  FROM EMP WHERE EMPNO=1001;
    IF sal1>=5000 THEN
      dbms_output.put_line(Name1);
      dbms_output.put_line(sal1);
    ELSE
     Update EMP SET Sal=5000 where ENAME=Name1;  
    END IF;
   
END;
```
