## Views
SQL view is nothing but a logical table or a virtual table stored in a database. We can also define a VIEW as SELECT Statement with a name which is stored in a database as though it were a table. All the DML commands which you can perform on a table can be performed on a view also.

Use of SQL View in Oracle Database

### Views in any database are majorly used for two reasons – 
#### Security
Reducing complexity of a query.
Security:
Using a VIEW you can mask columns of a table and restrict any user to use the data from that column. For example,

Suppose you have a large table containing a mixture of both sensitive as well as general interest information. In this case it will be very handy for you to create a view which only queries the general interest columns of the original table and in turn grants privileges on this view to the general users. In this case the population of general users can query the view and have direct access only to the general information omitting the sensitive information present in the underlying table. Thus in this way views can be used to give access to selective data in a table. 

Reducing the complexity of a query

Another reason for using a VIEW is to reduce the complexity of a query which is made by joining various tables. For example,

A view built on a complex join can be created in order to include the complexity in the view itself. The result of this is a regular view object that looks to be a single table which could be queried by you as any regular table. The view can be joined with other views and tables as well. Thus here in this way, view can be used to reduce the complexity of a common Join. 
```sql
Syntax of SQL VIEW in Oracle Database
CREATE VIEW  view_name  AS  
  SELECT  column_name(s)  FROM  table_name  WHERE condition;

This is a syntax of a very simple view which starts with the CREATE and VIEW keyword followed by the name of the View, you can assign any name of your desire to your view. Next we have “AS” which is again an oracle reserved keyword and followed this we have our Select statement.
Suggested Tutorial: How to retrieve data using SELECT DML statement in Oracle Database

Prerequisites
To create a view in your own schema, you must have the CREATE VIEW system privilege. To create a view in another user’s schema, you must have the CREATE ANY VIEW system privilege.

Create a Simple View
In this example I will create a view by the name of vw_rebellion on Employees table of HR schema. You can give whatever name you want to your view. 

CREATE VIEW  vw_rebellion  AS 
  SELECT  first_name,  email,  phone_number  FROM  employees;

This is a very simple view created on “Employees” table of HR user and it will hold all the rows of First name, email and phone number columns of the base table employees. Once a view is created, it can be referred to in your select statement as if it were a table.

How to recreate a View (OR REPLACE)
We use OR REPLACE to recreate the definition of a view after creating it. Suppose in the above view vw_rebellion you realize that along with the first name column you also want to have the last name column. There are two options to do this task either drop the view and recreate it from scratch or just recreate the view without dropping it. Let’s see how:

CREATE  OR REPLACE  VIEW  vw_rebellion  AS 
  SELECT  first_name,  last_name,  email,  phone_number  FROM  employees; 

Apart from the OR REPLACE and the column LAST NAME nothing is different in the query. This query will replace the definition of old vw_rebellion view by the definition of new vw_rebellion view.

As I mentioned earlier that once you have created a view you can execute all the DML statements on that view as though it were a table. Let’s see how.

How to check the definition of a SQL VIEW in Oracle Database (Describe/ desc dml)
You can use Describe/ DESC dml command to see the definition of your view e.g.

DESC vw_rebellion;

I know “Describe” is a DDL statement not DML but I thought this tip is worth sharing.

How To retrieve Rows from a VIEW in Oracle Database (SELECT ddl)
You can use SELECT ddl command to retrieve rows from a VIEW similar to the way we do with tables in oracle database.

SELECT * FROM vw_rebellion

You can also use ORDER BY clause to sort the result.

SELECT * FROM vw_rebellion ORDER BY first_name;

Furthermore you can even use WHERE clause in your SELECT statement to filter the result.

SELECT * FROM vw_rebellion WHERE first_name = ‘Nancy’;

Info Byte: In case you want to use WHERE and ORDER BY clause in a single SELECT statement then always remember WHERE clause will come before the ORDER BY clause in the query. For Example 

SELECT  *  FROM  vw_rebellion   WHERE  first_name =  ‘Nancy’  ORDER BY  first_name;

How to UPDATE rows in a VIEW (UPDATE ddl)
Similar to the SELECT ddl we can also execute UPDATE ddl on a VIEW. Suppose you want to update the email address of the employee Nancy then query for this will be: 

UPDATE vw_rebellion SET email =’nancy@example.com’ WHERE first_name =’Nancy’;

How to delete rows in a VIEW (DELETE ddl)
You can execute DELETE DML command to delete one or more rows from the table using VIEWS.

DELETE FROM vw_rebellion WHERE first_name = ‘Nancy’;

How to insert Row in a VIEW in Oracle Database (INSERT ddl)
To insert a row, a view has to satisfy all the constraints on any column of underlying table over which it’s created. Insert DML is subject to several restrictions when executed on a View in Oracle database such as:

A view must contain the entire Not Null column from underlying table. The failure to include any columns that have NOT NULL constraints from the underlying table in the view will result in the non-execution of the INSERT statement. However an UPDATE or DELETE statement can be issued.

If there is any column with referential key constraint in underlying table then view must contain that column and a proper value must be provided to that column while performing Insert dml on the View and many more.

Thus to perform an INSERT dml on a view, it has to include all the columns which either have NOT NULL constraint or Referential constraint or any other mandatory constraint from the base table employees.
E.g.

INSERT  INTO  vw_superheroes  VALUES  (‘Steve’, ‘Rogers’, 654765);

Where vw_supereheroes is another view created over Superheroes table which has 5 columns first name, last name, and real name, Phone number and SSN. This table has no constraint on any column.

How to create a complex view (View by joining two tables)
Complexity of a view depends upon the complexity of its SELECT statement. You can increase the complexity of a view by increasing the complexity of the SELECT statement. 

CREATE  OR  REPLACE  VIEW  vw_join  AS

  SELECT  first_name,  department_name  FROM  employees emp

   FULL  OUTER  JOIN  departments dept

  ON  (emp.DEPARTMENT_ID = dept.DEPARTMENT_ID);

As I told you above that by using a View you can reduce the complexity of a query. A view built on a complex join can be created in order to include the complexity in the view itself. The result of this is a regular view object that looks to be a single table which could be queried by you as any regular table. 
```
