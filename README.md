## Задача 1

Используя docker поднимите инстанс PostgreSQL (версию 13). Данные БД сохраните в volume.

Подключитесь к БД PostgreSQL используя `psql`.

Воспользуйтесь командой `\?` для вывода подсказки по имеющимся в `psql` управляющим командам.

**Найдите и приведите** управляющие команды для:
- вывода списка БД
- подключения к БД
- вывода списка таблиц
- вывода описания содержимого таблиц
- выхода из psql

## Ответ  
```
docker volume create vol_pg13 && \
docker container run  \
--name pg13_devops -e POSTGRES_PASSWORD=strongpass \
-e POSTGRES_USER=pgusr -p 5434:5432 -v vol_pg13:/var/lib/postgresql/data \
-d postgres:13

Unable to find image 'postgres:13' locally
13: Pulling from library/postgres
025c56f98b67: Pull complete
26dc25c16f4e: Pull complete
a032d8a894de: Pull complete
40dba7d35750: Pull complete
8ebb44a56070: Pull complete
813fd6cf203b: Pull complete
7024f61bf8f5: Pull complete
23f986b322e8: Pull complete
946700296c28: Pull complete
f71725be6659: Pull complete
d4ca28c644eb: Pull complete
337909ee7a07: Pull complete
3c8a44dcc354: Pull complete
Digest: sha256:5fec4106f03419cb92dd604a8dd2ae85e724c640af743ba3d24ea2198f762250
Status: Downloaded newer image for postgres:13
b7d1ac37be2eb2e296dc1c98cd0ebd92cd8c9d28e6ed0133a0caab486921664a

docker container ps
CONTAINER ID   IMAGE         COMMAND                  CREATED              STATUS          PORTS                    NAMES
b7d1ac37be2e   postgres:13   "docker-entrypoint.s…"   About a minute ago   Up 58 seconds   0.0.0.0:5434->5432/tcp   pg13_devops

docker exec -it pg13_devops bash
root@b7d1ac37be2e:/# psql -U pgusr
psql (13.9 (Debian 13.9-1.pgdg110+1))
Type "help" for help.

pgusr=# \?
General
  \copyright             show PostgreSQL usage and distribution terms
  \crosstabview [COLUMNS] execute query and display results in crosstab
  \errverbose            show most recent error message at maximum verbosity
  \g [(OPTIONS)] [FILE]  execute query (and send results to file or |pipe);
                         \g with no arguments is equivalent to a semicolon
  \gdesc                 describe result of query, without executing it
  \gexec                 execute query, then execute each value in its result
  \gset [PREFIX]         execute query and store results in psql variables
  \gx [(OPTIONS)] [FILE] as \g, but forces expanded output mode
  \q                     quit psql
  \watch [SEC]           execute query every SEC seconds

Help
  \? [commands]          show help on backslash commands
  \? options             show help on psql command-line options
  \? variables           show help on special variables
  \h [NAME]              help on syntax of SQL commands, * for all commands

Query Buffer
  \e [FILE] [LINE]       edit the query buffer (or file) with external editor
  \ef [FUNCNAME [LINE]]  edit function definition with external editor
  \ev [VIEWNAME [LINE]]  edit view definition with external editor
  \p                     show the contents of the query buffer
  \r                     reset (clear) the query buffer
  \s [FILE]              display history or save it to file
  \w FILE                write query buffer to file

Input/Output
  \copy ...              perform SQL COPY with data stream to the client host
  \echo [-n] [STRING]    write string to standard output (-n for no newline)
  \i FILE                execute commands from file
  \ir FILE               as \i, but relative to location of current script
  \o [FILE]              send all query results to file or |pipe
  \qecho [-n] [STRING]   write string to \o output stream (-n for no newline)
  \warn [-n] [STRING]    write string to standard error (-n for no newline)

Conditional
  \if EXPR               begin conditional block
  \elif EXPR             alternative within current conditional block
  \else                  final alternative within current conditional block
  \endif                 end conditional block

Informational
  (options: S = show system objects, + = additional detail)
  \d[S+]                 list tables, views, and sequences
  \d[S+]  NAME           describe table, view, sequence, or index
  \da[S]  [PATTERN]      list aggregates
  \dA[+]  [PATTERN]      list access methods
  \dAc[+] [AMPTRN [TYPEPTRN]]  list operator classes
  \dAf[+] [AMPTRN [TYPEPTRN]]  list operator families
  \dAo[+] [AMPTRN [OPFPTRN]]   list operators of operator families
  \dAp[+] [AMPTRN [OPFPTRN]]   list support functions of operator families
  \db[+]  [PATTERN]      list tablespaces
  \dc[S+] [PATTERN]      list conversions
  \dC[+]  [PATTERN]      list casts
  \dd[S]  [PATTERN]      show object descriptions not displayed elsewhere
  \dD[S+] [PATTERN]      list domains
  \ddp    [PATTERN]      list default privileges
  \dE[S+] [PATTERN]      list foreign tables
  \det[+] [PATTERN]      list foreign tables
  \des[+] [PATTERN]      list foreign servers
  \deu[+] [PATTERN]      list user mappings
  \dew[+] [PATTERN]      list foreign-data wrappers
  \df[anptw][S+] [PATRN] list [only agg/normal/procedures/trigger/window] functions
  \dF[+]  [PATTERN]      list text search configurations
  \dFd[+] [PATTERN]      list text search dictionaries
  \dFp[+] [PATTERN]      list text search parsers
  \dFt[+] [PATTERN]      list text search templates
  \dg[S+] [PATTERN]      list roles
  \di[S+] [PATTERN]      list indexes
  \dl                    list large objects, same as \lo_list
  \dL[S+] [PATTERN]      list procedural languages
  \dm[S+] [PATTERN]      list materialized views
  \dn[S+] [PATTERN]      list schemas
  \do[S+] [PATTERN]      list operators
  \dO[S+] [PATTERN]      list collations
  \dp     [PATTERN]      list table, view, and sequence access privileges
  \dP[itn+] [PATTERN]    list [only index/table] partitioned relations [n=nested]
  \drds [PATRN1 [PATRN2]] list per-database role settings
  \dRp[+] [PATTERN]      list replication publications
  \dRs[+] [PATTERN]      list replication subscriptions
  \ds[S+] [PATTERN]      list sequences
  \dt[S+] [PATTERN]      list tables
  \dT[S+] [PATTERN]      list data types
  \du[S+] [PATTERN]      list roles
  \dv[S+] [PATTERN]      list views
  \dx[+]  [PATTERN]      list extensions
  \dy[+]  [PATTERN]      list event triggers
  \l[+]   [PATTERN]      list databases
  \sf[+]  FUNCNAME       show a function's definition
  \sv[+]  VIEWNAME       show a view's definition
  \z      [PATTERN]      same as \dp

Formatting
  \a                     toggle between unaligned and aligned output mode
  \C [STRING]            set table title, or unset if none
  \f [STRING]            show or set field separator for unaligned query output
  \H                     toggle HTML output mode (currently off)
  \pset [NAME [VALUE]]   set table output option
                         (border|columns|csv_fieldsep|expanded|fieldsep|
                         fieldsep_zero|footer|format|linestyle|null|
                         numericlocale|pager|pager_min_lines|recordsep|
                         recordsep_zero|tableattr|title|tuples_only|
                         unicode_border_linestyle|unicode_column_linestyle|
                         unicode_header_linestyle)
  \t [on|off]            show only rows (currently off)
  \T [STRING]            set HTML <table> tag attributes, or unset if none
  \x [on|off|auto]       toggle expanded output (currently off)

Connection
  \c[onnect] {[DBNAME|- USER|- HOST|- PORT|-] | conninfo}
                         connect to new database (currently "pgusr")
  \conninfo              display information about current connection
  \encoding [ENCODING]   show or set client encoding
  \password [USERNAME]   securely change the password for a user

Operating System
  \cd [DIR]              change the current working directory
  \setenv NAME [VALUE]   set or unset environment variable
  \timing [on|off]       toggle timing of commands (currently off)
  \! [COMMAND]           execute command in shell or start interactive shell

Variables
  \prompt [TEXT] NAME    prompt user to set internal variable
  \set [NAME [VALUE]]    set internal variable, or list all if no parameters
  \unset NAME            unset (delete) internal variable

Large Objects
  \lo_export LOBOID FILE
  \lo_import FILE [COMMENT]
  \lo_list
  \lo_unlink LOBOID      large object operations
pgusr=#
pgusr=# \l
                             List of databases
   Name    | Owner | Encoding |  Collate   |   Ctype    | Access privileges
-----------+-------+----------+------------+------------+-------------------
 pgusr     | pgusr | UTF8     | en_US.utf8 | en_US.utf8 |
 postgres  | pgusr | UTF8     | en_US.utf8 | en_US.utf8 |
 template0 | pgusr | UTF8     | en_US.utf8 | en_US.utf8 | =c/pgusr         +
           |       |          |            |            | pgusr=CTc/pgusr
 template1 | pgusr | UTF8     | en_US.utf8 | en_US.utf8 | =c/pgusr         +
           |       |          |            |            | pgusr=CTc/pgusr
(4 rows)
pgusr=# \c postgres
You are now connected to database "postgres" as user "pgusr".
pgusr=# \dt
Did not find any relations.
pgusr=# \dtS
                  List of relations
   Schema   |          Name           | Type  | Owner
------------+-------------------------+-------+-------
 pg_catalog | pg_aggregate            | table | pgusr
 pg_catalog | pg_am                   | table | pgusr
 pg_catalog | pg_amop                 | table | pgusr
 pg_catalog | pg_amproc               | table | pgusr
 pg_catalog | pg_attrdef              | table | pgusr
 pg_catalog | pg_attribute            | table | pgusr
 pg_catalog | pg_auth_members         | table | pgusr
 pg_catalog | pg_authid               | table | pgusr
 pg_catalog | pg_cast                 | table | pgusr
 pg_catalog | pg_class                | table | pgusr
 pg_catalog | pg_collation            | table | pgusr
 pg_catalog | pg_constraint           | table | pgusr
 pg_catalog | pg_conversion           | table | pgusr
 pg_catalog | pg_database             | table | pgusr
 pg_catalog | pg_db_role_setting      | table | pgusr
 pg_catalog | pg_default_acl          | table | pgusr
 pg_catalog | pg_depend               | table | pgusr
 pg_catalog | pg_description          | table | pgusr
 pg_catalog | pg_enum                 | table | pgusr
 pg_catalog | pg_event_trigger        | table | pgusr
 pg_catalog | pg_extension            | table | pgusr
 pg_catalog | pg_foreign_data_wrapper | table | pgusr
 pg_catalog | pg_foreign_server       | table | pgusr
...
...
...
 pg_catalog | pg_tablespace           | table | pgusr
 pg_catalog | pg_transform            | table | pgusr
 pg_catalog | pg_trigger              | table | pgusr
 pg_catalog | pg_ts_config            | table | pgusr
 pg_catalog | pg_ts_config_map        | table | pgusr
 pg_catalog | pg_ts_dict              | table | pgusr
 pg_catalog | pg_ts_parser            | table | pgusr
 pg_catalog | pg_ts_template          | table | pgusr
 pg_catalog | pg_type                 | table | pgusr
 pg_catalog | pg_user_mapping         | table | pgusr
(62 rows)

pgusr=# \dS+ pg_inherits
                               Table "pg_catalog.pg_inherits"
  Column   |  Type   | Collation | Nullable | Default | Storage | Stats target | Description
-----------+---------+-----------+----------+---------+---------+--------------+-------------
 inhrelid  | oid     |           | not null |         | plain   |              |
 inhparent | oid     |           | not null |         | plain   |              |
 inhseqno  | integer |           | not null |         | plain   |              |
Indexes:
    "pg_inherits_parent_index" btree (inhparent)
    "pg_inherits_relid_seqno_index" UNIQUE, btree (inhrelid, inhseqno)
Access method: heap

pgusr=# \dS+ pg_ts_config_map
                              Table "pg_catalog.pg_ts_config_map"
    Column    |  Type   | Collation | Nullable | Default | Storage | Stats target | Description
--------------+---------+-----------+----------+---------+---------+--------------+-------------
 mapcfg       | oid     |           | not null |         | plain   |              |
 maptokentype | integer |           | not null |         | plain   |              |
 mapseqno     | integer |           | not null |         | plain   |              |
 mapdict      | oid     |           | not null |         | plain   |              |
Indexes:
    "pg_ts_config_map_index" UNIQUE, btree (mapcfg, maptokentype, mapseqno)
Access method: heap

pgusr=# \dS+ pg_index
                                      Table "pg_catalog.pg_index"
     Column     |     Type     | Collation | Nullable | Default | Storage  | Stats target | Description
----------------+--------------+-----------+----------+---------+----------+--------------+-------------
 indexrelid     | oid          |           | not null |         | plain    |              |
 indrelid       | oid          |           | not null |         | plain    |              |
 indnatts       | smallint     |           | not null |         | plain    |              |
 indnkeyatts    | smallint     |           | not null |         | plain    |              |
 indisunique    | boolean      |           | not null |         | plain    |              |
 indisprimary   | boolean      |           | not null |         | plain    |              |
 indisexclusion | boolean      |           | not null |         | plain    |              |
 indimmediate   | boolean      |           | not null |         | plain    |              |
 indisclustered | boolean      |           | not null |         | plain    |              |
 indisvalid     | boolean      |           | not null |         | plain    |              |
 indcheckxmin   | boolean      |           | not null |         | plain    |              |
 indisready     | boolean      |           | not null |         | plain    |              |
 indislive      | boolean      |           | not null |         | plain    |              |
 indisreplident | boolean      |           | not null |         | plain    |              |
 indkey         | int2vector   |           | not null |         | plain    |              |
 indcollation   | oidvector    |           | not null |         | plain    |              |
 indclass       | oidvector    |           | not null |         | plain    |              |
 indoption      | int2vector   |           | not null |         | plain    |              |
 indexprs       | pg_node_tree | C         |          |         | extended |              |
 indpred        | pg_node_tree | C         |          |         | extended |              |
Indexes:
    "pg_index_indexrelid_index" UNIQUE, btree (indexrelid)
    "pg_index_indrelid_index" btree (indrelid)
Access method: heap

pgusr=# \q
root@b7d1ac37be2e:/#
```

