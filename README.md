1)create VM from template
2)Install necessary soft:
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo apt install pg-activity
3)create db as user postgres
sudo su postgres
psql
create database homeworkdb;
4)connect to homeworkdb as user postgres and check there is nothing in db
\c homeworkdb
\dt+
5)exit from user postgres and clone some postgres data base schema from git
exit
exit
git clone https://github.com/pthom/northwind_psql.git
6)create tables in db and wheck it it's successsfull
sudo su postgres
psql -d homeworkdb -f /home/elena.razgulayeva/northwind_psql/northwind.sql
psql
\c homeworkdb
\dt+
7)create dump
exit
mkdir /tmp/dump_backup
pg_dump homeworkdb > /tmp/dump_backup/prod.dump.sql
8)check if we have file with dump
cd /tmp/dump_backup
ls -lah
9)drop db and check it's dropped (You should see "FATAL:  database "homeworkdb" does not exist" when trying to connect)
cd ~
dropdb homeworkdb
psql
\c homeworkdb
exit
10)create data base and restore the content from backup, then check that it's restored
psql
create database homeworkdb;
exit
psql -U postgres -d homeworkdb -f /tmp/dump_backup/prod.dump.sql
psql
\c homeworkdb
\dt+
