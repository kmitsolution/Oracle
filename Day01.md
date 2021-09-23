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
