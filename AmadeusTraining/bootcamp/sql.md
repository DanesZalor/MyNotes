# SQL best practice

T-SQL microsoft's propreitary <sub><sup>garbage</sub></sup>

database contains tables that ocntains records (rows) with data

|Id|fname|lname|
|-|-|-|
|1|bob|by|
|2|bob|ong|
|...|...|...|

# Data types
- **numerical** self explanatory, usable for arithmetic operations and shit
```SQL
WHERE Id = 1
```
- **character** char, varchar, nvarchar. can convert numerical to character
```SQL
WHERE fname = 'bob'
```
- **datetime**, date, time and can compare.
    - format is dynamic
```SQL
WHERE birthDate > '02/05/2022'

WHERE birthDate < '2022/05/10'
```


# Categories of SQL Command
- Data Definition Language
    - `CREATE` (table, proc, trigger, function)
    - `ALTER` modifies schema definition like add/removing a column
    - `DROP` deletes existing object (table/database)

- Data Manipulation Language
    manipulating the data itself inside the structure
    - `INSERT` row into table
    - `SELECT` 
    ```SQL
    SELECT * INTO account_copy FROM account
    ```
    - `UPDATE` a value from existing record
    ```SQL
    UPDATE account
    SET dateOfBirth = '8/1/2011'
    WHERE fname = 'Alice'
    ```
    - `DELETE` deleting rows from table
    ```SQL
    DELETE FROM account WHERE lname='amogus'
    ```
    - `TRUNCATE` cannot specify any conditions, will wipe out all data within the table and is non-logged operation so it's very fast
    ```SQL
    TRUNCATE TABLE account
    ```
    - `SELECT`
    ```SQL
    SELECT fname, lname FROM ACcount
    SELECT lname + ', ' + fname FROM account;
    ```