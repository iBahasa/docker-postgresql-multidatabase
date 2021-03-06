# Docker Multiple Database for PostgreSQL

Based on Postgresql 9.5 (Can be used to any versions) with Persistent Data.

## Usage
- Stop your current postgresql default system (If you have installed postgresql on PORT 5432):
```
$ sudo service postgresql stop
```
- Build the Dockerfile and compose it!

```
$ docker build -t postgres_multi .
$ docker-compose up -d
```

It will create 3 database for you `prod_db`, `dev_db`, and `test_db` within `postgres` User.

In order to test `psql` command, you can stop postgresql system by `sudo service postgresql stop` that uses PORT 5432.

And then:
> Show created database

```
$ psql -h localhost -p 5432 -U postgres
Password for user postgres: 
psql (9.5.5, server 9.5.12)
Type "help" for help.
postgres=# \l
                                 List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
-----------+----------+----------+------------+------------+-----------------------
 dev_db    | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/postgres         +
           |          |          |            |            | postgres=CTc/postgres
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 prod_db   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/postgres         +
           |          |          |            |            | postgres=CTc/postgres
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
           |          |          |            |            | postgres=CTc/postgres
 test_db   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/postgres         +
           |          |          |            |            | postgres=CTc/postgres
(6 rows)
postgres=# \q
```

> Use psql -d (database) option

> Show database table
```
$ psql -h localhost -p 5432 -U postgres -d prod_db
```

> Use docker exec, See container ID before by 'docker ps' command

```
$ docker ps
$ docker exec -it [container-id] bash
$ psql -U postgres
```
