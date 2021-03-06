## Create Emp Table
CREATE Table EMP (
EMPNO number(4), ENAME varchar2(30), JOB char(10), MGR number(4),
HIREDATE date, SAL number(7,2), DEPTNO number(2));

## Insert some records

INSERT INTO EMP VALUES(1001,'SHAVANI','SE',1008,'20-SEP-2000',10000,1)

INSERT INTO EMP VALUES(1002,'DHAIVAT','SSE',1008,'20-SEP-1998',15000,2)

INSERT INTO EMP VALUES(1003,'GUJHRATHI','SE',1007,'20-SEP-2002',10000,2)

INSERT INTO EMP VALUES(1004,'KUMAVAT','SSE',1007,'2-AUG-2006',15000,1)

INSERT INTO EMP VALUES(1005,'RAVI','MGR',1008,'2-AUG-2006',18000,1)

INSERT INTO EMP VALUES(1006,'RAJNISH','MGR',1007,'2-AUG-2008',16000,1)


## CREATE DEPT TABLE
CREATE TABLE DEPT ( DEPTNO NUMBER,DNAME VARCHAR(30),LOC VARCHAR(30))

## INSERT SOME RECORDS
INSERT INTO DEPT VALUES(1,'PROJECT MGMT','BANGALORE')

INSERT INTO DEPT VALUES(2,'HR MGMT','NY')

INSERT INTO DEPT VALUES(3,'SAL MGMT','BANGALORE')

INSERT INTO DEPT VALUES(4,'HIRING MGMT','NY')

## CREATE TABLE SALGRADE
CREATE TABLE SALGRADE(GRADE VARCHAR(30),LOSAL NUMBER,HISAL NUMBER)

## INSERT SOME OF THE RECORDS
INSERT INTO SALGRADE VALUES(1,10000,20000)

INSERT INTO SALGRADE VALUES(2,7000,15000)

INSERT INTO SALGRADE VALUES(3,5000,10000)

INSERT INTO SALGRADE VALUES(4,3000,7000)


### Let's have some fun with the queries

<b>TO FIND ALL THE EMPLOYESS WHICH BELONGS TO PROJECT MGMT DEPT NAME</b>

SELECT ENAME FROM EMP JOIN DEPT ON EMP.DEPTNO=DEPT.DEPTNO 
WHERE  DNAME='PROJECT MGMT'

<b> DISPLAY EMP DETAILS IN ASC ORDER OF DEPT NUMBER AND DESCENDING ORDER OF HIREDATE</b>

select ENAME, DNAME, HIREDATE 
from EMP E  JOIN DEPT D ON E.DEPTNO=D.DEPTNO
order by E.DEPTNO , HIREDATE desc;

### DISPLAY ALL EMP NAME AND THEIR SALARY WHO BELONGS TO BANGLORE DEPT CITY

SELECT ENAME,SAL FROM EMP E JOIN DEPT D ON E.DEPTNO=D.DEPTNO
WHERE LOC='BANGALORE'

### DISPLAY TOTAL NUMBER OF EMPLOYEES IN EACH DEPT.
SELECT DEPTNO,COUNT(ENAME) AS TOTALEMP FROM EMP GROUP BY DEPTNO

### EXERCISE
1. Find all the employees whose salary is more than 10000
2. Display all the Department Names
3. Display all the employees who belongs to Project mgmt department and residing in Bangalore
4. Insert a new record in Emp table with emp no=1010,name=Rajesh,DeptNo=4,Hiredate=23-Jul-1998,Sal=20000


### Constraint

