Pagila
======

Our version of Pagila is based on [this repository](https://github.com/ganeshan/pagila) but with few modifications

- We tried it on Postgres 12 and are modifing it to be runnable in this version
- Primary keys and foreign keys are now aligned to proper data types. Some primary keys were defined as integers but fkeyed as smallint and vice versa
- Partition tables are now created for year 2020
- Data are also created for year 2020


FULLTEXT SEARCH
---------------

Fulltext functionality is built in PostgreSQL, so parts of the schema exist
in the main schema file. 

Example usage:

SELECT * FROM film WHERE fulltext @@ to_tsquery('fate&india');


PARTITIONED TABLES
------------------

The payment table is designed as a partitioned table with a 6 month timespan
for the date ranges. 
If you want to take full advantage of table partitioning, you need to make
sure constraint_exclusion is turned on in your database. You can do this by
setting "constraint_exclusion = on" in your postgresql.conf, or by issuing the
command "ALTER DATABASE pagila SET constraint_exclusion = on" (substitute
pagila for your database name if installing into a database with a different
name)


INSTALL NOTE
------------

The pagila-data.sql file and the pagila-insert-data.sql both contain the same
data, the former using COPY commands, the latter using INSERT commands, so you 
only need to install one of them. Both formats are provided for those who have
trouble using one version or another.
