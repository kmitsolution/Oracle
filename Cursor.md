## Implicit Cursor

### Example
```sql
DECLARE  
   total_rows number(2); 
BEGIN 
   UPDATE emp 
   SET sal = sal + 500; 
   IF sql%notfound THEN 
      dbms_output.put_line('no customers selected'); 
   ELSIF sql%found THEN 
      total_rows := sql%rowcount;
      dbms_output.put_line( total_rows || ' employees update '); 
   END IF;  
END; 
```

## Explicit cursor

### Example
```sql
DECLARE
emprec emp%RowType;
cursor cur1 is
 select * from emp;
 BEGIN
 Open cur1;
 LOOP
   FETCH cur1 into emprec;
      EXIT when cur1%notfound;
   DBMS_OUTPUT.put_line(emprec.ename);

 END LOOP;
 close cur1;
 END;
```
