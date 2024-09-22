# Check if postgres is installed
```
aafak@aafak-virtual-machine:~$ psql --version
psql (PostgreSQL) 14.13 (Ubuntu 14.13-0ubuntu0.22.04.1)
aafak@aafak-virtual-machine:~$ ps aux | grep postgres
postgres    1167  0.0  0.5 220944 29952 ?        Ss   14:26   0:01 /usr/lib/postgresql/14/bin/postgres -D /var/lib/postgresql/14/main -c config_file=/etc/postgresql/14/main/postgresql.conf
postgres    1455  0.0  0.1 221060  9164 ?        Ss   14:27   0:00 postgres: 14/main: checkpointer
postgres    1456  0.0  0.1 220944  8268 ?        Ss   14:27   0:00 postgres: 14/main: background writer
postgres    1457  0.0  0.1 220944 11724 ?        Ss   14:27   0:00 postgres: 14/main: walwriter
postgres    1458  0.0  0.1 221612  9932 ?        Ss   14:27   0:00 postgres: 14/main: autovacuum launcher
postgres    1464  0.0  0.1  75668  7116 ?        Ss   14:27   0:00 postgres: 14/main: stats collector
postgres    1474  0.0  0.1 221376  8908 ?        Ss   14:27   0:00 postgres: 14/main: logical replication launcher
aafak       9650  0.0  0.0   9212  2432 pts/0    S+   15:49   0:00 grep --color=auto postgres
aafak@aafak-virtual-machine:~$ sudo -u postgres psql
[sudo] password for aafak:
could not change directory to "/home/aafak": Permission denied
psql (14.13 (Ubuntu 14.13-0ubuntu0.22.04.1))
Type "help" for help.

postgres=# \d
Did not find any relations.
postgres=# \l
                             List of databases
   Name    |  Owner   | Encoding | Collate | Ctype |   Access privileges
-----------+----------+----------+---------+-------+-----------------------
 postgres  | postgres | UTF8     | en_IN   | en_IN |
 template0 | postgres | UTF8     | en_IN   | en_IN | =c/postgres          +
           |          |          |         |       | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_IN   | en_IN | =c/postgres          +
           |          |          |         |       | postgres=CTc/postgres
 testdb    | postgres | UTF8     | en_IN   | en_IN | =Tc/postgres         +
           |          |          |         |       | postgres=CTc/postgres+
           |          |          |         |       | aafak2=CTc/postgres
(4 rows)

postgres=#

```

# Login to test DB
```
aafak@aafak-virtual-machine:~$ su aafak2
Password:

aafak2@aafak-virtual-machine:/home/aafak$ psql -U aafak2 -d testdb
could not change directory to "/home/aafak": Permission denied
psql (14.13 (Ubuntu 14.13-0ubuntu0.22.04.1))
Type "help" for help.

testdb=#
```
