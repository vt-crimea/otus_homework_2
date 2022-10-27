# Домашнее задание
## Работа с уровнями изоляции транзакции в PostgreSQL

<img width="300" alt="1" src="https://user-images.githubusercontent.com/44090170/198328975-50373955-5487-4853-b99e-f8297034f3f6.png">


$ sudo apt-get update

$ pg_lsclusters
14  main    5432 online postgres /var/lib/postgresql/14/main /var/log/postgresql/postgresql-14-main.log

подключаемся к postgres
$ sudo -i -u postgres
postgres=# psql

создаем БД для экспериментов:
# create database homework;

Список баз данных:
postgres=# \l
                                  List of databases
   Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges
-----------+----------+----------+-------------+-------------+-----------------------
 homework  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
(4 rows)

Подключаемся к созданной бд:
postgres=# \c homework
You are now connected to database "homework" as user "postgres".

