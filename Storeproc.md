## Stored Procedure
These are set of statments which are under a single name and can be compiled and execute.

## Exec
Exec <<Procedure Name>>
  

## Example1
```sql
CREATE OR REPLACE Procedure GradeProc 
AS
BEGIN
DECLARE
type namesarray IS VARRAY(5) OF VARCHAR2(10);
type grades IS VARRAY(5) OF INTEGER;
names namesarray;
marks grades;
total integer;
BEGIN
names := namesarray('Kavita', 'Pritam', 'Ayan', 'Rishav', 'Aziz');
marks:= grades(98, 97, 78, 87, 92);
total := names.count;
dbms_output.put_line('Total '|| total || ' Students');
FOR i in 1 .. total LOOP
dbms_output.put_line('Student: ' || names(i) || '
Marks: ' || marks(i));
END LOOP;
END;
END;

```
## Example
```sql
      CREATE OR REPLACE Procedure RANK
    AS
    BEGIN
    declare
    name1 varchar(20);
    Sal1 number;
    BEGIN
        SELECT ENAME,SAL INTO Name1,Sal1  FROM EMP Where Empno=1001;
        IF sal1>=1500 THEN
         dbms_output.put_line('manager'||Name1);
         END IF;
      IF sal1>=1000 and sal1<1500 THEN
          dbms_output.put_line('asst manager'||Name1);
        END IF;
    IF sal1<1000 THEN
     
          dbms_output.put_line('develoeper'||Name1);
       END IF;
   END;
 END;
 
 EXEC Rank
```  

 ## Example 
  ```sql
  CREATE Procedure rowtype
AS
BEGIN
DECLARE
emp1 emp%Rowtype;
BEGIN

select * into emp1 from EMP where empno=1001;
DBMS_OUTPUT.put_line(emp1.ename);
END;
END;  
 ```
  
### Example Stored proc with input parameter
```sql
  CREATE or Replace Procedure rowtype(n number,name varchar)
AS
BEGIN
DECLARE
emp1 emp%Rowtype;
BEGIN

select * into emp1 from EMP where empno=n;
DBMS_OUTPUT.put_line(emp1.ename);
DBMS_OUTPUT.PUT_LINE(name);
END;
END;
EXEC rowtype(1003,'cognixia') ; 
```  

  ### Example
  ```sql
  create procedure first
AS
Begin
DBMS_OUTPUT.PUT_LINE('First Procedure is executed');
End;

CREATE or replace Procedure Second
AS
Begin
first;
DBMS_OUTPUT.PUT_LINE('Second Procedure');
End;

Exec Second
  ```
  ### Example --Find the Dept of a particurlar emp and print its Dname using Join
-- Find the Dept of a particurlar emp and print its Dname using below procedure
   DeptProcedure(Deptno) returns the Dname from Dept Table --one proc

  ### Example IN and OUT
  ```sql
  CREATE PROCEDURE findMin(x IN number, y IN number, z OUT number) IS 
BEGIN 
   IF x < y THEN 
      z:= x; 
   ELSE 
      z:= y; 
   END IF; 
END;   

DECLARE 
   a number; 
   b number; 
   c number;
BEGIN 
   a:= 23; 
   b:= 45; 
   findMin(a, b, c); 
   dbms_output.put_line(' Minimum of (23, 45) : ' || c); 
END; 



  ```
## Example of in out parameter           
```sql
CREATE OR REPLACE Procedure rowtype(emp1 out  emp%Rowtype,n number)
AS
BEGIN
DECLARE

BEGIN
select * into emp1 from EMP where empno=n;
DBMS_OUTPUT.put_line(emp1.ename);
END;
END;  

DECLARE
emp1 emp%Rowtype;
BEGIN
rowtype(emp1,1001);
dbms_output.put_line(emp1.ename);
END;           
```           
           
