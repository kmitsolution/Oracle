## Examples
```sql
-- PLSQL Program to Find the EmpName whose EmpNo =1001
DECLARE
Name1 VARCHAR2(20);
BEGIN
SELECT ENAME INTO Name1 FROM EMP WHERE EMPNO=1001;
dbms_output.put_line(Name1);
END;
```