### Example
```sql
Create table Student(
Id int constraint pks Primary key,
Admno int unique,
Name Varchar(20) not null,
Marks int constraint markscheck check(Marks>=80),
StreetAddress Varchar(30),
City Varchar(20) default 'Bangalore')

insert into Student values(1,101,'Shubham',90,'S1','Bhopal')

insert into Student (Id,Admno,Name,Marks,StreetAddress)values(2,102,'Dhaivat',92,'S2')

insert into Student (Id,Admno,Name,Marks,StreetAddress)values(3,103,'Shivani',93,'S3')

insert into Student (Id,Admno,Name,Marks,StreetAddress,City)values(4,104,'Ravi',80,'S4','Mumbai')

insert into Student (Id,Admno,Name,Marks,StreetAddress,City)values(5,105,'Rajneesh',85,'S5','Mumbai')

Create Table Sports
(
SportsId int Primary key,
Name Varchar(30) not null,
Coach varchar(30),
Id int References Student(Id))

insert into Sports values(1001,'Cricket','Ravi Shastri',1)

insert into Sports values(1002,'Hockey','Singh',2)

```
  
  ### Alter Table
  
  ```sql
  -- Add a column in Student table with name as State
Alter table student add  State Varchar(30)

-- Modify column State to Varchar(50)

Alter table Student Modify State Varchar(50)

-- Drop a column
Alter table Student drop column State 

--see all the constraint to a table
SELECT *
  FROM user_cons_columns
 WHERE lower(table_name) ='student'
 
--- remove a constraint

Alter table Student drop constraint MARKSCHECK

--- Add a Constraint

Alter table Student add constraint MARKSCHECK check (Marks>=70)

  ```
  ### Add Autoincrement column
  
  ```sql
  CREATE SEQUENCE dept_seq START WITH 1;

CREATE TABLE departments (
  ID           NUMBER(10)    DEFAULT dept_seq.nextval NOT NULL,
  DESCRIPTION  VARCHAR2(50)  NOT NULL);

ALTER TABLE departments ADD (
  CONSTRAINT dept_pk PRIMARY KEY (ID));
  
  insert into departments (DESCRIPTION) values('dept1');
  insert into departments (DESCRIPTION) values('dept2');
  
  select * from departments
  ```
  
  ### Delete Statement
  Delete the records from the table and it can be rolled back
  
  ```sql
  select * from departments
  delete from departments
  select * from departments
  --- rollback will revert back the changes deleted records we can see again
  rollback
    
  ```
  
  ### Truncate command
  Delete all the records permanently means cannot be rolledback
  
  ```sql
  Trucate table departments
  ```
  
  ### Update Statement
  To update record(s) in a table.

  
  ```sql
  
Update Student set streetaddress='S0' where id=1

Update Student set streetaddress=Concat(streetaddress , '-A1')
  ```
  
  ### Creating a Table from Existing Table
  ```sql
  --- Creating an empty table from Existing table
create table Student2 
as
Select * from Student where 1=0

-- inserting into Student1 table from student
insert into Student1
select * from Student 
  ```
  

### Retrieve all employees who are working in department 1 and who earn at least as much as any (i.e., at least one) employee working in department 2:
```sql
select * from EMP
where SAL > any
(select SAL from EMP
where DEPTNO = 2)
and DEPTNO = 1;
```
### List all employees who are not working in department 1 and who earn more than all employees working in department 1:
```sql
select * from EMP
where SAL >= all
(select SAL from EMP
where DEPTNO = 1)
and DEPTNO <> 1;
```
### List all departments that have no employees:
```sql
select * from DEPT
where  not exists
(select * from EMP
where DEPTNO = DEPT.DEPTNO);
```

### ResultSet Commands

Example: Assume that we have a table EMP2 that has the same structure and columns
as the table EMP:
```sql
 All employee numbers and names from both tables:
select EMPNO, ENAME from EMP
union
select EMPNO, ENAME from EMP2;
 Employees who are listed in both EMP and EMP2:
select * from EMP
intersect
select * from EMP2;
 Employees who are only listed in EMP:
select * from EMP
minus
select * from EMP2;

```

### Drop Table
```sql
  Drop table Student2
```
### Case End Statement
```sql
SELECT ENAME,SAL, 
CASE 
  WHEN SAL>=20000
  THEN 'Elgible for Manager'
  WHEN SAL>=15000
  THEN 'ELigible for Asst Mgr'
  ELSE
  'Do your Regular work'
  END Promotion
  From Emp
```
### Sql Functions Refernces

https://docs.oracle.com/cd/B19306_01/server.102/b14200/functions001.htm
