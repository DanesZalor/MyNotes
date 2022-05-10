# [MariaDB](https://wiki.archlinux.org/title/MariaDB)

### Resources
- [MySQL cheat sheet](https://devhints.io/mysql)
- [Field Data types](https://www.w3schools.com/sql/sql_datatypes.asp)
- [SQL datetime format](https://dev.mysql.com/doc/refman/8.0/en/datetime.html)

To open MariaDB:
```bash
~$ mysql -u <user> -p <pass>
```

## Database Operations
To create database:
```SQL
CREATE DATABASE databaseName;
```

To open database:
```SQL
USE databaseName;
```
> You need to use database before you do operations on them like Adding tables.


To delete database:
```SQL
DROP DATABASE databaseName;
```

## Table Operations
### Create Table
```SQL
CREATE TABLE tableName(
    field1 type1,
    field2 type2,
    ...,
    PRIMARY KEY (field1,...)
);
```

#### Foreign Key
```SQL
CREATE TABLE tableName(
    ..., FOREIGN KEY (fieldName) REFERENCES table2 (table2field)
);
```

### Table Data
#### Adding data to table
```SQL
INSERT INTO tableName(
    field1, field2, ...
) VALUES (
    value1, value2, ...
);
```
#### Show table data
```SQL
SELECT * FROM tableName;
```
or with conditions
```SQL
SELECT * FROM tableName WHERE conditions;
```


