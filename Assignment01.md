```
1. Create a Table Employee which has (Empno int and unique,Ename 30 chars and not null,Address char 30, City Char 30)
Add some Employees of City Bangalore and some of city Delhi
2. Create SalarySlab table which has following fields
   Salaryslabid int unique autoincremented
   Allowances int
   Deductions  int
   BaseSal   int

3. Create a Payroll table which indicates the salary breakups for the employes and it has following fields
   1. ID int unique
   2. EmpNo int and refer to Employee table
   3. Salaryslabid int refer SalarySlab table 

Create Following reports using sql queries

1. Display all the Employees Total Salary (BaseSal + Allowances -Deductions).
2. Update SalarySlab of an Employee
3. Display Empname whose salary is maximum
4. Display all the employees citywise who are getting maximum salary.
5. Display all Salary Slab of each employee
6. Update the deduction of deduction +10% for all salary Slabs.
```
