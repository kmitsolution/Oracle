## Examples
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
