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

\# create database homework;

Список баз данных:

postgres=# \l

<img width="200" alt="10" src="https://user-images.githubusercontent.com/44090170/198339161-37a1d5cd-1e2e-440d-af1a-372d919d80ba.png">

Подключаемся к созданной бд:

postgres=# \c homework

создаем таблицу:

create table persons(id serial, first_name text, second_name text);

CREATE TABLE

список таблиц:

\dt

<img width="195" alt="11" src="https://user-images.githubusercontent.com/44090170/198340599-c779a7d7-d131-42d6-ac5a-298e7caba4d6.png">

выключаем AUTOCOMMIT:

\set AUTOCOMMIT false

Вставляем записи:

postgres=# insert into persons(first_name, second_name) values('ivan', 'ivanov'); </br>
INSERT 0 1 </br>
postgres=\*# insert into persons(first_name, second_name) values('petr', 'petrov');</br>
INSERT 0 1</br>
postgres=\*# commit; </br>
*в командной строке появился символ \*, т.к. мы внутри транзакции* </br>
COMMIT </br>

текущий уровень изоляции:

postgres=# show transaction isolation level; </br>
transaction_isolation </br>
---------------------------</br>
read committed </br>

в первой сессии добавить новую запись insert into persons(first_name, second_name) values('sergey', 'sergeev');</br>
сделать select * from persons во второй сессии</br>

postgres=# select * from persons;</br>
 id | first_name | second_name</br>
----+------------+-------------</br>
  5 | ivan       | ivanov</br>
  6 | petr       | petrov</br>
(2 rows)</br>

видите ли вы новую запись и если да то почему?

завершить первую транзакцию - commit;

сделать select * from persons во второй сессии </br>
postgres=# select * from persons;</br>
 id | first_name | second_name</br>
----+------------+-------------</br>
  5 | ivan       | ivanov</br>
  6 | petr       | petrov</br>
  7 | petr       | petrov</br>
(2 rows)</br>
видите ли вы новую запись и если да то почему?

завершите транзакцию во второй сессии </br>
postgres=\*# commit;</br>
COMMIT</br>

начать новые но уже repeatable read транзации - set transaction isolation level repeatable read; </br>
в первой сессии добавить новую запись 
insert into persons(first_name, second_name) values('sveta', 'svetova');

сделать select * from persons во второй сессии
видите ли вы новую запись и если да то почему?
завершить первую транзакцию - commit;
сделать select * from persons во второй сессии
видите ли вы новую запись и если да то почему?
завершить вторую транзакцию
сделать select * from persons во второй сессии
видите ли вы новую запись и если да то почему?





