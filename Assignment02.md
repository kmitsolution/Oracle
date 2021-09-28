```sql
1. Create a Table Employee with EMPNO(primary key),EMPNAME,HIREDATE,SAL,GRADE
2. Insert Some Records in this table but GRADE should be null
3. Create a Dept table with DEPTNO(primary key),DEPTNAME,CITY
4. Insert some records in the table
5. Create a Table DEPT_EMP with ID(primary key),DEPTNO(Reference key to DeptNo of DEPT table),EMPNO(Reference key to EMPNO of Employee table)
6. Insert some records in this table. This table indicates that which employee belongs to which dept. An employee can belong to multiple depts
7. Create a procedure to find a particular employee's department
8. Create a procedure which takes 2 parameters empno and varchar (which can be y or n). and in this procedure increase all employees sal by 10% and if second parameter is y then it should be permanent change and if it is n then increase salary should be rolled back.
9. Create function which finds the grade on an employee on the basis of salary
    if salary >=10000   GRADE 'A'
    if salary >=70000   GRADE 'B'
    ELSE GRADE 'C'
10. Update Grade for all the employees
11. Create a proceudre to find the employees who belongs to a particular dept number or name
```
