# [postgresql](https://wiki.archlinux.org/title/PostgreSQL)

## Setup
1. install [postgresql](https://archlinux.org/packages/extra/x86_64/postgresql/)
2. switch to the PostgreSQL user 
```bash
$ sudo -iu postgres
```
3. initialize database cluster:
```bash
[postgres]$ initdb -D /var/lib/postgres/data
```
4. enable and start **postgresql.service**

[**Cheat Sheet**](https://quickref.me/postgres)

# [PDO](https://www.php.net/manual/en/book.pdo.php)

PDO Represents a connection between PHP and a database server.

```php
public PDO::__construct(
    string $dsn,
    ?string $username = null,
    ?string $password = null,
    ?array $options = null
)
```

Example:
```php
$dbconn = new PDO(
    "pgsql:host=${host};port=${port};dbname=${dbname};",
    $dbuser, $dbpass
);

if(!$dbconn) die("Couldn't connect");
```

Making queries
```php
$query_res = $pdo->query("SELECT * FROM customers");

foreach($query_res as $row)
    echo $row['id'].": ".$row['name']."<br>";
```