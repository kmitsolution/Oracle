## functions
These are set of PL/SQL Statements which returns a value.

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
