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

