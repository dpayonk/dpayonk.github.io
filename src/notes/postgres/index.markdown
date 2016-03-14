---
layout: page
title: "My Postgres Notes"
date: 2013-06-05 14:12
comments: true
sharing: true
footer: true
---
## Database size
```
SELECT pg_size_pretty(pg_database_size('geekdb'));
```
## Table size
```
SELECT relname, relpages FROM pg_class ORDER BY relpages DESC limit 1;
SELECT pg_size_pretty(pg_total_relation_size('big_table'));--with indexes
SELECT pg_size_pretty(pg_relation_size('big_table'));--w/o indexes
```
## Monitoring
```
SELECT pg_terminate_backend(procpid) FROM pg_stat_activity
WHERE procpid <> pg_backend_pid() AND datname ='xsell_integration'; -- Kill Process
SELECT * FROM pg_stat_activity;
select * from Pg_stat_user_indexes;--indexes
----- Buffer Cache --------------
SELECT c.relname, count(*) AS buffers FROM pg_buffercache b INNER JOIN pg_class c
ON b.relfilenode = pg_relation_filenode(c.oid)
    AND b.reldatabase
    IN (0, (SELECT oid FROM pg_database
WHERE datname = current_database()))
GROUP BY c.relname
ORDER BY 2 DESC
LIMIT 10;
```
## Indexes
```
\d table_name
```
## Utilities
```
select generate_series(1,1000);
select uuid_generate_v1();
```
## Admin
List all functions
```
SELECT  distinct proname
FROM    pg_catalog.pg_namespace n
JOIN    pg_catalog.pg_proc p
ON      pronamespace = n.oid
WHERE   nspname = 'public'
order by 1
```

```
$ psql postgres postgres
ALTER USER postgres WITH PASSWORD 'tmppassword';
/etc/init.d/postgresql status
--- Configurations and postgres file location ---
SHOW ALL
```

Use split. The split command allows you to split the output into pieces that are acceptable in size to the underlying file system. For example, to make chunks of 1 megabyte:
```
pg_dump dbname | gzip > filename.gz
pg_dump dbname | split -b 1m - filename
```

Reload with:
```
cat filename* | psql dbname
```


##Configuration

+ Effective_cache_size should be half or more of memory
+ select * from pg_setting
+ Shared_buffers should be at least 25 percent, but not so big 512 on 32 bit and 1 gb on 64 but
+ Turn off enable_seqscan

##Linux System Notes
+ /var/lib/pgsql/data is default location on RHEL
+ PG_DATA global variable creates stuff

##Security
+ 172.16.100.0/24 should be the smaller subnet if you want to limit it to the .100 subnet you have
+ 172.16.0.0/16 would allow all instances in the last 2 subnets

##Utilities
+ http://www.thegeekstuff.com/2009/05/15-advanced-postgresql-commands-with-examples/
Database Extensions

--dblink,pg_buffercache,adminpack
--redis_fdw - Required downloading the hiredis library from git and compiling it AND
--#downloading the redis_fdw repository from git and compiling and installing it

##Database Extensions
The following extensions I've found most useful
+ hstore
+ file_fdw,
+ redis_fdw
+ uuid-ossp

###HStore
This is now a standard part of Postgres after 9.2.  It's awesome and can replace tag
fields and/or NoSQL databases in some instances.

###REDIS FDW
```
    CREATE SERVER redis_server
    FOREIGN DATA WRAPPER redis_fdw
    OPTIONS (address '127.0.0.1', port '6379');

    CREATE FOREIGN TABLE redis_db0(key text, value text)
    SERVER redis_server
    OPTIONS(database '0');

    --MUST CREATE USER MAPPING
    CREATE USER MAPPING FOR PUBLIC
    SERVER redis_server
    OPTIONS(password 'XSELL')--Doesnt matter i bet

    CREATE FOREIGN TABLE myredishash(key text, value text[])
    SERVER redis_server
    OPTIONS(database '0', tabletype 'hash', tablekeyprefix 'insureon:Feature:#GeneralLiability:TokenFrequency');


    CREATE FOREIGN TABLE myredishashtest(key text, value text[])
    SERVER redis_server
    OPTIONS(database '0', tabletype 'hash', tablekeyprefix 'insureon:Feature:');

    select * from myredishashtest
```

###FILE FDW
```
    CREATE SCHEMA filess

    CREATE SERVER file_server FOREIGN DATA WRAPPER file_fdw;
    --http://www.postgresql.org/docs/9.1/static/file-fdw.html
    CREATE FOREIGN TABLE files.purchases (
        client_id varchar(255),
        response int,
        lead_uid varchar(255),
        response_date date,
        is_bound int
       ) SERVER file_server
    OPTIONS (format 'csv',header 'true'
    , filename '/var/lib/file_data/purchases.csv', delimiter E',', null '');
```

###DBLINK
```
    SELECT dblink_connect('production','hostaddr=107.21.45.199 port=5432 dbname=xsell_prod user=xsell_dashboard password=X$ELL_DASHBOARD230lasalle')

    SELECT * FROM dblink('production','SELECT id FROM Users') AS t(a int);
```