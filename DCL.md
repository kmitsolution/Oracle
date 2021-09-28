### Connect to a user id with its password to a database
 connect SYSTEM/India123@XEPDB1

#### To display current database
 SELECT * from GLOBAL_NAME

### To create the user
```sql
CREATE USER raman IDENTIFIED BY password123;
```

### To delete the user
```sql
DROP USER raman
```

### To provide connect permission to database
```sql
GRANT CONNECT TO RAMAN;
```


### To provide session permission
```sql
GRANT CREATE SESSION TO RAMAN
```

### Grant SELECT and DELETE permission to user raman

```sql
GRANT SELECT,DELETE on System.EMP to raman 
```

### Revoke permission from user raman

```sql
Revoke SELECT,DELETE ON EMP from raman
``

### To provide admin access
```sql
GRANT sysdba TO username
```

### Create any table
```sql
GRANT CREATE ANY TABLE TO username
```

### Drop any table

```sql
GRANT DROP ANY TABLE TO username
```

### Revoke permission
```sql
REVOKE CREATE TABLE FROM username
```



