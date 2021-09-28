## Packages
```sql
SET SERVEROUT ON
CREATE or REPLACE PACKAGE cust_sal AS 
   PROCEDURE find_sal(c_id EMP.EMPNO%type); 
END cust_sal; 

CREATE OR REPLACE PACKAGE BODY cust_sal AS  
   
   PROCEDURE find_sal(c_id EMP.EMPNO%type) IS 
   c_sal EMP.sal%TYPE; 
   BEGIN 
      SELECT sal INTO c_sal 
      FROM EMP
      WHERE EMPNO = c_id; 
      dbms_output.put_line('Salary: '|| c_sal); 
   END find_sal; 
END cust_sal; 


DECLARE 
   code EMP.EMPNO%type := &cc_id; 
BEGIN 
   cust_sal.find_sal(code); 
END; 


```