## Задача 2

Используя `psql` создайте БД `test_database`.

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/master/06-db-04-postgresql/test_data).

Восстановите бэкап БД в `test_database`.

Перейдите в управляющую консоль `psql` внутри контейнера.

Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.

Используя таблицу [pg_stats](https://postgrespro.ru/docs/postgresql/12/view-pg-stats), найдите столбец таблицы `orders` 
с наибольшим средним значением размера элементов в байтах.

**Приведите в ответе** команду, которую вы использовали для вычисления и полученный результат.

## Ответ  
```
root@b7d1ac37be2e:/# psql -U pgusr
psql (13.9 (Debian 13.9-1.pgdg110+1))
Type "help" for help.

pgusr=# CREATE DATABASE test_database;
CREATE DATABASE
pgusr=# \l
                               List of databases
     Name      | Owner | Encoding |  Collate   |   Ctype    | Access privileges
---------------+-------+----------+------------+------------+-------------------
 pgusr         | pgusr | UTF8     | en_US.utf8 | en_US.utf8 |
 postgres      | pgusr | UTF8     | en_US.utf8 | en_US.utf8 |
 template0     | pgusr | UTF8     | en_US.utf8 | en_US.utf8 | =c/pgusr         +
               |       |          |            |            | pgusr=CTc/pgusr
 template1     | pgusr | UTF8     | en_US.utf8 | en_US.utf8 | =c/pgusr         +
               |       |          |            |            | pgusr=CTc/pgusr
 test_database | pgusr | UTF8     | en_US.utf8 | en_US.utf8 |
(5 rows)
```
Копируем backup в контейнер:
```
docker cp ~/netology/virt-homeworks/06-db-04-postgresql/test_data/test_dump.sql pg13_devops:/tmp
docker exec -it pg13_devops bash
root@b7d1ac37be2e:/# cd /var/lib/postgresql/data/
root@b7d1ac37be2e:/var/lib/postgresql/data# psql -U pgusr -f /tmp/test_dump.sql test_database
SET
SET
SET
SET
SET
 set_config
------------

(1 row)

SET
SET
SET
SET
SET
SET
CREATE TABLE
psql:/tmp/test_dump.sql:34: ERROR:  role "postgres" does not exist
CREATE SEQUENCE
psql:/tmp/test_dump.sql:49: ERROR:  role "postgres" does not exist
ALTER SEQUENCE
ALTER TABLE
COPY 8
 setval
--------
      8
(1 row)

ALTER TABLE
root@b7d1ac37be2e:/var/lib/postgresql/data# psql -U pgusr
psql (13.9 (Debian 13.9-1.pgdg110+1))
Type "help" for help.

pgusr=# \c test_database
You are now connected to database "test_database" as user "pgusr".
test_database=# \dt
        List of relations
 Schema |  Name  | Type  | Owner
--------+--------+-------+-------
 public | orders | table | pgusr
(1 row)

test_database=# ANALYZE VERBOSE public.orders;
INFO:  analyzing "public.orders"
INFO:  "orders": scanned 1 of 1 pages, containing 8 live rows and 0 dead rows; 8 rows in sample, 8 estimated total rows
ANALYZE
test_database=# select avg_width from pg_stats where tablename='orders';
 avg_width
-----------
         4
        16
         4
(3 rows)
```

## Задача 3

Архитектор и администратор БД выяснили, что ваша таблица orders разрослась до невиданных размеров и
поиск по ней занимает долгое время. Вам, как успешному выпускнику курсов DevOps в нетологии предложили
провести разбиение таблицы на 2 (шардировать на orders_1 - price>499 и orders_2 - price<=499).

Предложите SQL-транзакцию для проведения данной операции.

Можно ли было изначально исключить "ручное" разбиение при проектировании таблицы orders?

## Ответ  
```
create table orders_1 (like orders);
create table orders_2 (like orders);
insert into orders_1 SELECT * from orders where price > 499;
delete from orders where price > 499;
insert into orders_2 select * from orders whewe price <= 499;
delete from orders where price <= 499;
```
Да, можно.  

## Задача 4

Используя утилиту `pg_dump` создайте бекап БД `test_database`.

Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца `title` для таблиц `test_database`?


## Ответ  
```
root@b7d1ac37be2e:/var/lib/postgresql/data# pg_
pg_archivecleanup  pg_buildext        pg_conftool        pg_ctl             pg_dump            pg_lsclusters      pg_recvlogical     pg_restore         pg_standby         pg_updatedicts     pg_verifybackup
pg_backupcluster   pg_checksums       pg_controldata     pg_ctlcluster      pg_dumpall         pg_receivewal      pg_renamecluster   pg_restorecluster  pg_test_fsync      pg_upgrade         pg_virtualenv
pg_basebackup      pg_config          pg_createcluster   pg_dropcluster     pg_isready         pg_receivexlog     pg_resetwal        pg_rewind          pg_test_timing     pg_upgradecluster  pg_waldump
root@b7d1ac37be2e:/var/lib/postgresql/data# pg_dump -U pgusr -d test_database > test_database_dump.sql
root@b7d1ac37be2e:/var/lib/postgresql/data# ls
base    pg_commit_ts  pg_hba.conf    pg_logical    pg_notify    pg_serial     pg_stat      pg_subtrans  pg_twophase  pg_wal   postgresql.auto.conf  postmaster.opts  test_database_dump.sql
global  pg_dynshmem   pg_ident.conf  pg_multixact  pg_replslot  pg_snapshots  pg_stat_tmp  pg_tblspc    PG_VERSION   pg_xact  postgresql.conf       postmaster.pid

 CREATE TABLE orders (id integer NOT NULL, title character varying(80) NOT NULL UNIQUE, price integer DEFAULT 0);
```
