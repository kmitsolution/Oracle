## Example 1
```sql
DECLARE 
   emprec EMP%Rowtype;
   
BEGIN 
   SELECT  * INTO  emprec
   FROM EMP
   WHERE EMPNO = 1010;  
   
   DBMS_OUTPUT.PUT_LINE ('Name: '||  emprec.Ename); 
   DBMS_OUTPUT.PUT_LINE ('SAL: ' || emprec.sal); 
EXCEPTION 
   
   WHEN no_data_found THEN 
      dbms_output.put_line('No such customer!'); 
   WHEN others THEN 
      dbms_output.put_line('Error!'); 

END; 

```

### Example 2- Raise Exception

```sql
DECLARE 
   emprec EMP%Rowtype;
   
BEGIN 
   SELECT  * INTO  emprec
   FROM EMP
   WHERE EMPNO = 1001;  
   IF emprec.sal<=10000  then
    RAISE CASE_NOT_FOUND;
   end if;
   DBMS_OUTPUT.PUT_LINE ('Name: '||  emprec.Ename); 
   DBMS_OUTPUT.PUT_LINE ('SAL: ' || emprec.sal); 
EXCEPTION 
   
   WHEN CASE_NOT_FOUND THEN 
      dbms_output.put_line('Not Consider for hike'); 
   WHEN others THEN 
      dbms_output.put_line('Error!'); 

END; 

```

### Example 3 - User defined exception

```sql
DECLARE 
   emprec EMP%Rowtype;
   ex_invalid_id  EXCEPTION; 
BEGIN 
   SELECT  * INTO  emprec
   FROM EMP
   WHERE EMPNO = 1001;  
   IF emprec.sal<=10000  then
    RAISE ex_invalid_id;
   end if;
   DBMS_OUTPUT.PUT_LINE ('Name: '||  emprec.Ename); 
   DBMS_OUTPUT.PUT_LINE ('SAL: ' || emprec.sal); 
EXCEPTION 
   
   WHEN ex_invalid_id THEN 
      dbms_output.put_line('Not Consider for hike'); 
   WHEN others THEN 
      dbms_output.put_line('Error!'); 

END; 
```
