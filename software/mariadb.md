MariaDB
=======

Create new database
-------------------
```sql
CREATE DATABASE `dbname` CHARACTER SET utf8 COLLATE utf8_general_ci;
```
```bash
mysql -h localhost -uuser -ppassword -e "CREATE DATABASE dbname CHARACTER SET utf8 COLLATE utf8_general_ci"
```

Dump database structure only
----------------------------
Add the "d" flag to mysqldump.
```bash
mysqldump -d
mysqldump -d -h localhost -uuser -ppassword database > database.sql
```

Import from a dump file
-----------------------
```bash
mysql -h localhost -uuser -ppassword database < database.sql
```

Compare data structure of two databases
---------------------------------------
```bash
mysqldbcompare -t --skip-data-check --server1=user:password@localhost --server2=user:password@localhost --difftype=sql dbname:dbname
```
